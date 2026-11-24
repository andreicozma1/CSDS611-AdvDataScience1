# Bayesian optimization for the assignment CSV

The fitting objective is raw SSE over both populations at the 27 times in
[LV_data.csv](../LV_data.csv), using all four assignment bounds. Numerical
error against a checked trajectory is a separate quantity. The
[synthetic recovery study](../benchmarks/archived-synthetic-recovery/README.md)
and [fixed-pool studies](../benchmarks/archived-fixed-pool-4096/README.md)
are archived and excluded from active implementation and main comparisons.

## Terminology

| Term | Meaning |
| --- | --- |
| Initial design points | The 50 physical rate vectors evaluated before BO |
| Halton initialization samples | Cheap locations used to initialize acquisition optimization |
| L-BFGS-B starting points | Sampled locations selected for bounded local optimization |
| L-BFGS-B results | Returned locations, including finite results that did not converge |
| Next evaluation point | One physical rate vector selected for the ODE objective |
| Objective evaluation | A solver call and the raw SSE calculation |

Use **Halton samples** and **L-BFGS-B runs** as compact acquisition-search
headers. The incumbent is an additional starting-point candidate outside the
Halton count; it remains ineligible for another objective call.

| Current identifier | Meaning |
| --- | --- |
| `sampling.initial_rates` | One shared Halton initial-design implementation |
| `sampling.acquisition_trials` | Iteration-specific acquisition initialization samples |
| `AcquisitionConfig.halton_samples` | Number of cheap Halton samples |
| `AcquisitionConfig.lbfgsb_runs` | Total number of bounded local optimizations |
| `AcquisitionConfig.maxiter` | Iteration limit per L-BFGS-B run |
| `GPConfig.optimizer_restarts` | Restarts for fitting GP hyperparameters |

Earlier `search_starts`, `local_restarts`, and `matern` method names belong to
historical records. Current search methods are `bo`, `halton`, and `uniform`.
Use **Follow-up attempts** on progress axes that include failed solver calls.

## Components and responsibilities

| Component | Responsibility | Code |
| --- | --- | --- |
| Initial design | Map Halton unit points to physical rates | `sampling.py` |
| GP surrogate | Fit measured scores and predict a mean and uncertainty | `surrogate.py` |
| Acquisition function | Score possible queries from the fixed GP posterior | `continuous_bo.acquisition_values` |
| Acquisition optimizer | Search the continuous bounds for a high acquisition score | `continuous_bo.optimize_acquisition` |
| ODE evaluator | Integrate at physical rates and calculate raw SSE | `ode_objective.py` |
| Runner | Sequence attempts, save outcomes, and resume | `run_bo.py` |

The assignment's [Step 2 handout](../project_step_2.pdf) and
[lecture sources](../../lectures/README.md) motivate the GP surrogate and
sequential acquisition loop. The numerical solver, GP, acquisition rule, and
acquisition optimizer have separate settings.

## One sequential BO iteration

1. Collect all valid measured scores from the initial design and prior follow-ups.
2. Transform GP inputs and targets, then fit its kernel hyperparameters and posterior.
3. Hold that posterior fixed while calculating and optimizing the acquisition.
4. Select one unattempted physical rate vector over the full assignment bounds.
5. Save the pending attempt before calling the configured ODE evaluator.
6. Save predictions and raw SSE, or a separate failure/timeout outcome.
7. Include the new valid score before choosing the next query.

Acquisition evaluations never call the ODE solver or become GP observations.
The GP is refitted at every BO proposal, including after a failed objective
attempt; failed attempts add no score. A numerical acquisition search provides
an approximate maximizer rather than a guaranteed global maximum.

## What each choice belongs to

`GPConfig` makes the following choices explicit. Its implementation defaults
retain the earlier policy and do not settle the final scientific choice.

| GP setting | Supported values | Implementation default |
| --- | --- | --- |
| Inputs | Physical, scaled physical, log, scaled log | `scaled_log` |
| Target | Raw SSE or log SSE | `log` |
| Centering | None, initial mean, current mean | `current_mean` |
| Scaling | None, initial SD, current SD, initial IQR / 1.349 | `initial_sd` |
| Kernel | RBF, Matérn 3/2, Matérn 5/2 | `matern52` |
| Initial length scales | One initial value, fitted independently for four rates | 0.25 |
| Length-scale bounds | Bounds in the selected GP input units | 0.01 to 10 |
| Kernel amplitude | Initial value and bounds | 1; 0.01 to 100 |
| Diagonal regularizer | `alpha` in standardized target units | `1e-6` |
| Hyperparameter restarts | Separate from acquisition-search runs | 3 |
| GP fitting seed | Separate from the initial-design seed | 611 |

Target means and SDs are calculated from valid objective scores, not from CSV
population means. Frozen initial SD uses the valid initial targets with
`ddof=0`. Current mean/SD uses all valid targets available at that proposal.
The GP predicts back in raw-SSE or log-SSE units before acquisition scoring.
A zero or nonfinite selected target scale makes that BO policy unavailable;
there is no silent switch to another scaling rule. A failed GP factorization
is also recorded as unavailable without assigning an objective score.

## Open sampling and representation choices

Initial sampling and GP inputs are independent. For bounds `L,U` and unit
points `u`, physical sampling uses `L + u*(U-L)` and log sampling uses
`exp(log(L) + u*(log(U)-log(L)))`. Both return physical rates to the solver.
The default initial mapping remains physical, with seed 612 and 50 points.

A sampling-space comparison shares the underlying Halton unit points and
changes their mapping. A GP-input or GP-target comparison shares the same
physical initial queries and compatible measured scores. Neither geometric
coverage nor archived fixed-pool rankings settles the preferred representation.
See [sampling spaces](sampling-and-acquisition.md) for the tradeoffs.

## Where the loop lives

[run_bo.py](../code/python/run_bo.py) is the active assignment runner.
[surrogate.py](../code/python/surrogate.py) fits the GP;
[continuous_bo.py](../code/python/continuous_bo.py) constructs and optimizes
its acquisition. [sampling.py](../code/python/sampling.py) owns both Halton
samplers and the coordinate maps.

The earlier [700-query study](../benchmarks/2026-11-17/bo-full-bounds/README.md)
is a saved comparison of one policy against controls. Its historical names,
settings, scores, and query budgets remain unchanged.

## Acquisition-search policy

`AcquisitionConfig` holds the acquisition rule and its numerical search settings:

| Rule | Quantity maximized |
| --- | --- |
| `ei_raw` | Expected improvement in raw SSE, using the selected GP target distribution |
| `ei_log` | Expected improvement in log SSE; requires a log-SSE GP |
| `lcb_target` | Negative lower confidence bound in the GP target units |

With a log-SSE GP, raw-SSE EI integrates improvement under a lognormal
predictive distribution. With a raw-SSE GP, it uses a Gaussian predictive
distribution. EI is calculated in log arithmetic to avoid underflow; that
does not change the objective or turn raw-SSE EI into log-SSE EI.
LCB uses `mean - beta*SD`, with an explicit default `beta=2`.

The search draws a reproducible scrambled Halton batch in bound-normalized
physical or log coordinates corresponding to the GP inputs. It also considers
the incumbent, selects the requested number of starting points, and uses bounded
L-BFGS-B. Finite local-search results remain candidates even if the optimizer
reports nonconvergence; their status is saved. Zero local runs selects the best
eligible sampled point. Counts larger than the available starts are rejected.

### Sequence state, repeated locations, and reuse

Each acquisition scramble uses `(run seed, BO iteration, stream 1)`. Larger
sample budgets share prefixes at a fixed seed and iteration. Samples may recur
across different iterations; their acquisition scores are recomputed using the
current posterior. The search is never restricted to one persistent finite pool.

Prior successful, failed, timed-out, and interrupted objective attempts are
excluded from repeat proposals. `duplicate_distance` retains the earlier
`1e-10` threshold in the acquisition's normalized coordinates. This is an
explicit, unvalidated proximity heuristic; zero requests exact-coordinate
exclusion. Choosing its final value remains open.

Each BO record saves the Halton points and scores, incumbent score, selected
local-start indices, local endpoints, optimizer status/messages, `nfev`,
iterations and elapsed times, selected physical rate, fitted kernel, target
mean/scale, GP fitting warnings, and proposal time. `null` acquisition scores
represent zero EI whose logarithm is negative infinity.

The runner saves predictions in physical population units as little-endian
float64 pairs. A compatible initialization checkpoint can supply an initial
prefix through `--initial-results`; imported records retain their original
timings and a `reused_from` path. Different BO policies use new output
directories. No general cross-study cache or historical schema adapter is added.

## Evaluator, failures, and resume

Every run requires an explicit solver. Direct `rk4` and `rk8` require
`max_step`; `folded_rk8` requires `tolerance`. There is no automatic switch to
period folding or a compensated evaluator. Direct RK4 at `h=1/256` is
provisional for initialization analysis; review the
[step-refinement results](rk4-step-refinement.md) before filling its remaining
queries. Qualification for BO remains open.
Direct RK4/RK8 integrate population variables; folded RK8 uses its existing
log-population kernel internally and returns predictions in population units.

A reusable child process evaluates one query at a time. The 300-second default
wall-time limit includes worker startup, compilation, and communication. The
recorded `solve_seconds` measures the worker's objective call and can include
first-call compilation. These are not warmed Step 1 benchmark timings.
A timeout terminates the worker; the next query gets a new worker.

The SQLite record is saved as `pending` before the solver call, and committed
as `completed`, `failed`, or `timeout` afterward. An interrupted attempt stays
visible and spends one attempt; resume marks an unfinished pending record
`interrupted` instead of evaluating that rate again. Unexpected programming
errors are recorded and propagated. Both species' RMSEs come from the candidate
whose total raw SSE is being reported.

The database binds observations, source versions, bounds, initial mapping,
solver settings, numerical library versions, Python version, and platform. BO policy settings are bound
separately when follow-ups begin. A short file lock gives one runner ownership
of an output directory; database write transactions cover only saved-state
updates, so readers remain usable during solves. Exact zero SSE stops that
method and identifies its query. Otherwise the requested attempt budget governs
completion; no convergence-based stopping threshold has been selected.

## Staged acquisition-search comparison

The accepted pilot compares 50 Halton samples with 0, 5, 10, or 15 L-BFGS-B
runs. Each arm shares the same 50 seed-612 initial scores and makes 50
sequential follow-up attempts. Hold the chosen evaluator, GP policy, and
acquisition rule fixed while varying acquisition-search effort.

| Stage | Halton samples | Candidate L-BFGS-B runs | Gate |
| --- | ---: | --- | --- |
| 1 | 50 | 0, 5, 10, 15 | Review before expanding |
| 2 | 100 | Retain counts after stage 1 | Review before expanding |
| 3 | 150 | Retain counts after stage 2 | Review retained comparisons |

The later sample counts are conditional, not a commitment to run every arm.
At each gate compare raw-SSE progress, species RMSEs, timing, acquisition cost,
and solver outcomes. No automatic elimination threshold or production search
budget has been selected. The common effort for the separate raw-versus-log
GP-target comparison also remains open.

## Implementation status

The runner exposes both acquisition-search counts and the GP settings above.
Its search method is `bo`; the previous `matern` CLI value and old checkpoint
schema are unsupported. `--followups 0` generates only the shared initial
design. BO follow-ups require explicit `--halton-samples` and `--lbfgsb-runs`.
Use the [code README](../code/README.md#search-the-full-rate-bounds) for commands.
This cleanup does not launch the pilot or select its remaining settings.

### Pruning guidance for stage reviews

Use loss progress, final loss, and runtime together when deciding which settings
to carry forward. Clear dominance is a proposed basis for pruning; no automatic
elimination rule or universal percentage cutoff has been adopted.

Let $b(q)$ be the best observed raw SSE after $q$ follow-up attempts, including
the shared 50 initial design points. Thus $b(0)$ is the common best initial SSE.

| Metric | Meaning | Role |
| --- | --- | --- |
| $b(50)$ | Best fit found at the agreed budget | Primary outcome |
| Average $b(q)$ over attempts 1–50 | How quickly good fits were found | Early progress |
| Total follow-up time | Actual cost of the BO run | Cost comparison |
| Acquisition-search time and evaluation count | Cost of additional L-BFGS-B runs | Explains overhead |
| Failed objective calls | Budget spent without obtaining scores | Reliability |
| Prey and predator RMSE | Which population benefits or suffers | Diagnostic breakdown |

The progress summary is

$$
A=\frac{1}{50}\sum_{q=1}^{50}b(q).
$$

Lower is better. This averages over attempt positions, not seeds, and equals the
discrete area under the best-SSE curve divided by the attempt budget. A failed
call consumes an attempt and leaves the incumbent unchanged. Both species'
RMSEs must come from the same candidate that minimizes total SSE.

Tracking final performance and best-observed loss over time is established
benchmarking practice. HPOBench reports both and includes optimizer overhead in
elapsed time. Its repeated-seed evaluation is distinct from our one-seed pilot.
[HPOBench study](https://datasets-benchmarks-proceedings.neurips.cc/paper_files/paper/2021/file/93db85ed909c13838ff95ccfa94cebd9-Paper-round2.pdf)

After every arm finishes its 50 follow-ups:

1. Check that initial scores, solver, GP policy, acquisition, and query budget
   are matched.
2. Identify settings dominated by another: no better final SSE, no better
   average best-SSE progress, and no lower runtime, with at least one clear
   disadvantage.
3. Retain tradeoffs, such as better final loss at greater cost or faster
   early progress followed by worse final loss, until priorities are discussed.
4. Retain unresolved cases, including tiny differences, differences near the
   solver's numerical resolution, or crossing curves without a clear winner.

For example, these hypothetical results would make ten L-BFGS-B runs a
candidate for removal:

| L-BFGS-B runs | Final best SSE | Average best SSE | Time (s) |
| ---: | ---: | ---: | ---: |
| 5 | 900 | 1,020 | 120 |
| 10 | 930 | 1,080 | 180 |

The five-run setting performs better on both loss measures and costs less. If ten
runs instead reached SSE 850, it would offer a tradeoff worth retaining.

With seed 612 alone, pruning is a pilot decision, not evidence that a setting
is generally inferior. The 50 successive BO attempts are not 50 independent
repetitions and must not be treated as such in a significance calculation.
Absolute and percentage differences can be reported, but neither defines
"substantial" automatically. Small or ambiguous differences favor retention.

Poor performance with zero L-BFGS-B runs at 50 samples does not establish poor
performance at 100 or 150: more Halton samples could compensate for missing
L-BFGS-B runs. Retaining zero runs at the next sample count, when
affordable, tests this interaction. If it is omitted to save computation,
record that as a budget decision based on the preceding stage, not a result
demonstrated at the new sample count. Any such choice remains for user review.

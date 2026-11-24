# Final project decision ledger

Updated November 19, 2026. This records the current choices that affect the project work. Run records remain the source for exact experimental settings and results.

## Settled

| Choice | Decision |
| --- | --- |
| Immediate priority | Work on the required Step 1 and Step 2 deliverables using the professor's CSV. The synthetic-data study is archived. |
| Synthetic recovery archive | Keep scripts, generated datasets, results, notes, and figure links together in the [synthetic archive](../benchmarks/archived-synthetic-recovery/README.md), outside active BO maintenance and main comparisons. The local launchd collector was unloaded and its SSH wait stopped; workstation computations were not changed or inspected. |
| Report | Add the authorized Part 2 passage on sampling spaces, GP input representations, and raw/log SSE targets as open choices. Keep other report changes on hold while the methods and results are checked. |
| Objective | Use raw SSE across the 27 paired prey and predator observations. Keep numerical error against a checked solution separate from fit error against the CSV. |
| Search domain | Apply all four assignment rate bounds to every BO proposal and solver evaluation. |
| Initial BO design | Use 50 scrambled Halton initial design points per seed; paired comparisons share the same evaluated rates. |
| Open sampling and GP representations | Keep physical/log initial sampling, physical/scaled-physical/log/scaled-log GP inputs, and raw/log SSE GP targets available for matched comparison. None is selected as the final representation. An initialization comparison shares underlying unit points, while GP comparisons share physical queries. Record sampling tradeoffs in Part 2 before adding experimental comparison results. |
| New BO seed count | Use seed 612 and the same 50 scrambled Halton starting rates across new BO policy comparisons. The first direct-solver benchmark uses positions 1–5 of those 50. |
| Sequential BO | Fit the GP to valid measured scores, optimize the acquisition over the continuous bounds, evaluate one new rate vector, and include its score before selecting the next. |
| BO components | Retain the required GP surrogate, the acquisition function derived from its predictions, and the numerical acquisition optimizer as separate components. Fit GP hyperparameters from measured scores; hold the GP fixed during acquisition maximization over rates. Only measured objective results update the GP. |
| BO terminology | Use the [canonical terms](bayesian-optimization.md#terminology). Current method names are bo/halton/uniform; the GP kernel is separate. Historical records keep their original labels. |
| Acquisition initialization sampler | Use scrambled Halton in the GP's normalized input coordinates, reproducibly keyed by run seed and BO iteration. Retain bounded L-BFGS-B from selected starting points and matching prefixes across sample budgets. This does not change the initial 50 design points; earlier uniform-random acquisition initialization keeps its original identity. |
| Archived work | The 4,096-candidate fixed-pool comparisons remain archived and do not support main rankings of continuous-search BO policies. |
| Local acquisition optimizer | Keep bounded L-BFGS-B for all positive run counts. Drop the proposed Nelder–Mead comparison. |
| Acquisition-search comparison | Use the [staged plan](bayesian-optimization.md#staged-acquisition-search-comparison): 50, 100, and 150 Halton samples, each with 0/5/10/15 L-BFGS-B runs as candidate settings. Begin at 50 samples and review before each expansion; later combinations remain conditional. |
| Completed solver timing comparison | Used direct Numba RK4 at `1/128`, `1/256`, `1/512` and direct Numba RK8 at `1/128`, `1/256`, plus default SciPy RK45, DOP853, and LSODA. The user cancelled `1/64` for both custom methods and `1/512` for RK8; their existing records remain historical and excluded from active tables. Timed one warmed full objective call per retained setting at each of the first five seed-612 Halton rates, with a 300-second cap. Accuracy was deferred to the refinement check below; BO's use of period folding remains open. |
| Provisional forward solver | The user selected direct Numba RK4 at `h=1/256` for the next initialization analysis. This is a provisional numerical setting; its accuracy and qualification for BO remain open. Five exact matching saved calls are reusable. |
| Order after solver timings | Check numerical accuracy before filling the remaining 45 initialization points. The user selected adjacent-step prediction changes plus runtime, retaining individual curves for the five cases. Reuse `1/128`, `1/256`, and `1/512`; add `1/1024` and `1/2048` with the same direct solver, rates, outputs, and 300-second cap. |
| Refinement figure inclusion | Include a step size only when all five rate vectors complete with finite positive predictions; compare adjacent halvings only when both levels qualify. Retain failed records outside the figures and keep `1/64` excluded. No numerical accuracy cutoff or final step size is selected. |
| Local uncapped SciPy comparison | Stopped at the user's request on 2026-11-20: four completed calls remain saved, and the third RK45 call was interrupted without predictions. The uncapped local campaign is superseded by the fresh workstation comparison below. These are numerical baselines, not checked accuracy references. See the [local record](../benchmarks/2026-11-19/scipy-defaults-five-halton-no-limit/README.md). |
| Fresh workstation SciPy comparison | Run RK45 and LSODA through `solve_ivp` at `rtol=1e-3`, `atol=1e-6`, on all five identical seed-612 vectors and 27 CSV times on com2044. The user selected one worker and 30 minutes per solver call, ten fresh calls total; record numerical failures and timeouts separately without automatic limit increases. See the [study README](../benchmarks/2026-11-20/scipy-defaults-five-halton/README.md). |
| Workstation execution and handoff | The user selected detached tmux with return after verified startup. The fresh SciPy producer runs in `csds611-scipy-defaults-halton5`, independently of SSH; it owns incremental checkpoints, tables, exit status, and completion. No attached agent monitor is retained after handoff. The source and startup receipts are in the study record. |
| Workstation experiment hierarchy | Use `codex-experiments/<project>/YYYY-MM-DD/<study>/`; subproject levels are optional. The user approved stopping the archived synthetic campaign and comparison watcher to migrate all old `runs/` folders. The sole com2044 study moved and was verified; com2048 had no old run tree. See [workstation-experiment-storage.md](workstation-experiment-storage.md). |
| First full BO acquisition-search comparison | After selecting the scorer and GP policy, begin with 50 Halton samples and 0/5/10/15 L-BFGS-B runs. Share the 50 seed-612 initial scores and use 50 sequential follow-up attempts per arm. Review before expanding. |
| GP policy for acquisition-search comparison | Choose one GP representation after the paired raw-versus-log BO comparison, then hold it fixed across retained acquisition-search arms. |
| Stage-boundary decisions | Before 100 Halton samples, review whether to retain zero L-BFGS-B runs and other run counts; repeat before 150. Later candidate sets are conditional, with no numerical pruning threshold selected. |
| Grid versus implementation | The runner now exposes Halton sample and L-BFGS-B run counts and binds them to each BO policy. Both counts are required for BO follow-ups. The grid does not select a production default or authorize a run. |
| Proposed pruning guidance | Saved [stage-review metrics and dominance guidance](bayesian-optimization.md#pruning-guidance-for-stage-reviews). Retain tradeoffs and unresolved cases; elimination remains a user decision. |
| Raw-versus-log GP comparison | From the same 50 seed-612 initial design points, run separate 50-follow-up-attempt sequential BO chains that differ only in whether the GP models raw SSE or log SSE. Hold GP input coordinates, Matérn 5/2 kernel, target centering/scaling rule, and expected improvement in raw SSE fixed. Plot each chain's best observed raw SSE against follow-up attempts. Choose the common acquisition-search effort later, before either chain runs. |
| Questions | Ask for decisions with blocking structured input. An unanswered or dismissed question does not authorize dependent work. |
| Original timing host | The completed 300-second five-rate pilot ran on this MacBook with one solver process at a time. The newly authorized 30-minute default-SciPy comparison uses com2044 and fresh records; do not combine their timings as one host population. See the [original record](../benchmarks/2026-11-19/direct-solvers-five-halton/README.md). |
| Reuse solver outputs | Preserve predictions, inputs, settings, source/runtime identity, timings, and failures. Reuse exact matching predictions; recompute SSE when observations change. Label reused wall times historical and keep fresh timing separate from cache access. |
| Direct-solver benchmark storage | Keep its dated JSONL/manifest/source bundle and exact-match prediction lookup. This applies to the five-rate timing campaign; BO uses its own per-run SQLite checkpoint. |
| Progress tables | Finish the retained settings at one rate before moving to the next. Post a cumulative table after each complete rate. Show mean ± sample SD followed by separate completed, failed, and timeout columns. Name maximum step `h` for custom methods and explicit `rtol`/`atol` for SciPy; omit min, max, and total from presentation tables. |
| Solver review repairs | Singleton initial-time requests in both SciPy wrappers and runner recovery/accounting are repaired and tested. The amended runner finished the nine missing retained calls, preserving the original manifest, executed runner, and numerical source. |

## Active BO code cleanup

The authorized cleanup keeps one assignment-CSV workflow. `sampling.py` owns
initialization; `surrogate.py` fits the GP; `continuous_bo.py` scores and searches
the acquisition; `run_bo.py` checkpoints sequential attempts. Solver settings
are explicit through `ode_objective.SolverConfig`. No default promotes the
provisional RK4 step to a validated BO setting.

The duplicate initial-design command, GP helper, unused compensated fallback,
and historical source aliases are removed from active use. Compatible initial
checkpoints can be imported into a new policy arm, with reused timings labeled.
Old results and the synthetic archive remain intact. This cleanup does not
launch experiments or alter the report. Verification: 53 unit/integration tests pass; the fresh-output CLI check uses a one-time-point fixture, 50 initial calls and two BO follow-ups, then resumes without repeating rows. These checks do not establish long-horizon solver accuracy or a preferred BO policy.

## Completed direct-solver comparison

The five-rate comparison is complete: 40 retained calls yielded 26 completed
solves, two failures, and 12 timeouts. The raw record also retains 12 excluded
historical outcomes. See the [timing notes](direct-solver-timing.md) and
[run record](../benchmarks/2026-11-19/direct-solvers-five-halton/README.md)
for settings, interruptions, source bindings, and recovery checks.

Do not add rates or launch BO before the next decision. The cached RK4
`1/256` and `1/512` predictions differ substantially; that comparison is not
an error against a checked reference.

## Open before new experiments

1. Review the completed [RK4 step-refinement results](rk4-step-refinement.md) before completing the remaining initialization scores. All five cases completed at every retained level through `1/2048`, but prediction changes did not taper down and the conserved quantity still changed materially in several cases. Decide how to establish stable predictions; no final step size or accuracy threshold is selected.
2. Choose the common acquisition-search effort for the raw-versus-log BO chains after the solver and initial-design checks. The same 50 initial query scores alone produce the same best-observed-SSE curve for either GP target.
3. At each acquisition-search stage boundary, compare raw-SSE progress and endpoints, runtime, acquisition cost, and failures before choosing retained L-BFGS-B run counts. No automatic pruning rule is selected; every arm shares the initial observations and updates its own GP sequentially.
4. Decide whether to run the physical-versus-log initialization comparison and which GP input, target, centering, scaling, kernel, and acquisition comparisons belong in Step 2 or a later BO study. Keep final representations open; archived fixed-pool rankings do not settle continuous-search choices.
5. Confirm the Step 1 and Step 2 acceptance evidence and the order of any remaining implementation and write-up work. Keep the current report hold until explicitly lifted.

## Deferred

- The archived 45-dataset synthetic rate-recovery study, including MATLAB fits and any extension to 500 follow-up queries, requires a new decision before resuming.
- The proposed three-saved-GP-state acquisition screen as a BO performance comparison. It could assess one acquisition choice but cannot establish the best SSE after a full BO run; no screen was executed.

## Sources

- [Step 1 contract and bounds](../AGENTS.md#step-1-evaluation-contract)
- [BO loop and component definitions](bayesian-optimization.md)
- [Step 2 handout](../project_step_2.pdf)
- [Existing continuous-search study](../benchmarks/bo-progress/full-rate-bounds/README.md)
- [Archived fixed-pool results](../benchmarks/archived-fixed-pool-4096/README.md)

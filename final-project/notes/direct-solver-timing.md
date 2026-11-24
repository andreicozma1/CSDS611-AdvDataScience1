# Direct ODE solver timings

November 19, 2026

We compared direct Numba RK4 and RK8 with SciPy's default RK45, DOP853, and
LSODA at five fixed rate vectors. The retained custom settings completed all
five cases. RK45 and DOP853 reached the 300-second cap in every case; LSODA
completed one, failed twice, and timed out twice. These are runtime contenders;
the forward solver for the next study is still a decision to make.

## Workload and timing

- Every call integrates directly from zero to 2,960,000, starting from prey
  2.11 and predator 1.35, in the original population variables.
- Both populations are returned at the 27 assignment CSV times, and raw SSE
  is calculated from all 54 residuals in the same timed call.
- Imports, input loading, and a short warm-up including Numba compilation are
  outside the timer; prediction validation and SSE are inside it.
- Calls run sequentially on this MacBook, with a 300-second result deadline
  per warmed call and one measured call per rate and setting.
- There is no period folding in any of these calls.

The five vectors are positions 1–5 of the saved 50-point scrambled Halton design
with seed 612, scaled linearly to the assignment bounds. Regenerating all 50
with `qmc.Halton(d=4, scramble=True, rng=612)` gave an exact match. The older
`seed=` API produces a different scramble; reproduction should use the recorded
`rng=` call and SciPy version. All 50 rates were checked against the bounds.

The displayed rates are rounded; the saved manifest retains full precision.

| Halton position | $\theta_1$ | $\theta_2$ | $\theta_3$ | $\theta_4$ |
| ---: | ---: | ---: | ---: | ---: |
| 1 | 49.320387 | 1.751547 | 3.925601 | 0.997145 |
| 2 | 24.370387 | 1.088214 | 4.905601 | 1.281430 |
| 3 | 36.845387 | 0.424881 | 0.985601 | 0.712859 |
| 4 | 11.895387 | 1.972658 | 1.965601 | 0.428573 |
| 5 | 43.082887 | 1.309325 | 2.945601 | 1.565716 |

## Completed five-rate comparison

Mean and sample SD describe variation across completed rate cases, rather than
repeated runs at one vector. Failed and timed-out calls do not enter those
statistics. A failure is an error or invalid output; a timeout means the call
had not returned within 300 seconds. SD is undefined for one completed call.

### Ours · direct Numba

| Solver | Max step $h$ | Mean ± SD (s) | Completed | Failed | Timeouts |
| --- | ---: | ---: | ---: | ---: | ---: |
| Ours-RK4 | 1/128 | 5.815 ± 0.585 | 5 | 0 | 0 |
| Ours-RK4 | 1/256 | 11.965 ± 2.463 | 5 | 0 | 0 |
| Ours-RK4 | 1/512 | 22.631 ± 1.910 | 5 | 0 | 0 |
| Ours-RK8 | 1/128 | 36.809 ± 0.917 | 5 | 0 | 0 |
| Ours-RK8 | 1/256 | 75.785 ± 2.193 | 5 | 0 | 0 |

Here $h$ is the maximum step in the model's time units; reported runtimes are
wall-clock seconds. Both implementations use fixed steps that carry the state
forward through the requested outputs.

### SciPy · direct `solve_ivp`

| Solver | `rtol` | `atol` | Mean ± SD (s) | Completed | Failed | Timeouts |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| RK45 | 0.001 | 0.000001 | — | 0 | 0 | 5 |
| DOP853 | 0.001 | 0.000001 | — | 0 | 0 | 5 |
| LSODA | 0.001 | 0.000001 | 277.974 | 1 | 2 | 2 |

These are the installed API defaults, with no imposed maximum internal step.
The adaptive methods choose their own internal steps; the 27 CSV timestamps
specify outputs.

## Findings

- RK4 was faster than RK8 at matched steps in this check: about 5.8 versus
  36.8 seconds at 1/128, and 12.0 versus 75.8 seconds at 1/256.
- The implementations do different work per step: RK4 uses four derivative
  evaluations, while RK8 uses twelve and loops over its coefficient table.
- Smaller steps increased runtime; that cost alone does not establish how much
  numerical accuracy they gained over this long interval.
- LSODA completed only at Halton position 4, in 277.974 seconds, so its single
  completed time describes that case alone.
- At position 3, LSODA returned nonfinite populations with an overflow warning;
  at position 5, it reported `Unexpected istate in LSODA` with repeated error-test
  failures.
- The earlier SciPy times of roughly 96, 93, and 55 seconds used rates
  (1.62, 1, 2.11, 1), rather than these Halton vectors; the wrapper source,
  tolerances, package versions, initial state, and output times were unchanged.

The completed custom settings remain candidates for further comparison. Their
numerical accuracy still needs checking before choosing a fitting or BO scorer:
the independent review found substantial artificial damping in the first-rate
RK4 predictions, including at 1/512. Finite positive outputs and a finite SSE
establish completion, while the review's orbit diagnostic exposes a remaining
accuracy concern. The stored SSE is a data-fit score at the supplied rates.

## Cached step-halving check

After selecting Numba RK4 at $h=1/256$ provisionally, we compared its saved
predictions with the saved $h=1/512$ predictions. No additional solves were
needed. Each entry is the largest absolute change across the 27 CSV times,
in population units, rather than an error against a numerical reference.

| Halton position | Prey change | Predator change |
| ---: | ---: | ---: |
| 1 | 21.286 | 24.933 |
| 2 | 20.437 | 54.239 |
| 3 | 17.760 | 193.979 |
| 4 | 34.250 | 13.386 |
| 5 | 15.837 | 38.144 |

The predictions have not stabilized between these settings. A distribution of
SSE values at $h=1/256$ would describe the computed objective at that setting;
its numerical distortion remains a concern before using those scores for BO.

## Removed trials and code checks

The user removed 1/64 for both custom solvers after observed nonfinite-state
failures, and removed RK8 at 1/512 because of its runtime. The saved results from
those settings remain historical evidence and are absent from the main tables.
For RK8 at the first rate, a short diagnostic traced a negative population near
$t=9{,}722$, followed by overflow near $t=9{,}724$.

Two independent reviews found no mistake in the inspected equations, parameter
order, state coupling, RK stages, SciPy dispatch, or requested output times.
They found a zero-horizon wrapper bug and restart/accounting gaps. Both SciPy
wrappers now return the known populations for a singleton time-zero request.
The revised runner records elapsed time on worker crashes, checks resume
identity, preserves interrupted checkpoint bytes, and publishes tables
atomically. The wrapper/reader checks passed 10 tests with 29 subtests; the
recovery and amendment checks passed 21 tests.

The original run stopped after 43 recorded calls to apply the cancellations;
its unfinished rate-4 LSODA call is recorded separately as an interruption.
Nine missing retained calls then ran with the same frozen numerical source.
The final files contain 40 retained results plus 12 historical excluded results.
The original manifest and 43-record prefix were verified unchanged, along with
all saved successful predictions, SSE, and species RMSE values.

## Saved records and next decisions

The run used Python 3.12.12, NumPy 2.3.5, SciPy 1.17.0, and Numba 0.62.1 on an
ARM64 MacBook. Exact settings, versions, rates, and times are in the manifest.

- [Run instructions and scope change](../benchmarks/2026-11-19/direct-solvers-five-halton/README.md)
- [Individual calls and predictions](../benchmarks/2026-11-19/direct-solvers-five-halton/calls.jsonl)
- [Machine-readable summary](../benchmarks/2026-11-19/direct-solvers-five-halton/summary.csv)
- [Manifest](../benchmarks/2026-11-19/direct-solvers-five-halton/manifest.json) and [approved amendment](../benchmarks/2026-11-19/direct-solvers-five-halton/amendment.json)
- [Independent reviews and numerical diagnostic](../benchmarks/2026-11-19/direct-solvers-five-halton/review.md)
- [Read-only prediction lookup](../code/python/solver_results.py)
- [Decision ledger](decision-ledger.md)

Saved predictions can be reused for an exact matching solver request and
rescored if only the observations change. Their original wall times remain
historical measurements. The provisional choice for the next initialization
analysis is direct Numba RK4 at $h=1/256$. The user selected an
[accuracy-first refinement check](rk4-step-refinement.md) before completing
the remaining 45 initialization points.

## Default SciPy follow-up without a time limit

The user requested fresh RK45 and LSODA solves through `solve_ivp` at all five
of the same seed-612 rates, with no wall-time limit. Both use the API-default
tolerances `rtol=1e-3`, `atol=1e-6`, automatic internal steps without a step cap,
and the original population coordinates. The full objective timing and 27-time
workload match the earlier screen.

The run finishes both solvers at one rate before proceeding to the next and
saves every terminal result. Earlier timeouts remain historical evidence;
genuine numerical failures are still recorded as failures. Completion of a
default solve does not make its predictions a checked accuracy reference.

The user stopped this comparison on 2026-11-20 with four completed calls
preserved; the third RK45 call was interrupted without predictions. Its
[run record and cumulative tables](../benchmarks/2026-11-19/scipy-defaults-five-halton-no-limit/README.md)
retain the original settings and outcomes. The authorized fresh com2044
comparison uses the same five vectors and methods with 30 minutes per call;
see its [README.md](../benchmarks/2026-11-20/scipy-defaults-five-halton/README.md)
and [workstation storage note](workstation-experiment-storage.md).

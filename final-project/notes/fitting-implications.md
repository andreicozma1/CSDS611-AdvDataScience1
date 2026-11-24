# What the Lotka–Volterra fitting results imply

The assignment is feasible as a bounded least-squares problem. The lowest-SSE
checked fit found so far has an SSE of **495.69**, a **45.4% reduction** from the
best constant prediction for each species. The continuous model’s SSE is
at least **249.53** under the assignment’s initial conditions, rate bounds,
and observation times. This rules out an exact match to the instructor’s CSV
and leaves a gap of **246.16 SSE** between the lower bound and the checked
fit. [Fit quality](fit-quality.md) · [Lower-bound calculation](sse-lower-bounds.md)

## What the diagnostic tests establish

- **Orbit shape and timing matter separately.** For one candidate orbit,
  matching each observed pair to its nearest point on the curve gave
  **1.33 SSE**. The best timed candidate in the saved scan of that shape
  gave **732.95 SSE**. The gap shows how much the observation times matter
  even when the population pairs lie close to the same orbit.
  [Nearest-point comparison](trajectory-diagnostics.md#nearest-point-on-a-fixed-orbit)
- **Shifting whole blocks explains little at the checked fit.** On the orbit
  and period of the **495.69** fit, independently shifting the three observation
  blocks reduced SSE by only **0.17**. This tests a constant shift within
  each block on that particular orbit and period.
  [Block-offset results](trajectory-diagnostics.md#phase-offsets-for-the-three-observation-blocks)
- **An archived synthetic diagnostic illustrates rate ambiguity.** Giving the
  synthetic fitter the true rate ratios and using a phase-guided search
  brought SSE below $1.5\times10^{-9}$ on all 18 tested period-folded RK4 and
  RK8 datasets. In the interior-draw case, different rates produced nearly
  identical sampled populations because the fitted trajectory completed
  1,885 fewer whole cycles per 5,000 time units and every observation time
  was a multiple of 5,000. [Known-ratio fits and sampling aliasing](../benchmarks/archived-synthetic-recovery/known-rate-ratios.md#fitting-synthetic-data-with-known-rate-ratios)

## What MATLAB may explain

Default MATLAB `ode45` controls estimated local error per step. The requested
output times and integration endpoints can affect the internal steps it takes.
On long oscillating trajectories, small timing errors can accumulate. In the
synthetic midpoint case, default `ode45` and the checked continuous trajectory
at the **same generating rates** differed by **26,704.61 SSE** at the 27 output
times. All nine MATLAB-generated CSVs also replayed at zero SSE with their own
rates and settings. Together these results show how using a different solver
can change the fitting target. The instructor’s exact generation setup is
unknown, so the fraction of the assignment CSV’s mismatch attributable to the
solver remains open. [MATLAB tolerance options](https://www.mathworks.com/help/matlab/ref/odeset.html)
· [MATLAB time-span behavior](https://www.mathworks.com/help/matlab/ref/ode45.html)
· [Generator errors](../benchmarks/archived-synthetic-recovery/blind-solver-recovery/tolerance-study/generator.csv)
· [Matched replay records](../benchmarks/archived-synthetic-recovery/blind-solver-recovery/tolerance-study/matched-results-v2/datasets.json)

## Priorities for the assignment and further tests

1. **Check the objective before increasing the search budget.** At the same
   fitted rates, direct RK4 with step `1/1024` gave **1,039.07 SSE** and the
   checked trajectory gave **495.69**. Verify the solver at representative
   in-bounds rates and rescore finalists with one checked evaluator. For
   Step 1, time one complete Runge–Kutta objective evaluation, including
   the calculation of SSE. [Solver comparison](../benchmarks/2026-11-17/objective-comparison/README.md)
   · [Step 1 handout](../project_step_1.pdf)
2. **Compare a blind shape-and-phase search with the existing optimizers.**
   Estimate the orbit shape from the paired populations, scan for a common
   sampling phase, and refine against the original timestamps within the
   assignment bounds. Count the cost of the phase scan when comparing
   methods. Report total SSE, both species’ RMSEs, and any alternative rate
   vectors that give equivalent predictions.
The [synthetic recovery study](../benchmarks/archived-synthetic-recovery/README.md)
is archived; its proposed follow-ups are outside the current assignment work.

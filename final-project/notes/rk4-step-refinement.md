# RK4 step refinement

## Question and comparison

How much do the predicted populations change when we halve RK4's step, and
how much additional runtime does each halving cost?

Use the same five seed-612 scrambled Halton rate vectors as the
[direct timing comparison](direct-solver-timing.md), all within the assignment
bounds. Start at $(2.11,1.35)$ at time zero, integrate directly through
$2{,}960{,}000$, and return both populations at the 27 CSV times.

The selected ladder is

$$
h\in\left\{\frac1{128},\frac1{256},\frac1{512},
\frac1{1024},\frac1{2048}\right\}.
$$

The first three levels reuse saved predictions and timings. The last two add
ten calls in total, one per rate vector and step size, on the same MacBook
with the same frozen numerical code and library versions. Each new call has
a 300-second limit after warm-up. Run all five cases at $1/1024$ before
continuing to $1/2048$.

For consecutive levels, calculate

$$
\Delta_x(h)=\max_{i=1,\ldots,27}|x_{h/2}(t_i)-x_h(t_i)|,
\qquad
\Delta_y(h)=\max_{i=1,\ldots,27}|y_{h/2}(t_i)-y_h(t_i)|.
$$

These are changes between computed solutions, in population units. The CSV
supplies the observation times; its measured populations are not the accuracy
comparator. They enter only the raw SSE calculation inside the timed objective.

## Figures and interpretation

- Show five individual curves, with prey and predator in separate panels.
- Compare consecutive halvings, rather than comparing every level with a
  finest run whose accuracy has not been established.
- Show objective time against $\max(\Delta_x,\Delta_y)$ in a second figure.
- Include a step size only when all five cases return finite positive predictions.
- Keep failed records, but omit a halving pair if either level is ineligible.

Smaller changes under successive halvings would support convergence on these
five cases. Small changes alone can be misleading if two coarse runs have
both damped the oscillations, so also inspect the conserved quantity

$$
H(x,y)=\theta_3\left(\frac{x}{x_*}-1-\log\frac{x}{x_*}\right)
+\theta_1\left(\frac{y}{y_*}-1-\log\frac{y}{y_*}\right),
\qquad x_*=\frac{\theta_3}{\theta_4},\quad
y_*=\frac{\theta_1}{\theta_2}.
$$

The saved diagnostic is the maximum change in $H$ at the observation times,
divided by its initial value. Preserving $H$ does not by itself check
oscillation timing.

Timing includes the full objective wrapper, output validation, and raw SSE;
imports, compilation, comparisons, and plotting are outside the timer. Mean
and sample SD, when shown, describe variation across these five rate vectors.
There is one timing per case and setting.

## Results

All ten new calls completed. Every level in the selected ladder has five
completed cases, with no failures or timeouts. The new timed objective calls
totaled 676.813 seconds; setup and figure generation were additional.

### Runtime

| Maximum step $h$ | Objective time (s), mean ± sample SD | Completed |
| --- | ---: | ---: |
| 1/128 | 5.815 ± 0.585 | 5/5 |
| 1/256 | 11.965 ± 2.463 | 5/5 |
| 1/512 | 22.631 ± 1.910 | 5/5 |
| 1/1024 | 48.028 ± 3.715 | 5/5 |
| 1/2048 | 87.334 ± 4.524 | 5/5 |

The first three rows reuse the original timings; the last two were measured
in this extension on the same host, frozen numerical source, and runtime.
Each mean and SD summarize one call at each of the five rate vectors.

### Changes between consecutive steps

Each cell below is a maximum absolute prediction change across the 27 times,
in population units.

**Prey, $\Delta_x$**

| Case | 128 → 256 | 256 → 512 | 512 → 1024 | 1024 → 2048 |
| --- | ---: | ---: | ---: | ---: |
| 1 | 4.765 | 21.286 | 49.460 | 114.667 |
| 2 | 10.000 | 20.437 | 24.195 | 45.530 |
| 3 | 17.220 | 17.760 | 96.724 | 96.724 |
| 4 | 21.926 | 34.250 | 34.421 | 34.429 |
| 5 | 4.170 | 15.837 | 46.368 | 48.390 |

**Predator, $\Delta_y$**

| Case | 128 → 256 | 256 → 512 | 512 → 1024 | 1024 → 2048 |
| --- | ---: | ---: | ---: | ---: |
| 1 | 13.634 | 24.933 | 74.250 | 104.162 |
| 2 | 25.602 | 54.239 | 54.686 | 45.723 |
| 3 | 79.480 | 193.979 | 425.118 | 481.758 |
| 4 | 10.743 | 13.386 | 14.079 | 14.711 |
| 5 | 19.973 | 38.144 | 92.703 | 126.023 |

The headers give step denominators: 128 → 256 means comparing $h=1/128$
with $h=1/256$. The changes do not taper down across this ladder. For the
final halving, only the predator change in case 2 is smaller than for the
preceding pair; the other changes grow or remain nearly unchanged.

### Conserved quantity

Every sampled value of $H$ lies below its initial value. The table shows
the maximum relative loss in $H$ across the 27 times, as a percentage.

| Maximum step $h$ | Case 1 (%) | Case 2 (%) | Case 3 (%) | Case 4 (%) | Case 5 (%) |
| --- | ---: | ---: | ---: | ---: | ---: |
| 1/128 | 99.9997 | 99.4515 | 99.0839 | 71.1634 | 99.8749 |
| 1/256 | 98.5306 | 92.8007 | 95.7474 | 21.2029 | 97.7134 |
| 1/512 | 93.0083 | 70.0322 | 81.1693 | 1.7596 | 89.7219 |
| 1/1024 | 69.9142 | 19.5694 | 37.0402 | 0.1103 | 57.9778 |
| 1/2048 | 19.3981 | 1.5513 | 4.0499 | 0.0068 | 10.8489 |

Refinement reduces this loss for every case, but at $h=1/2048$ case 1
still loses about 19.4% and case 5 about 10.8%. The smaller differences
between coarse predictions therefore do not indicate greater accuracy:
their substantial loss of $H$ shows numerical damping toward equilibrium.
Finer steps preserve the orbit better, while the requested predictions
remain sensitive to the step size. This check does not separate timing
differences from changes in oscillation amplitude.

### Figures

**RK4 step-halving changes.** Maximum changes in prey and predator predictions
at the 27 observation times, shown separately for the five seed-612 cases.

![RK4 step-halving changes](/Users/acozma/GitHub/CSDS611-AdvDataScience1/final-project/benchmarks/2026-11-19/rk4-step-refinement/figures/01-rk4-step-changes--five-cases--v01.png)

**RK4 runtime and prediction change.** For each halving, time is the finer
objective call and change is the larger of the two population changes.

![RK4 runtime and prediction change](/Users/acozma/GitHub/CSDS611-AdvDataScience1/final-project/benchmarks/2026-11-19/rk4-step-refinement/figures/02-rk4-runtime-change--five-cases--v01.png)

### Decision still open

No tested step has established stable full-interval predictions across
these five cases. Keep $h=1/256$ provisional; the remaining 45 initial
design scores and subsequent BO runs have not been launched.

### Verification

Replayed the analysis without ODE calls and reconciled all ten new and
15 reused records. Checked unique call IDs, positive finite $(27,2)$
predictions, exact rates and CSV times, recomputed SSE/RMSE, and unchanged
original evidence. Focused checks also covered the all-five eligibility
rule, exclusion of failed levels, and rejection of nonfinite completed
outputs. Both rendered figures passed geometry and raster checks and were
visually inspected for labels, clipping, legends, and spacing.

## Audit of the increasing differences

The follow-up audit found no defect in the inspected RK4 stages, coupled
derivatives, state carryover, step partition, or comparison indexing. All 25
saved RK4 records match their rates, observation grid, source hashes, and
settings. Independently recomputing all 40 species-specific differences gave
the saved values exactly. Every observation gap is an integer multiple of
the requested binary step size, so the effective step equals the requested
step throughout this ladder. The compiled counts are 64-bit.

A short diagnostic over $t=0$ to $1$, at all five rate vectors and step sizes,
checked the numerical update separately from long-interval accumulation:

- Plain Python and Numba predictions were bitwise equal.
- A separately written array-valued RK4 calculation agreed within
  $2.28\times10^{-13}$ population units.
- On the last halving, errors against a tightly resolved short DOP853 solution
  fell by factors of 15.5 to 18.3 across the two species and five cases.
- Tightening that short reference changed its predictions by at most
  $2.23\times10^{-11}$ population units; each change was below the
  corresponding RK4 error for that case and species.

The short check took about one second and did not repeat any full-interval
integration. It checks the implementation and its small-step behavior on the
short interval; it does not establish full-interval accuracy.

The larger long-interval changes have two visible contributors:

1. **Damping.** At the final time, case 1 retains 0.00034%, 1.47%, 6.99%,
   30.09%, and 80.60% of initial $H$ as the step is refined from $1/128$ to
   $1/2048$. Two coarse solutions can look similar because both have lost much
   of their oscillation. A finer solution retains more of the orbit and can
   differ more from its coarser neighbor.
2. **Position within the oscillation.** In case 4 at $t=2{,}840{,}000$, the
   two finest RK4 runs predict prey values of 34.4484 and 0.0195, although
   they retain 99.894% and 99.993% of initial $H$. Nearly matching the orbit
   level does not make the populations match at a particular time.

An independent read-only scientific review agreed with these findings. It
also compared saved direct RK8 refinements: some cases still disagree
substantially despite good invariant preservation. Those RK8 predictions are
not a checked full-interval reference. The true prediction-error ranking and
the size and direction of phase error remain unresolved.

The comparison arithmetic is valid, but the increasing adjacent-step changes
cannot show that finer steps are less accurate. No new solver setting was
adopted and no further full-interval run was launched.

- [Short-check results and independent invariant recomputation](../benchmarks/2026-11-19/rk4-step-refinement/audit.json)
- [Numerical stability and the distinction between fixed-interval convergence and long-time behavior](https://fncbook.com/julia/absstab-diffusion/)

## Reproduction and evidence

- [Run, resume, and plotting instructions](../benchmarks/2026-11-19/rk4-step-refinement/README.md)
- [Exact inputs and source/runtime identity](../benchmarks/2026-11-19/rk4-step-refinement/manifest.json)
- [New calls and predictions](../benchmarks/2026-11-19/rk4-step-refinement/calls.jsonl)
- [Combined analysis](../benchmarks/2026-11-19/rk4-step-refinement/analysis.json)
- [Decisions](decision-ledger.md)

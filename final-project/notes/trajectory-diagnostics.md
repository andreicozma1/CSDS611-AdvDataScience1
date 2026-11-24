# Diagnosing orbit shape and timing

A Lotka–Volterra fit must match both the curve traced by prey and predator
and the position on that curve at each observation time. The **orbit** is the
curve in the prey–predator plane. The **phase** is the fraction of a period
elapsed along that orbit from the required initial populations $(2.11,1.35)$.
The score is the sum of squared errors (SSE) across both populations at the
27 observation times.

## Nearest point on a fixed orbit

One diagnostic gives each observed prey–predator pair the closest point on a
single candidate orbit. Each pair can choose its own phase. For the same
orbit, a second calculation varies the speed and evaluates one trajectory
from time zero at all 27 observation times.

| How points were selected on the same orbit | SSE |
| --- | ---: |
| Nearest point to each observed pair | **1.33** |
| Best timed candidate in the saved phase scan | **732.95** |

The comparison shows that the shape alone can account for the observed
population pairs much better than the timed candidates on that orbit.
The nearest-point score measures distance to the curve. It is also influenced
by which orbit was chosen. The timed score is the best found by the saved
finite scan for that particular shape. [Saved orbit and phase scan](../benchmarks/2026-11-13/deeper-orbit-search/projection/shape-prey-box.json)

## Phase offsets for the three observation blocks

Allowing one phase offset per block reduced total SSE from **495.688 to
495.519**, a **0.034%** improvement on the checked fit. The orbit and period
were fixed throughout.

### Method

The baseline uses the checked fit’s rates
$(11.4529671670, 2, 0.1, 0.5902581544)$ and period $P=26.7415874326$.
The original prediction uses the orbit at $t\bmod P$. For each block,
the adjusted prediction uses $(t+\Delta)\bmod P$, where one offset $\Delta$
minimizes the block’s SSE across both populations. The shift preserves the
spacing between every pair of observations within the block.
[Assignment data](../LV_data.csv) · [Checked fit and period](../benchmarks/2026-11-13/adaptive-phase-scan/branch-17-186.json)

The search scanned a full cycle at grids of 32,768 and 131,072 points and
refined the detected minima. The two resolutions and the cross-check with a
second integrator gave the same block SSEs to within $10^{-7}$.

### Results

Each pair of values shows the original prediction followed by the prediction
with a block offset. Overall RMSE is computed across all 27 observations for
each species.

| Observation times | Pairs | SSE before → after | Prey RMSE before → after | Predator RMSE before → after |
| --- | ---: | ---: | ---: | ---: |
| 700,000–895,000 | 14 | 328.451 → 328.315 | 3.369 → 3.369 | 3.480 → 3.479 |
| 1,350,000–1,500,000 | 6 | 37.130 → 37.108 | 0.330 → 0.308 | 2.466 → 2.468 |
| 2,600,000–2,960,000 | 7 | 130.106 → 130.096 | 0.554 → 0.537 | 4.275 → 4.277 |
| **Overall** | **27** | **495.688 → 495.519** | **2.448 → 2.445** | **3.517 → 3.518** |

The offsets were $+0.01497$, $+0.00118$, and $-0.00100$ time units,
respectively. The small changes indicate that shifts between observation
blocks explain little of the remaining error at this orbit and period.
Overall prey RMSE improved slightly and predator RMSE increased slightly.

## Archived synthetic diagnostic

The [known-rate-ratio fits](../benchmarks/archived-synthetic-recovery/known-rate-ratios.md)
are retained with the archived synthetic study, outside the assignment comparison.

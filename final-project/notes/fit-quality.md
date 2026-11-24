# Interpreting fit error

On the instructor’s Lotka–Volterra dataset, the best checked fit has an SSE of
**495.69**, a **45.4% reduction** from predicting each species’ observed mean
at every time. The improvement is larger for predator, and a few substantial
misses still account for most of the total error.

## SSE and RMSE

The CSV contains one prey and one predator observation at each of 27 times.
Let $e_{x,i}$ and $e_{y,i}$ be the predicted minus observed populations at
time $t_i$. The sum of squared errors (SSE) and the species-specific root mean
squared errors (RMSEs) are

$$
\mathrm{SSE} = \sum_{i=1}^{27} \big(e_{x,i}^2 + e_{y,i}^2\big), \qquad
\mathrm{RMSE}_x = \sqrt{\frac{1}{27}\sum_{i=1}^{27}e_{x,i}^2}, \qquad
\mathrm{RMSE}_y = \sqrt{\frac{1}{27}\sum_{i=1}^{27}e_{y,i}^2}.
$$

SSE is the fitting objective. RMSE expresses the error in the original
population units. The RMSE pooled across both species is
$\sqrt{\mathrm{SSE}/54}$. [Assignment data](../LV_data.csv) · [Step 1 handout](../project_step_1.pdf)

## Constant-prediction baselines

A constant predictor returns the same population value at every timestamp.
For one species with observations $z_1,\ldots,z_{27}$, the SSE at any constant
$c$ is

$$
\sum_{i=1}^{27}(z_i-c)^2
= \sum_{i=1}^{27}(z_i-\bar z)^2 + 27(c-\bar z)^2.
$$

The first term is fixed and the second is smallest at $c=\bar z$. Applying
this to each species gives the first row below. Each SSE uses the unrounded
constants.

| Constant prediction | Prey | Predator | Total SSE |
| --- | ---: | ---: | ---: |
| Mean of each species | 1.9315 | 5.7472 | **907.38** |
| One mean across all 54 values | 3.8394 | 3.8394 | 1,103.94 |
| Lotka–Volterra equilibrium at the required initial populations | 2.1100 | 1.3500 | 1,430.31 |

The separate-means baseline measures how much a fit improves on the best
constant predictions for these observations. A constant model trajectory that
starts at time zero is fixed at the given initial populations. It is attainable
with in-bounds rates $(1.35,1,2.11,1)$. [Data](../LV_data.csv) · [Model and rate bounds](../lotka-volterra-objective.md#1-set-up-the-problem-and-the-loss)

## What the scores mean on the instructor’s CSV

| Prediction | Raw SSE | Pooled RMSE | SSE reduction vs. separate means |
| --- | ---: | ---: | ---: |
| Separate species means | 907.38 | 4.10 | 0% |
| Example score of 900 | 900.00 | 4.08 | 0.8% |
| Best checked fit | 495.69 | 3.03 | 45.4% |

For the checked fit, prey RMSE falls from **2.87 to 2.45** and predator RMSE
from **5.04 to 3.52**, relative to the separate means. Roughly **71%** of the
fit’s total SSE comes from five of the 27 timestamps. At $t=730{,}000$, for
example, observed prey was **9.02** and the predicted value was effectively
zero. [Saved fit and predictions](../benchmarks/2026-11-13/adaptive-phase-scan/summary.json)

## Comparing results across rates and datasets

- **Changing the fitted rates** changes the predicted oscillations on a fixed
  dataset. The observations and the constant baseline stay fixed.
- **Changing the generating rates** in a synthetic experiment changes the
  observations and their spread. Using the same period-folded RK8 solver, the
  constant baseline SSE was about **8,211** for the lower-bound rate vector
  and **152,930** for the interior draw. [Lower-bound case](../benchmarks/archived-synthetic-recovery/blind-solver-recovery/tolerance-study/data/lower-rk8-folded.csv) · [Interior case](../benchmarks/archived-synthetic-recovery/blind-solver-recovery/tolerance-study/data/draw-rk8-folded.csv)
- **Changing the units or number of observations** also changes raw SSE.
  RMSE accounts for the number of residuals and still depends on the
  population scale. For comparisons across CSVs, report each species’ RMSE
  and the SSE reduction against that CSV’s own constant baseline.

The constant baseline and the [global SSE bound](sse-lower-bounds.md) answer
different questions about fit quality. An absolute threshold for acceptable
error would require a practical tolerance or evidence about the expected
measurement and numerical errors in the observations.

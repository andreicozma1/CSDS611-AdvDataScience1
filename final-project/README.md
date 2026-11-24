# CSDS 611 Final Project

The final project is a group implementation of Bayesian optimization on an
instructor-selected benchmark. The work progresses from setting up the objective
to fitting a surrogate and running the optimization loop.

- [Code (GitHub submodule)](code/) contains the Python and MATLAB
  implementations, saved results, and reproduction instructions.
- [Report (Overleaf submodule)](report/) contains the LaTeX source and figures.
  The report starts at [main.tex](report/main.tex).
- [Direct solver timing notes](notes/direct-solver-timing.md) contain the
  five-rate Python comparison, completion counts, and findings.
- [RK4 step refinement](notes/rk4-step-refinement.md) compares prediction
  changes under step halving with the additional runtime.

## Bayesian optimization results

- [Bayesian optimization method and current settings](notes/bayesian-optimization.md)
- [Search over the full rate bounds](benchmarks/bo-progress/full-rate-bounds/README.md) — results using the professor's CSV.
- [Archived synthetic recovery study](benchmarks/archived-synthetic-recovery/README.md) — generated datasets, scripts, and results; excluded from active work.

The assignment-CSV comparison tests one Matérn BO configuration against
continued Halton and independent uniform sampling. Earlier rankings of GP
settings and acquisition functions used a fixed list of follow-up rates.
[Full-bounds results](benchmarks/2026-11-17/bo-full-bounds/README.md) · [Which archived conclusions change](benchmarks/archived-fixed-pool-4096/README.md#which-conclusions-change)

## Parameter fitting notes

- [What the Lotka–Volterra fitting results imply](notes/fitting-implications.md)
- [Interpreting fit error](notes/fit-quality.md)
- [Lower bounds on the Lotka–Volterra fit](notes/sse-lower-bounds.md)
- [Diagnosing orbit shape and timing](notes/trajectory-diagnostics.md)

## Schedule

| Date | Work planned in the November 10 briefing |
| --- | --- |
| Thu, Nov 12 | First part on Canvas. Set up the objective, check the code, and visualize the problem. |
| Tue, Nov 17 | Set up the surrogate, choose and fit kernel parameters, and select the initial design. |
| Thu, Nov 19 | Implement the Bayesian optimization rule. |
| Fourth meeting, if needed | Work on the report. |

The report is due after Thanksgiving. The November 5 lecture mentioned both
the Tuesday after Thanksgiving (December 1) and December 3. Check Canvas for
the exact deadline. [November 5 transcript, 00:03:58–00:04:21](../lectures/2026-11-05_13D4A044.scribe-v3.md)
· [November 10 transcript, 00:00:40–00:02:15](../lectures/2026-11-10_8F5F2BB7.scribe-v3.md)

## What we know

- The syllabus calls for **one typed PDF per group of 2–3 students**. The project
  is worth **40%** of the course grade. [Syllabus, p. 3](../CSDS_611_syllabus.pdf#page=3)
- The lecture setup uses a real-valued scalar objective over a bounded search
  space. A Gaussian-process surrogate guides the choice of new evaluation
  points. [Lecture 20, slides 2–6](<../lectures/CSDS 611 - Lecture 20 - Bayesian Optimization - Surrogates.pdf>)
- Steps 1 and 2 specify a least-squares objective over four continuous rate
  intervals, about 50 initial space-filling queries, an assessment of raw versus
  log objective values, and GP hyperparameter fitting on the initial data.
  [Step 2 handout](project_step_2.pdf)
- Each group member is expected to contribute. The professor allows AI as an aid
  alongside the group's own work. [November 5, 00:02:43–00:03:33](../lectures/2026-11-05_13D4A044.scribe-v3.md)
  · [October 13, 00:00:00–00:01:22](../lectures/2026-10-13_09627C3C.scribe-v3.md)

## Details to confirm on Canvas

- Any required follow-up budget, kernels, acquisition rules, or comparisons.
- Required plots, report format or length, and any separate code or presentation deliverables.

## Lecture references

| Reference | Topic |
| --- | --- |
| [Lecture 19, slides 2–5](<../lectures/CSDS 611 - Lecture 19 - Implementing Gaussian Process Regression.pdf>) | GP predictions and efficient Cholesky updates. |
| [Lecture 20, slides 2–6](<../lectures/CSDS 611 - Lecture 20 - Bayesian Optimization - Surrogates.pdf>) | Objective, surrogate, initial design, and optimization loop. |
| [Lecture 21, slides 3–10](<../lectures/CSDS 611 - Lecture 21 - Bayesian Optimization - Acquisition Functions.pdf>) | Acquisition rules and the setup for the worked example. |
| [November 10, 00:48:08 onward](../lectures/2026-11-10_8F5F2BB7.scribe-v3.md) | Worked example with a running best-value plot. |

See the [lecture and recording index](../lectures/README.md) for the full collection.

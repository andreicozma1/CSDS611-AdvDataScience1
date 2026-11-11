# CSDS 611 lecture materials

This directory contains the Fall 2026 lecture slides and their Markdown
transcriptions, plus the Goodnotes recordings and their Scribe v3 transcripts.

[Slides by lecture](#slides-by-lecture) · [Recordings by date](#recordings-by-date)

## Slides by lecture

Use Markdown to search the decks. Use the original PDF to check equations,
figures, and slide numbers. The [lecture library](https://app.notion.com/p/341ee83111d3494594a421e2221c95fb)
has detailed outlines and slide references.

| Lecture | Presentation title | Topics covered | Files |
| --- | --- | --- | --- |
| 02 | BO preliminaries | Bayesian optimization loop, exploration versus exploitation, acquisition functions | [PDF](<CSDS 611 - Lecture 02 - Bayesian Optimization Preliminaries.pdf>) · [Markdown](<CSDS 611 - Lecture 02 - Bayesian Optimization Preliminaries.md>) |
| 03 | Uncertain quantities of interest | Random variables, statistical notation, probability rules, joint distributions | [PDF](<CSDS 611 - Lecture 03 - Uncertain Quantities of Interest.pdf>) · [Markdown](<CSDS 611 - Lecture 03 - Uncertain Quantities of Interest.md>) |
| 04 | Intro Bayes | Priors, likelihoods, Bayes’ theorem, models with multiple quantities, Bayesian workflow | [PDF](<CSDS 611 - Lecture 04 - Introduction to Bayes.pdf>) · [Markdown](<CSDS 611 - Lecture 04 - Introduction to Bayes.md>) |
| 05 | Random variables | Non-Gaussian discrete and continuous distributions, including binomial, Poisson, beta, gamma, and Student’s t | [PDF](<CSDS 611 - Lecture 05 - Non-Gaussian Random Variables.pdf>) · [Markdown](<CSDS 611 - Lecture 05 - Non-Gaussian Random Variables.md>) |
| 06 | Gaussian random scalars | Univariate normal simulation, transformations, credible intervals, Bayesian inference | [PDF](<CSDS 611 - Lecture 06 - Gaussian Random Scalars.pdf>) · [Markdown](<CSDS 611 - Lecture 06 - Gaussian Random Scalars.md>) |
| 07 | Gaussian random vectors | Multivariate normal simulation, linear transformations, covariance factorizations and square roots | [PDF](<CSDS 611 - Lecture 07 - Gaussian Vectors - Transformations and Covariance Factors.pdf>) · [Markdown](<CSDS 611 - Lecture 07 - Gaussian Vectors - Transformations and Covariance Factors.md>) |
| 08 | Gaussian random vectors | Independence, marginal and conditional distributions, whitening, sequential updates, credible ellipses | [PDF](<CSDS 611 - Lecture 08 - Gaussian Vectors - Conditioning and Credible Ellipses.pdf>) · [Markdown](<CSDS 611 - Lecture 08 - Gaussian Vectors - Conditioning and Credible Ellipses.md>) |
| 09 | Bayesian hypothesis tests | Categorical data, spam detection, binary and general tests, uncertain model parameters | [PDF](<CSDS 611 - Lecture 09 - Bayesian Hypothesis Tests.pdf>) · [Markdown](<CSDS 611 - Lecture 09 - Bayesian Hypothesis Tests.md>) |
| 10 | The exponential family | Exponential-family models, conjugate updates, hypothesis testing, signal detection | [PDF](<CSDS 611 - Lecture 10 - The Exponential Family.pdf>) · [Markdown](<CSDS 611 - Lecture 10 - The Exponential Family.md>) |
| 11 | Bayesian decision theory | Actions and losses, posterior expected loss, posterior mean, median, and mode as point estimates | [PDF](<CSDS 611 - Lecture 11 - Bayesian Decision Theory.pdf>) · [Markdown](<CSDS 611 - Lecture 11 - Bayesian Decision Theory.md>) |
| 12 | Applied decision problems | Clinical decisions with missing test information, recommendation systems | [PDF](<CSDS 611 - Lecture 12 - Applied Decision Problems.pdf>) · [Markdown](<CSDS 611 - Lecture 12 - Applied Decision Problems.md>) |
| 13 | Linear regression | Basis functions, ordinary and ridge least squares, Bayesian regression | [PDF](<CSDS 611 - Lecture 13 - Linear Regression.pdf>) · [Markdown](<CSDS 611 - Lecture 13 - Linear Regression.md>) |
| 14 | Model selection | Comparing regression models, model priors, marginal likelihood, posterior model probabilities | [PDF](<CSDS 611 - Lecture 14 - Model Selection.pdf>) · [Markdown](<CSDS 611 - Lecture 14 - Model Selection.md>) |
| 15 | Predictions | Posterior predictive distributions, joint predictions, Bayesian model averaging | [PDF](<CSDS 611 - Lecture 15 - Posterior Prediction.pdf>) · [Markdown](<CSDS 611 - Lecture 15 - Posterior Prediction.md>) |
| 16 | Kernel regression | Basis functions in Bayesian linear regression, covariance functions, kernels | [PDF](<CSDS 611 - Lecture 16 - Kernel Regression.pdf>) · [Markdown](<CSDS 611 - Lecture 16 - Kernel Regression.md>) |
| 17 | Gaussian processes | From kernel regression to Gaussian process priors, finite collections of function values | [PDF](<CSDS 611 - Lecture 17 - Gaussian Processes.pdf>) · [Markdown](<CSDS 611 - Lecture 17 - Gaussian Processes.md>) |
| 18 | Gaussian processes regression | Gaussian process regression, posterior mean and covariance, squared exponential kernel | [PDF](<CSDS 611 - Lecture 18 - Gaussian Process Regression.pdf>) · [Markdown](<CSDS 611 - Lecture 18 - Gaussian Process Regression.md>) |
| 19 | Implementation of Gaussian processes regression | Cholesky factorization and updates, predictive statistics, noise, periodic, and diffusion kernels | [PDF](<CSDS 611 - Lecture 19 - Implementing Gaussian Process Regression.pdf>) · [Markdown](<CSDS 611 - Lecture 19 - Implementing Gaussian Process Regression.md>) |
| 20 | BO | Bayesian optimization with probabilistic surrogates | [PDF](<CSDS 611 - Lecture 20 - Bayesian Optimization - Surrogates.pdf>) · [Markdown](<CSDS 611 - Lecture 20 - Bayesian Optimization - Surrogates.md>) · [Notion](https://app.notion.com/p/415f723fb8cc818a8085c9a2ca6c0aa3) |
| 21 | BO | Acquisition functions, including confidence bounds, improvement criteria, and Thompson sampling | [PDF](<CSDS 611 - Lecture 21 - Bayesian Optimization - Acquisition Functions.pdf>) · [Markdown](<CSDS 611 - Lecture 21 - Bayesian Optimization - Acquisition Functions.md>) · [Notion](https://app.notion.com/p/415f723fb8cc81ca83b2d596748d0725) |

Lecture 17’s title is shown with its spelling corrected.

## Recordings by date

Select a date to open the audio. Each recording has a readable Markdown
transcript and the original Scribe v3 JSON with word timestamps. The
[review log](transcript-review.md) records uncertain wording, speaker labels,
and technical corrections. The [glossary](transcription-glossary.md) lists the
keyterms used during transcription.

Dates use Eastern time. The mapping to numbered slide decks is unverified,
and some recordings may cover part of a class.

| Recording date | Playback duration | Transcript |
| --- | ---: | --- |
| [2026-08-20](2026-08-20_FB8DE074.m4a) | 66:23 | [Markdown](2026-08-20_FB8DE074.scribe-v3.md) · [Timed JSON](2026-08-20_FB8DE074.scribe-v3.json) |
| [2026-08-25](2026-08-25_3D786893.m4a) | 64:46 | [Markdown](2026-08-25_3D786893.scribe-v3.md) · [Timed JSON](2026-08-25_3D786893.scribe-v3.json) |
| [2026-08-27](2026-08-27_0A2DB600.m4a) | 58:16 | [Markdown](2026-08-27_0A2DB600.scribe-v3.md) · [Timed JSON](2026-08-27_0A2DB600.scribe-v3.json) |
| [2026-09-01](2026-09-01_D708E20C.m4a) | 67:01 | [Markdown](2026-09-01_D708E20C.scribe-v3.md) · [Timed JSON](2026-09-01_D708E20C.scribe-v3.json) |
| [2026-09-03](2026-09-03_C995A7EF.m4a) | 59:27 | [Markdown](2026-09-03_C995A7EF.scribe-v3.md) · [Timed JSON](2026-09-03_C995A7EF.scribe-v3.json) |
| [2026-09-08](2026-09-08_FE79D51A.m4a) | 66:58 | [Markdown](2026-09-08_FE79D51A.scribe-v3.md) · [Timed JSON](2026-09-08_FE79D51A.scribe-v3.json) |
| [2026-09-10](2026-09-10_349E6F2E.m4a) | 65:44 | [Markdown](2026-09-10_349E6F2E.scribe-v3.md) · [Timed JSON](2026-09-10_349E6F2E.scribe-v3.json) |
| [2026-09-17](2026-09-17_0EF7DF90.m4a) | 61:11 | [Markdown](2026-09-17_0EF7DF90.scribe-v3.md) · [Timed JSON](2026-09-17_0EF7DF90.scribe-v3.json) |
| [2026-09-22](2026-09-22_0C09C6AA.m4a) | 48:10 | [Markdown](2026-09-22_0C09C6AA.scribe-v3.md) · [Timed JSON](2026-09-22_0C09C6AA.scribe-v3.json) |
| [2026-09-24](2026-09-24_2C2C7B9F.m4a) | 76:26 | [Markdown](2026-09-24_2C2C7B9F.scribe-v3.md) · [Timed JSON](2026-09-24_2C2C7B9F.scribe-v3.json) |
| [2026-09-29](2026-09-29_17950960.m4a) | 60:43 | [Markdown](2026-09-29_17950960.scribe-v3.md) · [Timed JSON](2026-09-29_17950960.scribe-v3.json) |
| [2026-10-01](2026-10-01_9A3E8C58.m4a) | 51:14 | [Markdown](2026-10-01_9A3E8C58.scribe-v3.md) · [Timed JSON](2026-10-01_9A3E8C58.scribe-v3.json) |
| [2026-10-08](2026-10-08_52291E85.m4a) | 60:12 | [Markdown](2026-10-08_52291E85.scribe-v3.md) · [Timed JSON](2026-10-08_52291E85.scribe-v3.json) |
| [2026-10-13](2026-10-13_09627C3C.m4a) | 58:25 | [Markdown](2026-10-13_09627C3C.scribe-v3.md) · [Timed JSON](2026-10-13_09627C3C.scribe-v3.json) |
| [2026-10-27](2026-10-27_0AF31E51.m4a) | 53:54 | [Markdown](2026-10-27_0AF31E51.scribe-v3.md) · [Timed JSON](2026-10-27_0AF31E51.scribe-v3.json) |
| [2026-10-29](2026-10-29_B21AFBFC.m4a) | 64:10 | [Markdown](2026-10-29_B21AFBFC.scribe-v3.md) · [Timed JSON](2026-10-29_B21AFBFC.scribe-v3.json) |
| [2026-11-05](2026-11-05_13D4A044.m4a) | 69:27 | [Markdown](2026-11-05_13D4A044.scribe-v3.md) · [Timed JSON](2026-11-05_13D4A044.scribe-v3.json) |

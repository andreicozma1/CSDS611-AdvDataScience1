# CSDS 611 lecture materials

This directory contains the Fall 2026 lecture slides and their Markdown
transcriptions, plus the Goodnotes recordings and their Scribe v3 transcripts.

[Slides by lecture](#slides-by-lecture) · [Class schedule](#class-schedule) · [Recordings by date](#recordings-by-date)

## Slides by lecture

Use Markdown to search the decks. Use the original PDF to check equations,
figures, and slide numbers. The [lecture library](https://app.notion.com/p/341ee83111d3494594a421e2221c95fb)
has detailed outlines and slide references.

| Lecture | Presentation title | Topics covered | Files |
| --- | --- | --- | --- |
| 02 | BO preliminaries | Bayesian optimization loop, exploration versus exploitation, acquisition functions | [PDF](<CSDS 611 - Lecture 02 - Bayesian Optimization Preliminaries.pdf>) · [Markdown](<CSDS 611 - Lecture 02 - Bayesian Optimization Preliminaries.md>) · [Notion](https://app.notion.com/p/40af723fb8cc8168b497f24bc8d5a2fd) |
| 03 | Uncertain quantities of interest | Random variables, statistical notation, probability rules, joint distributions | [PDF](<CSDS 611 - Lecture 03 - Uncertain Quantities of Interest.pdf>) · [Markdown](<CSDS 611 - Lecture 03 - Uncertain Quantities of Interest.md>) · [Notion](https://app.notion.com/p/40af723fb8cc811f84bdeacaa81e4b64) |
| 04 | Intro Bayes | Priors, likelihoods, Bayes’ theorem, models with multiple quantities, Bayesian workflow | [PDF](<CSDS 611 - Lecture 04 - Introduction to Bayes.pdf>) · [Markdown](<CSDS 611 - Lecture 04 - Introduction to Bayes.md>) · [Notion](https://app.notion.com/p/40af723fb8cc81399b66f56a517a4e5c) |
| 05 | Random variables | Non-Gaussian discrete and continuous distributions, including binomial, Poisson, beta, gamma, and Student’s t | [PDF](<CSDS 611 - Lecture 05 - Non-Gaussian Random Variables.pdf>) · [Markdown](<CSDS 611 - Lecture 05 - Non-Gaussian Random Variables.md>) · [Notion](https://app.notion.com/p/40af723fb8cc816fbc1fc4bacf59340a) |
| 06 | Gaussian random scalars | Univariate normal simulation, transformations, credible intervals, Bayesian inference | [PDF](<CSDS 611 - Lecture 06 - Gaussian Random Scalars.pdf>) · [Markdown](<CSDS 611 - Lecture 06 - Gaussian Random Scalars.md>) · [Notion](https://app.notion.com/p/40af723fb8cc81ed92f1d674f9b06bde) |
| 07 | Gaussian random vectors | Multivariate normal simulation, linear transformations, covariance factorizations and square roots | [PDF](<CSDS 611 - Lecture 07 - Gaussian Vectors - Transformations and Covariance Factors.pdf>) · [Markdown](<CSDS 611 - Lecture 07 - Gaussian Vectors - Transformations and Covariance Factors.md>) · [Notion](https://app.notion.com/p/40af723fb8cc81828b79e3e4cb0e0c0a) |
| 08 | Gaussian random vectors | Independence, marginal and conditional distributions, whitening, sequential updates, credible ellipses | [PDF](<CSDS 611 - Lecture 08 - Gaussian Vectors - Conditioning and Credible Ellipses.pdf>) · [Markdown](<CSDS 611 - Lecture 08 - Gaussian Vectors - Conditioning and Credible Ellipses.md>) · [Notion](https://app.notion.com/p/40af723fb8cc8195900cf256824b47bf) |
| 09 | Bayesian hypothesis tests | Categorical data, spam detection, binary and general tests, uncertain model parameters | [PDF](<CSDS 611 - Lecture 09 - Bayesian Hypothesis Tests.pdf>) · [Markdown](<CSDS 611 - Lecture 09 - Bayesian Hypothesis Tests.md>) · [Notion](https://app.notion.com/p/40af723fb8cc8137a9dfd5ceb9147032) |
| 10 | The exponential family | Exponential-family models, conjugate updates, hypothesis testing, signal detection | [PDF](<CSDS 611 - Lecture 10 - The Exponential Family.pdf>) · [Markdown](<CSDS 611 - Lecture 10 - The Exponential Family.md>) · [Notion](https://app.notion.com/p/40af723fb8cc81788aabef1eef13c0fd) |
| 11 | Bayesian decision theory | Actions and losses, posterior expected loss, posterior mean, median, and mode as point estimates | [PDF](<CSDS 611 - Lecture 11 - Bayesian Decision Theory.pdf>) · [Markdown](<CSDS 611 - Lecture 11 - Bayesian Decision Theory.md>) · [Notion](https://app.notion.com/p/40af723fb8cc817c8199e06a77a08431) |
| 12 | Applied decision problems | Clinical decisions with missing test information, recommendation systems | [PDF](<CSDS 611 - Lecture 12 - Applied Decision Problems.pdf>) · [Markdown](<CSDS 611 - Lecture 12 - Applied Decision Problems.md>) · [Notion](https://app.notion.com/p/40af723fb8cc81e59a8df32d1b14d783) |
| 13 | Linear regression | Basis functions, ordinary and ridge least squares, Bayesian regression | [PDF](<CSDS 611 - Lecture 13 - Linear Regression.pdf>) · [Markdown](<CSDS 611 - Lecture 13 - Linear Regression.md>) · [Notion](https://app.notion.com/p/40af723fb8cc8185bf5fc8ec5a5b240d) |
| 14 | Model selection | Comparing regression models, model priors, marginal likelihood, posterior model probabilities | [PDF](<CSDS 611 - Lecture 14 - Model Selection.pdf>) · [Markdown](<CSDS 611 - Lecture 14 - Model Selection.md>) · [Notion](https://app.notion.com/p/40af723fb8cc811aba1eefc9089a2927) |
| 15 | Predictions | Posterior predictive distributions, joint predictions, Bayesian model averaging | [PDF](<CSDS 611 - Lecture 15 - Posterior Prediction.pdf>) · [Markdown](<CSDS 611 - Lecture 15 - Posterior Prediction.md>) · [Notion](https://app.notion.com/p/40af723fb8cc81919c9aee204238e68e) |
| 16 | Kernel regression | Basis functions in Bayesian linear regression, covariance functions, kernels | [PDF](<CSDS 611 - Lecture 16 - Kernel Regression.pdf>) · [Markdown](<CSDS 611 - Lecture 16 - Kernel Regression.md>) · [Notion](https://app.notion.com/p/40af723fb8cc81658c49c34529af2fac) |
| 17 | Gaussian processes | From kernel regression to Gaussian process priors, finite collections of function values | [PDF](<CSDS 611 - Lecture 17 - Gaussian Processes.pdf>) · [Markdown](<CSDS 611 - Lecture 17 - Gaussian Processes.md>) · [Notion](https://app.notion.com/p/40af723fb8cc81289f59fbdb9fdf6ff5) |
| 18 | Gaussian processes regression | Gaussian process regression, posterior mean and covariance, squared exponential kernel | [PDF](<CSDS 611 - Lecture 18 - Gaussian Process Regression.pdf>) · [Markdown](<CSDS 611 - Lecture 18 - Gaussian Process Regression.md>) · [Notion](https://app.notion.com/p/40af723fb8cc81bdaa06d6d7c720bcb4) |
| 19 | Implementation of Gaussian processes regression | Cholesky factorization and updates, predictive statistics, noise, periodic, and diffusion kernels | [PDF](<CSDS 611 - Lecture 19 - Implementing Gaussian Process Regression.pdf>) · [Markdown](<CSDS 611 - Lecture 19 - Implementing Gaussian Process Regression.md>) · [Notion](https://app.notion.com/p/40af723fb8cc8113938cceac101df9a5) |
| 20 | BO | Bayesian optimization with probabilistic surrogates | [PDF](<CSDS 611 - Lecture 20 - Bayesian Optimization - Surrogates.pdf>) · [Markdown](<CSDS 611 - Lecture 20 - Bayesian Optimization - Surrogates.md>) · [Notion](https://app.notion.com/p/415f723fb8cc818a8085c9a2ca6c0aa3) |
| 21 | BO | Acquisition functions, including confidence bounds, improvement criteria, and Thompson sampling | [PDF](<CSDS 611 - Lecture 21 - Bayesian Optimization - Acquisition Functions.pdf>) · [Markdown](<CSDS 611 - Lecture 21 - Bayesian Optimization - Acquisition Functions.md>) · [Notion](https://app.notion.com/p/415f723fb8cc81ca83b2d596748d0725) |

Lecture 17’s title is shown with its spelling corrected.

## Class schedule

The schedule below maps the numbered slide decks to class dates and lists every
Tuesday and Thursday from August 18 through December 1, 2026. Week 1 is
August 17–23; semester week numbers continue through breaks. The
[syllabus](../CSDS_611_syllabus.md) establishes Tuesday/Thursday meetings,
2:30–3:45 p.m. Eastern. Its tentative topic outline differs from the actual
slide sequence, so the dates below also use transcripts, Canvas notifications,
and PDF metadata.

Checked November 20, 2026. **Confirmed** means direct evidence supports the
date and session mapping. **High confidence** means the mapping is supported
without a matching recording. **Scheduled** and **announced** describe plans,
not verification that a future session occurred. Recording availability refers
to this repository; a missing recording does not mean class was canceled.
Topic matches do not establish complete audio coverage of every slide.

### August 2026

| Week | Date | Slides / session | Recording | Certainty |
| --- | --- | --- | --- | --- |
| 1 | Tue Aug 18 | Course introduction; no local Lecture 01 deck | No | Confirmed |
| 1 | Thu Aug 20 | **02:** BO preliminaries | Yes | Confirmed |
| 2 | Tue Aug 25 | **03:** Uncertain quantities | Yes | Confirmed |
| 2 | Thu Aug 27 | **04:** Introduction to Bayes | Yes | Confirmed |

### September 2026

| Week | Date | Slides / session | Recording | Certainty |
| --- | --- | --- | --- | --- |
| 3 | Tue Sep 1 | **05:** Non-Gaussian random variables | Yes | Confirmed |
| 3 | Thu Sep 3 | **06:** Gaussian random scalars | Yes | Confirmed |
| 4 | Tue Sep 8 | **07:** Gaussian vectors: transformations | Yes | Confirmed |
| 4 | Thu Sep 10 | **08:** Gaussian vectors: conditioning | Yes | Confirmed |
| 5 | Tue Sep 15 | **09:** Bayesian hypothesis tests | **Missing** | **High confidence** |
| 5 | Thu Sep 17 | **10:** Exponential family | Yes | Confirmed |
| 6 | Tue Sep 22 | **11:** Bayesian decision theory | Yes | Confirmed |
| 6 | Thu Sep 24 | **12:** Applied decision problems | Yes | Confirmed |
| 7 | Tue Sep 29 | **13:** Linear regression | Yes | Confirmed |

### October 2026

| Week | Date | Slides / session | Recording | Certainty |
| --- | --- | --- | --- | --- |
| 7 | Thu Oct 1 | **14:** Model selection | Yes | Confirmed |
| 8 | Tue Oct 6 | **No class: university fall break** | — | Confirmed |
| 8 | Thu Oct 8 | **15:** Posterior prediction | Yes | Confirmed |
| 9 | Tue Oct 13 | **16:** Kernel regression | Yes | Confirmed |
| 9 | Thu Oct 15 | **17:** Gaussian processes | **Missing** | **High confidence** |
| 10 | Tue Oct 20 | **No class: professor traveling that week** | — | Confirmed |
| 10 | Thu Oct 22 | **No class: professor traveling that week** | — | Confirmed |
| 11 | Tue Oct 27 | **18:** Gaussian process regression | Yes; starts mid-explanation | Confirmed |
| 11 | Thu Oct 29 | **19:** Implementing GP regression | Yes | Confirmed |

### November 2026

| Week | Date | Slides / session | Recording | Certainty |
| --- | --- | --- | --- | --- |
| 12 | Tue Nov 3 | **No class: Election Day university holiday** | — | Confirmed |
| 12 | Thu Nov 5 | **20:** BO surrogates | Yes | Confirmed |
| 13 | Tue Nov 10 | **21:** BO acquisition functions | Yes | Confirmed |
| 13 | Thu Nov 12 | In-class project: Step 1 | No | Scheduled; upload confirmed |
| 14 | Tue Nov 17 | In-class project: Step 2 | No | Scheduled; upload confirmed |
| 14 | Thu Nov 19 | In-class project: Step 3 | No | Confirmed |
| 15 | Tue Nov 24 | **Office hours instead of class**, at the usual meeting time | — | Announced |
| 15 | Thu Nov 26 | **No class: Thanksgiving recess** | — | Confirmed calendar |

### December 2026

| Week | Date | Slides / session | Recording | Certainty |
| --- | --- | --- | --- | --- |
| 16 | Tue Dec 1 | **Office hours instead of class; final project due** | — | Announced |

### Schedule evidence and limits

There are four skipped class periods before Lecture 21, plus Thanksgiving on
November 26. November 24 and December 1 replace class with office hours.
The likely missing lecture recordings are September 15 and October 15.
Whether an introductory Lecture 01 deck existed is unverified.

- **Semester boundaries and university holidays:** the [official UTK calendar](https://registrar.utk.edu/wp-content/uploads/sites/4/2025/12/2026-2027-Published-Calendar.pdf) lists the August 17 start, October 6 fall break, November 3 Election Day holiday, November 25–27 Thanksgiving recess, and December 1 end.
- **August 18 introduction:** the professor’s [August 12 welcome email](https://mail.google.com/mail/u/?authuser=acozma%40vols.utk.edu#all/19ff6db5030725f9) gives the first meeting date and describes introductions and syllabus review.
- **Recorded lectures:** the [review log](transcript-review.md) records transcript-to-slide comparisons, with two older associations clarified here: October 27 maps primarily to Lecture 18, and November 5 to Lecture 20.
- **September 15 / Lecture 09:** the [Canvas upload notification](https://mail.google.com/mail/u/?authuser=acozma%40vols.utk.edu#all/1a0a6af804b1fd87) names `meeting_09.pdf` and `meeting_08.pdf`, with the surrounding recordings supporting September 15 for Lecture 09.
- **October 15 / Lecture 17:** the [October 13 transcript, 03:41](2026-10-13_09627C3C.scribe-v3.md) previews Gaussian processes for the next lecture, and [Lecture 17’s PDF](<CSDS 611 - Lecture 17 - Gaussian Processes.pdf>) has a creation timestamp of October 15, 3:44:46 p.m. Eastern.
- **Travel cancellations:** the [October 13 transcript, 02:11](2026-10-13_09627C3C.scribe-v3.md) explicitly announces no class the following Tuesday and Thursday because the professor is traveling; the conference purpose remains unverified.
- **Other no-class announcements:** the [October 1 transcript, 00:00–00:44](2026-10-01_9A3E8C58.scribe-v3.md) announces the October 6 break, and the [October 29 transcript, 00:38](2026-10-29_B21AFBFC.scribe-v3.md) announces no class on November 3.
- **Project sessions:** the [November 10 briefing](2026-11-10_8F5F2BB7.scribe-v3.md) gives the [project schedule](../final-project/README.md#schedule), and Canvas upload notifications corroborate [Step 1 on November 12](https://mail.google.com/mail/u/?authuser=acozma%40vols.utk.edu#all/1a1d50a306a4226c), [Step 2 on November 17](https://mail.google.com/mail/u/?authuser=acozma%40vols.utk.edu#all/1a1eae7db944af61), and [Step 3 on November 19](https://mail.google.com/mail/u/?authuser=acozma%40vols.utk.edu#all/1a1f53b54dee154c).
- **Office hours and deadline:** the professor’s [November 20 email](https://mail.google.com/mail/u/?authuser=acozma%40vols.utk.edu#all/1a1f9126c47adccc) confirms class met November 19, replaces November 24 and December 1 meetings with office hours, and sets the final project deadline to December 1.

Upload dates and PDF creation dates support the reconstruction but do not
independently prove when material was taught. This schedule does not replace
Canvas instructions or later announcements.

## Recordings by date

Select a date to open the audio. When available, the transcript links include
readable Markdown and the original Scribe v3 JSON with word timestamps. The
[review log](transcript-review.md) records uncertain wording, speaker labels,
and technical corrections. The [glossary](transcription-glossary.md) lists the
keyterms used during transcription.

Dates use Eastern time. See the [class schedule](#class-schedule) for slide-deck
mappings and confidence labels; some recordings cover only part of a class.

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
| [2026-11-10](2026-11-10_8F5F2BB7.m4a) | 65:57 | [Markdown](2026-11-10_8F5F2BB7.scribe-v3.md) · [Timed JSON](2026-11-10_8F5F2BB7.scribe-v3.json) |

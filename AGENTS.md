# CSDS 611 Repository Instructions

## Make choices together

After a quick check of the requirements and existing files, use the permitted
structured input tool early when the user's preference would change what you
deliver or how they use it. This includes reversible choices such as where
recordings live, how files are named, or how much detail goes into a report.
Ask before making the dependent change. Continue work that is independent of
the answer.

- Start with the choice that rules out the most irrelevant options. Offer two
  or three viable choices or a yes/no question. Use actual paths, names, or
  outcomes in the labels and explain the tradeoffs in the descriptions.
- Recommend one option when the evidence supports it. Let the user redirect,
  defer, or combine compatible choices. Ask a follow-up only if the first
  answer leaves a decision that would still change the result.
- Proceed directly when the user has already chosen, the assignment fixes the
  answer, or the remaining detail is routine. Follow the broader tool and
  authorization rules if a choice requires permission or the tool is unavailable.

## Final project report (Overleaf)

The [Overleaf submodule](final-project-report/) holds the LaTeX source for
the CSDS 611 final project report. For report edits, start with
[`main.tex`](final-project-report/main.tex) inside the submodule.

The course repository pins a specific report commit. The submodule is
configured to track Overleaf's `main` branch for remote updates.

## Finding course evidence

For coursework, derivations, and lecture summaries, use the
[Notion lecture library](https://app.notion.com/p/341ee83111d3494594a421e2221c95fb) to find
topics, slide references, equations, figures, and source corrections. Browse in
[lecture order](https://app.notion.com/p/341ee83111d3494594a421e2221c95fb?v=40af723fb8cc811186ef000cbda7c787)
or use the library's **Find a topic** view.

Read the [slide-reading instructions](lectures/AGENTS.md) before citing lecture
evidence. They explain how to search local Markdown, verify equations and
figures in the original PDFs, and combine evidence across decks. If Notion is
unavailable, use the same local workflow.

Use the original assignment PDF to establish the question and requirements.
Use lectures to find applicable methods, and label added assumptions and
independent derivations. For the coin test, start with the
[Assignment 2 instructions](assignment-2/AGENTS.md#lecture-evidence).

### Lecture contents

Lectures 02–21 are listed in deck order. Each link opens the corresponding
Notion lecture page with its notes, slide references, and sources. For local
files, see the [slide index](lectures/README.md#slides-by-lecture).

- [Lecture 02 — BO preliminaries](https://app.notion.com/40af723fb8cc8168b497f24bc8d5a2fd). Optimization,
  surrogates, the BO loop, exploration/exploitation, acquisition, roadmap.
- [Lecture 03 — Uncertain quantities](https://app.notion.com/40af723fb8cc811f84bdeacaa81e4b64). Random
  variables/processes, notation, PMFs/PDFs, simulation, joint/marginal/conditional rules.
- [Lecture 04 — Intro Bayes](https://app.notion.com/40af723fb8cc81399b66f56a517a4e5c). Priors, likelihoods,
  Bayes' theorem, normalization, multiple observations, Bayesian work-cycle.
- [Lecture 05 — Non-Gaussian variables](https://app.notion.com/40af723fb8cc816fbc1fc4bacf59340a). Bernoulli,
  binomial, Poisson, geometric, uniform, beta, von Mises, exponential, gamma,
  Weibull, beta-prime, chi, chi-square, Student-t; supports and simulation.
- [Lecture 06 — Gaussian scalars](https://app.notion.com/40af723fb8cc81ed92f1d674f9b06bde). Normal density,
  whitening, sums/norms, CDF/quantiles, credible intervals, precision and conjugacy.
- [Lecture 07 — Gaussian vectors](https://app.notion.com/40af723fb8cc81828b79e3e4cb0e0c0a). Covariance,
  affine transforms, sampling, Cholesky/eigen/SVD factors, linear Gaussian inference.
- [Lecture 08 — Gaussian conditioning](https://app.notion.com/40af723fb8cc8195900cf256824b47bf). Independence,
  marginals, permutations, block conditionals, sequential updates, credible ellipses.
- [Lecture 09 — Hypothesis tests](https://app.notion.com/40af723fb8cc8137a9dfd5ceb9147032). Categorical models,
  spam example, Bayes factors, posterior odds, MAP/ML, uncertain-parameter evidence.
- [Lecture 10 — Exponential families](https://app.notion.com/40af723fb8cc81788aabef1eef13c0fd). Sufficient
  statistics, conjugate updates, normalizing constants, marginal likelihood, detection.
- [Lecture 11 — Decision theory](https://app.notion.com/40af723fb8cc817c8199e06a77a08431). States/data/actions,
  loss, posterior risk, Bayes rules, mean/median/mode estimators, BO decisions.
- [Lecture 12 — Applied decisions](https://app.notion.com/40af723fb8cc81e59a8df32d1b14d783). Missing test
  identity, clinical losses, Dirichlet preferences, reactions, recommendation.
- [Lecture 13 — Linear regression](https://app.notion.com/40af723fb8cc8185bf5fc8ec5a5b240d). Basis/design,
  normal equations, pseudoinverse, ridge, Gaussian coefficient posterior and MAP.
- [Lecture 14 — Model selection](https://app.notion.com/40af723fb8cc811aba1eefc9089a2927). Candidate bases,
  model indicators, integrated evidence, Gaussian regression comparison.
- [Lecture 15 — Prediction](https://app.notion.com/40af723fb8cc81919c9aee204238e68e). Posterior predictive
  integration, joint queries, parameter/noise uncertainty, Bayesian model averaging.
- [Lecture 16 — Kernel regression](https://app.notion.com/40af723fb8cc81658c49c34529af2fac). Function-space
  means/covariances, training/query blocks, conditioning, PSD kernels and composition.
- [Lecture 17 — Gaussian processes](https://app.notion.com/40af723fb8cc81289f59fbdb9fdf6ff5). Finite-dimensional
  definition, heteroscedastic noise, consistency, function priors and samples.
- [Lecture 18 — GP regression](https://app.notion.com/40af723fb8cc81bdaa06d6d7c720bcb4). Posterior derivation,
  predictive mean/variance, observation noise, squared-exponential correlations.
- [Lecture 19 — GP implementation](https://app.notion.com/40af723fb8cc8113938cceac101df9a5). Triangular solves,
  Cholesky reuse, costs, squared-exponential/white/constant/periodic/diffusion kernels.
- [Lecture 20 — Bayesian optimization with GP surrogates](https://app.notion.com/p/415f723fb8cc818a8085c9a2ca6c0aa3).
  Expensive objectives, GP surrogate and observation model, space-filling
  initial designs, the sequential query loop, and upper and lower confidence bounds.
- [Lecture 21 — Bayesian optimization acquisition functions](https://app.notion.com/p/415f723fb8cc81ca83b2d596748d0725).
  Confidence bounds, expected and probability of improvement, jitter,
  Thompson sampling, planning horizon, and a one-dimensional comparison.

## Assignment submission filenames

For a student-authored solution to assignment number `N`, use the basename
`assignment_N_acozma` for its LaTeX source and submission PDF. For example,
Assignment 2 uses `assignment_2_acozma.tex` and
`assignment_2_acozma.pdf`. Keep generated build files under the same basename
when they are retained. Check the source, PDF, and references after a rename.

This convention applies to student-authored solutions. Keep instructor-provided
assignment prompts and source archives under their source filenames. Use the
[lecture filename convention](lectures/AGENTS.md#locate-only-the-necessary-material)
for lecture files. Follow an explicit assignment submission filename if one is given.

## Student report voice and structure

Apply this section when drafting or reviewing a student-authored assignment
solution or report in this repository. The target is a **concise worked solution
written by a careful student for the instructor**: clear enough to follow on a
first reading, detailed enough to check, and direct about choices and limits.
Think of a well-edited answer sheet with explanations, rather than a textbook
chapter, study guide, research paper, or transcript of the solving process.
The assignment prompt and any required template take priority over these
defaults.

### Build the answer around the task

- Start with the given data or question and define only notation needed for the
  solution. State modeling choices as choices, separate from facts stated in the
  assignment.
- Organize by the steps the reader needs to verify: setup, method or calculation,
  comparison or result, and a direct conclusion. Use only headings that help a
  reader find those steps; the exact headings can vary with the assignment.
- Show enough intermediate equations and short explanations to reproduce a
  non-obvious result. Explain why a method or comparison applies, without
  narrating every algebraic move or re-teaching the whole lecture.
- End with the requested answer and its actual conditions. Keep uncertainty
  proportional to the evidence. A caveat belongs where it prevents a likely
  misinterpretation, not as a catalog of all possible alternatives.
- Use the lecture slides and study notes to check the method and notation.
  Bring material into the submitted report only when it supports a required
  step, explains a necessary choice, or resolves a plausible ambiguity.

### Make it sound like the student's own work

- Prefer plain, precise sentences and ordinary transitions that show the
  connection between steps: "Under this assumption," "Substituting," or
  "Therefore" when those words describe the actual reasoning.
- Use first person for a genuine author choice ("I assume...", "I use...")
  when it makes ownership clearer. State calculations and results directly.
  Neither first person nor impersonal phrasing needs to appear in every paragraph.
- In submitted prose, name the assignment or question when necessary, or state
  the relevant fact directly. Do not call the assignment "the prompt"; that is
  drafting language. In study notes or instructions, "assignment prompt" may
  identify the source document.
- Keep paragraphs focused and reasonably short. Pair displayed equations with
  enough nearby prose to say what they calculate and why the result matters.
- Avoid ceremonial or textbook-like openings ("We now turn our attention to"),
  generic praise of the method, repeated restatements, and transitions that
  announce a section without advancing the solution. Avoid unexplained jargon,
  inflated certainty, and details included only because they are interesting.

| Instead of | Prefer |
| --- | --- |
| "We now proceed to calculate the marginal likelihood under the alternative hypothesis." | "Under the alternative, I average the likelihood over the stated prior." |
| "It is important to note that the result does not conclusively prove fairness." | "These data favor the fair-coin model under the stated assumptions; six flips do not establish fairness." |
| A page of optional prior examples before answering the question | The chosen prior, its effect on the calculation, and a brief conditional conclusion |

### Review with discriminating questions

Read the complete report without the drafting conversation. For every answer
below that is "no," revise the passage or identify a real requirement that
justifies it; do not rewrite merely to satisfy a word-count rule.

1. Can the instructor locate the requested answer and trace each essential
   result back to the given data, assumptions, and calculation?
2. Is every assumption or author choice labeled, while the assignment's facts and
   required hypotheses remain exact?
3. Does each paragraph perform a job needed for the answer: set up a quantity,
   justify a step, interpret a result, or state a relevant limit? If removed,
   what would the reader actually lose?
4. Can a classmate new to this method explain why the next equation follows,
   using only the report? If not, add the missing bridge, not a lecture recap.
5. Does the prose sound like a student explaining their own work to a professor
   when read aloud? Flag stock phrases, abrupt topic changes, overlong
   paragraphs, and sentences that sound like a textbook or generic AI essay.
6. Are optional examples, side calculations, and caveats placed only where they
   change the decision or prevent a likely error? Keep extended teaching in
   study notes when it is not part of the submission.
7. Does the conclusion answer the exact question at the strength supported by
   the calculation and stated decision rule, without implying certainty or a
   uniquely required choice when inputs were unspecified?
8. In the rendered document, are body text, paragraph gaps, equations, and
   margins comfortable to read, with no crowded blocks or stranded headings?

For a new standalone LaTeX report with no required template, the current
Assignment 2 source is a starting point for restrained formatting: 11-point
type, one-inch margins, modest line spacing, and visible paragraph separation.
Adjust these for the actual content and any page limit; check the rendered
pages rather than assuming source settings guarantee readability.

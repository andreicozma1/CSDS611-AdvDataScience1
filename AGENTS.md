# CSDS 611 Repository Instructions

## Finding course evidence

For coursework, statistical questions, derivations, or lecture summaries, start
with the relevant entries below and the
[problem-oriented lookup paths](slides/lecture-guide.md#lookup-by-problem).
Read [slide-reading instructions](slides/AGENTS.md) before extracting or citing
lecture evidence, including when working from an assignment directory.
The [lecture guide](slides/lecture-guide.md) owns detailed slide outlines,
equation locations, notation changes, and source corrections. Load only the
sections needed for the task; verify the cited PDF pages before using a result.
Assignment prompts define the question and required assumptions; lecture examples
supply methods. Label additional assumptions and independently derived steps.

### Lecture contents

The checked collection is Lectures 02–19: 18 PDF/Markdown pairs, 209 slides,
inventoried on 2026-10-31. Each link opens an outline with links to both formats.
Recheck this inventory when source decks are added or replaced.

- [L02: BO preliminaries](slides/lecture-guide.md#lecture-02): optimization,
  surrogates, the BO loop, exploration/exploitation, acquisition, roadmap.
- [L03: Uncertain quantities](slides/lecture-guide.md#lecture-03): random
  variables/processes, notation, PMFs/PDFs, simulation, joint/marginal/conditional rules.
- [L04: Intro Bayes](slides/lecture-guide.md#lecture-04): priors, likelihoods,
  Bayes' theorem, normalization, multiple observations, Bayesian work-cycle.
- [L05: Non-Gaussian variables](slides/lecture-guide.md#lecture-05): Bernoulli,
  binomial, Poisson, geometric, uniform, beta, von Mises, exponential, gamma,
  Weibull, beta-prime, chi, chi-square, Student-t; supports and simulation.
- [L06: Gaussian scalars](slides/lecture-guide.md#lecture-06): normal density,
  whitening, sums/norms, CDF/quantiles, credible intervals, precision and conjugacy.
- [L07: Gaussian vectors](slides/lecture-guide.md#lecture-07): covariance,
  affine transforms, sampling, Cholesky/eigen/SVD factors, linear Gaussian inference.
- [L08: Gaussian conditioning](slides/lecture-guide.md#lecture-08): independence,
  marginals, permutations, block conditionals, sequential updates, credible ellipses.
- [L09: Hypothesis tests](slides/lecture-guide.md#lecture-09): categorical models,
  spam example, Bayes factors, posterior odds, MAP/ML, uncertain-parameter evidence.
- [L10: Exponential families](slides/lecture-guide.md#lecture-10): sufficient
  statistics, conjugate updates, normalizing constants, marginal likelihood, detection.
- [L11: Decision theory](slides/lecture-guide.md#lecture-11): states/data/actions,
  loss, posterior risk, Bayes rules, mean/median/mode estimators, BO decisions.
- [L12: Applied decisions](slides/lecture-guide.md#lecture-12): missing test
  identity, clinical losses, Dirichlet preferences, reactions, recommendation.
- [L13: Linear regression](slides/lecture-guide.md#lecture-13): basis/design,
  normal equations, pseudoinverse, ridge, Gaussian coefficient posterior and MAP.
- [L14: Model selection](slides/lecture-guide.md#lecture-14): candidate bases,
  model indicators, integrated evidence, Gaussian regression comparison.
- [L15: Prediction](slides/lecture-guide.md#lecture-15): posterior predictive
  integration, joint queries, parameter/noise uncertainty, Bayesian model averaging.
- [L16: Kernel regression](slides/lecture-guide.md#lecture-16): function-space
  means/covariances, training/query blocks, conditioning, PSD kernels and composition.
- [L17: Gaussian processes](slides/lecture-guide.md#lecture-17): finite-dimensional
  definition, heteroscedastic noise, consistency, function priors and samples.
- [L18: GP regression](slides/lecture-guide.md#lecture-18): posterior derivation,
  predictive mean/variance, observation noise, squared-exponential correlations.
- [L19: GP implementation](slides/lecture-guide.md#lecture-19): triangular solves,
  Cholesky reuse, costs, squared-exponential/white/constant/periodic/diffusion kernels.

### Assignment-specific context

- Read [Assignment 2 instructions](assignment-2/AGENTS.md) when working on the
  coin test; its [lecture guide](assignment-2/lecture-slide-guide.md) is a
  task-specific selection, not the course-wide inventory.
- Use each assignment's original PDF and any local instructions. The report
  conventions below apply to student-authored solutions across assignments.

## Assignment submission filenames

For a student-authored solution to assignment number `N`, use the basename
`assignment_N_acozma` for its LaTeX source and submission PDF. For example,
Assignment 2 uses `assignment_2_acozma.tex` and
`assignment_2_acozma.pdf`. Keep generated build files under the same basename
when they are retained. Check the source, PDF, and references after a rename.

This convention applies to student-authored solutions. Keep instructor-provided
assignment prompts, source archives, and lecture materials under their source
filenames. Follow an explicit assignment submission filename if one is given.

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

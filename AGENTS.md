# CSDS 611 Repository Instructions

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
  solution. State modeling choices as choices, separate from facts in the prompt.
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

# Reading CSDS 611 Lecture Sources

This file governs work in `slides/`. The root also routes here whenever an
assignment or question uses lecture evidence. Follow the root conventions;
keep instructor PDFs and their Markdown transcriptions under their source names.

## Locate only the necessary material

Use [the lecture guide](lecture-guide.md) for problem-oriented reading paths,
slide-level outlines, equation locations, and known source issues. Choose the
relevant sections, then inspect the actual sources. An index entry identifies
where to look; it is not a substitute for the cited slide.

Search from the repository root, for example:

```sh
rg -n -i 'marginal likelihood|hypothesis|posterior odds' slides/CSDS611_Lecture_*.md
rg -n -i 'conditionals|Cholesky|predictive|positive semi' slides/CSDS611_Lecture_*.md
rg -n -F '\Phi' slides/CSDS611_Lecture_13.md
```

Try descriptive synonyms as well as symbols: evidence/marginal likelihood,
variance/precision, whitening/de-whitening, kernel/covariance, feature/basis/design,
prediction/posterior. Repeated headings and OCR errors can hide exact matches.

## PDF and Markdown have different roles

- Use Markdown for fast topic search and readable LaTeX. It is a transcription
  that may omit, reorder, duplicate, or misrecognize text, equations, or headings.
  Its heading count is not a slide counter. For example, L08's PDF slide 5 is
  titled "Marginals", while the corresponding Markdown has another
  "Rearrangements" heading. Markdown line numbers are not slide references.
- Use the PDF to establish the printed slide number, equation layout, block
  dimensions, parameter labels, footnotes, and figure content. In the checked
  collection, PDF pages and printed slide numbers coincide; verify after updates.
- Extracted PDF text can scramble columns, fractions, superscripts, matrices,
  and reading order. Compare with Markdown, then render the complete page when
  an equation's meaning depends on those features. Neither text representation
  alone establishes a visual claim.
- Markdown image URLs are pointers to crops, often hosted externally. Prefer
  the local PDF, which supplies the whole slide and its context. A local PDF
  does not require downloading those remote images.

## Read equations and derivations

Read the setup and neighboring derivation slides, not only a final formula.
Check support, parameterization, conditioning, independence, rank/invertibility,
units, and dimensions before adapting a result. Distinguish variance, standard
deviation, precision, and gamma scale/rate. Use the guide's notation and source
notes when symbols or dimensions change between lectures.

If Markdown and the PDF disagree, first distinguish transcription error from a
source error. Check a related derivation or identity; show the printed expression
and justify any correction. Label your extension or algebraic derivation as
such. Never silently repair instructor materials or present an unfinished
source derivation as completed in the slides.

## Inspect figures

Use the PDF skill and a verified available runtime. `pypdf`/`pdfplumber` can
extract text; Poppler or `pypdfium2` can render pages. Check installed tools
before choosing commands; follow the host guidance for runtime selection.
If rendering is unavailable, state the visual-verification limitation rather
than inferring a plot from its caption. Keep disposable renders in a task-owned
temporary directory and remove those renders after inspection.

Inspect complete relevant pages at a readable size. Contact sheets help locate
figures; enlarge pages to read axes, legends, parameters, points, and bands.
Record axis orientation and units, plotted support, sample size, parameter
values, and whether a band represents standard deviations, probability content,
or another quantity. Describe unlabelled bands conservatively. Static PDF
snapshots do not establish unseen animation steps.

Figure-heavy locations include L02:4,7–8; L08:9–11; L14:4,10–12; L15:8;
L17:11; L18:8–9,11–12; L19:7,9,11,13,15,17. Distribution plots in L03/L05
often place the variable vertically and mass/density horizontally.

## Combine evidence across decks

For each requested result, identify the model/setup, the applicable identity,
the derivation or example, and the interpretation/decision rule. A short working
record can map each claim to `LNN, slide(s), source path, assumptions, role`.
Keep this in task context unless a durable record is actually needed.

Follow only relevant dependencies. For example, a GP variance calculation may
need L08:7 for Gaussian conditioning, L17:5 for observation noise, L18:6–7 for
the posterior, and L19:3 for implementation. A coin test instead starts from
L05:4, L09:5,9–11 and, if losses matter, L11:5. Verify that the problem's
assumptions permit combining these results.

Before reporting, verify cited pages and equation consistency. Give deck and
slide numbers and link the source PDF. Separate lecture facts, assignment facts,
modeling choices, numerical calculations, and independently derived results.
Use current tool citation syntax when required. Only include teaching detail
in a submission when it supports the requested answer.

## Maintain the map when sources change

When asked to maintain lecture guidance after a deck is added/replaced, recount
its pages and confirm printed numbering, revise its outline and relevant task
routes in [the guide](lecture-guide.md), then update the root contents list and
inventory. Recheck affected source notes; do not assume an old typo persists.
Keep original source material intact unless its modification is requested.
Do not add instructions to generated output folders solely for completeness.

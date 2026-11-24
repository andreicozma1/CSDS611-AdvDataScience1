# Email drafting retrospective

November 19, 2026

The email was sent, according to Andrei's confirmation in this chat. Drafting
took repeated corrections because the assistant kept changing settled meaning,
occasionally described proposed edits as saved changes, and repeatedly read
on-screen text aloud during voice mode. The useful result came from keeping one
editable draft, preserving Andrei's wording, and connecting each technical fact
to the question it justified.

## Scope and evidence

This review covers the email-drafting exchanges in this side conversation,
including the voice transcripts, file reads, edits, and readbacks. The
[saved draft](../professor-email-draft.md) includes Andrei's own edits and is
preserved as it stands. The exact email delivered to the professor was not
retrieved, and this review makes no claim about the professor's response.

Some voice transcripts report actions that the saved file later contradicted.
The review therefore distinguishes spoken claims, displayed proposals, and
verified file changes. The voice frontend also read drafts that the backend
had displayed on screen; guidance can address the requested delivery behavior,
but this retrospective does not establish a fix in the voice application.

## What helped

- **One saved draft.** Moving the email into a Markdown file gave both people a
  common place to review and edit.
- **A clear recipient and purpose.** The email became a short request for
  clarification from the instructor, with a course-specific subject and greeting.
- **Context before the question.** Explaining the sampling grid made the question
  about the original rates easier to understand.
- **Concrete questions.** Asking about changed solver options and added noise
  was more useful than a broad heading asking how the CSV was generated.
- **Visible alternatives.** Current wording followed by labeled alternatives
  helped Andrei choose specific phrasing.
- **Checking authoritative sources.** The handout resolved what was already
  given, the CSV confirmed the sampling grid, and MATLAB documentation corrected
  the explanation of how output times relate to internal steps.
- **Preserving user edits.** Later reads recovered Andrei's own changes before
  making a narrow replacement.

## Where the process failed

### Meaning changed during wording edits

The central question concerned estimating the particular rates that generated
the CSV when the sampled data admit other rate vectors with identical model
predictions. Rewrites repeatedly changed it into a question about whether a
close fit was sufficient, how many solutions to list, or whether the professor
would compare rate estimates. Those are related questions, but they did not
preserve the full concern Andrei wanted to express.

The assistant also turned an established premise into a hypothetical by
repeatedly writing “if several sets of rates...”. Andrei wanted the email to
start from what had been found and ask what that meant for the assignment.

**Better practice.** Before editing, retain the passage's facts, relationship,
qualification, consequence, and requested answer. Change the selected wording
while keeping accepted clauses stable. When accuracy requires a qualification,
explain the specific correction briefly and preserve the rest.

### Simpler wording sometimes removed the point

Phrases such as “several sets of rates can fit equally well” and “more timing
information could help narrow the possibilities” were short but left the reader
to infer why they mattered. Other versions included the mechanism but ended
before explaining its effect on estimating the original rates.

Breaking the same explanation into many short sentences made it choppy.
Repeated synonyms and fresh formulations made settled passages feel unstable.

**Better practice.** Keep the necessary connection from observation to mechanism
to consequence. Use sentence breaks where the topic changes, and retain a
connected sentence when its clauses express one line of reasoning.

### Questions needed a specific purpose

Several suggested questions asked about givens or unsupported possibilities.
The assignment already supplied the initial populations and model interval.
There was no evidence that the professor restarted the solver. Asking whether
our implementation should reproduce MATLAB's numerical behavior confused the
data-generation diagnostic with the assignment's implementation requirement.

The time-vector question had a legitimate purpose, but that purpose was
initially missing. The assistant also incorrectly described the alternative as
fixed-step integration before checking the MATLAB documentation. Both ways of
requesting outputs can use adaptive integration.

**Better practice.** Check what is already known and identify what decision an
answer would change. Ask the remaining concrete question and explain its purpose
only when the reader would otherwise have to guess. Reuse verified documentation
instead of repeatedly announcing another check of unchanged behavior.

### Presentation did not match the medium

Andrei rejected the robotic headings in the email, repeated full drafts in
chat, inline wording menus that were hard to compare, and overly abrupt closing
questions. The assistant also kept adding generic offers to make more changes
or read the text aloud.

Most seriously, the voice interaction repeatedly recited drafts after Andrei
explicitly asked to read them on screen. Displaying a draft was followed by a
spoken repetition of the same content.

**Better practice.** Use short transitions in the email. During revision, show
the changed passage or file link. For alternatives, give each requested passage
its own section, put the current wording first, label each variant separately,
place the wording in text blocks, and separate passages with horizontal rules.
In voice mode, deliver requested text visually and keep the spoken response to
the minimum status the interface requires.

### Announced edits were not always saved

The user twice had to point out that text described as removed or changed was
still visible. A later file read confirmed that the paragraph comparing SSE
values around 496 and 907 was still present after a spoken claim of removal.
Other exchanges offered wording after the user had asked for a file edit.

**Better practice.** Read the live passage, apply the authorized change, then
read it back. Claim completion only after checking the saved text. When the
user cannot see a claimed change, inspect the file and visible document before
assuming the cause. Keep the sent draft intact unless asked to revise it.

## Specific choices and corrections to retain

### Email content and voice

- Use “CSDS 611 final project questions” as this email's subject.
- Open with “Good afternoon, Dr. Sgouralis,” using the syllabus spelling.
- Begin directly with a few questions about the project.
- Ask how close estimates should be to the specific original rates, while
  distinguishing that from fitting the recorded population values.
- Introduce the 5,000-unit sampling grid before its consequence for rate estimates.
- Connect requests for off-grid observations or a cycle length to that ambiguity.
- Ask whether all other solver options were left at their defaults, building on
  the professor's statement about default tolerances.
- Keep the noise question in its own paragraph with a natural lead-in.
- Close with “Best regards” and the full name, Andrei Cozma.

The rejected phrases included “I forgot to ask about the rest of the setup,”
“if getting close to the original rates is important,” “if we're working with
the current data,” and “why the data don't clearly distinguish it from the
others.” They were indirect, redundant, or obscured the actual question in
these passages; they are examples to reason from, rather than a universal
word blacklist.

### Structure and alternatives

The initial preference for one question per bullet evolved into merging the
requests for extra observations and a cycle length, because either served the
same purpose. Distinct questions about solver settings and noise stayed
separate. The useful principle is one decision per question, with related
alternatives together when the author prefers that form.

“Observed prey and predator populations” was rejected in one repetitive
conditional and later preferred in the opening comparison because it clarified
what was being fitted. A correction applies to its meaning and location.

Andrei requested literal preservation once, then asked for a fluent cleanup
that retained every substantive point. Quoting the spoken hesitations back was
appropriate only for the literal request; the subsequent revision needed to
remove disfluencies while preserving the argument.

### Technical accuracy and result provenance

- Identical predictions at the 27 recorded times concern the sampled values;
  the continuous trajectories can differ between those times.
- Particular common scaling factors can preserve those predictions; “any
  multiple” would overstate the mathematical claim.
- Convergence to an alternative fit does not make reaching the original rates
  impossible, but sampled predictions may fail to identify them uniquely.
- The fit near 496 SSE came from a separate search over cycle shape and timing
  followed by bounded least squares.
- Step 2 asks for approximately 50 space-filling evaluations and GP fitting,
  including assessing the objective transformation and tuning hyperparameters.
- Sequential BO follow-ups go beyond that initial-design requirement.
- The exploratory result and constant baseline were ultimately deferred from
  this email, after their provenance made the draft harder to follow.

These points explain why an editor must preserve technical meaning while
respecting the author's wording. They do not require reopening the experiments
or adding a technical appendix to a short email.

## A shorter process for the next draft

Existing writing guidance already required preserving meaning and reading live
files before editing. This incident shows failures in applying those rules at
the point of revision and in checking completion claims. The accessible record
does not establish which guidance the voice frontend loaded. The skill changes
therefore put a short reminder and a direct route at the drafting boundary;
they do not assume that adding more generic prose will solve compliance.

1. Establish the recipient, purpose, known facts, and answers the email needs.
2. Create or reuse one draft file once the user asks for saved revisions.
3. For each correction, reread the live passage and change the smallest coherent
   span while preserving the author's current edits and accepted meaning.
4. When asked for alternatives, show the current text and a small set of variants
   in the agreed comparison format, with one short recommendation.
5. Apply a selected variant in the existing draft when editing is authorized.
6. Check the saved change and its immediate transitions before reporting success.
7. Show the changed location, and stop when the requested edit is complete.

This needs one document and focused readbacks. Extra drafting states, repeated
permission questions, full rewrites, and repeated technical checks would add
work without addressing the failures observed here.

## Guidance updated and verification limits

The reusable workflow is maintained in the user-owned `writing` skill's
`references/draft-collaboration.md`, routed from `SKILL.md`. Its line-editing
guidance and regression examples cover premise preservation and focused edits.
The user-owned `fix-ai-speak` skill routes ordinary iterative drafting to that
workflow while keeping its explicit audit procedure.

Verification for this maintenance consists of saved-file checks, route and
format checks, and manual walkthroughs of the incidents above. Future agent
compliance and voice-frontend behavior remain untested. This retrospective
records the process; the professor's reply will answer the open project questions.

Both edited skills passed the installed skill validator. Their UI YAML parsed,
and the relative Markdown links in the changed files resolved. Manual
walkthroughs checked that a selected edit is saved, an alternatives request
awaits selection, a technical correction preserves the author's intended
question, and an explicit request to hear a draft remains allowed.

Character counts for the skill maintenance are recorded below. These count
Unicode characters, including whitespace, in each UTF-8 document.

| File within the user-owned skills directory | Before | After | Change |
| --- | ---: | ---: | ---: |
| `writing/SKILL.md` | 14,237 | 15,259 | +1,022 |
| `writing/references/draft-collaboration.md` | 0 | 4,556 | +4,556 |
| `writing/references/edit.md` | 4,575 | 5,025 | +450 |
| `writing/references/technical-prose-regression-cases.md` | 18,002 | 19,146 | +1,144 |
| `fix-ai-speak/SKILL.md` | 10,346 | 10,684 | +338 |

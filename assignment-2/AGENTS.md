# Assignment 2: Coin Fairness Test

This file applies only to work in `assignment-2/`. Follow broader instructions
as well. The assignment prompt is `assignment_2.pdf`; `assignment_2.md` is a
text transcription. Check the prompt before changing the problem statement.

## The Given Problem

The observed sequence of six flips is **Heads, Heads, Heads, Tails, Tails,
Heads**. It contains four heads and two tails. The task is to perform a
hypothesis test and decide whether the coin is fair, using these hypotheses:

- **H0:** The coin is fair; its heads probability is the fixed, known value
  theta = 1/2.
- **HA:** The coin is described as unfair; its heads probability theta is
  uncertain and lies in [0, 1].

Preserve the distinction between a fixed value under H0 and an uncertain
parameter under HA. The stated interval includes 1/2; do not silently rewrite
the alternative as a different set.

## Interpreting and Solving the Task

- The prompt gives the ordered outcomes. Treating the flips as independent
  Bernoulli trials with one shared theta is a modeling assumption to state, not
  additional wording from the prompt. Under that assumption, the likelihood
  of the exact sequence at a given theta is theta^4 (1 - theta)^2.
- If using only the count of heads, the corresponding binomial likelihood is
  C(6, 4) theta^4 (1 - theta)^2. Keep the data representation consistent across
  H0 and HA; the common combinatorial factor cancels in their likelihood ratio.
- An uncertain theta is not a specified prior distribution. For a Bayesian
  test, identify a prior for theta under HA, prior odds for the hypotheses, and
  a decision rule. The prompt supplies none of these. Label any choices as
  assumptions, and do not present one resulting decision as uniquely required
  by the prompt. A Uniform[0, 1] or Beta(1, 1) prior is an example, not a
  stated requirement.
- When presenting a solution, show how the evidence under each hypothesis is
  obtained, state the comparison and decision rule, and interpret the result
  under the chosen assumptions. Estimating theta alone does not complete the
  requested hypothesis test.

## Lecture Evidence

Before explaining or solving this assignment, read the applicable entries in
[Lecture Slide Guide](#lecture-slide-guide). It inventories all 13
available decks, identifies the relevant slides by number and title, and
explains what each contributes. The shortest useful path is Lecture 5 slide 4
for coin flips; Lecture 3 slide 5 for the count of heads; Lecture 5 slides
9-10 for possible priors; and Lecture 9 slides 4-6 and 8-11 for the hypothesis
test. Consult Lecture 11 slides 3-5 if the decision uses explicit losses.

The slides explain methods; they do not add a prior or decision rule to the
assignment prompt. Recheck the PDFs if a deck changes before citing its slides.


## Study Context and Prerequisites

The assignment's source of truth is assignment_2.pdf, with assignment_2.md as
a transcription. It gives the ordered outcomes H, H, H, T, T, H and specifies
a fixed fair-coin model H0 with heads probability \(\theta=1/2\) and an
uncertain-parameter alternative HA with \(\theta\in[0,1]\). It does not state
that flips are independent or give a prior over \(\theta\), prior
probabilities for H0 and HA, or a decision rule. Treat those as modeling and
decision choices, not hidden requirements.

The [Lecture Slide Guide](#lecture-slide-guide) inventories the 13
available lecture decks (147 slides) and explains the 34 slides relevant
to this assignment. Lecture 9 supplies the direct hypothesis-testing
framework. Lectures 3-5 supply probability, Bayes' rule, Bernoulli/binomial
models, and possible priors; Lecture 11 supplies loss-based decisions.
Lecture 5 slide 5 contains a binomial-exponent typo; Lecture 3 slide 5
prints the correct formula.

### Definitions to know before using the walkthrough

- **Trial and outcome:** One coin flip is a trial with outcome H or T.
  The six observed outcomes form the data \(D=(H,H,H,T,T,H)\).
- **Sample space:** The possible ordered data are the \(2^6=64\) sequences
  in \(\{H,T\}^6\). A count such as \(K=4\) heads groups
  \(\binom{6}{4}=15\) different ordered sequences.
- **Parameter:** \(\theta\) denotes the probability of heads in a
  single flip. A fixed \(\theta\) specifies one coin model. An unknown
  \(\theta\) needs a rule for handling uncertainty.
- **Hypothesis or model:** H0 and HA are two competing explanations of
  how the data were generated. H0 places all its weight on
  \(\theta=1/2\); a Bayesian HA assigns a distribution to possible
  \(\theta\) values.
- **Independent and identically distributed (i.i.d.):** Conditional on
  one shared \(\theta\), each flip has the same Bernoulli distribution
  and the outcome of one flip does not change another flip's conditional
  probability. This assumption justifies multiplying six single-flip
  probabilities. Fair marginal heads probability alone does not establish
  independence.
- **Likelihood:** \(p(D\mid\theta)\) evaluates how compatible the
  observed data are with a specified parameter value. As a function of
  \(\theta\), a likelihood is not automatically a probability density
  over \(\theta\).
- **Parameter prior versus hypothesis prior:** \(p(\theta\mid H_A)\)
  weights possible biases *within* HA. \(P(H_A)\) and \(P(H_0)\)
  weight the two models *before* observing the flips. These are distinct
  choices.
- **Marginal likelihood or model evidence:** \(p(D\mid H_A)\)
  averages the conditional likelihood across \(\theta\), weighted by
  its parameter prior. Under H0, it is the likelihood evaluated at
  \(\theta=1/2\). Both use the same definition of the data.
- **Posterior:** \(P(H\mid D)\) is the probability assigned to a
  hypothesis after the data, conditional on the stated model set and
  priors. The posterior density \(p(\theta\mid D,H_A)\) is instead
  about the bias *assuming HA*; it is not \(P(H_A\mid D)\).
- **Bayes factor:** \(\mathrm{BF}_{A0}=p(D\mid H_A)/p(D\mid H_0)\).
  It measures the data's relative support for the models before
  multiplying by prior odds. State which model is in the numerator.
- **Decision rule:** A rule converts posterior probabilities or odds
  into an action. MAP chooses the hypothesis with the larger posterior
  probability. With unequal consequences for mistakes, specify a loss
  function and minimize posterior expected loss instead.
- **Frequentist test:** This is a different framework. A p-value is a
  tail probability of data under H0, not \(P(H_0\mid D)\). Do not mix
  a p-value, a Bayes factor, and a posterior probability as though they
  were interchangeable.

### Minimum calculation tools

For independent Bernoulli outcomes \(x_i\in\{0,1\}\), with heads coded
as 1, multiply \(p(x_i\mid\theta)=\theta^{x_i}
(1-\theta)^{1-x_i}\). The exponents sum to the observed four heads and
two tails. For a head count, multiply the ordered-sequence likelihood by
\(\binom{6}{4}=6!/(4!2!)=15\).

For a uniform prior on \([0,1]\), the density is 1 and
\(\int_0^1\theta^m\,d\theta=1/(m+1)\) for \(m>-1\).
A general Beta\((a,b)\) prior has density
\(\theta^{a-1}(1-\theta)^{b-1}/B(a,b)\), where
\(B(a,b)=\int_0^1\theta^{a-1}(1-\theta)^{b-1}\,d\theta\).
For the ordered four-head, two-tail sequence, its marginal likelihood
would be \(B(a+4,b+2)/B(a,b)\). This formula is an optional extension,
not a prior specified by the assignment.

Bayes' rule for the two models can be written
\(P(H_j\mid D)=p(D\mid H_j)P(H_j)/
\sum_{h\in\{H_0,H_A\}}p(D\mid h)P(h)\).
The probabilities sum to 1 only within the stated two-model set.
For a loss-based decision, compare actions using
\(R(a\mid D)=\sum_h L(a,h)P(h\mid D)\); the chosen action has the
smallest posterior expected loss.

## Saved Student Walkthrough (Verbatim)

The following text is reproduced exactly from the prior explanation in this
chat. Its Uniform\([0,1]\) parameter prior, equal hypothesis priors,
and MAP rule are illustrative assumptions. The prompt remains the authority
for what is required.

<!-- BEGIN VERBATIM STUDENT WALKTHROUGH -->
The clean mental model is **two competing ways the six flips could have been generated**. Under \(H_0\), the heads probability is fixed at \(1/2\). Under \(H_A\), the heads probability is unknown. A hypothesis test compares how well *each whole model* predicts the observed data, then applies a stated rule for deciding between them.

The important catch in the [assignment prompt](/Users/acozma/GitHub/CSDS611-AdvDataScience1/assignment-2/assignment_2.pdf) is that it gives the range \(\theta\in[0,1]\), but **does not give a probability distribution over that range, prior odds for the hypotheses, or a decision threshold**. Those choices must be stated; they must not be presented as facts from the prompt.

## How a student can find the method

Start by turning each question raised by the prompt into a question for the slides:

| Question | Where to look | What to take from it |
| --- | --- | --- |
| How do I model one heads-or-tails outcome? | [Lecture 5, slide 4](/Users/acozma/GitHub/CSDS611-AdvDataScience1/slides/CSDS611_Lecture_05.pdf) | The Bernoulli likelihood. |
| What if I use “four heads in six flips” instead of the exact order? | [Lecture 3, slide 5](/Users/acozma/GitHub/CSDS611-AdvDataScience1/slides/CSDS611_Lecture_03.pdf) | The binomial likelihood and its combinatorial factor. |
| What could describe an uncertain \(\theta\)? | Lecture 5, slides 9–10 | Uniform and Beta distributions are *possible priors*, not assigned priors. |
| How do I compare \(H_0\) with \(H_A\)? | [Lecture 9, slides 4–6 and 8–11](/Users/acozma/GitHub/CSDS611-AdvDataScience1/slides/CSDS611_Lecture_09.pdf) | Marginal likelihood, Bayes factor, prior odds, and decision rule. |
| What if wrong decisions have different costs? | [Lecture 11, slides 3–5](/Users/acozma/GitHub/CSDS611-AdvDataScience1/slides/CSDS611_Lecture_11.pdf) | Choose the action with the lowest posterior expected loss. |

The [slide guide](/Users/acozma/GitHub/CSDS611-AdvDataScience1/assignment-2/lecture-slide-guide.md) explains those pages in more detail. One source check matters: Lecture 5, slide 5 has a typo in the binomial formula; use Lecture 3, slide 5 for its correct exponent \(6-k\).

## Work through the problem

**1. Record the data without interpreting it yet.** Write heads as 1 and tails as 0:

\[
D=(1,1,1,0,0,1),\qquad n=6,\quad k=4\text{ heads},\quad 2\text{ tails}.
\]

The sequence is given in the prompt. Counting four heads is a useful summary; it is not yet evidence that the coin is fair or unfair.

**2. State the sampling assumption.** The usual model assumes that, conditional on one shared \(\theta\), the flips are independent Bernoulli trials. The prompt does not spell out independence, so a careful solution says it is an assumption.

For one flip \(x_i\),

\[
p(x_i\mid\theta)=\theta^{x_i}(1-\theta)^{1-x_i}.
\]

Multiplying the six terms gives the probability of the **particular ordered sequence**:

\[
p(D\mid\theta)=\theta^4(1-\theta)^2.
\]

The order does not appear in the final product because, under this model, every sequence with four heads and two tails has the same probability.

**3. Evaluate the fixed model.** Under \(H_0\), substitute \(\theta=1/2\):

\[
p(D\mid H_0)=(1/2)^4(1/2)^2=\frac1{64}.
\]

This is a likelihood for the *data assuming \(H_0\)*. It is **not** the probability that \(H_0\) is true.

**4. Handle the uncertain parameter properly.** Under \(H_A\), \(\theta\) can take many values. To obtain one likelihood for the entire alternative model in a Bayesian test, average \(p(D\mid\theta)\) using a prior density \(p(\theta\mid H_A)\):

\[
p(D\mid H_A)
=\int_0^1 \theta^4(1-\theta)^2p(\theta\mid H_A)\,d\theta.
\]

This is the *marginal likelihood*. Lecture 9, slides 9–11 supply this step. Selecting the best-fitting \(\theta=4/6\) instead would **maximize** the likelihood; it would not calculate the Bayesian marginal likelihood.

**5. Make an illustrative prior choice—and label it.** Suppose, for a worked example, that \(\theta\mid H_A\sim\mathrm{Uniform}[0,1]\). Its density is 1 on that interval. This is equivalent to a \(\mathrm{Beta}(1,1)\) prior, but the assignment did **not** require it.

The integral can be done with elementary algebra, without knowing the Beta function:

\[
\begin{aligned}
p(D\mid H_A)
&=\int_0^1\theta^4(1-\theta)^2\,d\theta\\
&=\int_0^1(\theta^4-2\theta^5+\theta^6)\,d\theta\\
&=\frac15-\frac13+\frac17
=\frac1{105}.
\end{aligned}
\]

The intuition is that this model spreads its predictions over many possible biases. Some predict this sequence well; others predict it poorly. Its evidence is their **prior-weighted average**, not its best prediction.

**6. Compare the evidence.** Orient the Bayes factor explicitly as alternative over null:

\[
\mathrm{BF}_{A0}
=\frac{p(D\mid H_A)}{p(D\mid H_0)}
=\frac{1/105}{1/64}
=\frac{64}{105}\approx0.610.
\]

With the illustrative uniform prior, the data favor \(H_0\) over \(H_A\), but only modestly. Reversing the ratio would instead give \(105/64\approx1.64\) in favor of \(H_0\); the direction must always be named.

**7. Turn evidence into a decision using stated assumptions.** Posterior odds equal Bayes factor times prior odds:

\[
\frac{P(H_A\mid D)}{P(H_0\mid D)}
=\mathrm{BF}_{A0}\frac{P(H_A)}{P(H_0)}.
\]

If we *also assume* equal prior probabilities for the two hypotheses and use the MAP rule from Lecture 9, slide 6, the posterior probabilities are

\[
P(H_0\mid D)=\frac{105}{169}\approx0.621,\qquad
P(H_A\mid D)=\frac{64}{169}\approx0.379.
\]

That rule selects \(H_0\). The correct wording is: **“Under an independent-flip model, a uniform prior under \(H_A\), equal hypothesis priors, and a MAP decision rule, these data favor the fair-coin hypothesis.”** It does not prove the coin fair.

There is no assumption-free Bayesian yes/no answer here. For example, prior odds of \(2{:}1\) in favor of \(H_A\) would turn the same Bayes factor into posterior odds \(128{:}105\) in favor of \(H_A\). That is why the missing prior odds matter.

## Checks that catch common mistakes

1. **Check which data you modeled.** For the exact sequence, use \(\theta^4(1-\theta)^2\). For the count \(K=4\), use \(\binom64\theta^4(1-\theta)^2\). The factor \(\binom64=15\) appears under *both* hypotheses and cancels in the Bayes factor. Mixing a sequence likelihood for one model with a count likelihood for the other gives a false comparison.
2. **Check the roles of the probabilities.** \(p(D\mid H_0)\), \(p(D\mid H_A)\), and \(P(H_0\mid D)\) are different quantities. A probability of data under a hypothesis is not automatically a probability of the hypothesis.
3. **Check the prior.** A range \([0,1]\) gives possible values, not their weights. Verify that any chosen density integrates to 1, and state it before drawing a conclusion.
4. **Check the operation.** An *uncertain* \(\theta\) in Bayesian model comparison is integrated out. Estimating \(\theta\) under \(H_A\) answers a different question. Even a posterior estimate of \(\theta\) conditional on \(H_A\) is not \(P(H_A\mid D)\).
5. **Check the arithmetic independently.** Expanding the integral gives \(1/105\); the Beta-function calculation gives \(B(5,3)=1/105\). Posterior probabilities \(105/169\) and \(64/169\) sum to 1.
6. **Check the final sentence against the decision rule.** Name the prior, hypothesis prior odds, and threshold or loss assumptions. Describe evidence as stronger or weaker; do not say six flips establish fairness with certainty.

One subtlety: the prompt calls \(H_A\) “unfair” but writes \(\theta\in[0,1]\), which includes \(1/2\). Preserve the stated interval. With a continuous prior such as Uniform\([0,1]\), the single point \(\theta=1/2\) has zero prior probability under \(H_A\); \(H_0\) remains a separate model concentrated at that point.

**Check your mental model:** Why does plugging in \(\hat\theta=4/6\) answer a different question from integrating over \(\theta\) under \(H_A\)? If you can explain that distinction and identify every assumption in step 7, you have the central method.
<!-- END VERBATIM STUDENT WALKTHROUGH -->

## Lecture Slide Guide

This guide supports the coin fairness test in `assignment_2.pdf`. It inventories
all 13 lecture PDFs (147 slides) in `../slides/` and explains 34 relevant
slides in detail. The PDF page and the printed slide number coincide in these
decks. Titles and contents below were checked against the PDFs on 2026-10-01;
recheck a deck if its PDF changes. The assignment prompt, rather than a
lecture example, defines the required hypotheses.

### Reading Order

1. Model the six outcomes: Lecture 5 slide 4 (Bernoulli), then Lecture 3 slide
   5 if using the count of four heads.
2. Identify a possible distribution for the uncertain heads probability:
   Lecture 5 slides 9-10 (Uniform and Beta). Neither is specified by the prompt.
3. Form the hypothesis test: Lecture 9 slides 4-6, then slides 8-11. Slides
   9-11 are the closest match to the uncertain-parameter alternative.
4. Use Lecture 11 slides 3-5 only if the decision depends on an explicit loss
   for choosing the wrong hypothesis. Lecture 10 slides 9-11 give a more
   abstract route to the same marginal-likelihood idea.

### Every Deck at a Glance

| Deck | Slides | Relevance to Assignment 2 |
| --- | ---: | --- |
| [Lecture 2: BO preliminaries](../slides/CSDS611_Lecture_02.pdf) | 9 | Bayesian optimization, acquisition, and exploration. No direct role in this coin test. |
| [Lecture 3: Uncertain quantities of interest](../slides/CSDS611_Lecture_03.pdf) | 10 | Slides 3, 5, 9-10: parameter notation, correct binomial count formula, and probability rules. |
| [Lecture 4: Intro Bayes](../slides/CSDS611_Lecture_04.pdf) | 9 | Slides 2, 4-6, 8-9: prior, likelihood, joint, posterior, and repeated observations. |
| [Lecture 5: Random variables](../slides/CSDS611_Lecture_05.pdf) | 18 | Slides 4, 9-10: Bernoulli likelihood and candidate Uniform/Beta priors. Slide 5 discusses Binomial but has a formula typo. |
| [Lecture 6: Gaussian random scalars](../slides/CSDS611_Lecture_06.pdf) | 8 | Normal models and intervals; the coin outcome is Bernoulli, so this deck is not needed. |
| [Lecture 7: Gaussian random vectors](../slides/CSDS611_Lecture_07.pdf) | 9 | Multivariate normal models; no direct role. |
| [Lecture 8: Gaussian random vectors](../slides/CSDS611_Lecture_08.pdf) | 11 | Normal independence, marginals, and conditionals; the general ideas appear in more directly relevant decks. |
| [Lecture 9: Bayesian hypothesis tests](../slides/CSDS611_Lecture_09.pdf) | 11 | Core deck. Slides 4-6 give binary posterior odds and a decision rule; 8-11 handle uncertain parameters. Slides 2-3 and 7 add context. |
| [Lecture 10: The exponential family](../slides/CSDS611_Lecture_10.pdf) | 15 | Slides 9-11 give a general marginal-likelihood derivation; the worked likelihood family elsewhere in the deck is not the coin model. |
| [Lecture 11: Bayesian decision theory](../slides/CSDS611_Lecture_11.pdf) | 10 | Slides 3-5 explain actions, loss, and posterior expected loss if a decision cost is specified. |
| [Lecture 12: Applied decision problems](../slides/CSDS611_Lecture_12.pdf) | 15 | Slide 2 recaps the decision rule; clinical and recommendation examples are not needed. |
| [Lecture 13: Linear regression](../slides/CSDS611_Lecture_13.pdf) | 10 | Regression and normal-data models; no direct role. |
| [Lecture 14: Model selection](../slides/CSDS611_Lecture_14.pdf) | 12 | Slides 5-6 and 8 offer an optional analogy: compare models after integrating uncertain parameters. Its actual models are Gaussian regressions. |

### Slides That Supply the Coin Model and Probability Rules

#### Lecture 3: Uncertain quantities of interest

- **Slide 3, “Statistical notation”** distinguishes a distribution with a
  certain parameter from one conditioned on an uncertain parameter. This helps
  keep fixed theta under H0 distinct from uncertain theta under HA.
- **Slide 5, “Example 2”** gives the binomial mass function
  `C(J, w) pi^w (1-pi)^(J-w)`. Use J = 6 and w = 4 when analyzing the number of
  heads rather than the particular order of heads and tails.
- **Slide 9, “Probability rules”** contrasts sums over discrete outcomes with
  integrals over continuous values. It supports integrating a continuous prior
  over theta when computing evidence under HA.
- **Slide 10, “Joint probability distributions”** shows joint factorization
  and marginalization. It supplies background for integrating theta out of a
  joint model to compare hypotheses.

#### Lecture 4: Intro Bayes

- **Slide 2, “Bayesian models”** introduces an unknown parameter with a prior
  and data conditional on that parameter. This is the general structure of a
  Bayesian model under HA.
- **Slide 4, “Bayesian methods”** identifies prior, likelihood, and their
  product as the joint distribution. Keep those three quantities separate.
- **Slide 5, “Bayes’ theorem”** states the posterior as likelihood times prior
  divided by evidence.
- **Slide 6, “Bayesian methods”** gives the proportional posterior form. It
  supports comparing hypotheses after computing their likelihoods or marginal
  likelihoods.
- **Slide 8, “Bayesian models with multiple quantities”** writes a product of
  data likelihoods for its model with multiple observations. Apply a product to
  the six flips only after stating the shared-theta, independent-flip model.
- **Slide 9, “The Bayesian work-cycle”** separates likelihood, prior,
  posterior, and inference. The assignment asks for the final inference about
  fairness, not only an estimate of theta.

#### Lecture 5: Random variables

- **Slide 4, “Bernoulli”** gives `p(w | theta) = theta^w (1-theta)^(1-w)` for
  a binary outcome coded as heads = 1. Under independent flips with one shared
  theta, the observed ordered sequence has likelihood
  `theta^4 (1-theta)^2`.
- **Slide 5, “Binomial”** relates a head count to a sum of Bernoulli variables.
  Its displayed mass function prints `(1-pi)^w`; that exponent is incorrect.
  Use the correct `J-w` exponent from Lecture 3 slide 5.
- **Slide 9, “Uniform”** gives the density on a bounded interval. A
  Uniform[0, 1] prior is one possible assumption for theta under HA, not a
  prior stated in the assignment.
- **Slide 10, “Beta”** gives a density on [0, 1] and notes its use as a prior
  for Bernoulli data. Beta(1, 1) is uniform; other Beta parameters express
  other prior assumptions.

### Slides That Define the Hypothesis Test

#### Lecture 9: Bayesian hypothesis tests

- **Slide 2, “Categorical random variables”** defines the distribution used
  for a model indicator with alternatives such as H0 and HA. It is background
  for assigning prior probabilities to the two hypotheses.
- **Slide 3, “Spam detection”** illustrates how baseline odds, data evidence,
  and a chosen threshold affect a binary decision. Its numbers are an example,
  not inputs for the coin test.
- **Slide 4, “Binary hypothesis tests”** sets up two hypotheses with prior
  probabilities and gives the posterior relation
  `p(hypothesis | data) proportional to p(data | hypothesis) p(hypothesis)`.
- **Slide 5, “Binary hypothesis tests”** expresses posterior odds as a Bayes
  factor times prior odds. This is the comparison after finding evidence under
  H0 and HA.
- **Slide 6, “Binary hypothesis tests”** chooses a hypothesis by comparing
  posterior odds with a threshold. The slide identifies MAP threshold 1 and
  distinguishes it from a likelihood-based choice; the assignment sets no
  threshold or prior odds.
- **Slide 7, “General hypothesis tests”** extends posterior comparison to
  several hypotheses. It is a cross-check for the two-hypothesis rule, though
  the assignment needs only H0 and HA.
- **Slide 8, “Hypothesis tests with uncertain parameters”** introduces
  hypothesis-specific uncertain parameters and begins the marginalization of
  their joint posterior.
- **Slide 9, “Hypothesis tests with uncertain parameters”** reduces that
  marginalization to the parameter belonging to the selected hypothesis. For
  this assignment, HA has uncertain theta and H0 has fixed theta.
- **Slide 10, “Hypothesis tests with uncertain parameters”** gives the key
  rule: a hypothesis's marginal posterior is proportional to its prior
  probability times its likelihood integrated against its parameter prior.
- **Slide 11, “Hypothesis tests with uncertain parameters”** names the
  resulting integrals marginal likelihoods. This is the evidence to compare
  with the fixed-theta likelihood under H0.

Lecture 9 states the general method; it does not supply the coin-specific
prior. For the ordered six-flip sequence, an independent-flip model gives
`p(data | H0) = (1/2)^6` and
`p(data | HA) = integral_0^1 theta^4 (1-theta)^2 p(theta | HA) dtheta`.
These are applications of the slides to the prompt, not equations printed in
the deck. If using the count of four heads, multiply both expressions by
`C(6, 4)`; the factor cancels in their ratio.

### Optional Deeper Treatments

#### Lecture 10: The exponential family

- **Slide 9, “Hypothesis tests with uncertain parameters”** restates the MAP
  comparison and the need for each hypothesis's marginal likelihood.
- **Slide 10, “Hypothesis tests within the exponential family”** starts a
  general calculation of marginal likelihood for a conjugate prior/likelihood
  pair.
- **Slide 11, “Hypothesis tests within the exponential family”** uses the
  prior and posterior normalization factors to finish that calculation. It is
  an optional algebraic method; it does not give a worked coin example.

#### Lecture 11: Bayesian decision theory

- **Slide 3, “Decision problems”** defines states, data, actions, a decision
  rule, and a loss function. Here the actions would be choosing H0 or HA.
- **Slide 4, “Bayesian decision problems”** combines a probabilistic model
  with a loss function to derive a decision rule.
- **Slide 5, “Bayesian decision problems”** chooses the action with the lowest
  posterior expected loss. Use this only when decision costs are specified or
  explicitly assumed; the assignment does not give them.

#### Lecture 12: Applied decision problems

- **Slide 2, “Decision and Bayesian decision problems”** summarizes the
  posterior-expected-loss rule from Lecture 11. It is a brief recap, not
  additional machinery needed for the coin calculation.

#### Lecture 14: Model selection

- **Slide 5, “Bayesian model selection”** says that choosing among models with
  uncertain parameters reduces to hypothesis testing with uncertain
  parameters. This parallels fair versus uncertain-bias coin models.
- **Slide 6, “Bayesian model selection”** selects a model by its marginal
  posterior under a MAP rule.
- **Slide 8, “Bayesian model selection”** integrates only the parameters of
  the model under consideration. Its example uses regression coefficients,
  so it is an analogy rather than a coin-test derivation.

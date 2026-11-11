## Intro Bayes

- Bayesian methods
- Bayesian models

## Bayesian models

A Bayesian model attains the general form

$$
\begin{aligned}
q & \sim Q \\
w \mid q & \sim P_{q}
\end{aligned}
$$

and consists of, at least, two uncertain quantities of interest

- an independent $q$...this is most often called the unknown parameter or solution
- a dependent $w$...this is most often called the measurement or data

Bayesian models
![](https://cdn.mathpix.com/cropped/7d1c40e4-5ece-43d3-8b8d-7e60c500c324-3.jpg?height=381&width=1306&top_left_y=122&top_left_x=121)

With a Bayesian model we seek to characterize the posterior probability distribution

$$
p(q \mid w)
$$

that corresponds to the given data

## Bayesian methods

We consider a Bayesian model

$$
\begin{aligned}
q & \sim Q \\
w \mid q & \sim P_{q}
\end{aligned}
$$

This model provides direct descriptions of:

- the prior distribution: this corresponds to the probability function
$$
p(q)=Q(q)
$$
- the likelihood distribution: this corresponds to the probability function
$$
p(w \mid q)=P_{q}(w)
$$

This model provides almost direct description of:

- the joint distribution: this corresponds to the probability function
$$
p(w, q)=p(w \mid q) p(q)=P_{q}(w) Q(q)
$$

## Bayes' theorem

We consider two parametric quantities of interest $x$ and $y$
Their probability function is

$$
\begin{aligned}
& & p(x, y) & =p(y, x) \\
\Longrightarrow & & p(x \mid y) p(y) & =p(y \mid x) p(x) \\
\Longrightarrow & & p(x \mid y) & =\frac{p(y \mid x) p(x)}{p(y)}
\end{aligned}
$$

This is Bayes' theorem
Bayes' rule generalizes to any quantity of interest, no matter if parametric or non-parametric

## Bayesian methods

We consider a Bayesian model

$$
\begin{aligned}
q & \sim Q \\
w \mid q & \sim P_{q}
\end{aligned}
$$

This model provides direct descriptions of:

- the prior distribution: this corresponds to the probability function
$$
p(q)=Q(q)
$$
- the likelihood distribution: this corresponds to the probability function
$$
p(w \mid q)=P_{q}(w)
$$

This model provides indirect description of:

- the posterior distribution: this corresponds to the probability function
$$
p(q \mid w)=\frac{p(w \mid q) p(q)}{p(w)} \propto p(w \mid q) p(q)=P_{q}(w) Q(q)
$$

## Example

We consider binomial data with unknown trials

$$
\begin{aligned}
J & \sim \operatorname{Poisson}(\mu) \\
w \mid J & \sim \operatorname{Binomial}(J, \pi)
\end{aligned}
$$

Our posterior is given by

$$
\begin{aligned}
p(J \mid w) & \propto p(w \mid J) p(J) \\
& =\operatorname{Binomial}(w ; J, \pi) \operatorname{Poisson}(J ; \mu) \\
& =\binom{J}{w} \pi^{w}(1-\pi)^{J-w} \frac{\mu^{J}}{J!} e^{-\mu} \\
& =\frac{J!}{w!(J-w)!} \pi^{w}(1-\pi)^{J-w} \frac{\mu^{J}}{J!} e^{-\mu} \\
& =\frac{\mu^{J} e^{-\mu}}{w!(J-w)!} \pi^{w}(1-\pi)^{J-w} \\
& \propto \frac{\mu^{J}}{(J-w)!}(1-\pi)^{J-w}
\end{aligned}
$$

We recover the missing constants with normalization

$$
\begin{aligned}
1 & =\sum_{J=0}^{\infty} p(J \mid w) \\
& =\sum_{J=0}^{\infty} C \frac{\mu^{J}}{(J-w)!}(1-\pi)^{J-w} \\
& =C \sum_{J=0}^{\infty} \frac{\mu^{J}}{(J-w)!}(1-\pi)^{J-w} \\
& =C \mu^{w} e^{\mu(1-\pi)} \\
\Longrightarrow p(J \mid w) & =\frac{\mu^{J-w}}{(J-w)!}(1-\pi)^{J-w} e^{\mu(\pi-1)}
\end{aligned}
$$

## Bayesian models with multiple quantities

A Bayesian model with $M$ unknowns and $N$ datapoints attains the general form

$$
\begin{aligned}
q^{m} & \sim Q^{m}, & m & =1, \ldots, M \\
w^{n} \mid q^{1: M} & \sim P_{q^{1: M}}^{n}, & n & =1, \ldots, N
\end{aligned}
$$

The priors/likelihoods may or may not differ among unknowns/datapoints
The posterior of this model is given by

$$
\begin{aligned}
p\left(q^{1: M} \mid w^{1: N}\right) & \propto p\left(w^{1: N} \mid q^{1: M}\right) p\left(q^{1: M}\right) \\
& =\prod_{n=1}^{N} p\left(w^{n} \mid q^{1: M}\right) \times \prod_{m=1}^{M} p\left(q^{m}\right) \\
& =\prod_{n=1}^{N} P_{q^{1: M}}^{m}\left(w^{n}\right) \times \prod_{m=1}^{M} Q\left(q^{m}\right)
\end{aligned}
$$

## The Bayesian work-cycle

There are four main stages to probabilistic inference:

- Likelihood: we represent the likelihood by describing the mechanism giving rise to our data assuming hypothetical solution values
- Prior: we represent the prior by summarizing our beliefs about possible solution values
- Posterior: we derive the posterior distribution using our specific data values
- Inference: we use the posterior distribution to reach further conclusions as required by the task at hand

In the inference stage we may use the posterior to:

- estimate solution values ...like in parameter estimation, inverse problems, and data assimilation
- predict new data ...like in supervised learning
- cluster or classify existing data ...like in unsupervised learning
- guide the acquisition of new data ...like in experiment design, active learning, and BO

and many more including hypothesis testing, model comparison, and model selection


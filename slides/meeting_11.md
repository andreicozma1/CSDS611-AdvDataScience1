## Bayesian decision theory

- Problem definition
- Point-estimation problems

## BO

In BO, we rely on probabilistic surrogates of the objective function
We evaluate the objective only at query points and use them to

- refine the surrogate
- approximate the optimum and the optimizer
- decide on termination

We use the surrogate to guide the acquisition of subsequent queries
Termination and query selection are actions we take in view of the current surrogate which depends upon our past queries and, in this way, our past actions

Because our objective function is unknown, both actions give rise to (sequential) decision problems

In BO, the decision problems are inherently Bayesian

## Decision problems

A decision problem involves three spaces

- space of states $\mathcal{Q}$
- space of data $\mathcal{W}$
- space of actions $\mathcal{A}$
...this is our state-space...
...this is our data-space...
…this is our action-space…
...our states live here, $q \in \mathcal{Q}$
...our data live here, $w \in \mathcal{W}$
...our actions live here, $\alpha \in \mathcal{A}$

and asks for

- a decision rule

$$
D: \mathcal{W} \mapsto \mathcal{A}
$$

that selects an action $D(w)=\alpha \in \mathcal{A}$ given data $w \in \mathcal{W}$
Decision rules are derived through loss functions

$$
L: \mathcal{A} \times \mathcal{Q} \mapsto(-\infty,+\infty)
$$

The loss $\ell=L(\alpha, q)$ encodes the consequences of action $\alpha$ provided our state attains value $q$
...higher losses mean worse outcomes
...lower losses mean better outcomes

## Bayesian decision problems

A Bayesian decision problem consists of

- a Bayesian model that couples states and data

$$
\begin{aligned}
q & \sim Q \\
w \mid q & \sim P_{q}
\end{aligned}
$$

...our model's prior $Q$ is a probability distribution on the state-space $\mathcal{Q}$
...our model's likelihood $\left\{P_{q}\right\}_{q \in \mathcal{Q}}$ is a family of probability distributions on the data-space $\mathcal{W}$

- a loss function that couples states with actions

$$
L: \mathcal{A} \times \mathcal{Q} \mapsto(-\infty,+\infty)
$$

...our model's loss $L$ is a function on the joint action/state-space $\mathcal{A} \times \mathcal{Q}$ Our main goal is to derive a decision rule

## Bayesian decision problems

Given a Bayesian decision problem

$$
\begin{aligned}
q & \sim Q \\
w \mid q & \sim P_{q}
\end{aligned}
$$

The posterior expected loss of action $\alpha$ under data $w$ is given by

$$
\rho(\alpha, w)=\underbrace{\mathbb{E}_{q \mid w} L(\alpha, q)}_{\substack{\text { posterior } \\ \text { expectation }}} \quad \rho(\alpha, w)=\underbrace{\int_{\mathcal{Q}} d q L(\alpha, q) p(q \mid w)}_{\substack{\text { continuous } \\ \text { states }}} \quad \rho(\alpha, w)=\underbrace{\sum_{q \in \mathcal{Q}} L(\alpha, q) p(q \mid w)}_{\substack{\text { discrete } \\ \text { states }}}
$$

A Bayes action $\alpha_{w}^{*}$ under data $w$ is the minimizer

$$
\alpha_{w}^{*}=\operatorname{argmin}_{\alpha \in \mathcal{A}} \rho(\alpha, w)
$$

and the Bayes rule is
...this decision rule selects only Bayes actions

$$
D^{*}(w)=\alpha_{w}^{*}
$$

## Point estimation

In point-estimation, we seek to estimate a single value $\hat{\theta}$ for an unknown parameter $\theta$ of interest

- First, we develop a Bayesian model
$$
\begin{aligned}
\theta & \sim \Pi \\
\omega_{n} \mid \theta & \sim \Lambda_{\theta}, \quad n=1, \ldots, N
\end{aligned}
$$
for appropriate prior $\Pi$ and likelihood $\left\{\Lambda_{\theta}\right\}_{\theta}$
in this problem, the state-space is the parameter-space and the data-space is composite
- Then, we acquire our data $\omega_{1: N}$
- Finally, we choose a value $\hat{\theta}\left(\omega_{1: N}\right)$ from the parameter space in response to our acquired data $\omega_{1: N}$ in this problem, the action-space is the parameter-space

In the last step, we need to solve a decision problem ...which is Bayesian
Our decision problem is completed with a loss function and the derivation of the associated Bayes estimator which minimizes the posterior expected loss

## Point estimation

We seek a point-estimate for a continuous scalar parameter of interest $\theta \in \mathbb{R}$ under the squared deviation loss

$$
L(\hat{\theta}, \theta)=(\hat{\theta}-\theta)^{2}
$$

Our posterior expected loss is given by

$$
\begin{aligned}
\rho\left(\hat{\theta}, \omega_{1: N}\right) & =\mathbb{E}_{\theta \mid \omega_{1: N}} L(\hat{\theta}, \theta) \\
& =\int d \theta L(\hat{\theta}, \theta) p\left(\theta \mid \omega_{1: N}\right) \\
& =\int d \theta(\hat{\theta}-\theta)^{2} p\left(\theta \mid \omega_{1: N}\right) \\
& =\int d \theta\left(\hat{\theta}^{2}-2 \hat{\theta} \theta+\theta^{2}\right) p\left(\theta \mid \omega_{1: N}\right) \\
& =\hat{\theta}^{2} \int d \theta p\left(\theta \mid \omega_{1: N}\right)-2 \hat{\theta} \int d \theta \theta p\left(\theta \mid \omega_{1: N}\right)+\int d \theta \theta^{2} p\left(\theta \mid \omega_{1: N}\right) \\
& =\hat{\theta}^{2}-2 \hat{\theta} \underbrace{\mathbb{E}_{\theta \mid \omega_{1: N}} \theta}_{\text {posterior mean }}+\int d \theta \theta^{2} p\left(\theta \mid \omega_{1: N}\right)
\end{aligned}
$$

## Point estimation

We seek a point-estimate for a continuous scalar parameter of interest $\theta \in \mathbb{R}$ under the squared deviation loss

$$
L(\hat{\theta}, \theta)=(\hat{\theta}-\theta)^{2}
$$

Our posterior expected loss is given by

$$
\rho\left(\hat{\theta}, \omega_{1: N}\right)=\hat{\theta}^{2}-2 \hat{\theta} \mathbb{E}_{\theta \mid \omega_{1: N}} \theta+\int d \theta \theta^{2} p\left(\theta \mid \omega_{1: N}\right)
$$

The minimizer of the posterior expected loss solves

$$
\begin{aligned}
0 & =\frac{\partial}{\partial \hat{\theta}} \rho\left(\hat{\theta}, \omega_{1: N}\right) \\
& =\frac{\partial}{\partial \hat{\theta}}\left(\hat{\theta}^{2}-2 \hat{\theta} \mathbb{E}_{\theta \mid \omega_{1: N}} \theta+\int d \theta \theta^{2} p\left(\theta \mid \omega_{1: N}\right)\right) \\
& =\left(\frac{\partial}{\partial \hat{\theta}} \hat{\theta}^{2}\right)-2\left(\frac{\partial}{\partial \hat{\theta}} \hat{\theta}\right) \mathbb{E}_{\theta \mid \omega_{1: N}} \theta+\left(\frac{\partial}{\partial \hat{\theta}} \int d \theta \theta^{2} p\left(\theta \mid \omega_{1: N}\right)\right) \\
& =2 \hat{\theta}-2 \mathbb{E}_{\theta \mid \omega_{1: N}} \theta
\end{aligned}
$$

## Point estimation

We seek a point-estimate for a continuous scalar parameter of interest $\theta \in \mathbb{R}$ under the squared deviation loss

$$
L(\hat{\theta}, \theta)=(\hat{\theta}-\theta)^{2}
$$

Our posterior expected loss is given by

$$
\rho\left(\hat{\theta}, \omega_{1: N}\right)=\hat{\theta}^{2}-2 \hat{\theta} \mathbb{E}_{\theta \mid \omega_{1: N}} \theta+\int d \theta \theta^{2} p\left(\theta \mid \omega_{1: N}\right)
$$

Our Bayes estimator is

$$
\hat{\theta}=\mathbb{E}_{\theta \mid \omega_{1: N}} \theta
$$

## Summary of point estimation

We seek a point-estimate for a continuous scalar parameter of interest $\theta \in \mathbb{R}$
with the squared deviation loss

$$
L(\hat{\theta}, \theta)=(\hat{\theta}-\theta)^{2}
$$

the Bayes estimator is

$$
\hat{\theta}=\left(\begin{array}{c}
\text { posterior } \\
\text { mean } \\
\text { of } \theta
\end{array}\right)
$$

with the absolute deviation loss

$$
L(\hat{\theta}, \theta)=|\hat{\theta}-\theta|
$$

the Bayes estimator is

$$
\hat{\theta}=\left(\begin{array}{c}
\text { posterior } \\
\text { median } \\
\text { of } \theta
\end{array}\right)
$$

with the relaxed 0-1 loss

$$
L_{\epsilon}(\hat{\theta}, \theta)= \begin{cases}1, & |\hat{\theta}-\theta| \geq \epsilon \\ 0, & |\hat{\theta}-\theta|<\epsilon\end{cases}
$$

the (limiting) Bayes estimator is

$$
\lim _{\epsilon \rightarrow 0} \hat{\theta}_{\epsilon}=\left(\begin{array}{c}
\text { posterior } \\
\text { mode } \\
\text { of } \theta
\end{array}\right)
$$


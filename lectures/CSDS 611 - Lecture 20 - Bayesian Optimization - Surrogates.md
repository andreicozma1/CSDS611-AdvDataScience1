## BO

- Introduction to BO
- Surrogates in BO

## BO problems

An optimization problem is denoted with

$$
\min _{x \in \mathcal{X}} f(x) \quad \text { or } \quad \max _{x \in \mathcal{X}} f(x)
$$

The objective is a function $f: \mathcal{X} \mapsto \mathbb{R} \quad \ldots$ this is computable but very expensive
The search space is a set $\mathcal{X} \subset \mathbb{R}^{d}$...this must be bounded
The queries are points $x \in \mathcal{X}$
In Bayesian optimization, the objective is relatively expensive to compute
…a critical requirement is the evaluation of the objective only a few times
In Bayesian optimization, the objective is replaced by a probabilistic surrogate
...a surrogate is an inexpensive approximation of the objective
...a probabilistic surrogate provides a full probability distribution for every query
In Bayesian optimization, the surrogate is used to guide the selection of query points
...new queries provide data used to refine the surrogate
…the refined surrogate is used to select new queries
In Bayesian optimization, the policy is the rule that leads from existing data to new queries
…this includes the refinement of the surrogate and its usage

## BO surrogates

We consider an optimization problem

$$
\min _{x \in \mathcal{X}} f(x) \quad \text { or } \quad \max _{x \in \mathcal{X}} f(x)
$$

for an objective $f$ on a search space $\mathcal{X}$
...our objective must be real and scalar

- Our optimization policy is based on a surrogate
...we seek to establish $g \approx f$

$$
g \sim \mathrm{GP}_{\mathcal{X}}(m, C)
$$

for an appropriate mean $m: \mathcal{X} \mapsto \mathbb{R}$ and kernel $C: \mathcal{X} \times \mathcal{X} \mapsto \mathbb{R}$

- Our data are based on a likelihood

$$
y_{n} \mid g \sim \operatorname{Normal}\left(g\left(x_{n}\right), \sigma^{2}\right),
$$

...our likelihood allows for $N \rightarrow \infty$ and $\sigma \rightarrow 0$

$$
n=1, \ldots, N
$$

for an appropriate noise $\sigma \in \mathbb{R}$

- Our framework is determined by pre-selected $m, C$ and $\sigma$


## BO loops

We consider an optimization problem

$$
\min _{x \in \mathcal{X}} f(x) \quad \text { or } \quad \max _{x \in \mathcal{X}} f(x)
$$

with a surrogate

$$
\begin{aligned}
g & \sim \operatorname{GP}_{\mathcal{X}}(m, C) \\
y_{n} \mid g & \sim \operatorname{Normal}\left(g\left(x_{n}\right), \sigma^{2}\right),
\end{aligned}
$$

BO starts with:

- a pre-selected set of queries $\left\{x_{n}\right\}_{n=1}^{N^{0}} \subset \mathcal{X}$
- a pre-evaluated set of targets $\left\{y_{n}\right\}_{n=1}^{N^{0}} \subset \mathbb{R}$

BO proceeds iteratively:

- form posterior surrogate using existing data
- apply the surrogate to select new query
- evaluate new target
- update data ...our new data consist of $\left\{\left(x_{n}, y_{n}\right)\right\}_{n=1}^{N_{j}} \subset \mathcal{X} \times \mathbb{R}$ of size $N^{j}=N^{0}+j$

$$
n=1, \ldots, N
$$

...initial queries are obtained by space-filling designs ...targets are obtained by the objective, $y_{n}=f\left(x_{n}\right)$ ...at iteration $j=1,2, \ldots$ $g(x) \mid y_{1: N^{j-1}} \sim \operatorname{Normal}\left(m\left(x ; y_{1: N^{j-1}}\right), v\left(x ; y_{1: N^{j-1}}\right)\right)$ ...our new query is $x_{n}$ with $n=N^{0}+j$
...our new target is obtained by the objective, $y_{n}=f\left(x_{n}\right)$

## Space filling designs

We consider a bounded search space $\mathcal{X} \subset \mathbb{R}^{d}$ and seek a space-filling design
...space-filling designs spread queries near-evenly without large gaps or clusters

Monte Carlo space-filling designs include

- Uniform sampling ...highly inefficient
- Latin hyper-cube sampling ...improved coverage

![](https://cdn.mathpix.com/cropped/be86205c-0803-429d-97f0-ebeb33c3b3bc-5.jpg?height=264&width=268&top_left_y=195&top_left_x=870)
![](https://cdn.mathpix.com/cropped/be86205c-0803-429d-97f0-ebeb33c3b3bc-5.jpg?height=264&width=264&top_left_y=195&top_left_x=1192)

Quasi-Monte Carlo space-filling designs include

- Sobol sets ...preferable in high dimension
- Halton sets ...preferable in low dimension

Sobol and Halton sets are low-discrepancy quasi-random sequences
![](https://cdn.mathpix.com/cropped/be86205c-0803-429d-97f0-ebeb33c3b3bc-5.jpg?height=263&width=266&top_left_y=497&top_left_x=871)
![](https://cdn.mathpix.com/cropped/be86205c-0803-429d-97f0-ebeb33c3b3bc-5.jpg?height=262&width=263&top_left_y=498&top_left_x=1193)

## Query selection

Within our BO loop, at iteration $j=1,2, \ldots$ we have data and posterior surrogate

$$
\begin{aligned}
\left\{\left(x_{n}, y_{n}\right)\right\}_{n=1}^{N^{j-1}} & \subset \mathcal{X} \times \mathbb{R} \\
g(x) \mid y_{1: N^{j-1}} & \sim \operatorname{Normal}\left(m\left(x ; y_{1: N^{j-1}}\right), v\left(x ; y_{1: N^{j-1}}\right)\right)
\end{aligned}
$$

To balance exploitation/exploration across the search space, we derive an acquisition function $\quad \alpha: \mathcal{X} \mapsto \mathbb{R}$

- For maximization problems

$$
\max _{x \in \mathcal{X}} f(x)
$$

the upper confidence bound is

$$
\alpha_{U C B}\left(x ; y_{1: N^{j-1}}\right)=m\left(x ; y_{1: N^{j-1}}\right)+\beta \sqrt{v\left(x ; y_{1: N^{j-1}}\right)}
$$

and the next query is selected by

$$
x_{N^{j}}=\operatorname{argmax}_{x \in \mathcal{X}} \alpha_{U C B}\left(x ; y_{1: N^{j-1}}\right)
$$

In both cases, $\beta>0$ controls the exploitation/exploration trade-off

- For minimization problems

$$
\min _{x \in \mathcal{X}} f(x)
$$

the lower confidence bound is

$$
\alpha_{L C B}\left(x ; y_{1: N^{j-1}}\right)=m\left(x ; y_{1: N^{j-1}}\right)-\beta \sqrt{v\left(x ; y_{1: N^{j-1}}\right)}
$$

and the next query is selected by

$$
x_{N^{j}}=\operatorname{argmin}_{x \in \mathcal{X}} \alpha_{L C B}\left(x ; y_{1: N^{j-1}}\right)
$$

## Demonstration

![](https://cdn.mathpix.com/cropped/be86205c-0803-429d-97f0-ebeb33c3b3bc-7.jpg?height=198&width=1161&top_left_y=130&top_left_x=203)
![](https://cdn.mathpix.com/cropped/be86205c-0803-429d-97f0-ebeb33c3b3bc-7.jpg?height=427&width=1167&top_left_y=363&top_left_x=204)


## BO

- Acquisition functions in BO
- Examples

## BO loops

We consider an optimization problem

$$
\min _{x \in \mathcal{X}} f(x) \quad \text { or } \quad \max _{x \in \mathcal{X}} f(x)
$$

with a probabilistic surrogate

$$
\begin{aligned}
g & \sim \operatorname{GP}_{\mathcal{X}}(m, C) \\
y_{n} \mid g & \sim \operatorname{Normal}\left(g\left(x_{n}\right), \sigma^{2}\right),
\end{aligned}
$$

$$
n=1, \ldots, N
$$

for appropriate $m, C$ and $\sigma$

BO starts with: ...this is the initialization stage

- a pre-selected set of queries
- a pre-evaluated set of targets at the queries
...iteration $j=0$

BO proceeds iteratively: …this is the main loop

- form posterior surrogate using existing data
- apply the surrogate to select new query
- evaluate new target
- update data
...iterations $j=1,2, \ldots$

## Acquisition functions

Within our BO loop, at iteration $j=1,2, \ldots$ we have data and posterior surrogate

$$
\begin{aligned}
\left\{\left(x_{n}, y_{n}\right)\right\}_{n=1}^{N^{j-1}} & \subset \mathcal{X} \times \mathbb{R} \\
g(x) \mid y_{1: N^{j-1}} & \sim \operatorname{Normal}\left(m\left(x ; y_{1: N^{j-1}}\right), v\left(x ; y_{1: N^{j-1}}\right)\right)
\end{aligned}
$$

To balance exploitation/exploration across the search space, we derive acquisition functions

$$
\alpha^{j}: \mathcal{X} \mapsto \mathbb{R}
$$

We cast the selection of the next query point as an optimization

$$
\begin{aligned}
& x_{N^{j}}=\operatorname{argmax}_{x \in \mathcal{X}} \alpha^{j}(x) \\
& y_{N^{j}}=f\left(x_{N^{j}}\right)
\end{aligned}
$$

$$
\begin{aligned}
& x_{N^{j}}=\operatorname{argmin}_{x \in \mathcal{X}} \alpha^{j}(x) \\
& y_{N^{j}}=f\left(x_{N^{j}}\right)
\end{aligned}
$$

since $\alpha^{j}$ models expected utility or expected loss under posterior uncertainty

## UCB/LCB

Within our BO loop, at iteration $j=1,2, \ldots$ we have data and posterior surrogate

$$
\begin{aligned}
\left\{\left(x_{n}, y_{n}\right)\right\}_{n=1}^{N^{j-1}} & \subset \mathcal{X} \times \mathbb{R} \\
g(x) \mid y_{1: N^{j-1}} & \sim \operatorname{Normal}\left(m\left(x ; y_{1: N^{j-1}}\right), v\left(x ; y_{1: N^{j-1}}\right)\right)
\end{aligned}
$$

- For maximization problems, $\max _{x \in \mathcal{X}} f(x)$, the upper confidence bound is
$$
\alpha^{j}(x)=m(x)+\beta \sqrt{v(x)}
$$
and the next query is selected by
$$
x_{N^{j}}=\operatorname{argmax}_{x \in \mathcal{X}} \alpha^{j}(x)
$$
- For minimization problems, $\min _{x \in \mathcal{X}} f(x)$, the lower confidence bound is
$$
\alpha^{j}(x)=m(x)-\beta \sqrt{v(x)}
$$
and the next query is selected by
$$
x_{N^{j}}=\operatorname{argmin}_{x \in \mathcal{X}} \alpha^{j}(x)
$$

In both cases, $\beta>0$ controls the exploitation/exploration trade-off
...with $\beta \ll 1$ favoring exploitation
...with $\beta \gg 1$ favoring exploration

## EI

Within our BO loop, at iteration $j=1,2, \ldots$ we have data and posterior surrogate

$$
\begin{aligned}
\left\{\left(x_{n}, y_{n}\right)\right\}_{n=1}^{N^{j-1}} & \subset \mathcal{X} \times \mathbb{R} \\
g(x) \mid y_{1: N^{j-1}} & \sim \operatorname{Normal}\left(m\left(x ; y_{1: N^{j-1}}\right), v\left(x ; y_{1: N^{j-1}}\right)\right)
\end{aligned}
$$

- For maximization problems, $\max _{x \in \mathcal{X}} f(x)$, the expected improvement is
$$
\begin{aligned}
y_{*}^{j} & =\max y_{1: N^{j-1}} \\
\alpha^{j}(x) & =\left(\mu(x)-y_{*}^{j}\right) \Phi\left(\frac{\mu(x)-y_{*}^{j}}{\sqrt{v(x)}}\right) \\
& +\sqrt{v(x)} \phi\left(\frac{\mu(x)-y_{*}^{j}}{\sqrt{v(x)}}\right)
\end{aligned}
$$
and the next query is selected by
$$
x_{N j}=\operatorname{argmax}_{x \in \mathcal{X}} \alpha^{j}(x)
$$
- For maximization problems, $\min _{x \in \mathcal{X}} f(x)$, the expected improvement is
$$
\begin{aligned}
y_{*}^{j} & =\min y_{1: N^{j-1}} \\
\alpha^{j}(x) & =\left(y_{*}^{j}-\mu(x)\right) \Phi\left(\frac{y_{*}^{j}-\mu(x)}{\sqrt{v(x)}}\right) \\
& +\sqrt{v(x)} \phi\left(\frac{y_{*}^{j}-\mu(x)}{\sqrt{v(x)}}\right)
\end{aligned}
$$
and the next query is selected by
$$
x_{N j}=\operatorname{argmax}_{x \in \mathcal{X}} \alpha^{j}(x)
$$
In both cases, $\Phi(z)$ and $\phi(z)$ denote the CDF and PDF of the standard normal

## El with jitter

Within our BO loop, at iteration $j=1,2, \ldots$ we have data and posterior surrogate

$$
\begin{aligned}
\left\{\left(x_{n}, y_{n}\right)\right\}_{n=1}^{N^{j-1}} & \subset \mathcal{X} \times \mathbb{R} \\
g(x) \mid y_{1: N^{j-1}} & \sim \operatorname{Normal}\left(m\left(x ; y_{1: N^{j-1}}\right), v\left(x ; y_{1: N^{j-1}}\right)\right)
\end{aligned}
$$

- For maximization problems, $\max _{x \in \mathcal{X}} f(x)$, the expected improvement is
$$
\begin{aligned}
y_{*}^{j} & =\max y_{1: N^{j-1}}+\xi \\
\alpha^{j}(x) & =\left(\mu(x)-y_{*}^{j}\right) \Phi\left(\frac{\mu(x)-y_{*}^{j}}{\sqrt{v(x)}}\right) \\
& +\sqrt{v(x)} \phi\left(\frac{\mu(x)-y_{*}^{j}}{\sqrt{v(x)}}\right)
\end{aligned}
$$
and the next query is selected by
$$
x_{N j}=\operatorname{argmax}_{x \in \mathcal{X}} \alpha^{j}(x)
$$
In both cases, $\xi>0$ encourages more exploration
- For maximization problems, $\min _{x \in \mathcal{X}} f(x)$, the expected improvement is
$$
\begin{aligned}
y_{*}^{j} & =\min y_{1: N^{j-1}}-\xi \\
\alpha^{j}(x) & =\left(y_{*}^{j}-\mu(x)\right) \Phi\left(\frac{y_{*}^{j}-\mu(x)}{\sqrt{v(x)}}\right) \\
& +\sqrt{v(x)} \phi\left(\frac{y_{*}^{j}-\mu(x)}{\sqrt{v(x)}}\right)
\end{aligned}
$$
and the next query is selected by
$$
x_{N^{j}}=\operatorname{argmax}_{x \in \mathcal{X}} \alpha^{j}(x)
$$

## PI with jitter

Within our BO loop, at iteration $j=1,2, \ldots$ we have data and posterior surrogate

$$
\begin{aligned}
\left\{\left(x_{n}, y_{n}\right)\right\}_{n=1}^{N^{j-1}} & \subset \mathcal{X} \times \mathbb{R} \\
g(x) \mid y_{1: N^{j-1}} & \sim \operatorname{Normal}\left(m\left(x ; y_{1: N^{j-1}}\right), v\left(x ; y_{1: N^{j-1}}\right)\right)
\end{aligned}
$$

- For maximization problems, $\max _{x \in \mathcal{X}} f(x)$, the probability of improvement is
$$
\begin{aligned}
y_{*}^{j} & =\max y_{1: N^{j-1}}+\xi \\
\alpha^{j}(x) & =\Phi\left(\frac{\mu(x)-y_{*}^{j}}{\sqrt{v(x)}}\right)
\end{aligned}
$$
and the next query is selected by
$$
x_{N^{j}}=\operatorname{argmax}_{x \in \mathcal{X}} \alpha^{j}(x)
$$
In both cases, $\xi \geq 0$ encourages more exploration
- For maximization problems, $\min _{x \in \mathcal{X}} f(x)$, the probability of improvement is
$$
\begin{aligned}
y_{*}^{j} & =\min y_{1: N^{j-1}}-\xi \\
\alpha^{j}(x) & =\Phi\left(\frac{y_{*}^{j}-\mu(x)}{\sqrt{v(x)}}\right)
\end{aligned}
$$
and the next query is selected by
$$
x_{N^{j}}=\operatorname{argmax}_{x \in \mathcal{X}} \alpha^{j}(x)
$$

## TS

Within our BO loop, at iteration $j=1,2, \ldots$ we have data and posterior surrogate

$$
\begin{aligned}
\left\{\left(x_{n}, y_{n}\right)\right\}_{n=1}^{N^{j-1}} & \subset \mathcal{X} \times \mathbb{R} \\
g(x) \mid y_{1: N^{j-1}} & \sim \operatorname{Normal}\left(m\left(x ; y_{1: N^{j-1}}\right), v\left(x ; y_{1: N^{j-1}}\right)\right)
\end{aligned}
$$

- For maximization problems, $\max _{x \in \mathcal{X}} f(x)$,
Thompson sampling proceeds stochastically

$$
\alpha^{j}=g \mid y_{1: N^{j-1}}
$$

and the next query is selected by

$$
x_{N^{j}}=\operatorname{argmax}_{x \in \mathcal{X}} \alpha^{j}(x)
$$

- For maximization problems, $\min _{x \in \mathcal{X}} f(x)$,
Thompson sampling proceeds stochastically

$$
\alpha^{j}=g \mid y_{1: N^{j-1}}
$$

and the next query is selected by

$$
x_{N^{j}}=\operatorname{argmax}_{x \in \mathcal{X}} \alpha^{j}(x)
$$

In both cases, the acquisition function is our posterior surrogate, which is generated stochastically in each iteration

## Myopic and non-myopic policies

Myopic policies use acquisition functions are those that consider only one-step ahead

...ie, evaluate the immediate benefit of acquiring a query assuming this is the final round
...typically come with closed-formulas

Non-myopic policies use acquisition functions are those that plan multiple-steps ahead

...ie, evaluate the immediate benefit of acquiring a query as well as its improvement on subsequent evaluations
...typically do not come with closed-formulas

Non-myopic acquisitions simulate a sequence of future queries and consider how each sequence reduces uncertainty while improving subsequent decisions across the remaining budget

…they are computationally expensive
…they rely on approximations

## Demonstration

We seek to maximize an expensive objective on a 1D search space

$$
f:\left[x_{\min }, x_{\max }\right] \mapsto \mathbb{R}, \quad x_{\min }=-5,
$$

$$
x_{\max }=+10
$$

- Our surrogate is determined by
$$
\begin{aligned}
g & \sim \mathrm{GP}_{\mathcal{X}}(m, C) \\
y_{n} \mid g & \sim \operatorname{Normal}\left(g\left(x_{n}\right), \sigma^{2}\right),
\end{aligned}
$$
$$
n=1, \ldots
$$

with hyper-settings given by

$$
\begin{aligned}
m(x) & =\zeta, & \zeta & =20 \\
C\left(x^{\prime}, x^{\prime \prime}\right) & =\gamma^{2} \exp \left(-\left(\frac{x^{\prime}-x^{\prime \prime}}{\ell}\right)^{2}\right), & \gamma & =10, \\
\sigma & \ll 1 & & \ell=1
\end{aligned}
$$

- Our initial design is determined by
$$
x_{n}=x_{\min }+n \frac{x_{\max }-x_{\min }}{N^{0}+1}, \quad n=1, \ldots, N^{0},
$$
$$
N^{0}=3
$$

## UCB

$$
\beta=3
$$

![](https://cdn.mathpix.com/cropped/09c8c9b7-6768-42cc-9c80-09269892bbe6-12.jpg?height=783&width=1499&top_left_y=70&top_left_x=43)

## UCB

$$
\beta=1
$$

![](https://cdn.mathpix.com/cropped/09c8c9b7-6768-42cc-9c80-09269892bbe6-14.jpg?height=786&width=1499&top_left_y=66&top_left_x=43)

## UCB

$$
\beta=5
$$

![](https://cdn.mathpix.com/cropped/09c8c9b7-6768-42cc-9c80-09269892bbe6-16.jpg?height=780&width=1497&top_left_y=72&top_left_x=45)

US
![](https://cdn.mathpix.com/cropped/09c8c9b7-6768-42cc-9c80-09269892bbe6-18.jpg?height=782&width=1495&top_left_y=68&top_left_x=47)

## EI

![](https://cdn.mathpix.com/cropped/09c8c9b7-6768-42cc-9c80-09269892bbe6-20.jpg?height=784&width=1497&top_left_y=68&top_left_x=45)

PI
![](https://cdn.mathpix.com/cropped/09c8c9b7-6768-42cc-9c80-09269892bbe6-22.jpg?height=785&width=1498&top_left_y=67&top_left_x=46)

TS
![](https://cdn.mathpix.com/cropped/09c8c9b7-6768-42cc-9c80-09269892bbe6-24.jpg?height=778&width=1498&top_left_y=74&top_left_x=45)


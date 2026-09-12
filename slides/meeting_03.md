## Uncertain quantities of interest

- Classification of random quantities
- Statistical notation
- Random variables
- Probability functions

## Fundamental classification

Basic types of quantities of interest include

- scalars
- vectors
- functions
- measures
...temperature, energy, mass, distance, impedance, susceptibility, etc
...displacement, velocity, force, magnetization, etc
...responses, trajectories, landscapes, Lagrangians, Hamiltonians, etc
...distributions, etc

When definite values are not enough, a Qol is uncertain
Uncertain Qols are classified as

- parametric: these are formed by finitely many real scalars ...ie uncertain scalar and vector quantities
- non-parametric: there are formed by infinitely many real scalars ...ie uncertain functions and measures

Parametric uncertain quantities are termed random variables and studied in parametric Statistics or Statistics Non-parametric uncertain quantities are termed stochastic processes and studied in non-parametric Statistics

BO relies mainly on uncertain functions and secondarily on uncertain scalars

## Statistical notation

A shorthand like this

$$
W \sim P_{\theta}
$$

indicates an uncertain $W$ and its distribution $P_{\theta}$ which depends upon a certain parameter $\theta$

A probability distribution is a shorthand for

- what values our uncertain quantity may attain
- how to compute probabilities associated with these values

A shorthand like this

$$
W \mid \theta \sim P_{\theta}
$$

indicates an uncertain $W$ and its distribution $P_{\theta}$ which depends upon a uncertain parameter $\theta$
A distribution requires parameters that keep it well-defined

## Example 1

A shorthand like

$$
W \sim \operatorname{Poisson}(\mu)
$$

stands for

- the values $w$ that $W$ may attain are integers $0,1,2, \ldots$
- the probability mass of $W$ has the form
$$
p(w)=\frac{\mu^{w}}{w!} e^{-\mu}
$$
- the probability of $W$ taking any value between some $w_{\min }$ and $w_{\max }$ is given by
$$
P_{w_{\min }, w_{\max }}=\sum_{w_{\min }}^{w_{\max }} p(w)
$$
- the probability mass of $W$ depends on one parameter $\mu$

![](https://cdn.mathpix.com/cropped/6c572fc5-e336-40d2-8280-365d1e548395-04.jpg?height=636&width=282&top_left_y=175&top_left_x=1182)

## Example 2

A shorthand like

## $W \sim \operatorname{Binomial}(J, \pi)$

stands for

- the values $w$ that $W$ may attain are integers $0,1, \ldots, J$
- the probability mass of $W$ has the form
$$
p(w)=\binom{J}{w} \pi^{w}(1-\pi)^{J-w}
$$
- the probability of $W$ taking any value between some $w_{\min }$ and $w_{\max }$ is given by
$$
P_{w_{\min }, w_{\max }}=\sum_{w_{\min }}^{w_{\max }} p(w)
$$
- the probability mass of $W$ depends on two parameters $J$ and $\pi$

![](https://cdn.mathpix.com/cropped/6c572fc5-e336-40d2-8280-365d1e548395-05.jpg?height=636&width=282&top_left_y=175&top_left_x=1182)

## Example 3

A shorthand like

$$
W \sim \text { Laplace }(m, b)
$$

stands for

- the values $w$ that $W$ may attain are reals in $(-\infty,+\infty)$
- the probability density of $W$ has the form
$$
p(w)=\frac{1}{2 b} e^{-\frac{|w-m|}{b}}
$$
- the probability of $W$ taking any value between some $w_{\min }$ and $w_{\max }$ is given by
$$
P_{w_{\min }, w_{\max }}=\int_{w_{\min }}^{w_{\max }} p(w) d w
$$
- the probability density of $W$ depends on two parameters $m$ and $b$

![](https://cdn.mathpix.com/cropped/6c572fc5-e336-40d2-8280-365d1e548395-06.jpg?height=638&width=295&top_left_y=175&top_left_x=1182)

## Example 4

A shorthand like

$$
W \sim \text { Uniform }_{\left[a_{\min }, a_{\max }\right]}
$$

stands for

- the values $w$ that $W$ may attain are real numbers in $(-\infty,+\infty)$
- the probability density of $W$ has the form
$$
p(w)= \begin{cases}1 /\left(a_{\max }-a_{\min }\right), & w \in\left[a_{\min }, a_{\max }\right] \\ 0, & \text { elsewise }\end{cases}
$$
- the probability of $W$ taking any value between some $w_{\min }$ and $w_{\max }$ is given by
$$
P_{w_{\min }, w_{\max }}=\int_{w_{\min }}^{w_{\max }} p(w) d w
$$
- the probability density of $W$ depends on two parameters $a_{\text {min }}$ and $a_{\text {max }}$

![](https://cdn.mathpix.com/cropped/6c572fc5-e336-40d2-8280-365d1e548395-07.jpg?height=640&width=281&top_left_y=171&top_left_x=1182)

## Probability distributions

Shorthands like these

$$
W \sim P_{\theta} \quad W \mid \theta \sim P_{\theta}
$$

indicate uncertain quantities. On the LHS we have the quantities and on the RHS we have their distributions Distributions are often described generatively

$$
W \sim \operatorname{Binomial}(J, \pi) \quad W \sim \text { Laplace }(m, b)
$$

Generate $u_{j} \sim$ Uniform $_{[0,1]}$ for $j=1, \ldots, J$
Set $W=\sum_{j} \mathbb{I}_{u_{j}<\pi}$

Generate $u \sim$ Uniform $_{[0,1]}$
Set $v=u-\frac{1}{2}$
Set $W=m+b \log (1-2|v|) \operatorname{sgn}(v)$
Alternative scheme
Generate $u \sim$ Uniform $_{[0,1]}$ and $v \sim$ Uniform $_{[0,1]}$
Set $W= \begin{cases}m+b \log u & v<1 / 2 \\ m-b \log u & \text { elsewise }\end{cases}$

## Probability rules

All distributions are probability measures ...we need measure theory

Only parametric distributions are characterized by probability functions ...we need calculus
The rules to compute parametric probabilities depend on the values of the random variable

- A random variable may be discrete and we compute probabilities using a probability mass function
- A random variable may be continuous and we compute probabilities using a probability density function

Probability mass functions $p(w)$ of discrete random variables $W \sim P$ are non-negative and normalized

$$
p(w) \geq 0
$$

$$
\sum_{\substack{\text { all } \\ \text { values }}} p(w)=1
$$

Probability density functions $p(w)$ of continuous random variables $W \sim P$ are non-negative and normalized

$$
p(w) \geq 0
$$

$$
\int_{\text {vallues }} p(w) d w=1
$$

## Joint probability distributions

Separate equations indicate independence

$$
\begin{aligned}
& q \sim Q \\
& r \sim R
\end{aligned}
$$

Conditional equations indicate dependence

$$
\begin{aligned}
q \mid r & \sim Q_{r} \\
r & \sim R
\end{aligned}
$$

between the specified quantities
between the specified quantities

Such a model has a joint probability function
Such a model has a joint probability function

$$
p(q, r)=p(q) p(r)
$$

$$
p(q, r)=p(q \mid r) p(r)
$$

- No matter what the model is, joint and marginals are related by
$$
p(q)= \begin{cases}\int p(q, r) d r, & \text { for continuous } r \\ \sum p(q, r), & \text { for discrete } r\end{cases}
$$
$$
p(r)= \begin{cases}\int p(q, r) d q, & \text { for continuous } q \\ \sum p(q, r), & \text { for discrete } q\end{cases}
$$
- No matter what the model is, joint and conditionals are related by
$$
p(q, r)=p(q \mid r) p(r)
$$
$$
p(q, r)=p(r \mid q) p(q)
$$

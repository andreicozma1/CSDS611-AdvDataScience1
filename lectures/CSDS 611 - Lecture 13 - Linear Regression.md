## Linear regression

- Problem setup
- Least-squares solutions
- Bayesian solutions

## Regression problems

We consider input/output data
...ie, training examples

$$
\mathcal{D}=\left\{\left(x_{n}, y_{n}\right)\right\}_{n=1}^{N} \subset \mathbb{X} \times \mathbb{Y}
$$

with input space $x \in \mathbb{X}$ and output space $y \in \mathbb{Y}$
...ie, input features and target labels
Our goal is to obtain a regression function
...ie, supervised learning

$$
f: \mathbb{X} \mapsto \mathbb{Y}
$$

such that

$$
f\left(x_{n}\right) \approx y_{n},
$$

$n=1, \ldots, N$

- In the typical setting, our spaces are

$$
\begin{aligned}
& \mathbb{X} \equiv \mathbb{R}^{k} \\
& \mathbb{Y} \equiv \mathbb{R}
\end{aligned}
$$

and our requirement reads

$$
\left|y_{n}-f\left(x_{n}\right)\right| \approx 0,
$$

$$
n=1, \ldots, N
$$

## Linear regression problems

We consider data with $K$-dim features and 1 -dim targets

$$
\mathcal{D}=\left\{\left(x_{n}, y_{n}\right)\right\}_{n=1}^{N} \subset \mathbb{R}^{K} \times \mathbb{R}
$$

Our goal is to obtain a regression function

$$
f: \mathbb{R}^{K} \mapsto \mathbb{R}, \quad\left|y_{n}-f\left(x_{n}\right)\right| \approx 0, \quad n=1, \ldots, N
$$

Our problem is ill-posed
...because it fails uniqueness

- To work around non-uniqueness, in linear regression we choose a set of basis functions

$$
\phi^{m}: \mathbb{R}^{K} \mapsto \mathbb{R},
$$

$m=1, \ldots, M$
and seek only solutions of the form
...our basis functions may be non-linear

$$
f(x)=\sum_{m=1}^{M} c^{m} \phi^{m}(x)
$$

for appropriate coefficients $c^{1: M} \in \mathbb{R}$

## Linear regression problems

We consider data $\left\{\left(x_{n}, y_{n}\right)\right\}_{n=1}^{N} \subset \mathbb{R}^{K} \times \mathbb{R}$ and a set of basis functions $\left\{\phi^{m}\right\}_{m=1}^{M} \subset \mathbb{R}^{\mathbb{R}^{K}}$, our solution is

$$
f(x)=\sum_{m=1}^{M} c^{m} \phi^{m}(x)=\left[\begin{array}{llll}
\phi^{1}(x) & \phi^{2}(x) & \cdots & \phi^{M}(x)
\end{array}\right]\left(\begin{array}{c}
c^{1} \\
c^{2} \\
\vdots \\
c^{M}
\end{array}\right)=\phi(x) c
$$

Here, coefficients and basis are gathered in

$$
c \in \mathbb{R}^{M}, \quad \phi(x) \in \mathbb{R}^{1 \times M}
$$

Our requirement reads
...the design matrix is $\Phi$

$$
\left.\left.\begin{array}{c}
f\left(x_{1}\right) \approx y_{1} \\
f\left(x_{2}\right) \approx y_{2} \\
\ldots \\
f\left(x_{N}\right) \approx y_{N}
\end{array}\right\} \Longleftrightarrow \begin{array}{c}
\phi\left(x_{1}\right) c \approx y_{1} \\
\phi\left(x_{2}\right) c \approx y_{2} \\
\ldots \\
\phi\left(x_{N}\right) c \approx y_{N}
\end{array}\right\} \Longleftrightarrow\left[\begin{array}{c}
\phi\left(x_{1}\right) \\
\phi\left(x_{2}\right) \\
\vdots \\
\phi\left(x_{N}\right)
\end{array}\right] c \approx\left(\begin{array}{c}
y_{1} \\
y_{2} \\
\vdots \\
y_{N}
\end{array}\right) \Longleftrightarrow \Phi c \approx Y
$$

## Ordinary least-squares solution

We seek to solve a linear system of the form
$\Phi_{c} \approx Y$
$\Phi \in \mathbb{R}^{N \times M}$,
$c \in \mathbb{R}^{M}$,
$Y \in \mathbb{R}^{N}$
We cast this as a minimization problem

$$
c_{*}=\operatorname{argmin}_{c}\|\Phi c-Y\|=\operatorname{argmin}_{c}\|\Phi c-Y\|^{2}
$$

and obtain its solution via the normal equations

- Intuitively, this goes like this
$$
\begin{aligned}
\Phi c & =Y \\
\Phi^{t} \Phi c & =\Phi^{t} Y \\
\left(\Phi^{t} \Phi\right)^{-1}\left(\Phi^{t} \Phi\right) c & =\left(\Phi^{t} \Phi\right)^{-1} \Phi^{t} Y \\
c & =\left(\Phi^{t} \Phi\right)^{-1} \Phi^{t} Y \\
c & =\Phi^{\dagger} Y
\end{aligned}
$$
- Formally, this goes like this
$$
\begin{aligned}
0 & =\nabla_{c}\|\Phi c-Y\|^{2} \\
& =\nabla_{c}(\Phi c-Y)^{t}(\Phi c-Y) \\
& =\nabla_{c}\left[c^{t} \Phi^{t} \Phi c-2 c^{t} \Phi^{t} Y+Y^{t} Y\right] \\
& =2 \Phi^{t} \Phi c-2 \Phi^{t} Y \\
\Phi^{t} \Phi c & =\Phi^{t} Y
\end{aligned}
$$

Here,.$^{\dagger}$ denotes the Moore-Penrose pseudo-inverse
...the Gram matrix is $\Phi^{t} \Phi$

## Ridge least-squares solution

We seek to solve a linear system of the form
$\Phi_{c} \approx Y$
$\Phi \in \mathbb{R}^{N \times M}$,
$c \in \mathbb{R}^{M}$,
$Y \in \mathbb{R}^{N}$
We cast this as a minimization problem
...the regularizer is $\lambda>0$

$$
c_{*}=\operatorname{argmin}_{c}\left(\|\Phi c-Y\|^{2}+\lambda\|c\|^{2}\right)
$$

and obtain its solution via the ridge normal equations
This goes like this

$$
\begin{aligned}
0 & =\nabla_{c}\left[\|\Phi c-Y\|^{2}+\lambda\|c\|^{2}\right] \\
& =\nabla_{c}\left[(\Phi c-Y)^{t}(\Phi c-Y)+\lambda c^{t} c\right] \\
& =\nabla_{c}\left[c^{t} \Phi^{t} \Phi c-2 c^{t} \Phi^{t} Y+Y^{t} Y+\lambda c^{t} c\right] \\
& =2 \Phi^{t} \Phi c-2 \Phi^{t} Y+2 \lambda c
\end{aligned}
$$

$$
\begin{aligned}
\left(\Phi^{t} \Phi+\lambda I\right) c & =\Phi^{t} Y \\
c & =\left(\Phi^{t} \Phi+\lambda I\right)^{-1} \Phi^{t} Y
\end{aligned}
$$

## Bayesian regression

We consider data $\left\{\left(x_{n}, y_{n}\right)\right\}_{n=1}^{N} \subset \mathbb{R}^{K} \times \mathbb{R}$, a function $\phi: \mathbb{R}^{K} \mapsto \mathbb{R}^{1 \times M}$, and seek solutions

$$
f(x)=\phi(x) c
$$

This is a parameter estimation problem

- A basic Bayesian model consists of
$$
\begin{aligned}
c & \sim \operatorname{Normal}_{M}(\mu, C) \\
y_{n} \mid c & \sim \operatorname{Normal}\left(\phi\left(x_{n}\right) c, \eta\right), \quad n=1, \ldots, N
\end{aligned}
$$
- An extended model consists of
$$
\begin{array}{rlrl}
\tau & \sim \operatorname{Gamma}(\alpha, \psi) & & \\
c & \sim \operatorname{Normal}_{M}(\mu, C) & & \\
x_{n} & \sim \mathbb{F}, & & n=1, \ldots, N \\
y_{n} \mid c, \tau, x_{n} & \sim \operatorname{Normal}\left(\phi\left(x_{n}\right) c, 1 / \tau\right), & n=1, \ldots, N
\end{array}
$$

## Bayesian solution

Our basic Bayesian model is

$$
\begin{aligned}
c & \sim \operatorname{Normal}_{M}(\mu, C) \\
y_{n} \mid c & \sim \operatorname{Normal}\left(\phi\left(x_{n}\right) c, \eta\right), \quad n=1, \ldots, N
\end{aligned}
$$

This is equivalent to

$$
\begin{gathered}
c \sim \operatorname{Normal}_{M}(\mu, C) \\
\left(\begin{array}{c}
y_{1} \\
y_{2} \\
\vdots \\
y_{N}
\end{array}\right) \left\lvert\, c \sim \operatorname{Norma}_{N}\left(\left[\begin{array}{c}
\phi\left(x_{1}\right) \\
\phi\left(x_{2}\right) \\
\vdots \\
\phi\left(x_{N}\right)
\end{array}\right] c,\left[\begin{array}{cccc}
\eta & 0 & \cdots & 0 \\
0 & \eta & \cdots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \cdots & \eta
\end{array}\right]\right)\right.
\end{gathered}
$$

which, in turn, takes the form

$$
\begin{aligned}
c & \sim \operatorname{Normal}_{M}(\mu, C) \\
Y \mid c & \sim \operatorname{Normal}_{N}\left(\Phi_{c}, \eta I\right)
\end{aligned}
$$

## Bayesian solution

Our basic Bayesian model takes the form

$$
\begin{aligned}
c & \sim \operatorname{Normal}_{M}(\mu, C) \\
Y \mid c & \sim \operatorname{Normal}_{N}(\Phi c, \eta I)
\end{aligned}
$$

Because of conjugacy, our model's posterior is given by

$$
c \mid Y \sim \operatorname{Normal}_{M}\left(\mu^{\prime}, C^{\prime}\right)
$$

and the updated hyper-parameters are

$$
\begin{aligned}
& C^{\prime}=\left(C^{-1}+\frac{1}{\eta} \Phi^{t} \Phi\right)^{-1} \\
& \mu^{\prime}=C^{\prime}\left(C^{-1} \mu+\frac{1}{\eta} \Phi^{t} Y\right)
\end{aligned}
$$

Our MAP estimate is

$$
c_{*}=\mu^{\prime}=\left(C^{-1}+\frac{1}{\eta} \Phi^{t} \Phi\right)^{-1}\left(C^{-1} \mu+\frac{1}{\eta} \Phi^{t} Y\right)
$$

## Bayesian solution

Our basic Bayesian model takes the form

$$
\begin{aligned}
c & \sim \operatorname{Normal}_{M}(\mu, C) \\
Y \mid c & \sim \operatorname{Normal}_{N}(\Phi c, \eta I)
\end{aligned}
$$

Our MAP estimate is

$$
c_{*}=\left(C^{-1}+\frac{1}{\eta} \Phi^{t} \Phi\right)^{-1}\left(C^{-1} \mu+\frac{1}{\eta} \Phi^{t} Y\right)
$$

In the special case of $\eta=1$ and $\mu=0$ and $C=\frac{1}{\lambda} /$ ...this case recovers ridge regression

- our model is
$$
\begin{aligned}
c & \sim \operatorname{Normal}_{M}(0, I / \lambda) \\
Y \mid c & \sim \operatorname{Normal}_{N}(\Phi c, I)
\end{aligned}
$$
- our MAP estimate is
$$
c_{*}=\left(\lambda I+\Phi^{t} \Phi\right)^{-1} \Phi^{t} Y
$$

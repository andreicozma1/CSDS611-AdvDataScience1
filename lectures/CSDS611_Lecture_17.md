## Gaussian processess

- Kernel regression
- Definition

## Kernel regression

We have data $\left\{\left(x_{n}^{\sharp}, y_{n}^{\sharp}, \epsilon_{n}^{\sharp}\right)\right\}_{n=1}^{N^{\sharp}} \subset \mathbb{X} \times \mathbb{R} \times \mathbb{R}$ and seek predictions at $\left\{x_{n}^{\star}\right\}_{n=1}^{N^{\star}} \subset \mathbb{X}$ of an unknown function

$$
f: \mathbb{X} \mapsto \mathbb{R}
$$

We start with a mean and a symmetric positive semi-definite kernel

$$
\begin{aligned}
m: \mathbb{X} & \mapsto \mathbb{R} \\
v: \mathbb{X} \times \mathbb{X} & \mapsto \mathbb{R}
\end{aligned}
$$

In kernel regression, we follow these steps:

1. We discretize our input space
2. We discretize our regressor
3. We discretize our prior mean and covariance
4. We form our Bayesian model
5. We obtain our marginal posterior

## Kernel regression

- Step 1: we discretize our input space
$$
x^{\sharp}=\left(\begin{array}{c}
x_{1}^{\sharp} \\
\vdots \\
x_{N^{\sharp}}^{\sharp}
\end{array}\right) \in \mathbb{X}^{N^{\sharp}}
$$
$$
x^{\star}=\left(\begin{array}{c}
x_{1}^{\star} \\
\vdots \\
x_{N^{\star}}^{\star}
\end{array}\right) \in \mathbb{X}^{N^{\star}}
$$
- Step 2: we discretize our regressor
$$
f^{\sharp}=\left(\begin{array}{c}
f\left(x_{1}^{\sharp}\right) \\
\vdots \\
f\left(x_{N^{\sharp}}^{\sharp}\right)
\end{array}\right) \in \mathbb{R}^{N^{\sharp}}
$$
$$
f^{\star}=\left(\begin{array}{c}
f\left(x_{1}^{\star}\right) \\
\vdots \\
f\left(x_{N^{\star}}^{\star}\right)
\end{array}\right) \in \mathbb{R}^{N^{\star}}
$$

## Kernel regression

- Step 3: we discretize our prior mean...
$$
m^{\sharp}=\left(\begin{array}{c}
m\left(x_{1}^{\sharp}\right) \\
\vdots \\
m\left(x_{N^{\sharp}}^{\sharp}\right)
\end{array}\right) \in \mathbb{R}^{N^{\sharp}} \quad \quad m^{\star}=\left(\begin{array}{c}
m\left(x_{1}^{\star}\right) \\
\vdots \\
m\left(x_{N^{\star}}^{\star}\right)
\end{array}\right) \in \mathbb{R}^{N^{\star}}
$$
...and our prior covariance
$$
\begin{aligned}
& v^{\sharp \sharp}=\left[\begin{array}{ccc}
v\left(x_{1}^{\sharp}, x_{1}^{\sharp}\right) & \cdots & v\left(x_{1}^{\sharp}, x_{N^{\sharp}}^{\sharp}\right) \\
\vdots & \ddots & \vdots \\
v\left(x_{N^{\sharp}}^{\sharp}, x_{1}^{\sharp}\right) & \cdots & v\left(x_{N^{\sharp}}^{\sharp}, x_{N^{\sharp}}^{\sharp}\right)
\end{array}\right] \in \mathbb{R}_{\text {sym },+}^{N^{\sharp} \times N^{\sharp}} \quad v^{\sharp \star}=\left[\begin{array}{ccc}
v\left(x_{1}^{\sharp}, x_{1}^{\star}\right) & \cdots & v\left(x_{1}^{\sharp}, x_{N^{\star}}^{\star}\right) \\
\vdots & \ddots & \vdots \\
v\left(x_{N^{\sharp}}^{\sharp}, x_{1}^{\star}\right) & \cdots & v\left(x_{N^{\sharp}}^{\sharp}, x_{N^{\star}}^{\star}\right)
\end{array}\right] \in \mathbb{R}^{N^{\sharp} \times N^{\star}} \\
& v^{\star \sharp}=\left[\begin{array}{ccc}
v\left(x_{1}^{\star}, x_{1}^{\sharp}\right) & \cdots & v\left(x_{1}^{\star}, x_{N^{\sharp}}^{\sharp}\right) \\
\vdots & \ddots & \vdots \\
v\left(x_{N^{\star}}^{\star}, x_{1}^{\sharp}\right) & \cdots & v\left(x_{N^{\star}}^{\star}, x_{N^{\sharp}}^{\sharp}\right)
\end{array}\right] \in \mathbb{R}^{N^{\star} \times N^{\sharp}} \quad v^{\star \star}=\left[\begin{array}{ccc}
v\left(x_{1}^{\star}, x_{1}^{\star}\right) & \cdots & v\left(x_{1}^{\star}, x_{N^{\star}}^{\star}\right) \\
\vdots & \ddots & \vdots \\
v\left(x_{N^{\star}}^{\star}, x_{1}^{\star}\right) & \cdots & v\left(x_{N^{\star}}^{\star}, x_{N^{\star}}^{\star}\right)
\end{array}\right] \in \mathbb{R}_{s y m,+}^{N^{\star} \times N^{\star}}
\end{aligned}
$$

## Kernel regression

- Step 4: we form our Bayesian model
$$
\begin{aligned}
& \binom{f^{\sharp}}{f^{\star}} \sim \operatorname{Normal}_{N \sharp+N^{\star}}\left(\binom{m^{\sharp}}{m^{\star}},\left[\begin{array}{cc}
v^{\sharp \sharp} & v^{\sharp \star} \\
v^{\star \sharp} & v^{\star \star}
\end{array}\right]\right) \\
& y^{\#} \mid f^{\#} \sim \operatorname{Normal}_{N^{\#}}\left(f^{\#}, H^{\sharp \sharp}\right)
\end{aligned}
$$

Here, we gather measurements and errors in

$$
y^{\sharp}=\left(\begin{array}{c}
y_{1}^{\sharp} \\
\vdots \\
y_{N^{\sharp}}^{\sharp}
\end{array}\right) \in \mathbb{R}^{N^{\sharp}} \quad H^{\sharp \sharp}=\left[\begin{array}{ccc}
\left(\epsilon_{1}^{\sharp}\right)^{2} & \cdots & 0 \\
\vdots & \ddots & \vdots \\
0 & \cdots & \left(\epsilon_{N^{\sharp}}^{\sharp}\right)^{2}
\end{array}\right] \in \mathbb{R}_{\text {sym },+}^{N^{\sharp} \times N^{\sharp}}
$$

- Step 5: we obtain our marginal posterior
$$
f^{\star} \mid y^{\#} \sim \operatorname{Normal}_{N^{\star}}\left(\bar{m}^{\star}, \bar{v}^{\star \star}\right)
$$
...steps 1-5 define a recipe to work with probability distributions over uncertain functions ...these are non-parametric distributions

## Gaussian processes

A shorthand like

$$
f \sim \mathrm{GP}_{\mathbb{X}}(m, v)
$$

denotes a Gaussian process over $\mathbb{X}$
A Gaussian process is a random function

$$
f: \mathbb{X} \mapsto \mathbb{R}
$$

The parameters in the Gaussian process prior are

- the mean function $m$ which is a function
$$
m: \mathbb{X} \mapsto \mathbb{R}
$$
- the covariance kernel $v$ which is also a function
$$
v: \mathbb{X} \times \mathbb{X} \mapsto \mathbb{R}
$$
the covariance kernel is symmetric and positive semi-definite

## Gaussian processes

![](https://cdn.mathpix.com/cropped/b35df279-9d59-4bb1-8ea8-f83e43d0dbe2-07.jpg?height=103&width=263&top_left_y=88&top_left_x=190)

$$
f: \mathbb{X} \mapsto \mathbb{R}
$$

$$
m: \mathbb{X} \mapsto \mathbb{R}
$$

$$
v: \mathbb{X} \times \mathbb{X} \mapsto \mathbb{R}
$$

The probability distribution of a Gaussian process is given by ...there are no probability functions for GPs

- For any finite collection of input points ...includes variation in the positioning of $x_{n}$ and their sizing $N$

$$
x_{1}, x_{2}, \ldots, x_{N} \in \mathbb{X}
$$

the output values

$$
f\left(x_{1}\right), f\left(x_{2}\right), \ldots, f\left(x_{N}\right) \in \mathbb{R}
$$

are random variables

- These random variables jointly follow a multivariate normal distribution

$$
\left(\begin{array}{c}
f\left(x_{1}\right) \\
f\left(x_{2}\right) \\
\vdots \\
f\left(x_{N}\right)
\end{array}\right) \sim \operatorname{Normal}_{N}\left(\left(\begin{array}{c}
m\left(x_{1}\right) \\
m\left(x_{2}\right) \\
\vdots \\
m\left(x_{N}\right)
\end{array}\right),\left[\begin{array}{cccc}
v\left(x_{1}, x_{1}\right) & v\left(x_{1}, x_{2}\right) & \cdots & v\left(x_{1}, x_{N}\right) \\
v\left(x_{2}, x_{1}\right) & v\left(x_{2}, x_{2}\right) & \cdots & v\left(x_{2}, x_{N}\right) \\
\vdots & \vdots & \ddots & \vdots \\
v\left(x_{N}, x_{1}\right) & v\left(x_{N}, x_{2}\right) & \cdots & v\left(x_{N}, x_{N}\right)
\end{array}\right]\right)
$$

## Kernel regression revisited

We have data $\left\{\left(x_{n}^{\sharp}, y_{n}^{\sharp}, \epsilon_{n}^{\sharp}\right)\right\}_{n=1}^{N^{\sharp}} \subset \mathbb{X} \times \mathbb{R} \times \mathbb{R}$ of an unknown function

$$
f: \mathbb{X} \mapsto \mathbb{R}
$$

Kernel regression takes the form
…this fits more naturally within the Bayesian formalism

$$
\begin{aligned}
f & \sim \operatorname{GP}_{\mathbb{X}}(m, v) \\
y_{n}^{\sharp} \mid f & \sim \text { Normal }\left(f\left(x_{n}^{\sharp}\right),\left(\epsilon_{n}^{\sharp}\right)^{2}\right), \quad n=1, \ldots, N^{\sharp}
\end{aligned}
$$

for pre-selected mean and kernel functions

$$
\begin{aligned}
m: \mathbb{X} & \mapsto \mathbb{R} \\
v: \mathbb{X} \times \mathbb{X} & \mapsto \mathbb{R}
\end{aligned}
$$

## The Gaussian process prior

We consider a model $f \sim \mathrm{GP}_{\mathbb{X}}(m, v)$ and work on a problem with multiple targets of interest
…the targets of interest may include measurements, predictions, or both

- Our targets of interest are located at positions $x_{1}, \ldots, x_{N} \in \mathbb{X}$...our GP prior provides the statistics
$$
\left(\begin{array}{c}
f\left(x_{1}\right) \\
\vdots \\
f\left(x_{N}\right)
\end{array}\right) \sim \operatorname{Normal}_{N}\left(\left(\begin{array}{c}
m\left(x_{1}\right) \\
\vdots \\
m\left(x_{N}\right)
\end{array}\right),\left[\begin{array}{ccc}
v\left(x_{1}, x_{1}\right) & \cdots & v\left(x_{1}, x_{N}\right) \\
\vdots & \ddots & \vdots \\
v\left(x_{N}, x_{1}\right) & \cdots & v\left(x_{N}, x_{N}\right)
\end{array}\right]\right)
$$
- We add another target of interest $x_{?} \in \mathbb{X}$...our GP prior provides the statistics
$$
\left(\begin{array}{c}
f\left(x_{1}\right) \\
\vdots \\
f\left(x_{N}\right) \\
f\left(x_{?}\right)
\end{array}\right) \sim \operatorname{Normal}_{N+1}\left(\left(\begin{array}{c}
m\left(x_{1}\right) \\
\vdots \\
m\left(x_{N}\right) \\
m\left(x_{?}\right)
\end{array}\right),\left[\begin{array}{cccc}
v\left(x_{1}, x_{1}\right) & \cdots & v\left(x_{1}, x_{N}\right) & v\left(x_{1}, x_{?}\right) \\
\vdots & \ddots & \vdots & \vdots \\
v\left(x_{N}, x_{1}\right) & \cdots & v\left(x_{N}, x_{N}\right) & v\left(x_{N}, x_{?}\right) \\
v\left(x_{?}, x_{1}\right) & \cdots & v\left(x_{?}, x_{N}\right) & v\left(x_{?}, x_{?}\right)
\end{array}\right]\right)
$$

## The Gaussian process prior

In compact notation, our statistics are

$$
\begin{aligned}
& \left(\begin{array}{c}
f_{1} \\
\vdots \\
f_{N}
\end{array}\right) \sim \operatorname{Normal}_{N}\left(\left(\begin{array}{c}
m_{1} \\
\vdots \\
m_{N}
\end{array}\right),\left[\begin{array}{ccc}
v_{11} & \cdots & v_{1 N} \\
\vdots & \ddots & \vdots \\
v_{N 1} & \cdots & v_{N N}
\end{array}\right]\right) \\
& \left(\begin{array}{c}
f_{1} \\
\vdots \\
f_{N} \\
f_{?}
\end{array}\right) \sim \operatorname{Normal}_{N+1}\left(\left(\begin{array}{c}
m_{1} \\
\vdots \\
m_{N} \\
m_{?}
\end{array}\right),\left[\begin{array}{cccc}
v_{11} & \cdots & v_{1 N} & v_{1 ?} \\
\vdots & \ddots & \vdots & \vdots \\
v_{N 1} & \cdots & v_{N N} & v_{N ?} \\
v_{? 1} & \cdots & v_{? N} & v_{? ?}
\end{array}\right]\right)
\end{aligned}
$$

These are related by

$$
\begin{aligned}
p\left(f_{1}, \ldots, f_{N}\right) & =\int_{-\infty}^{+\infty} d f_{?} p\left(f_{1}, \ldots, f_{N}, f_{?}\right) \\
p\left(f_{1}, \ldots, f_{N}, f_{?}\right) & =p\left(f_{?} \mid f_{1}, \ldots, f_{N}\right) p\left(f_{1}, \ldots, f_{N}\right) \\
p\left(f_{?}\right) & =\int_{-\infty}^{+\infty} d f_{1} \cdots \int_{-\infty}^{+\infty} d f_{N} p\left(f_{1}, \ldots, f_{N}, f_{?}\right)
\end{aligned}
$$

## Demonstration

We consider a Gaussian process

$$
f \sim \mathrm{GP}_{\mathbb{R}}(m, v)
$$

over the real line $\mathbb{R}$

- Our mean function is
$$
m(x)=x^{2}, \quad x \in \mathbb{R}
$$
- Our covariance kernel is
$$
v\left(x^{\prime}, x^{\prime \prime}\right)=100 \exp \left(-\frac{\left(x^{\prime}-x^{\prime \prime}\right)^{2}}{2}\right), \quad x^{\prime}, x^{\prime \prime} \in \mathbb{R}
$$
…this is a squared-exponential kernel

![](https://cdn.mathpix.com/cropped/b35df279-9d59-4bb1-8ea8-f83e43d0dbe2-11.jpg?height=688&width=544&top_left_y=127&top_left_x=883)


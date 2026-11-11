## Gaussian random scalars

- Univariate normal distributions

## Univariate normal

A Normal random variable is denoted with

$$
w \sim \operatorname{Normal}(\mu, v)
$$

This variable attains real values in $(-\infty,+\infty) \equiv \mathbb{R}$
The probability density function is given by

$$
p(w)=\operatorname{Normal}(w ; \mu, v)=\frac{1}{\sqrt{2 \pi v}} \exp \left(-\frac{1}{2} \frac{(w-\mu)^{2}}{v}\right)
$$

The parameters are reals $\mu \in(-\infty,+\infty) \equiv \mathbb{R}$ and $v \in(0, \infty)$

- It matters because it is the basis for everything BO
- It is simulated by
$$
\mathrm{w}=\mathrm{mu}+\mathrm{s} * \text { randn } ;
$$
which reads $w=\mu+\sigma \zeta$ and $\zeta \sim \operatorname{Normal}(0,1)$

![](https://cdn.mathpix.com/cropped/9fe8faa3-3a57-4b5a-a81b-d3fd64705062-2.jpg?height=639&width=282&top_left_y=167&top_left_x=1182)

## Simulation

To generate a normal variate

$$
w \sim \operatorname{Normal}(\mu, v)
$$

- First, find a $\sigma$ such that
$$
\sigma^{2}=v
$$
- Then, generate a standard normal variate
$$
\zeta \sim \operatorname{Normal}(0,1)
$$

The algorithm works because of the de-whitening property

$$
\left.\begin{array}{r}
\zeta \sim \operatorname{Normal}(0,1) \\
w=\mu+\sigma \zeta
\end{array}\right\} \Rightarrow w \sim \operatorname{Normal}\left(\mu, \sigma^{2}\right)
$$

- Finally, transform

$$
w=\mu+\sigma \zeta
$$

In this algorithm, we have two choices

$$
\begin{aligned}
\sigma & =+\sqrt{v} & \sigma & =-\sqrt{v} \\
w & =\mu+\sqrt{v} \zeta & w & =\mu-\sqrt{v} \zeta
\end{aligned}
$$

## Transformation properties

De-whitening property

$$
\left.\begin{array}{rl}
\zeta & \sim \operatorname{Normal}(0,1) \\
w & =\mu+\sigma \zeta
\end{array}\right\} \Rightarrow w \sim \operatorname{Normal}\left(\mu, \sigma^{2}\right)
$$

Whitening property

$$
\left.\begin{array}{l}
x \sim \operatorname{Normal}(\mu, v) \\
y=\frac{x-\mu}{ \pm \sqrt{v}}
\end{array}\right\} \Rightarrow y \sim \operatorname{Normal}(0,1)
$$

General transformation property

$$
\left.\begin{array}{l}
x \sim \operatorname{Normal}(m, v) \\
y=\alpha+\beta x
\end{array}\right\} \Rightarrow y \sim \operatorname{Normal}\left(\alpha+\beta m, \beta^{2} v\right)
$$

## Other properties

Addition property

$$
\left.\begin{array}{l}
x_{1} \sim \operatorname{Normal}\left(m_{1}, v_{1}\right) \\
x_{2} \sim \operatorname{Normal}\left(m_{2}, v_{2}\right) \\
y=x_{1}+x_{2}
\end{array}\right\} \Rightarrow y \sim \operatorname{Normal}\left(m_{1}+m_{2}, v_{1}+v_{2}\right)
$$

Magnitude properties

$$
\left.\begin{array}{l}
x_{n} \sim \operatorname{Normal}(0,1) \\
y=\sum_{n=1}^{N} x_{n}^{2}
\end{array}\right\} \Rightarrow y \sim \chi_{N}^{2}
$$

## Important functions

The cumulative distribution function of $w \sim \operatorname{Normal}(\mu, v)$ is

$$
\begin{aligned}
C(w) & =\int_{-\infty}^{w} d w^{\prime} p\left(w^{\prime}\right) \\
& =\int_{-\infty}^{w} d w^{\prime} \operatorname{Normal}\left(w^{\prime} ; \mu, v\right) \\
& =\frac{1}{2}\left(1+\operatorname{erf}\left(\frac{1}{\sqrt{2}} \frac{w-\mu}{\sqrt{v}}\right)\right) \\
& =\Phi\left(\frac{w-\mu}{\sqrt{v}}\right)
\end{aligned}
$$

Our $C(w)$ is a continuous and strictly increasing function $C: \mathbb{R} \mapsto(0,1)$

The quantile function is the inverse $Q:(0,1) \mapsto \mathbb{R}$

$$
\begin{aligned}
Q(p) & =C^{-1}(p) \\
& =\mu+\sqrt{2 v} \operatorname{erf}^{-1}(2 p-1) \\
& =\mu+\sqrt{v} \Phi^{-1}(p)
\end{aligned}
$$

## Credible intervals

A credible set is a set of values with a designated total probability of containing the value of our uncertain quantity

The $\gamma$-credible interval is a symmetric interval with a total probability $\gamma \in[0,1]$

This is given by

$$
\left[Q\left(\frac{1}{2}-\frac{\gamma}{2}\right), Q\left(\frac{1}{2}+\frac{\gamma}{2}\right)\right] \subset \mathbb{R}
$$

![](https://cdn.mathpix.com/cropped/9fe8faa3-3a57-4b5a-a81b-d3fd64705062-7.jpg?height=645&width=643&top_left_y=166&top_left_x=837)

## Bayesian considerations

In Bayesian models, normals are more conveniently parametrized by precision $\tau=1 / v$

$$
w \sim \operatorname{Normal}(\mu, 1 / \tau)
$$

Unknown mean, known variance

$$
\begin{aligned}
\mu & \sim \operatorname{Normal}(M, 1 / T) \\
w \mid \mu & \sim \operatorname{Normal}(\mu, 1 / \tau)
\end{aligned}
$$

Known mean, unknown variance

$$
\begin{aligned}
\tau & \sim \operatorname{Gamma}(\Phi, \Psi) \\
w \mid \tau & \sim \operatorname{Normal}(\mu, 1 / \tau)
\end{aligned}
$$

Unknown mean, unknown variance

$$
\begin{aligned}
\tau & \sim \operatorname{Gamma}(\Phi, \Psi) \\
\mu \mid \tau & \sim \operatorname{Normal}(M, \eta / \tau) \\
w \mid \mu, \tau & \sim \operatorname{Normal}(\mu, 1 / \tau)
\end{aligned}
$$

The posterior is

$$
\begin{aligned}
\mu \mid w & \sim \operatorname{Normal}\left(M^{\prime}, 1 / T^{\prime}\right) \\
M^{\prime} & =\frac{T M+\tau \mu}{T+\tau} \\
T^{\prime} & =\frac{1}{T+\tau}
\end{aligned}
$$

The posterior is

$$
\begin{aligned}
\tau \mid w & \sim \operatorname{Gamma}\left(\Phi^{\prime}, \Psi^{\prime}\right) \\
\Phi^{\prime} & =\Phi+\frac{1}{2} \\
\Psi^{\prime} & =\frac{1}{\frac{1}{\Psi}+\frac{(w-\mu)^{2}}{2}}
\end{aligned}
$$

The posterior is

$$
\begin{aligned}
\tau \mid w & \sim \operatorname{Gamma}\left(\Phi^{\prime}, \Psi^{\prime}\right) \\
\mu \mid w, \tau & \sim \operatorname{Normal}\left(M^{\prime}, \eta^{\prime} / \tau\right) \\
\Phi^{\prime} & =\ldots \ldots \\
\Psi^{\prime} & =\ldots \ldots \\
M^{\prime} & =\ldots \ldots \\
\eta^{\prime} & =\ldots \ldots
\end{aligned}
$$


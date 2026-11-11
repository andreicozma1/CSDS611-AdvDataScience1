## Random variables

- Non-Gaussian distributions

## Statistical notation

Shorthands like these

$$
W \sim P_{\theta}
$$

$$
W \mid \theta \sim P_{\theta}
$$

indicate an uncertain quantity and its distribution which depends upon certain or uncertain parameters

A probability distribution is a shorthand for

- what values our uncertain quantity may attain
- how to compute probabilities associated with these values

Distributions of parametric quantities, ie random variables, are characterized by probability functions

- A random variable may be discrete and it is associated with a probability mass function
- A random variable may be continuous and it is associated with a probability density function

## Discrete random variables

## Bernoulli

A Bernoulli random variable is denoted with

$$
w \sim \operatorname{Bernoulli}(\pi)
$$

This variable attains integer values in \{0,1\}
The probability mass function is given by

$$
\begin{aligned}
p(w)=\operatorname{Bernoulli}(w ; \pi) & = \begin{cases}\pi, & \text { for } w=1 \\
1-\pi, & \text { for } w=0\end{cases} \\
& =\pi^{w}(1-\pi)^{1-w}
\end{aligned}
$$

The parameter is real $\pi \in[0,1]$

- It matters because it is a simple model for many systems
- It is simulated by

w = (rand<pi);
which reads $w=1_{u<\pi}$ and $u \sim$ Uniform $_{[0,1]}$
![](https://cdn.mathpix.com/cropped/cfb844fd-9b55-4e7d-bdb5-69f370cfefc9-04.jpg?height=639&width=284&top_left_y=167&top_left_x=1181)

## Binomial

A binomial random variable is denoted with

$$
w \sim \operatorname{Binomial}(J, \pi)
$$

This variable attains integer values in $\{0,1, \ldots, J\}$
The probability mass function is given by

$$
p(w)=\operatorname{Binomial}(w ; J, \pi)=\binom{J}{w} \pi^{w}(1-\pi)^{w}
$$

The parameters are integer $J=0,1, \ldots$ and real $\pi \in[0,1]$

- It matters because it is a simple model well suited for very many systems
- It is simulated by
$$
\mathrm{w}=\operatorname{sum}(\operatorname{rand}(\mathrm{J}, 1)<\mathrm{pi}) ;
$$
which reads $w=\sum_{j=1}^{J} \beta_{j}$ and $\beta_{j} \sim \operatorname{Bernoulli}(\pi)$

![](https://cdn.mathpix.com/cropped/cfb844fd-9b55-4e7d-bdb5-69f370cfefc9-05.jpg?height=639&width=290&top_left_y=167&top_left_x=1181)

## Poisson

A Poisson random variable is denoted with

$$
w \sim \text { Poisson }(\mu)
$$

This variable attains integer values in $\{0,1, \ldots\}$
The probability mass function is given by

$$
p(w)=\operatorname{Poisson}(w ; \mu)=\frac{\mu^{w}}{w!} e^{-\mu}
$$

The parameter is real $\mu \in(0, \infty)$

- It matters because it lets us calculate the probability of a specific number of random, independent events happening over a fixed block of time or space.
- It is approximated by
$$
\operatorname{Poisson}(\mu) \approx \operatorname{Binomial}(J, \mu / J), \quad J \gg 1
$$

![](https://cdn.mathpix.com/cropped/cfb844fd-9b55-4e7d-bdb5-69f370cfefc9-06.jpg?height=639&width=282&top_left_y=167&top_left_x=1182)

## Geometric

A geometric random variable is denoted with

$$
w \sim \operatorname{Geometric}(\pi)
$$

This variable attains integer values in $\{1,2, \ldots\}$
The probability mass function is given by

$$
p(w)=\text { Geometric }(w ; \pi)=(1-\pi)^{w-1} \pi
$$

The parameter is real $\pi \in(0,1]$

- It matters because it predicts the number of trials needed to achieve a single success in a series of independent events
- It matters also because it is characterized by memorylessness
$$
\operatorname{Prob}(w>s+t \mid w>s)=\operatorname{Prob}(w>t)
$$

![](https://cdn.mathpix.com/cropped/cfb844fd-9b55-4e7d-bdb5-69f370cfefc9-07.jpg?height=639&width=282&top_left_y=167&top_left_x=1182)

## Continuous random variables

## Uniform

A uniform random variable is denoted with

$$
w \sim \text { Uniform }_{[\alpha, \beta]}
$$

This variable attains real values in $[\alpha, \beta]$
The probability density function is given by

$$
p(w)= \begin{cases}\frac{1}{\beta-\alpha}, & \text { for } w \in[\alpha, \beta] \\ 0, & \text { for } w \notin[\alpha, \beta]\end{cases}
$$

The parameters are real $-\infty<\alpha<\beta<+\infty$

- It matters because it is the only random variable that can be simulated in a computer
![](https://cdn.mathpix.com/cropped/cfb844fd-9b55-4e7d-bdb5-69f370cfefc9-09.jpg?height=643&width=282&top_left_y=163&top_left_x=1182)


## Beta

A beta random variable is denoted with

$$
w \sim \operatorname{Beta}(\alpha, \beta)
$$

This variable attains real values in [0,1]
The probability density function is given by

$$
p(w)= \begin{cases}\frac{w^{\alpha-1}(1-w)^{\beta-1}}{B(\alpha, \beta)}, & \text { for } w \in[0,1] \\ 0, & \text { for } w \notin[0,1]\end{cases}
$$

The parameters are reals $\alpha, \beta \in(0, \infty)$

- It matters because it is a convenient prior for Bernoulli likelihoods in the natural parametrization

![](https://cdn.mathpix.com/cropped/cfb844fd-9b55-4e7d-bdb5-69f370cfefc9-10.jpg?height=638&width=282&top_left_y=168&top_left_x=1182)

## von Mises

A von Mises random variable is denoted with

$$
w \sim \operatorname{vonMises}(\mu, \kappa)
$$

This variable attains real values in $[0,2 \pi]$
The probability density function is given by

$$
p(w)= \begin{cases}\frac{e^{\kappa \cos (w-\mu)}}{2 \pi I_{0}(\kappa)}, & \text { for } w \in[0,2 \pi] \\ 0, & \text { for } w \notin[0,2 \pi]\end{cases}
$$

The parameters are reals $\mu \in(-\infty,+\infty)$ and $\kappa \in(0, \infty)$

- It matters because it is the circular analogue to the normal distribution for directional or angular data

![](https://cdn.mathpix.com/cropped/cfb844fd-9b55-4e7d-bdb5-69f370cfefc9-11.jpg?height=640&width=288&top_left_y=165&top_left_x=1182)

## Exponential

An exponential random variable is denoted with

$$
w \sim \text { Exponential }(\mu)
$$

This variable attains real values in $[0, \infty)$
The probability density function is given by

$$
p(w)= \begin{cases}\frac{1}{\mu} e^{-w / \mu}, & \text { for } w \geq 0 \\ 0, & \text { for } w<0\end{cases}
$$

The parameter is real $\mu \in(0, \infty)$

- It matters because it is characterized by memorylessness
$$
\operatorname{Prob}(w>s+t \mid w>s)=\operatorname{Prob}(w>t)
$$
- It is simulated by
$$
\mathrm{w}=-\mathrm{mu} * \log (\text { rand }) ;
$$

![](https://cdn.mathpix.com/cropped/cfb844fd-9b55-4e7d-bdb5-69f370cfefc9-12.jpg?height=638&width=282&top_left_y=175&top_left_x=1182)
which reads $w=-\mu \log (u)$ and $u \sim \operatorname{Uniform}_{[0,1]}$

## Gamma

A gamma random variable is denoted with

$$
w \sim \operatorname{Gamma}(\phi, \psi)
$$

This variable attains real values in $[0, \infty)$
The probability density function is given by

$$
p(w)= \begin{cases}\frac{1}{\Gamma(\phi) \psi^{\phi}} w^{\phi-1} e^{-w / \psi}, & \text { for } w \geq 0 \\ 0, & \text { for } w<0\end{cases}
$$

The parameters are real $\phi, \psi \in(0, \infty)$

- It matters because it generalizes exponential random variables
- It matters because it is a convenient prior for very many likelihoods

![](https://cdn.mathpix.com/cropped/cfb844fd-9b55-4e7d-bdb5-69f370cfefc9-13.jpg?height=639&width=284&top_left_y=167&top_left_x=1181)

## Weibull

A Weibull random variable is denoted with

$$
w \sim \text { Weibull }(\phi, \psi)
$$

This variable attains real values in $[0, \infty)$
The probability density function is given by

$$
p(w)= \begin{cases}\frac{\phi}{\psi}\left(\frac{w}{\psi}\right)^{\phi-1} e^{-(w / \psi)^{\phi}}, & \text { for } w \geq 0 \\ 0, & \text { for } w<0\end{cases}
$$

The parameters are real $\phi, \psi \in(0, \infty)$

- It is simulated by
$$
\mathrm{w}=\mathrm{psi} *(-\log (\text { rand })){ }^{\wedge}(1 / \mathrm{phi}) ;
$$
which reads $w=\psi(-\log (u))^{1 / \phi}$ and $u \sim \operatorname{Uniform}_{[0,1]}$

![](https://cdn.mathpix.com/cropped/cfb844fd-9b55-4e7d-bdb5-69f370cfefc9-14.jpg?height=636&width=284&top_left_y=169&top_left_x=1181)

## Beta-prime

A beta-prime random variable is denoted with

$$
w \sim \operatorname{BetaPrime}(\alpha, \beta)
$$

This variable attains real values in $[0, \infty)$
The probability density function is given by

$$
p(w)= \begin{cases}\frac{w^{\alpha-1}(1+w)^{-\alpha-\beta}}{B(\alpha, \beta)}, & \text { for } w \geq 0 \\ 0, & \text { for } w<0\end{cases}
$$

The parameters are reals $\alpha, \beta \in(0, \infty)$

- It matters because it is a convenient prior for Bernoulli likelihoods parametrized in terms of odds

![](https://cdn.mathpix.com/cropped/cfb844fd-9b55-4e7d-bdb5-69f370cfefc9-15.jpg?height=639&width=282&top_left_y=175&top_left_x=1182)

$$
\chi
$$

A $\chi$ random variable is denoted with

$$
w \sim \chi_{k}
$$

This variable attains real values in $[0, \infty)$
The probability density function is given by

$$
p(w)= \begin{cases}\frac{w^{k-1} e^{-w^{2} / 2}}{2^{k / 2-1} \Gamma(k / 2)}, & \text { for } w \geq 0 \\ 0, & \text { for } w<0\end{cases}
$$

The parameter is real $k \in(0, \infty)$

- It matters because it is distribution of the Euclidean norm of multivariate normals

![](https://cdn.mathpix.com/cropped/cfb844fd-9b55-4e7d-bdb5-69f370cfefc9-16.jpg?height=639&width=282&top_left_y=175&top_left_x=1182)

$$
\chi^{2}
$$

A $\chi^{2}$ random variable is denoted with

$$
w \sim \chi_{k}^{2}
$$

This variable attains real values in $[0, \infty)$
The probability density function is given by

$$
p(w)= \begin{cases}\frac{w^{k / 2-1} e^{-w / 2}}{2^{k / 2} \Gamma(k / 2)}, & \text { for } w \geq 0 \\ 0, & \text { for } w<0\end{cases}
$$

The parameter is real $k \in(0, \infty)$

- It matters because it is distribution of the squared Euclidean norm of multivariate normals

![](https://cdn.mathpix.com/cropped/cfb844fd-9b55-4e7d-bdb5-69f370cfefc9-17.jpg?height=648&width=282&top_left_y=166&top_left_x=1182)

## Student-t

A Student-t random variable is denoted with

$$
w \sim \text { Student }_{\nu}(\mu, v)
$$

This variable attains real values in $(-\infty,+\infty)$
The probability density function is given by

$$
p(w)=\frac{\Gamma\left(\frac{\nu+1}{2}\right)}{\Gamma\left(\frac{\nu}{2}\right) \sqrt{v \pi \nu}}\left(1+\frac{1}{\nu} \frac{(w-\mu)^{2}}{v}\right)^{-(\nu+1) / 2}
$$

The parameters are reals $\nu, v \in(0, \infty)$ and $\mu \in(-\infty,+\infty)$

- It matters because it has heavy tails
- It is approximated by
$$
\operatorname{Normal}\left(\mu, \sigma^{2}\right) \approx \operatorname{StudentT}_{\nu}\left(\mu, \sigma^{2}\right), \quad \nu \gg 1
$$

![](https://cdn.mathpix.com/cropped/cfb844fd-9b55-4e7d-bdb5-69f370cfefc9-18.jpg?height=643&width=282&top_left_y=163&top_left_x=1182)


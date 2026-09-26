## The exponential family

- Exponential families
- Hypothesis tests

## The exponential family of distributions

The exponential family of distributions contains the distributions whose probability functions attain the form

$$
p(w \mid \theta)=\xi(w) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) T_{s}(w)-A(\theta)\right)=\xi(w) \exp \left(\left(\begin{array}{c}
h_{1}(\theta) \\
h_{2}(\theta) \\
\vdots \\
h_{S}(\theta)
\end{array}\right) \cdot\left(\begin{array}{c}
T_{1}(w) \\
T_{2}(w) \\
\vdots \\
T_{S}(w)
\end{array}\right)-A(\theta)\right)
$$

Here, $\xi(w)$ and $T_{1: S}(w)$ are distribution-specific functions of the variable; while, $h_{1: S}(\theta)$ and $A(\theta)$ are distribution-specific functions of the parameters, and $S$ is the dimension of the parameter

Example: The Poisson distribution

$$
w \sim \text { Poisson }(\mu), \quad p(w \mid \mu)=\frac{\mu^{w}}{w!} e^{-\mu}=\frac{1}{w!} \exp (w \log \mu-\mu)
$$

belongs to the exponential family with

$$
S=1, \quad h(\mu)=\log \mu, \quad T(w)=w, \quad A(\mu)=\mu
$$

## The exponential family of Bayesian models

The exponential family of Bayesian models contains all models whose priors and likelihoods attain the form

$$
\begin{aligned}
p(\theta) & =\zeta\left(\nu, \chi_{1: S}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}-\nu A(\theta)\right) \\
p\left(w_{n} \mid \theta\right) & =\xi\left(w_{n}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) T_{s}\left(w_{n}\right)-A(\theta)\right),
\end{aligned}
$$

Here, $\xi\left(w_{n}\right)$ and $T_{1: S}\left(w_{n}\right)$ are model-specific functions of the measurements; while, $h_{1: S}(\theta)$ and $A(\theta)$ are model-specific functions of the parameters, $S$ is the dimension of the parameter, $\chi_{1: S}, \nu$ are the hyper-parameters, and $\zeta\left(\chi_{1: S}, \nu\right)$ is a model-specific function of the hyper-parameters

## The exponential family of Bayesian models

The exponential family of Bayesian models contains all models whose priors and likelihoods attain the form

$$
\begin{aligned}
p(\theta) & =\zeta\left(\nu, \chi_{1: S}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}-\nu A(\theta)\right) \\
p\left(w_{n} \mid \theta\right) & =\xi\left(w_{n}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) T_{s}\left(w_{n}\right)-A(\theta)\right),
\end{aligned}
$$

Example: The Gamma-Poisson model

$$
\begin{aligned}
\mu & \sim \operatorname{Gamma}(\phi, \psi), & p(\mu) & =\frac{\mu^{\phi-1} e^{-\mu / \psi}}{\Gamma(\phi) \psi^{\phi}}=\frac{1}{\Gamma(\phi) \psi^{\phi}} \exp \left((\phi-1) \log \mu-\frac{\mu}{\psi}\right) \\
w \mid \mu & \sim \operatorname{Poisson}(\mu), & p(w \mid \mu) & =\frac{\mu^{w}}{w!} e^{-\mu}=\frac{1}{w!} \exp (w \log \mu-\mu)
\end{aligned}
$$

belongs to the exponential family with

$$
S=1, \quad h(\mu)=\log \mu, \quad T(w)=w, \quad A(\mu)=\mu, \quad \chi=\phi-1, \quad \nu=1 / \psi
$$

## Bayesian updates within the exponential family

We consider a Bayesian model in the exponential family

$$
\begin{aligned}
p(\theta) & =\zeta\left(\nu, \chi_{1: S}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}-\nu A(\theta)\right) \\
p\left(w_{n} \mid \theta\right) & =\xi\left(w_{n}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) T_{s}\left(w_{n}\right)-A(\theta)\right),
\end{aligned}
$$

Our posterior is given by

$$
\begin{aligned}
p\left(\theta \mid w_{1: N}\right) & \propto p\left(w_{1: N} \mid \theta\right) p(\theta) \\
& =\left[\prod_{n=1}^{N} p\left(w_{n} \mid \theta\right)\right] p(\theta) \\
& =\left[\prod_{n=1}^{N} \xi\left(w_{n}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) T_{s}\left(w_{n}\right)-A(\theta)\right)\right] \zeta\left(\nu, \chi_{1: S}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}-\nu A(\theta)\right) \\
& \propto\left[\prod_{n=1}^{N} \exp \left(\sum_{s=1}^{S} h_{s}(\theta) T_{s}\left(w_{n}\right)-A(\theta)\right)\right] \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}-\nu A(\theta)\right)
\end{aligned}
$$

## Bayesian updates within the exponential family

We consider a Bayesian model in the exponential family

$$
\begin{aligned}
p(\theta) & =\zeta\left(\nu, \chi_{1: S}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}-\nu A(\theta)\right) \\
p\left(w_{n} \mid \theta\right) & =\xi\left(w_{n}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) T_{s}\left(w_{n}\right)-A(\theta)\right),
\end{aligned}
$$

Our posterior is given by

$$
\begin{aligned}
p\left(\theta \mid w_{1: N}\right) & \propto\left[\prod_{n=1}^{N} \exp \left(\sum_{s=1}^{S} h_{s}(\theta) T_{s}\left(w_{n}\right)-A(\theta)\right)\right] \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}-\nu A(\theta)\right) \\
& =\exp \left(\sum_{n=1}^{N}\left[\sum_{s=1}^{S} h_{s}(\theta) T_{s}\left(w_{n}\right)-A(\theta)\right]+\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}-\nu A(\theta)\right) \\
& =\exp \left(\sum_{s=1}^{S} h_{s}(\theta)\left(\chi_{s}+\sum_{n=1}^{N} T_{s}\left(w_{n}\right)\right)-(\nu+N) A(\theta)\right) \\
& =\exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}^{\prime}-\nu^{\prime} A(\theta)\right)
\end{aligned}
$$

## Bayesian updates within the exponential family

We consider a Bayesian model in the exponential family

$$
\begin{aligned}
p(\theta) & =\zeta\left(\nu, \chi_{1: S}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}-\nu A(\theta)\right) \\
p\left(w_{n} \mid \theta\right) & =\xi\left(w_{n}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) T_{s}\left(w_{n}\right)-A(\theta)\right),
\end{aligned}
$$

Our posterior is given by

$$
\begin{aligned}
p\left(\theta \mid w_{1: N}\right) & \propto \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}^{\prime}-\nu^{\prime} A(\theta)\right) \\
& =\frac{\zeta\left(\nu^{\prime}, \chi_{1: S}^{\prime}\right)}{\zeta\left(\nu^{\prime}, \chi_{1: S}^{\prime}\right)} \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}^{\prime}-\nu^{\prime} A(\theta)\right) \\
& \propto \zeta\left(\nu^{\prime}, \chi_{1: S}^{\prime}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}^{\prime}-\nu^{\prime} A(\theta)\right)
\end{aligned}
$$

## Bayesian updates within the exponential family

We consider a Bayesian model in the exponential family

$$
\begin{aligned}
p(\theta) & =\zeta\left(\nu, \chi_{1: S}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}-\nu A(\theta)\right) \\
p\left(w_{n} \mid \theta\right) & =\xi\left(w_{n}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) T_{s}\left(w_{n}\right)-A(\theta)\right),
\end{aligned}
$$

Our posterior is given by

$$
p\left(\theta \mid w_{1: N}\right)=\zeta\left(\nu^{\prime}, \chi_{1: S}^{\prime}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}^{\prime}-\nu^{\prime} A(\theta)\right)
$$

Our model is conjugate and the posterior hyper-parameters are

$$
\chi_{s}^{\prime}=\chi_{s}+\sum_{n=1}^{N} T_{s}\left(w_{n}\right) \quad \nu^{\prime}=\nu+N
$$

This means that our prior is equivalent to a pseudo-dataset with $\nu$ pseudo-measurements

## Hypothesis tests with uncertain parameters

We consider a hypothesis testing problem with uncertain parameters

$$
\begin{aligned}
\theta_{H_{1}} & \sim P_{H_{1}} \\
\theta_{H_{2}} & \sim P_{H_{2}} \\
\vdots & \\
\theta_{H_{M}} & \sim P_{H_{M}} \\
\eta & \sim \mathrm{Cat}_{H_{1}, H_{2}, \ldots, H_{M}}\left(\pi_{H_{1}}, \pi_{H_{2}}, \ldots, \pi_{H_{M}}\right) \\
w \mid \eta, \theta_{H_{1}}, \theta_{H_{2}}, \ldots, \theta_{H_{M}} & \sim L_{\eta}^{\theta_{h}}
\end{aligned}
$$

and seek a decision based on the marginal posterior

$$
\eta_{*}=\operatorname{argmax}_{\eta} p(\eta \mid w)
$$

In turn, this requires evaluation of the marginal likelihoods

$$
\ell_{\eta}=\int d \theta_{\eta} L_{\eta}^{\theta_{\eta}}(w) P_{\eta}\left(\theta_{\eta}\right)
$$

## Hypothesis tests within the exponential family

For each hypothesis, we consider prior/likelihood pairs within the exponential family

$$
P(\theta)=\zeta\left(\nu, \chi_{1: S}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}-\nu A(\theta)\right) \quad L^{\theta}(w)=\xi(w) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) T_{s}(w)-A(\theta)\right)
$$

Our marginal likelihood integrals are

$$
\begin{aligned}
\ell & =\int d \theta L^{\theta}(w) P(\theta) \\
& =\int d \theta \xi(w) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) T_{s}(w)-A(\theta)\right) \zeta\left(\nu, \chi_{1: S}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}-\nu A(\theta)\right) \\
& =\xi(w) \zeta\left(\nu, \chi_{1: S}\right) \int d \theta \exp \left(\sum_{s=1}^{S} h_{s}(\theta)\left(\chi_{s}+T_{s}(w)\right)-(\nu+1) A(\theta)\right) \\
& =\xi(w) \zeta\left(\nu, \chi_{1: S}\right) \int d \theta \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}^{\prime}-\nu^{\prime} A(\theta)\right)
\end{aligned}
$$

## Hypothesis tests within the exponential family

For each hypothesis, we consider prior/likelihood pairs within the exponential family

$$
P(\theta)=\zeta\left(\nu, \chi_{1: S}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}-\nu A(\theta)\right) \quad L^{\theta}(w)=\xi(w) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) T_{s}(w)-A(\theta)\right)
$$

Our marginal likelihood integrals are

$$
\begin{aligned}
\ell & =\xi(w) \zeta\left(\nu, \chi_{1: S}\right) \int d \theta \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}^{\prime}-\nu^{\prime} A(\theta)\right) \\
& =\xi(w) \zeta\left(\nu, \chi_{1: S}\right) \int d \theta \frac{\zeta\left(\nu^{\prime}, \chi_{1: S}^{\prime}\right)}{\zeta\left(\nu^{\prime}, \chi_{1: S}^{\prime}\right)} \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}^{\prime}-\nu^{\prime} A(\theta)\right) \\
& =\xi(w) \frac{\zeta\left(\nu, \chi_{1: S}\right)}{\zeta\left(\nu^{\prime}, \chi_{1: S}^{\prime}\right)} \int d \theta \zeta\left(\nu^{\prime}, \chi_{1: S}^{\prime}\right) \exp \left(\sum_{s=1}^{S} h_{s}(\theta) \chi_{s}^{\prime}-\nu^{\prime} A(\theta)\right) \\
& =\xi(w) \frac{\zeta\left(\nu, \chi_{1: S}\right)}{\zeta\left(\nu^{\prime}, \chi_{1: S}^{\prime}\right)}
\end{aligned}
$$

## Signal detection

We consider the detection of a signal with certain intensity levels $\mu_{1: M}$ transmitted over a noisy channel with uncertain intensity-dependent noise

Signal detection becomes a hypothesis testing problem

$$
\begin{aligned}
\eta & \sim \operatorname{Cat}_{1: M}\left(\frac{1}{M}, \frac{1}{M}, \ldots, \frac{1}{M}\right) & & \\
\tau_{m} & \sim \operatorname{Gamma}(\phi, \psi), & m & =1, \ldots, M \\
w_{n} \mid \eta, \tau_{1: M} & \sim \operatorname{Normal}\left(\mu_{\eta}, \frac{1}{\tau_{\eta}}\right), & & n=1, \ldots, N
\end{aligned}
$$

Our marginal posterior is given by

$$
\begin{aligned}
p\left(\eta \mid w_{1: N}\right) & =\int_{0}^{\infty} d \tau_{1} \int_{0}^{\infty} d \tau_{2} \cdots \int_{0}^{\infty} d \tau_{M} p\left(\eta, \tau_{1: M} \mid w_{1: N}\right) \\
& \propto \int_{0}^{\infty} d \tau_{1} \int_{0}^{\infty} d \tau_{2} \cdots \int_{0}^{\infty} d \tau_{M} p\left(w_{1: N} \mid \eta, \tau_{1: M}\right) p\left(\eta, \tau_{1: M}\right) \\
& =\int_{0}^{\infty} d \tau_{1} \int_{0}^{\infty} d \tau_{2} \cdots \int_{0}^{\infty} d \tau_{M}\left[\prod_{n=1}^{N} p\left(w_{n} \mid \eta, \tau_{1: M}\right)\right] p(\eta)\left[\prod_{m=1}^{M} p\left(\tau_{m}\right)\right]
\end{aligned}
$$

## Signal detection

Our marginal posterior is given by

$$
\begin{aligned}
p\left(\eta \mid w_{1: N}\right) & \propto \int_{0}^{\infty} d \tau_{1} \int_{0}^{\infty} d \tau_{2} \ldots \int_{0}^{\infty} d \tau_{M}\left[\prod_{n=1}^{N} p\left(w_{n} \mid \eta, \tau_{1: M}\right)\right] p(\eta)\left[\prod_{m=1}^{M} p\left(\tau_{m}\right)\right] \\
& =\int_{0}^{\infty} d \tau_{1} \int_{0}^{\infty} d \tau_{2} \ldots \int_{0}^{\infty} d \tau_{M}\left[\prod_{n=1}^{N} p\left(w_{n} \mid \eta, \tau_{\eta}\right)\right] p(\eta)\left[\prod_{m=1}^{M} p\left(\tau_{m}\right)\right] \\
& =p(\eta)\left(\int_{0}^{\infty} d \tau_{\eta}\left[\prod_{n=1}^{N} p\left(w_{n} \mid \eta, \tau_{\eta}\right)\right] p\left(\tau_{\eta}\right)\right) \underbrace{\int_{0}^{\infty} d \tau_{1} \int_{0}^{\infty} d \tau_{2} \cdots \int_{0}^{\infty} d \tau_{M}}_{m \neq \eta} \prod_{m \neq \eta} p\left(\tau_{m}\right) \\
& =p(\eta) \int_{0}^{\infty} d \tau_{\eta}\left[\prod_{n=1}^{N} p\left(w_{n} \mid \eta, \tau_{\eta}\right)\right] p\left(\tau_{\eta}\right) \\
& =p(\eta) \int_{0}^{\infty} d \tau_{\eta}\left[\prod_{n=1}^{N} \operatorname{Normal}\left(w_{n} ; \mu_{\eta}, \frac{1}{\tau_{\eta}}\right)\right] \operatorname{Gamma}\left(\tau_{\eta} ; \phi, \psi\right)
\end{aligned}
$$

## Signal detection

Our marginal posterior is given by

$$
\begin{aligned}
p\left(\eta \mid w_{1: N}\right) & \propto p(\eta) \int_{0}^{\infty} d \tau_{\eta}\left[\prod_{n=1}^{N} \text { Normal }\left(w_{n} ; \mu_{\eta}, \frac{1}{\tau_{\eta}}\right)\right] \text { Gamma }\left(\tau_{\eta} ; \phi, \psi\right) \\
& =p(\eta) \int_{0}^{\infty} d \tau_{\eta}\left[\prod_{n=1}^{N} \sqrt{\frac{\tau_{\eta}}{2 \pi}} e^{-\tau_{\eta} \frac{\left(w_{n}-\mu_{\eta}\right)^{2}}{2}}\right] \frac{1}{\Gamma(\phi) \psi^{\phi}} \tau_{\eta}^{\phi-1} e^{-\tau_{\eta} / \psi} \\
& =p(\eta) \int_{0}^{\infty} d \tau_{\eta}\left(\frac{\tau_{\eta}}{2 \pi}\right)^{N / 2} e^{-\tau_{\eta} \frac{\sum_{n=1}^{N}\left(w_{n}-\mu_{\eta}\right)^{2}}{2}} \frac{1}{\Gamma(\phi) \psi^{\phi}} \tau_{\eta}^{\phi-1} e^{-\tau_{\eta} / \psi} \\
& =\frac{p(\eta)}{(2 \pi)^{N / 2} \Gamma(\phi) \psi^{\phi}} \int_{0}^{\infty} d \tau_{\eta} \tau_{\eta}^{\phi+\frac{N}{2}-1} e^{-\tau_{\eta}\left(\frac{1}{\psi}+\frac{\sum_{n=1}^{N}\left(w_{n}-\mu_{\eta}\right)^{2}}{2}\right)} \\
& =\frac{p(\eta)}{(2 \pi)^{N / 2} \Gamma(\phi) \psi^{\phi}} \int_{0}^{\infty} d \tau_{\eta} \tau_{\eta}^{\phi^{\prime}-1} e^{-\frac{\tau_{\eta}}{\psi_{\eta}^{\prime}}} \\
& =\frac{p(\eta)}{(2 \pi)^{N / 2} \Gamma(\phi) \psi^{\phi}} \int_{0}^{\infty} d \tau_{\eta} \frac{\Gamma\left(\phi^{\prime}\right)\left(\psi^{\prime}\right)^{\phi^{\prime}}}{\Gamma\left(\phi^{\prime}\right)\left(\psi_{\eta}^{\prime}\right)^{\phi^{\prime}}} \tau_{\eta}^{\phi^{\prime}-1} e^{-\frac{\tau_{\eta}}{\psi_{\eta}^{\prime}}} \\
& =\frac{p(\eta)}{(2 \pi)^{N / 2}} \frac{\Gamma\left(\phi^{\prime}\right)\left(\psi_{\eta}^{\prime}\right)^{\phi^{\prime}}}{\Gamma(\phi) \psi^{\phi}}
\end{aligned}
$$

## Signal detection

Our marginal posterior is given by

$$
\begin{aligned}
p\left(\eta \mid w_{1: N}\right) & \propto \frac{p(\eta)}{(2 \pi)^{N / 2}} \frac{\Gamma\left(\phi^{\prime}\right)\left(\psi_{\eta}^{\prime}\right)^{\phi^{\prime}}}{\Gamma(\phi) \psi^{\phi}} \\
& =\frac{1 / M}{(2 \pi)^{N / 2}} \frac{\Gamma\left(\phi^{\prime}\right)\left(\psi_{\eta}^{\prime}\right)^{\phi^{\prime}}}{\Gamma(\phi) \psi^{\phi}} \\
& \propto\left(\psi_{\eta}^{\prime}\right)^{\phi^{\prime}} \\
& =\left(\frac{1}{\psi}+\frac{\sum_{n=1}^{N}\left(w_{n}-\mu_{\eta}\right)^{2}}{2}\right)^{-\phi-N / 2}
\end{aligned}
$$

Detection is determined by

$$
\begin{aligned}
\eta_{*} & =\operatorname{argmax}_{\eta} p\left(\eta \mid w_{1: N}\right) \\
& =\operatorname{argmax}_{\eta}\left(\frac{1}{\psi}+\frac{\sum_{n=1}^{N}\left(w_{n}-\mu_{\eta}\right)^{2}}{2}\right)^{-\phi-N / 2}
\end{aligned}
$$


## Bayesian hypothesis tests

- Problem formalization
- Introduction to decision theory

## Categorical random variables

Provided classes $\Omega=\left\{\omega_{m}\right\}_{m=1}^{M}$, a shorthand like

$$
W \sim \text { Categorical }_{\omega_{1}, \omega_{2}, \ldots, \omega_{M}}\left(\pi_{\omega_{1}}, \pi_{\omega_{2}}, \ldots, \pi_{\omega_{M}}\right)
$$

stands for

- the values $w$ that $W$ may attain are $\omega_{1}, \omega_{2}, \ldots, \omega_{M}$
- the probability mass of $W$ has the form

$$
p(w)=\pi_{w}=\pi_{\omega_{1}}^{\mathbb{I}_{w=\omega_{1}}} \pi_{\omega_{2}}^{\mathbb{I}_{w=\omega_{2}}} \cdots \pi_{\omega_{M}}^{\mathbb{I}_{w=\omega_{M}}}=\prod_{\omega \in \Omega} \pi_{\omega}^{\mathbb{I}_{w=\omega}}=\left\{\begin{array}{ll}
\pi_{\omega_{1}}, & w=\omega_{1} \\
\pi_{\omega_{2}}, & w=\omega_{2} \\
\cdots & \\
\pi_{\omega_{M},} & w=\omega_{M}
\end{array} \quad \mathbb{I}_{w=\omega}= \begin{cases}1, & w=\omega \\
0, & w \neq \omega\end{cases}\right.
$$

- the probability mass of $W$ depends on parameters
$$
\left\{\pi_{\omega}\right\}_{\omega \in \Omega} \subset[0,1] \quad 1=\sum_{\omega \in \Omega} \pi_{\omega}
$$
Our classes are exchangeable
$$
\operatorname{Cat}_{\omega_{1}, \omega_{2}, \omega_{3}}\left(\pi_{\omega_{1}}, \pi_{\omega_{2}}, \pi_{\omega_{3}}\right)=\operatorname{Cat}_{\omega_{3}, \omega_{2}, \omega_{1}}\left(\pi_{\omega_{3}}, \pi_{\omega_{2}}, \pi_{\omega_{1}}\right)
$$

## Spam detection

In the spam detection problem, we seek to determine if an incoming email is spam or ham (legitimate) For any incoming email, our task is to choose from two hypothesis:

- this email is ham
- this email is spam

To decide, we consider:

- Our baseline ...ie before reading the message To date, 20\% of our incoming mail had been ham and 80\% had been spam
- Our information …ie when reading the message To date, 1\% ham messages contained "urgent" and 99\% did not To date, 85\% spam messages contained "urgent" and 15\% did not and evaluate the odds-statistic ...ie after reading the message
$$
\gamma= \begin{cases}\frac{80 \%}{20 \%} \frac{85 \%}{1 \%}, & \text { message contains "urgent" } \\ \frac{80 \%}{20 \%} \frac{15 \%}{99 \%}, & \text { message does not contain "urgent" }\end{cases}
$$

Our message is classified as spam when $\gamma>\gamma_{*}$ and ham when $\gamma \leq \gamma_{*}$
...choices $\gamma_{*}=1,10,1000$ designate balanced, safe, and ultra safe settings

## Binary hypothesis tests

In a simple hypothesis testing problem, we have two completing hypothesis

- $H_{0}$ : null hypothesis
- $H_{A}$ : alternate hypothesis

and a model of the form

$$
\begin{aligned}
\eta & \sim \operatorname{Cat}_{H_{0}, H_{A}}\left(\pi_{H_{0}}, \pi_{H_{A}}\right) \\
w \mid \eta & \sim \begin{cases}\operatorname{Cat}_{\omega_{1}, \omega_{2}}\left(\rho_{H_{0} \rightarrow \omega_{1}}, \rho_{H_{0} \rightarrow \omega_{2}}\right), & \eta=H_{0} \\
\operatorname{Cat}_{\omega_{1}, \omega_{2}}\left(\rho_{H_{A} \rightarrow \omega_{1}}, \rho_{H_{A} \rightarrow \omega_{2}}\right), & \eta=H_{A}\end{cases}
\end{aligned}
$$

This is a Bayesian model and the posterior is

$$
p(\eta \mid w) \propto p(w \mid \eta) p(\eta)=\rho_{\eta \rightarrow w} \pi_{\eta}= \begin{cases}\rho_{H_{0} \rightarrow \omega_{1}} \pi_{H_{0}}, & \eta=H_{0} \& w=\omega_{1} \\ \rho_{H_{0} \rightarrow \omega_{2}} \pi_{H_{0}}, & \eta=H_{0} \& w=\omega_{2} \\ \rho_{H_{A} \rightarrow \omega_{1}} \pi_{H_{A}}, & \eta=H_{A} \& w=\omega_{1} \\ \rho_{H_{A} \rightarrow \omega_{2}} \pi_{H_{A}}, & \eta=H_{A} \& w=\omega_{2}\end{cases}
$$

## Binary hypothesis tests

In a simple hypothesis testing problem, we have two completing hypothesis

- $H_{0}$ : null hypothesis
- $H_{A}$ : alternate hypothesis

and a model of the form

$$
\begin{aligned}
\eta & \sim \operatorname{Cat}_{H_{0}, H_{A}}\left(\pi_{H_{0}}, \pi_{H_{A}}\right) \\
w \mid \eta & \sim \begin{cases}\operatorname{Cat}_{\omega_{1}, \omega_{2}}\left(\rho_{H_{0} \rightarrow \omega_{1}}, \rho_{H_{0} \rightarrow \omega_{2}}\right), & \eta=H_{0} \\
\operatorname{Cat}_{\omega_{1}, \omega_{2}}\left(\rho_{H_{A} \rightarrow \omega_{1}}, \rho_{H_{A} \rightarrow \omega_{2}}\right), & \eta=H_{A}\end{cases}
\end{aligned}
$$

Our odds-statistic is given by the ratio of the posteriors

$$
\gamma(w)=\frac{p\left(\eta=H_{A} \mid w\right)}{p\left(\eta=H_{0} \mid w\right)}=\underbrace{\frac{p\left(w \mid \eta=H_{A}\right)}{p\left(w \mid \eta=H_{0}\right)}}_{\text {Bayes factor }} \underbrace{\frac{p\left(\eta=H_{A}\right)}{p\left(\eta=H_{0}\right)}}_{\text {prior odds }}=\frac{\rho_{H_{A} \rightarrow w}}{\rho_{H_{0} \rightarrow w}} \frac{\pi_{H_{A}}}{\pi_{H_{0}}}= \begin{cases}\frac{\rho_{H_{A} \rightarrow \omega_{1}}}{\rho_{H_{0} \rightarrow \omega_{1}}} \frac{\pi_{H_{A}}}{\pi_{H_{0}}}, & w=\omega_{1} \\ \frac{\rho_{H_{A} \rightarrow \omega_{2}}}{\rho_{H_{0} \rightarrow \omega_{2}}} \frac{\pi_{H_{A}}}{\pi_{H_{0}}}, & w=\omega_{2}\end{cases}
$$

## Binary hypothesis tests

In a simple hypothesis testing problem, we have two completing hypothesis

- $H_{0}$ : null hypothesis
- $H_{A}$ : alternate hypothesis

and a model of the form

$$
\begin{aligned}
\eta & \sim \operatorname{Cat}_{H_{0}, H_{A}}\left(\pi_{H_{0}}, \pi_{H_{A}}\right) \\
w \mid \eta & \sim \begin{cases}\operatorname{Cat}_{\omega_{1}, \omega_{2}}\left(\rho_{H_{0} \rightarrow \omega_{1}}, \rho_{H_{0} \rightarrow \omega_{2}}\right), & \eta=H_{0} \\
\operatorname{Cat}_{\omega_{1}, \omega_{2}}\left(\rho_{H_{A} \rightarrow \omega_{1}}, \rho_{H_{A} \rightarrow \omega_{2}}\right), & \eta=H_{A}\end{cases}
\end{aligned}
$$

Our decision is based on the posterior odds

- We choose $H_{A}$, when
$$
\gamma(w)>\gamma_{*} \Longleftrightarrow p\left(\eta=H_{A} \mid w\right)>p\left(\eta=H_{0} \mid w\right) \gamma_{*}
$$
- We choose $H_{0}$, when
$$
\gamma(w) \leq \gamma_{*} \Longleftrightarrow p\left(\eta=H_{A} \mid w\right) \leq p\left(\eta=H_{0} \mid w\right) \gamma_{*}
$$

The MAP criterion chooses the hypothesis that has the highest posterior

$$
\gamma_{*}=1
$$

The ML criterion chooses the hypothesis that has the highest likelihood

$$
\gamma_{*}=p\left(\eta=H_{0}\right) / p\left(\eta=H_{A}\right)
$$

## General hypothesis tests

In a general hypothesis testing problem, we have multiple hypothesis $H_{1}, H_{2}, \ldots, H_{M}$ and a model of the form

$$
\begin{aligned}
\eta & \sim \operatorname{Cat}_{H_{1}, H_{2}, \ldots, H_{M}}\left(\pi_{H_{1}}, \pi_{H_{2}}, \ldots, \pi_{H_{M}}\right) \\
w \mid \eta & \sim L_{\eta}
\end{aligned}
$$

Our decision is still based on the posterior
The MAP criterion chooses the hypothesis that has the highest posterior

$$
\begin{aligned}
\eta_{*} & =\operatorname{argmax}_{\eta} p(\eta \mid w) \\
& \propto \operatorname{argmax}_{\eta} p(w \mid \eta) p(\eta) \\
& =\operatorname{argmax}_{\eta} L_{\eta}(w) \pi_{\eta}
\end{aligned}
$$

## Hypothesis tests with uncertain parameters

A hypothesis testing problem may depend on uncertain parameters

$$
\begin{aligned}
\theta_{H_{1}} & \sim P_{H_{1}} \\
\theta_{H_{2}} & \sim P_{H_{2}} \\
\vdots & \\
\theta_{H_{M}} & \sim P_{H_{M}} \\
\eta & \sim \mathrm{Cat}_{H_{1}, H_{2}, \ldots, H_{M}}\left(\pi_{H_{1}}, \pi_{H_{2}}, \ldots, \pi_{H_{M}}\right) \\
w \mid \eta, \theta_{H_{1}}, \theta_{H_{2}}, \ldots, \theta_{H_{M}} & \sim L_{\eta}^{\theta_{\eta}}
\end{aligned}
$$

Our decision is based on the marginal posterior

$$
\begin{aligned}
p(\eta \mid w) & =\int d \theta_{H_{1}} \int d \theta_{H_{2}} \cdots \int d \theta_{H_{M}} p\left(\eta, \theta_{H_{1}}, \theta_{H_{2}}, \ldots, \theta_{H_{M}} \mid w\right) \\
& \propto \int d \theta_{H_{1}} \int d \theta_{H_{2}} \cdots \int d \theta_{H_{M}} p\left(w \mid \eta, \theta_{H_{1}}, \theta_{H_{2}}, \ldots, \theta_{H_{M}}\right) p\left(\eta, \theta_{H_{1}}, \theta_{H_{2}}, \ldots, \theta_{H_{M}}\right) \\
& =\int d \theta_{H_{1}} \int d \theta_{H_{2}} \cdots \int d \theta_{H_{M}} p\left(w \mid \eta, \theta_{H_{1}}, \theta_{H_{2}}, \ldots, \theta_{H_{M}}\right) p(\eta) p\left(\theta_{H_{1}}\right) p\left(\theta_{H_{2}}\right) \ldots p\left(\theta_{H_{M}}\right)
\end{aligned}
$$

## Hypothesis tests with uncertain parameters

A hypothesis testing problem may depend on uncertain parameters

$$
\begin{aligned}
\theta_{H_{1}} & \sim P_{H_{1}} \\
\theta_{H_{2}} & \sim P_{H_{2}} \\
\vdots & \\
\theta_{H_{M}} & \sim P_{H_{M}} \\
\eta & \sim \mathrm{Cat}_{H_{1}, H_{2}, \ldots, H_{M}}\left(\pi_{H_{1}}, \pi_{H_{2}}, \ldots, \pi_{H_{M}}\right) \\
w \mid \eta, \theta_{H_{1}}, \theta_{H_{2}}, \ldots, \theta_{H_{M}} & \sim L_{\eta}^{\theta_{\eta}}
\end{aligned}
$$

Our decision is based on the marginal posterior

$$
\begin{aligned}
p(\eta \mid w) & \propto \int d \theta_{H_{1}} \int d \theta_{H_{2}} \cdots \int d \theta_{H_{M}} p\left(w \mid \eta, \theta_{H_{1}}, \theta_{H_{2}}, \ldots, \theta_{H_{M}}\right) p(\eta) p\left(\theta_{H_{1}}\right) p\left(\theta_{H_{2}}\right) \ldots p\left(\theta_{H_{M}}\right) \\
& =p(\eta) \int d \theta_{H_{1}} \int d \theta_{H_{2}} \cdots \int d \theta_{H_{M}} p\left(w \mid \eta, \theta_{\eta}\right) p\left(\theta_{H_{1}}\right) p\left(\theta_{H_{2}}\right) \ldots p\left(\theta_{H_{M}}\right) \\
& =p(\eta) \int d \theta_{\eta} p\left(w \mid \eta, \theta_{\eta}\right) p\left(\theta_{\eta}\right)
\end{aligned}
$$

## Hypothesis tests with uncertain parameters

A hypothesis testing problem may depend on uncertain parameters

$$
\begin{aligned}
\theta_{H_{1}} & \sim P_{H_{1}} \\
\theta_{H_{2}} & \sim P_{H_{2}} \\
\vdots & \\
\theta_{H_{M}} & \sim P_{H_{M}} \\
\eta & \sim \mathrm{Cat}_{H_{1}, H_{2}, \ldots, H_{M}}\left(\pi_{H_{1}}, \pi_{H_{2}}, \ldots, \pi_{H_{M}}\right) \\
w \mid \eta, \theta_{H_{1}}, \theta_{H_{2}}, \ldots, \theta_{H_{M}} & \sim L_{\eta}^{\theta_{\eta}}
\end{aligned}
$$

Our decision is based on the marginal posterior

$$
p(\eta \mid w) \propto p(\eta) \int d \theta_{\eta} p\left(w \mid \eta, \theta_{\eta}\right) p\left(\theta_{\eta}\right)=\pi_{\eta} \int d \theta_{\eta} L_{\eta}^{\theta_{\eta}}(w) P_{\eta}\left(\theta_{\eta}\right)
$$

## Hypothesis tests with uncertain parameters

A hypothesis testing problem may depend on uncertain parameters

$$
\begin{aligned}
\theta_{H_{1}} & \sim P_{H_{1}} \\
\theta_{H_{2}} & \sim P_{H_{2}} \\
\vdots & \\
\theta_{H_{M}} & \sim P_{H_{M}} \\
\eta & \sim \mathrm{Cat}_{H_{1}, H_{2}, \ldots, H_{M}}\left(\pi_{H_{1}}, \pi_{H_{2}}, \ldots, \pi_{H_{M}}\right) \\
w \mid \eta, \theta_{H_{1}}, \theta_{H_{2}}, \ldots, \theta_{H_{M}} & \sim L_{\eta}^{\theta_{\eta}}
\end{aligned}
$$

Our decision is based on the marginal posterior, which requires evaluation of the marginal likelihood integrals

$$
\begin{aligned}
\ell_{H_{1}} & =\int d \theta_{H_{1}} L_{H_{1}}^{\theta_{H_{1}}}(w) P_{H_{1}}\left(\theta_{H_{1}}\right) \\
\ell_{H_{2}} & =\int d \theta_{H_{2}} L_{H_{2}}^{\theta_{H_{2}}}(w) P_{H_{2}}\left(\theta_{H_{2}}\right) \\
& \ldots
\end{aligned}
$$


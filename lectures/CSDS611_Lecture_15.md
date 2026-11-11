## Predictions

- Problem setup
- Linear regression

## Prediction problems

We have input/output data

$$
\mathcal{D}=\left\{\left(x_{n}, y_{n}\right)\right\}_{n=1}^{N} \subset \mathbb{R}^{K} \times \mathbb{R}
$$

and seek a regression function $f: \mathbb{R}^{K} \mapsto \mathbb{R}$
In linear regression we apply a feature expansion

$$
\phi: \mathbb{R}^{K} \mapsto \mathbb{R}^{1 \times M}
$$

and seek only solutions of the form

$$
f_{c}(x)=\phi(x) c
$$

for appropriate coefficients $c \in \mathbb{R}^{M}$

- Our goal is to obtain predictions of the targets
$$
y^{*} \in \mathbb{R}
$$
at given queries $x^{*} \in \mathbb{R}^{K}$

![](https://cdn.mathpix.com/cropped/e5fcd5b6-a0cb-4831-8cb1-e948bd34f304-02.jpg?height=650&width=505&top_left_y=208&top_left_x=899)

## Bayesian prediction problems

We consider data $\left\{\left(x_{n}, y_{n}\right)\right\}_{n=1}^{N} \subset \mathbb{R}^{K} \times \mathbb{R}$, a function $\phi: \mathbb{R}^{K} \mapsto \mathbb{R}^{1 \times M}$, and seek solutions

$$
f_{c}(x)=\phi(x) c
$$

- Our basic Bayesian model consists of
$$
\begin{aligned}
& c \sim \operatorname{Normal}_{M}(\mu, C) \\
& y_{n} \mid c \sim \operatorname{Normal}\left(f_{c}\left(x_{n}\right), \eta\right), \\
& n=1, \ldots, N
\end{aligned}
$$
- To allow for predictions $y^{*}$ at a query $x^{*}$ we consider an extended model
$$
\begin{aligned}
c & \sim \operatorname{Normal}_{M}(\mu, C) \\
y_{n} \mid c & \sim \operatorname{Normal}\left(f_{c}\left(x_{n}\right), \eta\right), \\
y^{*} \mid c & \sim \operatorname{Normal}\left(f_{c}\left(x^{*}\right), \eta\right)
\end{aligned} \quad n=1, \ldots, N
$$

Our predictive distribution is

$$
p\left(y^{*} \mid y_{1: N}\right)=\int d c p\left(y^{*}, c \mid y_{1: N}\right)=\int d c p\left(y^{*} \mid c, y_{1: N}\right) p\left(c \mid y_{1: N}\right)=\int d c p\left(y^{*} \mid c\right) p\left(c \mid y_{1: N}\right)
$$

## Bayesian prediction problems

We consider data $\left\{\left(x_{n}, y_{n}\right)\right\}_{n=1}^{N} \subset \mathbb{R}^{K} \times \mathbb{R}$, a function $\phi: \mathbb{R}^{K} \mapsto \mathbb{R}^{1 \times M}$, and seek solutions

$$
f_{c}(x)=\phi(x) c
$$

- To allow for predictions $y_{\ell}^{*}$ at multiple queries $x_{\ell}^{*}$ we consider an extended model
$$
\begin{aligned}
c & \sim \operatorname{Normal}_{M}(\mu, C) & & \\
y_{n} \mid c & \sim \operatorname{Normal}\left(f_{c}\left(x_{n}\right), \eta\right), & n & =1, \ldots, N \\
y_{\ell}^{*} \mid c & \sim \operatorname{Normal}\left(f_{c}\left(x_{\ell}^{*}\right), \eta\right), & \ell & =1, \ldots, L
\end{aligned}
$$
Our predictive distribution is
$$
\begin{aligned}
p\left(y_{1: L}^{*} \mid y_{1: N}\right)=\int d c p\left(y_{1: L}^{*}, c \mid y_{1: N}\right) & =\int d c p\left(y_{1: L}^{*} \mid c, y_{1: N}\right) p\left(c \mid y_{1: N}\right) \\
& =\int d c p\left(y_{1: L}^{*} \mid c\right) p\left(c \mid y_{1: N}\right)
\end{aligned}
$$

## The predictive distribution

Our extended model consists of

$$
\begin{aligned}
c & \sim \operatorname{Normal}_{M}(\mu, C) & & \\
y_{n} \mid c & \sim \operatorname{Normal}\left(f_{c}\left(x_{n}\right), \eta\right), & n & =1, \ldots, N \\
y_{\ell}^{*} \mid c & \sim \operatorname{Normal}\left(f_{c}\left(x_{\ell}^{*}\right), \eta\right), & \ell & =1, \ldots, L
\end{aligned}
$$

This is equivalent to the model

$$
\begin{array}{cc}
c \sim \operatorname{Normal}_{M}(\mu, C) & c \sim \operatorname{Normal}_{M}(\mu, C) \\
\left(\begin{array}{c}
y_{1} \\
\vdots \\
y_{N}
\end{array}\right) \left\lvert\, c \sim \operatorname{Normal}_{N}\left(\left[\begin{array}{c}
\phi\left(x_{1}\right) \\
\vdots \\
\phi\left(x_{N}\right)
\end{array}\right] c, \eta\left[\begin{array}{ccc}
1 & \cdots & 0 \\
\vdots & \ddots & \vdots \\
0 & \cdots & 1
\end{array}\right]\right)\right. & Y \mid c \sim \operatorname{Normal}_{N}\left(\Phi c, \eta I_{N}\right) \\
\left(\begin{array}{c}
y_{1}^{*} \\
\vdots \\
y_{L}^{*}
\end{array}\right) \left\lvert\, c \sim \operatorname{Normal}_{L}\left(\left[\begin{array}{c}
\phi\left(x_{1}^{*}\right) \\
\vdots \\
\phi\left(x_{L}^{*}\right)
\end{array}\right] c, \eta\left[\begin{array}{ccc}
1 & \cdots & 0 \\
\vdots & \ddots & \vdots \\
0 & \cdots & 1
\end{array}\right]\right)\right. & Y^{*} \mid c \sim \operatorname{Normal}_{L}\left(\Phi^{*} c, \eta I_{L}\right)
\end{array}
$$

## The predictive distribution

Our extended model consists of

$$
\begin{aligned}
c & \sim \operatorname{Normal}_{M}(\mu, C) \\
Y \mid c & \sim \operatorname{Normal}_{N}\left(\Phi c, \eta I_{N}\right) \\
Y^{*} \mid c & \sim \operatorname{Normal}_{L}\left(\Phi^{*} c, \eta I_{L}\right)
\end{aligned}
$$

This model leads to

$$
\begin{aligned}
c \mid Y & \sim \operatorname{Normal}_{M}\left(\mu^{\prime}, C^{\prime}\right) \\
Y^{*} \mid c & \sim \operatorname{Normal}_{L}\left(\Phi^{*} c, \eta I_{L}\right)
\end{aligned} \quad \mu^{\prime}=C^{\prime}\left(C^{-1} \mu+\frac{1}{\eta} \Phi^{t} Y\right) \quad C^{\prime}=\left(C^{-1}+\frac{1}{\eta} \Phi^{t} \Phi\right)^{-1}
$$

Our predictive distribution is

$$
\begin{aligned}
p\left(Y^{*} \mid Y\right)=\int d c p\left(Y^{*}, c \mid Y\right) & =\int d c p\left(Y^{*} \mid c, Y\right) p(c \mid Y) \\
& =\int d c p\left(Y^{*} \mid c\right) p(c \mid Y) \\
& =\int d c \operatorname{NormaI}_{L}\left(Y^{*} ; \Phi^{*} c, \eta I_{L}\right) \operatorname{Normal}_{M}\left(c ; \mu^{\prime}, C^{\prime}\right)=\operatorname{Normal}_{L}\left(Y^{*} ; \mu^{\prime \prime}, C^{\prime \prime}\right)
\end{aligned}
$$

## The predictive distribution

Our extended model consists of

$$
\begin{aligned}
c & \sim \operatorname{Normal}_{M}(\mu, C) \\
Y \mid c & \sim \operatorname{Normal}_{N}\left(\Phi c, \eta I_{N}\right) \\
Y^{*} \mid c & \sim \operatorname{Normal}_{L}\left(\Phi^{*} c, \eta I_{L}\right)
\end{aligned}
$$

This model leads to

$$
\begin{array}{rlr}
c \mid Y & \sim \operatorname{Normal}_{M}\left(\mu^{\prime}, C^{\prime}\right) & \mu^{\prime}=C^{\prime}\left(C^{-1} \mu+\frac{1}{\eta} \Phi^{t} Y\right) \\
Y^{*} \mid c & \sim \operatorname{Normal}_{L}\left(\Phi^{*} c, \eta I_{L}\right)
\end{array}
$$

which, in turn, leads to

$$
Y^{*} \mid Y \sim \operatorname{Normal}_{L}\left(\mu^{\prime \prime}, C^{\prime \prime}\right) \quad \mu^{\prime \prime}=\Phi^{*} \mu^{\prime} \quad C^{\prime \prime}=\Phi^{*} C^{\prime}\left(\Phi^{*}\right)^{t}+\eta I_{L}
$$

## Example

![](https://cdn.mathpix.com/cropped/e5fcd5b6-a0cb-4831-8cb1-e948bd34f304-08.jpg?height=705&width=588&top_left_y=145&top_left_x=172)
![](https://cdn.mathpix.com/cropped/e5fcd5b6-a0cb-4831-8cb1-e948bd34f304-08.jpg?height=696&width=579&top_left_y=145&top_left_x=807)

## Bayesian prediction problems under model uncertainty

We have a pool with $K$ models, each characterized by potentially different sizes $M_{1: K}$, feature expansions $\phi_{1: K}(x)$, and coefficients $c_{1: K}$

Combining all models in the pool, we obtain a master model

$$
\begin{aligned}
\kappa & \sim \operatorname{Categorical}_{1: K}\left(\pi_{1}, \ldots, \pi_{K}\right) & & \\
c_{k} & \sim \operatorname{Normal}_{M_{k}}\left(\mu_{k}, C_{k}\right), & & k=1, \ldots, K \\
y_{n} \mid \kappa, c_{1: K} & \sim \operatorname{Normal}\left(\phi_{\kappa}\left(x_{n}\right) c_{\kappa}, \zeta\right), & n=1, \ldots, N &
\end{aligned}
$$

- To allow for predictions $y_{\ell}^{*}$ at queries $x_{\ell}^{*}$ we consider an extended master model
$$
\begin{aligned}
\kappa & \sim \text { Categorical }_{1: K}\left(\pi_{1}, \ldots, \pi_{K}\right) \\
c_{k} & \sim \operatorname{Normal}_{M_{k}}\left(\mu_{k}, C_{k}\right),
\end{aligned} \quad k=1, \ldots, K
$$
$$
\begin{array}{ll}
y_{n} \mid \kappa, c_{1: K} \sim \operatorname{Normal}\left(\phi_{\kappa}\left(x_{n}\right) c_{\kappa}, \zeta\right), & n=1, \ldots, N \\
y_{\ell}^{*} \mid \kappa, c_{1: K} \sim \operatorname{Normal}\left(\phi_{\kappa}\left(x_{\ell}^{*}\right) c_{\kappa}, \zeta\right), & \ell=1, \ldots, L
\end{array}
$$

## Bayesian prediction problems under model uncertainty

Our extended master model consists of

$$
\begin{aligned}
\kappa & \sim \operatorname{Categorical}_{1: K}\left(\pi_{1}, \ldots, \pi_{K}\right) & & \\
c_{k} & \sim \operatorname{Normal}_{M_{k}}\left(\mu_{k}, C_{k}\right), & & \\
y_{n} \mid \kappa, c_{1: K} & \sim \operatorname{Normal}\left(\phi_{\kappa}\left(x_{n}\right) c_{\kappa}, \zeta\right), & n=1, \ldots, N & \\
y_{\ell}^{*} \mid \kappa, c_{1: K} & \sim \operatorname{Normal}\left(\phi_{\kappa}\left(x_{\ell}^{*}\right) c_{\kappa}, \zeta\right), & & \ell=1, \ldots, L
\end{aligned}
$$

Our predictive distribution is

$$
\begin{aligned}
p\left(y_{1: L}^{*} \mid y_{1: N}\right) & =\sum_{\kappa=1}^{K} p\left(y_{1: L}^{*}, \kappa \mid y_{1: N}\right) \\
& =\underbrace{\sum_{\kappa=1}^{K} \underbrace{p\left(y_{1: L}^{*} \mid y_{1: N}, \kappa\right)}_{\substack{\kappa^{\text {th }} \text { model } \\
\text { predictions }}} \underbrace{p\left(\kappa \mid y_{1: N}\right)}_{\substack{\kappa^{\text {th }} \text { model } \\
\text { selection }}}}_{\text {model averaging }}
\end{aligned}
$$

This way, our predictions, are averaged over all models in the pool ...posterior mixture predictions


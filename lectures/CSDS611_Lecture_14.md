## Model selection

- Problem setup
- Linear regression

## Regression problems

We have input/output data

$$
\mathcal{D}=\left\{\left(x_{n}, y_{n}\right)\right\}_{n=1}^{N} \subset \mathbb{X} \times \mathbb{Y}
$$

and seek a regression function

$$
f: \mathbb{X} \mapsto \mathbb{Y}
$$

However, we are unsure about the basis

$$
\phi^{m}: \mathbb{X} \mapsto \mathbb{Y}, \quad m=1, \ldots, M
$$

that forms the feature expansion

$$
\phi(x)=\left[\phi^{1}(x), \cdots, \phi^{M}(x)\right]
$$

of our linear regression model

$$
f(x)=\phi(x) c=\sum_{m=1}^{M} c^{m} \phi^{m}(x)
$$

![](https://cdn.mathpix.com/cropped/a8da9f2a-cc38-48a1-9a4a-3490f9b5504b-02.jpg?height=650&width=505&top_left_y=208&top_left_x=899)

## Model selection problems

In general, we have a pool with $K$ different models
The $k^{\text {th }}$ model in the pool has size $M_{k} \ldots$ and its basis consists of

$$
\phi_{k}^{m}: \mathbb{X} \mapsto \mathbb{Y}, \quad m=1, \ldots, M_{k}
$$

...and its feature expansion is

$$
\phi_{k}(x)=\left[\phi_{k}^{1}(x), \cdots, \phi_{k}^{M_{k}}(x)\right]
$$

...and its linear regression model is

$$
f(x)=\phi_{k}(x) c_{k}=\sum_{m=1}^{M_{k}} c_{k}^{m} \phi_{k}^{m}(x)
$$

...and its unknown coefficients are

$$
c_{k}=\left(\begin{array}{c}
c_{k}^{1} \\
\vdots \\
c_{k}^{M_{k}}
\end{array}\right) \in \mathbb{R}^{M_{k}}
$$

The models in our pool

- may or may not be nested
- may or may not have same size
- may or may not share features

The only strict requirements is that all feature functions are compatible with our input and output data-spaces

$$
\begin{aligned}
\phi_{k}^{m}: \mathbb{X} & \mapsto \mathbb{Y} \\
m & =1, \ldots, M_{k} \\
k & =1, \ldots, K
\end{aligned}
$$

Model selection asks for choosing one of the models in the pool irrespective of their optimal coefficients

## Example

Our pool contains $K=3$ models

- model $k=1$ :
$$
\begin{array}{rlrl}
M_{1} & =2 & \phi_{1}(x) & =[1, x] \\
c_{1} & \in \mathbb{R}^{2} & f(x) & =\phi_{1}(x) c_{1}=c_{1}^{1}+c_{1}^{2} x
\end{array}
$$
- model $k=2$ :
$$
\begin{array}{rlrl}
M_{2} & =3 & \phi_{2}(x) & =\left[1, x, x^{2}\right] \\
c_{2} & \in \mathbb{R}^{3} & f(x) & =\phi_{2}(x) c_{2}=c_{2}^{1}+c_{2}^{2} x+c_{2}^{3} x^{2}
\end{array}
$$
- model $k=3$ :
$$
\begin{array}{rlrl}
M_{3} & =4 & \phi_{3}(x) & =\left[1, x, x^{2}, x^{3}\right] \\
c_{3} & \in \mathbb{R}^{4} & f(x) & =\phi_{3}(x) c_{3}=c_{3}^{1}+c_{3}^{2} x+c_{3}^{3} x^{2}+c_{3}^{4} x^{3}
\end{array}
$$

The models in our pool are nested
![](https://cdn.mathpix.com/cropped/a8da9f2a-cc38-48a1-9a4a-3490f9b5504b-04.jpg?height=650&width=504&top_left_y=208&top_left_x=934)

## Bayesian model selection

We have a pool with $K$ models, each characterized by potentially different sizes $M_{1: K}$, feature expansions $\phi_{1: K}(x)$, and coefficients $c_{1: K}$

Each model carries its own Bayesian formulation

$$
\begin{array}{rlrl}
c_{k} & \sim \operatorname{Normal}_{M_{k}}\left(\mu_{k}, C_{k}\right), & k & =1, \ldots, K \\
y_{n} \mid c_{k} & \left.\sim \operatorname{Normal}^{( } \phi_{k}\left(x_{n}\right) c_{k}, \zeta\right), & n=1, \ldots, N, & k \\
=1, \ldots, K
\end{array}
$$

with model-specific prior hyper-parameters $\mu_{k} \in \mathbb{R}^{M_{k}}$ and $C_{k} \in \mathbb{R}_{\text {sym },+}^{M_{k} \times M_{k}}$
Combining all models in the pool, we obtain a master Bayesian formulation

$$
\begin{aligned}
\kappa & \sim \operatorname{Categorical}_{1: K}\left(\pi_{1}, \ldots, \pi_{K}\right) & & \\
c_{k} & \sim \operatorname{Normal}_{M_{k}}\left(\mu_{k}, C_{k}\right), & & k=1, \ldots, K \\
y_{n} \mid \kappa, c_{1: K} & \sim \operatorname{Normal}\left(\phi_{\kappa}\left(x_{n}\right) c_{\kappa}, \zeta\right), & n=1, \ldots, N &
\end{aligned}
$$

This way model selection reduces to hypothesis testing ...with uncertain parameters

## Bayesian model selection

We have a pool with $K$ models, each characterized by potentially different sizes $M_{1: K}$, feature expansions $\phi_{1: K}(x)$, and coefficients $c_{1: K}$

Our master Bayesian formulation consists of

$$
\begin{aligned}
\kappa & \sim \operatorname{Categorical}_{1: K}\left(\pi_{1}, \ldots, \pi_{K}\right) \\
c_{k} & \sim \operatorname{Normal}_{M_{k}}\left(\mu_{k}, C_{k}\right), \\
y_{n} \mid \kappa, c_{1: K} & \sim \operatorname{Normal}\left(\phi_{\kappa}\left(x_{n}\right) c_{\kappa}, \zeta\right), \\
& \quad n=1, \ldots, N
\end{aligned}
$$

We select a model according to the MAP criterion

$$
\kappa_{*}=\operatorname{argmax}_{k=1, \ldots, K} p\left(\kappa \mid y_{1: N}\right)
$$

which is based on the marginal posterior

$$
p\left(\kappa \mid y_{1: N}\right)=\int d c_{1} \cdots \int d c_{K} p\left(\kappa, c_{1: K} \mid y_{1: N}\right)
$$

## Bayesian model selection

Our master Bayesian formulation consists of

$$
\begin{aligned}
\kappa & \sim \operatorname{Categorical}_{1: K}\left(\pi_{1}, \ldots, \pi_{K}\right) & & \\
c_{k} & \sim \operatorname{Normal}_{M_{k}}\left(\mu_{k}, C_{k}\right), & & k=1, \ldots, K \\
y_{n} \mid \kappa, c_{1: K} & \sim \operatorname{Normal}\left(\phi_{\kappa}\left(x_{n}\right) c_{\kappa}, \zeta\right), & n=1, \ldots, N &
\end{aligned}
$$

which is the same as

$$
\begin{array}{rlr}
\kappa & \sim \operatorname{Categorical}_{1: K}\left(\pi_{1}, \ldots, \pi_{K}\right) & \\
c_{k} & \sim \operatorname{Normal}_{M_{k}}\left(\mu_{k}, C_{k}\right), & k=1, \ldots, K \\
Y \mid \kappa, c_{1: K} & \sim \operatorname{Normal}_{N}\left(\Phi_{\kappa} c_{\kappa}, \zeta I\right)
\end{array}
$$

where, as usual, we gather data and features in

$$
Y=\left(\begin{array}{c}
y_{1}, \\
\vdots \\
y_{N}
\end{array}\right), \quad \Phi_{k}=\left[\begin{array}{c}
\phi_{k}\left(x_{1}\right) \\
\vdots \\
\phi_{k}\left(x_{N}\right)
\end{array}\right]=\left[\begin{array}{ccc}
\phi_{k}^{1}\left(x_{1}\right) & \cdots & \phi_{k}^{M_{k}}\left(x_{1}\right) \\
\vdots & \ddots & \vdots \\
\phi_{k}^{1}\left(x_{N}\right) & \cdots & \phi_{k}^{M_{k}}\left(x_{N}\right)
\end{array}\right], \quad k=1, \ldots, K
$$

## Bayesian model selection

Our master Bayesian formulation consists of

$$
\begin{aligned}
\kappa & \sim \text { Categorical }_{1: K}\left(\pi_{1}, \ldots, \pi_{K}\right) \\
c_{k} & \sim \operatorname{Normal}_{M_{k}}\left(\mu_{k}, C_{k}\right), \\
Y \mid \kappa, c_{1: K} & \sim \operatorname{Normal}_{N}\left(\Phi_{\kappa} c_{\kappa}, \zeta I\right)
\end{aligned} \quad k=1, \ldots, K
$$

Our marginal posterior is given by

$$
\begin{aligned}
p(\kappa \mid Y) & =\int d c_{1} \cdots \int d c_{K} p\left(\kappa, c_{1: K} \mid Y\right) \\
& \propto \int d c_{1} \cdots \int d c_{K} p\left(Y \mid \kappa, c_{1: K}\right) p\left(\kappa, c_{1: K}\right) \\
& =\int d c_{1} \cdots \int d c_{K} p\left(Y \mid \kappa, c_{1: K}\right) p(\kappa) p\left(c_{1: K}\right) \\
& =p(\kappa) \int d c_{1} \cdots \int d c_{K} p\left(Y \mid \kappa, c_{1: K}\right) \prod_{k=1}^{K} p\left(c_{k}\right) \\
& =p(\kappa) \int d c_{1} \cdots \int d c_{K} p\left(Y \mid c_{\kappa}\right) \prod_{k=1}^{K} p\left(c_{k}\right)=p(\kappa) \int d c_{\kappa} p\left(Y \mid c_{\kappa}\right) p\left(c_{\kappa}\right)
\end{aligned}
$$

## Bayesian model selection

Our master Bayesian formulation consists of

$$
\begin{aligned}
\kappa & \sim \text { Categorical }_{1: K}\left(\pi_{1}, \ldots, \pi_{K}\right) \\
c_{k} & \sim \operatorname{Normal}_{M_{k}}\left(\mu_{k}, C_{k}\right), \\
Y \mid \kappa, c_{1: K} & \sim \operatorname{Normal}_{N}\left(\Phi_{\kappa} c_{\kappa}, \zeta I\right)
\end{aligned} \quad k=1, \ldots, K
$$

Our marginal posterior is given by

$$
\begin{aligned}
p(\kappa \mid Y) & \propto p(\kappa) \int d c_{\kappa} p\left(Y \mid c_{\kappa}\right) p\left(c_{\kappa}\right) \\
& =\pi_{\kappa} \int d c_{\kappa} \operatorname{Normal}_{N}\left(Y ; \Phi_{\kappa} c_{\kappa}, \zeta I\right) \operatorname{Normal}_{M_{\kappa}}\left(c_{\kappa} ; \mu_{\kappa}, C_{\kappa}\right) \\
& =\pi_{\kappa} \operatorname{Normal}_{N}\left(Y ; \mu_{\kappa}^{\prime}, C_{\kappa}^{\prime}\right)
\end{aligned}
$$

where the updated hyper-parameters are given by

$$
\begin{aligned}
& \mu_{\kappa}^{\prime}=\Phi_{\kappa} \mu_{\kappa} \\
& C_{\kappa}^{\prime}=\Phi_{\kappa} C_{\kappa} \Phi_{\kappa}^{t}+\zeta l
\end{aligned}
$$

## Example

With a pool of $K=3$ models and sizes

$$
M_{1}=2, \quad M_{2}=3, \quad M_{3}=4
$$

Our master Bayesian formulation consists of priors

$$
\kappa \sim \text { Categorical }_{1: 3}\left(\frac{1}{3}, \frac{1}{3}, \frac{1}{3}\right)
$$

$$
c_{1} \sim \operatorname{Normal}_{2}\left(\binom{0}{0},\left[\begin{array}{l}
1,0 \\
0,1
\end{array}\right]\right)
$$

$$
c_{2} \sim \operatorname{Normal}_{3}\left(\left(\begin{array}{l}
0 \\
0 \\
0
\end{array}\right),\left[\begin{array}{ll}
1,0,0 \\
0,1,0 \\
0,0,1
\end{array}\right]\right)
$$

$$
c_{3} \sim \operatorname{Normal}_{4}\left(\left(\begin{array}{l}
0 \\
0 \\
0 \\
0
\end{array}\right),\left[\begin{array}{lll}
1,0,0, & 0 \\
0,1,0, & 0 \\
0,0,1,0 \\
0,0,0,1
\end{array}\right]\right)
$$

![](https://cdn.mathpix.com/cropped/a8da9f2a-cc38-48a1-9a4a-3490f9b5504b-10.jpg?height=650&width=505&top_left_y=208&top_left_x=906)

## Example

With a pool of $K=3$ models and sizes

$$
M_{1}=2, \quad M_{2}=3, \quad M_{3}=4
$$

Our master Bayesian formulation consists of a likelihood

$$
Y \mid \kappa, c_{1: 3} \sim \operatorname{Normal}_{N}\left(\Phi_{\kappa} c_{\kappa}, I\right)
$$

with designs

$$
\begin{aligned}
& \Phi_{1} \in \mathbb{R}^{N \times 2} \\
& \Phi_{2} \in \mathbb{R}^{N \times 3} \\
& \Phi_{3} \in \mathbb{R}^{N \times 4}
\end{aligned}
$$

![](https://cdn.mathpix.com/cropped/a8da9f2a-cc38-48a1-9a4a-3490f9b5504b-11.jpg?height=651&width=505&top_left_y=208&top_left_x=906)

## Example

With a pool of $K=3$ models and sizes

$$
M_{1}=2, \quad M_{2}=3, \quad M_{3}=4
$$

and $N=10$ datapoints, our marginal posterior evaluates at

$$
\begin{aligned}
& p(\kappa=1 \mid Y) \propto 0.14 \times 10^{-8} \\
& p(\kappa=2 \mid Y) \propto 0.23 \times 10^{-8} \\
& p(\kappa=3 \mid Y) \propto 0.06 \times 10^{-8}
\end{aligned}
$$

indicating that model 2 is selected
This model has a feature expansion of

$$
\phi(x)=\left[1, x, x^{2}\right]
$$

![](https://cdn.mathpix.com/cropped/a8da9f2a-cc38-48a1-9a4a-3490f9b5504b-12.jpg?height=649&width=505&top_left_y=209&top_left_x=905)


## Gaussian random vectors

- Independence
- Marginals and conditionals
- Demonstrations
- Credible ellipses

## Normal distributions

- A multivariate normal random variable is denoted with
$$
w \sim \operatorname{Normal}_{D}(\mu, V)
$$
The probability density function is given by
$$
p(w)=\operatorname{Normal}_{D}(w ; \mu, V)=\frac{1}{\sqrt{(2 \pi)^{D}|V|}} \exp \left(-\frac{(w-\mu)^{t} V^{-1}(w-\mu)}{2}\right)
$$
- A univariate normal random variables is denoted with
$$
w \sim \operatorname{Normal}(\mu, v)
$$
The probability density function is given by
$$
p(w)=\operatorname{Normal}(w ; \mu, v)=\frac{1}{\sqrt{2 \pi v}} \exp \left(-\frac{1}{2} \frac{(w-\mu)^{2}}{v}\right)
$$

## Independence

We consider a special multivariate random variable

$$
\left(\begin{array}{c}
w_{1} \\
w_{2} \\
\vdots \\
w_{D}
\end{array}\right) \sim \operatorname{Normal}_{D}\left(\left(\begin{array}{c}
\mu_{1} \\
\mu_{2} \\
\vdots \\
\mu_{D}
\end{array}\right),\left[\begin{array}{cccc}
v_{1} & 0 & \cdots & 0 \\
0 & v_{2} & \cdots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \cdots & v_{D}
\end{array}\right]\right), \quad w_{d} \in \mathbb{R}, \quad \mu_{d} \in \mathbb{R}, \quad v_{d} \in \mathbb{R}_{+}
$$

The probability density is

$$
p\left(\left(\begin{array}{c}
w_{1} \\
w_{2} \\
\vdots \\
w_{D}
\end{array}\right)\right)=\prod_{d=1}^{D} \operatorname{Normal}\left(w_{d} ; \mu_{d}, v_{d}\right) \Longrightarrow\left\{\begin{array}{c}
w_{d} \sim \operatorname{Normal}\left(\mu_{d}, v_{d}\right) \\
d=1, \ldots, D
\end{array}\right.
$$

Similarly, we also show that

$$
\left.\begin{array}{c}
w_{d} \sim \operatorname{Normal}\left(\mu_{d}, v_{d}\right) \\
d=1, \ldots, D
\end{array}\right\} \Longrightarrow\left(\begin{array}{c}
w_{1} \\
w_{2} \\
\vdots \\
w_{D}
\end{array}\right) \sim \operatorname{Normal}_{D}\left(\left(\begin{array}{c}
\mu_{1} \\
\mu_{2} \\
\vdots \\
\mu_{D}
\end{array}\right),\left[\begin{array}{cccc}
v_{1} & 0 & \cdots & 0 \\
0 & v_{2} & \cdots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \cdots & v_{D}
\end{array}\right]\right)
$$

## Independence

We consider a special multivariate random variable

$$
\left(\begin{array}{c}
w_{1} \\
w_{2} \\
\vdots \\
w_{D}
\end{array}\right) \sim \operatorname{Normal}_{D}\left(\left(\begin{array}{c}
\mu_{1} \\
\mu_{2} \\
\vdots \\
\mu_{D}
\end{array}\right),\left[\begin{array}{cccc}
v_{1} & 0 & \cdots & 0 \\
0 & v_{2} & \cdots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \cdots & v_{D}
\end{array}\right]\right), \quad w_{d} \in \mathbb{R}, \quad \mu_{d} \in \mathbb{R}, \quad v_{d} \in \mathbb{R}_{+}
$$

According to the probability densities, we have the equivalence

$$
\left.\begin{array}{c}
w_{d} \sim \operatorname{Normal}\left(\mu_{d}, v_{d}\right) \\
d=1, \ldots, D
\end{array}\right\} \Longleftrightarrow\left(\begin{array}{c}
w_{1} \\
w_{2} \\
\vdots \\
w_{D}
\end{array}\right) \sim \operatorname{Normal}_{D}\left(\left(\begin{array}{c}
\mu_{1} \\
\mu_{2} \\
\vdots \\
\mu_{D}
\end{array}\right),\left[\begin{array}{cccc}
v_{1} & 0 & \cdots & 0 \\
0 & v_{2} & \cdots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \cdots & v_{D}
\end{array}\right]\right)
$$

- One consequence is that
$$
\left(\begin{array}{c}
w_{1} \\
w_{2} \\
\vdots \\
w_{D}
\end{array}\right) \sim \operatorname{Normal}_{D}(0, I) \Longleftrightarrow\left\{\begin{array}{c}
w_{d} \sim \operatorname{Normal}(0,1) \\
d=1, \ldots, D
\end{array}\right.
$$
- By convention, we will be writing
$$
p\left(\left(\begin{array}{c}
w_{1} \\
w_{2} \\
\vdots \\
w_{D}
\end{array}\right)\right) \equiv p\left(w_{1}, w_{2}, \cdots, w_{D}\right)
$$

## Rearrangements

We consider a multivariate random variable and a linear transformation

$$
\left(\begin{array}{l}
w_{1} \\
w_{2} \\
w_{3}
\end{array}\right) \sim \operatorname{Normal}_{3}\left(\left(\begin{array}{l}
\mu_{1} \\
\mu_{2} \\
\mu_{3}
\end{array}\right),\left[\begin{array}{lll}
v_{11} & v_{12} & v_{13} \\
v_{21} & v_{22} & v_{23} \\
v_{31} & v_{32} & v_{33}
\end{array}\right]\right), \quad\left(\begin{array}{l}
w_{3} \\
w_{1} \\
w_{2}
\end{array}\right)=\left[\begin{array}{lll}
0 & 0 & 1 \\
1 & 0 & 0 \\
0 & 1 & 0
\end{array}\right]\left(\begin{array}{l}
w_{1} \\
w_{2} \\
w_{3}
\end{array}\right)
$$

Because of the general transformation property, we have

$$
\begin{aligned}
\left(\begin{array}{l}
w_{3} \\
w_{1} \\
w_{2}
\end{array}\right) & \sim \operatorname{Normal}_{3}\left(\left[\begin{array}{lll}
0 & 0 & 1 \\
1 & 0 & 0 \\
0 & 1 & 0
\end{array}\right]\left(\begin{array}{l}
\mu_{1} \\
\mu_{2} \\
\mu_{3}
\end{array}\right),\left[\begin{array}{lll}
0 & 0 & 1 \\
1 & 0 & 0 \\
0 & 1 & 0
\end{array}\right]\left[\begin{array}{lll}
v_{11} & v_{12} & v_{13} \\
v_{21} & v_{22} & v_{23} \\
v_{31} & v_{32} & v_{33}
\end{array}\right]\left[\begin{array}{lll}
0 & 0 & 1 \\
1 & 0 & 0 \\
0 & 1 & 0
\end{array}\right]^{t}\right) \\
& =\operatorname{Normal}_{3}\left(\left[\begin{array}{lll}
0 & 0 & 1 \\
1 & 0 & 0 \\
0 & 1 & 0
\end{array}\right]\left(\begin{array}{l}
\mu_{1} \\
\mu_{2} \\
\mu_{3}
\end{array}\right),\left[\begin{array}{lll}
0 & 0 & 1 \\
1 & 0 & 0 \\
0 & 1 & 0
\end{array}\right]\left[\begin{array}{lll}
v_{11} & v_{12} & v_{13} \\
v_{21} & v_{22} & v_{23} \\
v_{31} & v_{32} & v_{33}
\end{array}\right]\left[\begin{array}{lll}
0 & 1 & 0 \\
0 & 0 & 1 \\
1 & 0 & 0
\end{array}\right]\right) \\
& =\operatorname{Normal}_{3}\left(\left(\begin{array}{l}
\mu_{3} \\
\mu_{1} \\
\mu_{2}
\end{array}\right),\left[\begin{array}{lll}
v_{33} & v_{13} & v_{23} \\
v_{13} & v_{11} & v_{12} \\
v_{23} & v_{21} & v_{22}
\end{array}\right]\right)
\end{aligned}
$$

We construct similarly any other multivariate normal rearrangement

## Conditionals

We consider a multivariate random variable partitioned in two blocks

$$
\binom{W_{1}}{W_{2}} \sim \operatorname{Normal}_{D}\left(\binom{M_{1}}{M_{2}},\left[\begin{array}{ll}
V_{1} & C^{t} \\
C & V_{2}
\end{array}\right]\right), \quad D_{1}+D_{2}=D \quad W_{1} \in \mathbb{R}^{D_{1}} \quad M_{1} \in \mathbb{R}^{D_{1}} \quad V_{1} \in \mathbb{R}^{D_{1} \times D_{1}} \quad C \in \mathbb{R}^{D_{2} \times D_{1}}
$$

By the definition of conditionals, we have

$$
p\left(W_{1} \mid W_{2}\right)=\frac{p\left(W_{1}, W_{2}\right)}{p\left(W_{2}\right)}=\frac{\operatorname{Normal}_{D}\left(\binom{W_{1}}{W_{2}} ;\binom{M_{1}}{M_{2}},\left[\begin{array}{ll}
V_{1} & C^{t} \\
C & V_{2}
\end{array}\right]\right)}{\operatorname{Normal}_{D_{2}}\left(W_{2} ; M_{2}, V_{2}\right)}=\cdots=\operatorname{Normal}_{D_{1}}\left(W_{1} ; M_{1}^{\prime}, V_{1}^{\prime}\right)
$$

We obtain similarly any other multivariate normal conditional

$$
W_{1} \mid W_{2} \sim \operatorname{Normal}_{D_{1}}\left(M_{1}^{\prime}, V_{1}^{\prime}\right)
$$

The conditional parameters are

$$
\begin{aligned}
& M_{1}^{\prime}=M_{1}+C^{t} V_{2}^{-1}\left(W_{2}-M_{2}\right) \\
& V_{1}^{\prime}=V_{1}-C^{t} V_{2}^{-1} C
\end{aligned}
$$

## Bayesian considerations

We consider a Bayesian model with scalar observations and obtain its posterior sequentially

$$
\left.\left.\begin{array}{r}
\mu \sim \operatorname{Normal}(M, V) \\
w_{1} \mid \mu \sim \operatorname{Normal}\left(\beta_{1} \mu, v_{1}\right) \\
w_{2} \mid \mu \sim \operatorname{Normal}\left(\beta_{2} \mu, v_{2}\right)
\end{array}\right\} \Longrightarrow \begin{array}{l}
\mu \mid w_{1} \sim \operatorname{Normal}\left(M^{\prime}, V^{\prime}\right) \\
w_{2} \mid \mu \sim \operatorname{Normal}\left(\beta_{2} \mu, v_{2}\right)
\end{array}\right\} \Longrightarrow \mu \mid w_{1}, w_{2} \sim \operatorname{Norma} I_{D}\left(M^{\prime \prime}, V^{\prime \prime}\right)
$$

## Equivalently

We consider a Bayesian model with vector observations and obtain its posterior directly

$$
\begin{gathered}
\mu \sim \operatorname{Normal}_{D}(M, V) \\
\left.\binom{w_{1}}{w_{2}} \left\lvert\, \mu \sim \operatorname{Normal}_{2}\left(\left[\begin{array}{l}
\beta_{1} \\
\beta_{2}
\end{array}\right] \mu,\left[\begin{array}{cc}
v_{1} & 0 \\
0 & v_{2}
\end{array}\right]\right)\right.\right\} \Longrightarrow \mu \left\lvert\,\binom{ w_{1}}{w_{2}} \sim \operatorname{Normal}_{D}\left(M^{\prime \prime}, V^{\prime \prime}\right)\right.
\end{gathered}
$$

## Whitening transformations

![](https://cdn.mathpix.com/cropped/1fbcd257-b58c-4a2e-a2f0-7c44443858bb-09.jpg?height=646&width=1200&top_left_y=145&top_left_x=209)

## Sequential updates

![](https://cdn.mathpix.com/cropped/1fbcd257-b58c-4a2e-a2f0-7c44443858bb-10.jpg?height=584&width=1190&top_left_y=173&top_left_x=209)

## Bivariate normal distributions

- A bivariate normal random variable is denoted with
$$
w \sim \operatorname{Normal}_{2}\left(\binom{\mu_{1}}{\mu_{2}},\left[\begin{array}{cc}
v_{1} & \rho \sqrt{v_{1} v_{2}} \\
\rho \sqrt{v_{1} v_{2}} & v_{2}
\end{array}\right]\right), \quad w_{1}, w_{2} \in \mathbb{R},
$$
$$
\mu_{1}, \mu_{2} \in \mathbb{R}, \quad v_{1}, v_{2} \in \mathbb{R}_{+}, \quad \rho \in(-1+1)
$$
A credible set is a set of values with a designated total probability of containing the value of our uncertain quantity
The $\gamma$-credible ellipse is an ellipse with a total probability $\gamma \in[0,1]$
This is given by
![](https://cdn.mathpix.com/cropped/1fbcd257-b58c-4a2e-a2f0-7c44443858bb-11.jpg?height=277&width=471&top_left_y=263&top_left_x=923)
$$
\begin{aligned}
w_{1}(t) & =\mu_{1}+\sqrt{s v_{1}} \cos (t) \\
w_{2}(t) & =\mu_{2}+\sqrt{s v_{2}}\left(\rho \cos (t)+\sqrt{1-\rho^{2}} \sin (t)\right) \\
t & \in[0,2 \pi)
\end{aligned}
$$
for $s=-2 \log (1-\gamma)$
![](https://cdn.mathpix.com/cropped/1fbcd257-b58c-4a2e-a2f0-7c44443858bb-11.jpg?height=273&width=470&top_left_y=556&top_left_x=924)

## Kernel regression

- Definitions

## Regressors in Bayesian regression

We have data $\left\{\left(x_{n}, y_{n}\right)\right\}_{n=1}^{N} \subset \mathbb{X} \times \mathbb{R}$ with scalar targets and seek a function

$$
f: \mathbb{X} \mapsto \mathbb{R}
$$

In Bayesian linear regression we use a model of the form

$$
\begin{aligned}
c & \sim \operatorname{Normal}_{M}(\mu, C) \\
y_{n} \mid c & \sim \operatorname{Normal}\left(\phi\left(x_{n}\right) c, \eta\right), \quad n=1, \ldots, N
\end{aligned}
$$

for a pre-chosen expansion $\phi: \mathbb{X} \mapsto \mathbb{R}^{1 \times M}$
Our regressor is defined indirectly

$$
\begin{aligned}
c & \sim \operatorname{Normal}_{M}(\mu, C) \\
f(x) & =\phi(x) c, \quad \forall x \in \mathbb{X}
\end{aligned}
$$

## Regressors in Bayesian regression

Our regressor is defined indirectly

$$
\begin{aligned}
c & \sim \operatorname{Normal}_{M}(\mu, C) \\
f(x) & =\phi(x) c,
\end{aligned}
$$

$$
\forall x \in \mathbb{X}
$$

We consider 1 point $x_{1}$
Our model provides the statistics

$$
\begin{aligned}
f & =\left(f\left(x_{1}\right)\right)=\left[\phi\left(x_{1}\right)\right] c=\Phi c \\
f & \sim \operatorname{Normal}_{1}\left(\Phi \mu, \Phi C \Phi^{t}\right) \\
& =\operatorname{Normal}_{1}(M, V)
\end{aligned}
$$

We consider 2 points $x_{1}, x_{2}$
Our model provides the statistics

$$
\begin{aligned}
f & =\binom{f\left(x_{1}\right)}{f\left(x_{2}\right)}=\left[\begin{array}{l}
\phi\left(x_{1}\right) \\
\phi\left(x_{2}\right)
\end{array}\right] c=\Phi c \\
f & \sim \operatorname{Normal}_{2}\left(\Phi \mu, \Phi C \Phi^{t}\right) \\
& =\operatorname{Normal}_{2}(M, V)
\end{aligned}
$$

We consider 3 points $x_{1}, x_{2}, x_{3}$
Our model provides the statistics

$$
\begin{aligned}
f & =\left(\begin{array}{l}
f\left(x_{1}\right) \\
f\left(x_{2}\right) \\
f\left(x_{3}\right)
\end{array}\right)=\left[\begin{array}{l}
\phi\left(x_{1}\right) \\
\phi\left(x_{2}\right) \\
\phi\left(x_{3}\right)
\end{array}\right] c=\Phi c \\
f & \sim \operatorname{NormaI}_{3}\left(\Phi \mu, \Phi C \Phi^{t}\right) \\
& =\operatorname{Normal}_{3}(M, V)
\end{aligned}
$$

In this way, we can obtain the statistics of any discretization of the regressor

## Regressors in Bayesian regression

In general, with $N$ points $x_{1}, x_{2}, \ldots, x_{N} \in \mathbb{X}$, our model provides the statistics

$$
\begin{aligned}
f & =\left(\begin{array}{c}
f\left(x_{1}\right) \\
f\left(x_{2}\right) \\
\vdots \\
f\left(x_{N}\right)
\end{array}\right)=\left[\begin{array}{c}
\phi\left(x_{1}\right) \\
\phi\left(x_{2}\right) \\
\vdots \\
\phi\left(x_{N}\right)
\end{array}\right] c=\Phi c \\
f & \sim \operatorname{Normal}_{N}\left(\Phi \mu, \Phi C \Phi^{t}\right) \\
& =\operatorname{Normal}_{N}(M, V)
\end{aligned}
$$

This is the same as

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

with the mean and covariance defined by

$$
m\left(x^{\prime}\right)=\phi\left(x^{\prime}\right) \mu \quad v\left(x^{\prime}, x^{\prime \prime}\right)=\phi\left(x^{\prime}\right) C \phi^{t}\left(x^{\prime \prime}\right)
$$

## Regressors in Bayesian regression

In general, with $N$ points $x_{1}, x_{2}, \ldots, x_{N} \in \mathbb{X}$, our model provides the statistics

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

with the mean and covariance given by

$$
m\left(x^{\prime}\right)=\phi\left(x^{\prime}\right) \mu
$$

Instead of starting with

$$
\begin{gathered}
\mu \in \mathbb{R}^{M} \\
C \in \mathbb{R}_{\text {sym, }}^{M \times M} \\
\phi: \mathbb{X} \mapsto \mathbb{R}^{1 \times M}
\end{gathered}
$$

to obtain $m\left(x^{\prime}\right)$ and $v\left(x^{\prime}, x^{\prime \prime}\right)$

$$
v\left(x^{\prime}, x^{\prime \prime}\right)=\phi\left(x^{\prime}\right) C \phi^{t}\left(x^{\prime \prime}\right)
$$

a kernel regression starts directly with

$$
\begin{aligned}
m: \mathbb{X} & \mapsto \mathbb{R} \\
v: \mathbb{X} \times \mathbb{X} & \mapsto \mathbb{R}
\end{aligned}
$$

and, to ensure valid covariance matrices $V$, considers only symmetric positive semi-definite kernels $\boldsymbol{v}$

## Bayesian linear regression revisited

We have data $\left\{\left(x_{n}^{\sharp}, y_{n}^{\sharp}\right)\right\}_{n=1}^{N^{\sharp}} \subset \mathbb{X} \times \mathbb{R}$ with scalar targets and seek predictions at $\left\{x_{n}^{\star}\right\}_{n=1}^{N^{\star}} \subset \mathbb{X}$
We start with a mean and a symmetric positive semi-definite kernel

$$
\begin{aligned}
m: \mathbb{X} & \mapsto \mathbb{R} \\
v: \mathbb{X} \times \mathbb{X} & \mapsto \mathbb{R}
\end{aligned}
$$

and obtain the prior

$$
\left(\begin{array}{c}
f\left(x_{1}^{\sharp}\right) \\
\vdots \\
f\left(x_{N^{\sharp}}^{\sharp}\right) \\
f\left(x_{1}^{\star}\right) \\
\vdots \\
f\left(x_{N^{\star}}^{\star}\right)
\end{array}\right) \sim \operatorname{Normal}_{N^{\sharp}+N^{\star}}\left(\left(\begin{array}{c}
m\left(x_{1}^{\sharp}\right) \\
\vdots \\
m\left(x_{N^{\sharp}}^{\#}\right) \\
m\left(x_{1}^{\star}\right) \\
\vdots \\
m\left(x_{N^{\star}}^{\star}\right)
\end{array}\right),\left[\begin{array}{ccccc}
v\left(x_{1}^{\sharp}, x_{1}^{\sharp}\right) & \cdots & v\left(x_{1}^{\sharp}, x_{N^{\#}}^{\#}\right) & v\left(x_{1}^{\sharp}, x_{1}^{\star}\right) & \cdots \\
\vdots & \ddots & \vdots & \vdots & \ddots \\
v\left(x_{N^{\sharp}}^{\sharp}, x_{1}^{\sharp}, x_{N^{\star}}^{\star}\right) & \cdots & v\left(x_{N^{\sharp}}^{\sharp}, x_{N^{\sharp}}^{\sharp}\right) & v\left(x_{N^{\sharp}}^{\sharp}, x_{1}^{\star}\right) & \cdots \\
v\left(x_{1}^{\star}, x_{1}^{\sharp}\right) & \cdots & v\left(x_{1}^{\star}, x_{N^{\sharp}}^{\sharp}\right) & v\left(x_{1}^{\star}, x_{1}^{\star}\right) & \cdots \\
\vdots & \ddots & \vdots & \vdots & \ddots \\
v\left(x_{N^{\star}}^{\star}, x_{1}^{\star}\right) & \cdots & v\left(x_{N^{\star}}^{\star}, x_{N^{\star}}^{\sharp}\right) & v\left(x_{N^{\star}}^{\star}, x_{1}^{\star}\right) & \cdots \\
& v\left(x_{N^{\star}}^{\star}, x_{N^{\star}}^{\star}\right)
\end{array}\right]\right)
$$

## Bayesian linear regression revisited

$$
\left(\begin{array}{c}
f\left(x_{1}^{\sharp}\right) \\
\vdots \\
f\left(x_{N^{\sharp}}^{\sharp}\right) \\
f\left(x_{1}^{\star}\right) \\
\vdots \\
f\left(x_{N^{\star}}^{\star}\right)
\end{array}\right) \sim \operatorname{Normal}_{N^{\sharp}+N^{\star}}\left(\left(\begin{array}{c}
m\left(x_{1}^{\sharp}\right) \\
\vdots \\
m\left(x_{N^{\sharp}}^{\#}\right) \\
m\left(x_{1}^{\star}\right) \\
\vdots \\
m\left(x_{N^{\star}}^{\star}\right)
\end{array}\right),\left[\begin{array}{cccccc}
v\left(x_{1}^{\sharp}, x_{1}^{\sharp}\right) & \cdots & v\left(x_{1}^{\sharp}, x_{N^{\#}}^{\#}\right) & v\left(x_{1}^{\sharp}, x_{1}^{\star}\right) & \cdots & v\left(x_{1}^{\sharp}, x_{N^{\star}}^{\star}\right) \\
\vdots & \ddots & \vdots & \vdots & \ddots & \vdots \\
v\left(x_{N^{\sharp}}^{\sharp}, x_{1}^{\sharp}\right) & \cdots & v\left(x_{N^{\sharp}}^{\sharp}, x_{N^{\sharp}}^{\sharp}\right) & v\left(x_{N^{\sharp}}^{\sharp}, x_{1}^{\star}\right) & \cdots & v\left(x_{N^{\sharp}}^{\sharp}, x_{N^{\star}}^{\star}\right) \\
v\left(x_{1}^{\star}, x_{1}^{\sharp}\right) & \cdots & v\left(x_{1}^{\star}, x_{N^{\sharp}}^{\sharp}\right) & v\left(x_{1}^{\star}, x_{1}^{\star}\right) & \cdots & v\left(x_{1}^{\star}, x_{N^{\star}}^{\star}\right) \\
\vdots & \ddots & \vdots & \vdots & \ddots & \vdots \\
v\left(x_{N^{\star}}^{\star}, x_{1}^{\sharp}\right) & \cdots & v\left(x_{N^{\star}}^{\star}, x_{N^{\sharp}}^{\sharp}\right) & v\left(x_{N^{\star}}^{\star}, x_{1}^{\star}\right) & \cdots & v\left(x_{N^{\star}}^{\star}, x_{N^{\star}}^{\star}\right)
\end{array}\right]\right)
$$

Our likelihood take the form

$$
\left(\begin{array}{c}
y_{1}^{\sharp} \\
\vdots \\
y_{N^{\sharp}}^{\sharp}
\end{array}\right) \left\lvert\,\left(\begin{array}{c}
f\left(x_{1}^{\sharp}\right) \\
\vdots \\
f\left(x_{N^{\sharp}}^{\sharp}\right)
\end{array}\right) \sim \operatorname{Normal}_{N^{\sharp}}\left(\left(\begin{array}{c}
f\left(x_{1}^{\sharp}\right) \\
\vdots \\
f\left(x_{N^{\sharp}}^{\sharp}\right)
\end{array}\right), \eta\left[\begin{array}{ccc}
1 & \cdots & 0 \\
\vdots & \ddots & \vdots \\
0 & \cdots & 1
\end{array}\right]\right)\right.
$$

## Bayesian linear regression revisited

In more compact form, our mode is given by

$$
\begin{aligned}
& \binom{f^{\sharp}}{f^{\star}} \sim \operatorname{Normal}_{N^{\sharp}+N^{\star}}\left(\binom{m^{\sharp}}{m^{\star}},\left[\begin{array}{cc}
v^{\sharp \sharp} & v^{\sharp \star} \\
v^{\star \sharp} & v^{\star \star}
\end{array}\right]\right) \\
& y^{\#} f^{\#} \sim \operatorname{Normal}_{N^{\sharp}}\left(f^{\#}, \eta I^{\sharp \sharp}\right)
\end{aligned}
$$

Our model gives

$$
\begin{aligned}
& f^{\sharp} \sim \operatorname{Normal}_{N \sharp}\left(m^{\sharp}, v^{\sharp \sharp}\right) \\
& f^{\star} \mid f^{\sharp} \sim \operatorname{Normal}_{N^{\star}}\left(m^{\star}+v^{\star \sharp}\left(v^{\sharp \sharp}\right)^{-1}\left(f^{\sharp}-m^{\sharp}\right), v^{\star \star}-v^{\star \sharp}\left(v^{\sharp \sharp}\right)^{-1} v^{\sharp \star}\right) \\
& y^{\sharp} \mid f^{\sharp} \sim \operatorname{Normal}_{N^{\sharp}}\left(f^{\sharp}, \eta I^{\sharp \sharp}\right)
\end{aligned}
$$

## Bayesian linear regression revisited

Our model gives

$$
\begin{aligned}
& f^{\sharp} \sim \operatorname{Normal}_{N}\left(m^{\sharp}, v^{\sharp \sharp}\right) \\
& f^{\star} \mid f^{\sharp} \sim \operatorname{Normal}_{N^{\star}}\left(m^{\star}+v^{\star \sharp}\left(v^{\sharp \sharp}\right)^{-1}\left(f^{\#}-m^{\sharp}\right), v^{\star \star}-v^{\star \sharp}\left(v^{\sharp \sharp}\right)^{-1} v^{\sharp \star}\right) \\
& y^{\sharp} \mid f^{\sharp} \sim \operatorname{Normal}_{N^{\sharp}}\left(f^{\sharp}, \eta l^{\sharp \sharp}\right)
\end{aligned}
$$

In turn, this gives

$$
\begin{aligned}
& f^{\sharp} \mid y^{\sharp} \sim \operatorname{Normal}_{N}\left(\bar{m}^{\sharp}, \bar{v}^{\sharp \sharp}\right) \\
& f^{\star} \mid f^{\sharp} \sim \operatorname{Normal}_{N^{\star}}\left(m^{\star}+v^{\star \sharp}\left(v^{\sharp \sharp}\right)^{-1}\left(f^{\sharp}-m^{\sharp}\right), v^{\star \star}-v^{\star \sharp}\left(v^{\sharp \sharp}\right)^{-1} v^{\sharp \star}\right)
\end{aligned}
$$

with the updated hyper-parameters given by

$$
\bar{m}^{\sharp}=\bar{v}^{\sharp \sharp}\left(\left(v^{\sharp \sharp}\right)^{-1} m^{\sharp}+\frac{1}{\eta} y^{\sharp}\right), \quad \bar{v}^{\sharp \sharp}=\left(\left(v^{\sharp \sharp}\right)^{-1}+\frac{1}{\eta} l^{\sharp \sharp}\right)^{-1}
$$

## Bayesian linear regression revisited

Our model gives

$$
\begin{aligned}
& f^{\sharp} \mid y^{\sharp} \sim \operatorname{Normal}_{N^{\sharp}}\left(\bar{m}^{\sharp}, \bar{v}^{\sharp \sharp}\right) \\
& f^{\star} \mid f^{\sharp} \sim \operatorname{Normal}_{N^{\star}}\left(m^{\star}+v^{\star \sharp}\left(v^{\sharp \sharp}\right)^{-1}\left(f^{\sharp}-m^{\sharp}\right), v^{\star \star}-v^{\star \sharp}\left(v^{\sharp ⿱}\right)^{-1} v^{\sharp \star}\right)
\end{aligned}
$$

Finally, this gives

$$
f^{\star} \mid y^{\#} \sim \operatorname{Normal}_{N^{\star}}\left(\bar{m}^{\star}, \bar{v}^{\star \star}\right)
$$

with the hyper-parameters given by

$$
\begin{aligned}
\bar{m}^{\star} & =m^{\star}+v^{\star \sharp}\left(v^{\# \#}\right)^{-1}\left(\bar{m}^{\#}-m^{\#}\right), \\
\bar{v}^{\star \star} & =v^{\star \sharp}\left(v^{\# \sharp}\right)^{-1} \bar{v}^{\# \sharp}\left(v^{\# \#}\right)^{-1} v^{\sharp \star}+v^{\star \star}-v^{\star \sharp}\left(v^{\# \sharp}\right)^{-1} v^{\sharp \star} \\
& =v^{\star \sharp}\left[\left(v^{\# \sharp}\right)^{-1} \bar{v}^{\# \sharp}\left(v^{\# \#}\right)^{-1}-\left(v^{\#}\right)^{-1}\right] v^{\sharp \star}+v^{\star \star}
\end{aligned}
$$

## Bayesian linear regression revisited

Our model gives

$$
\begin{aligned}
& f^{\sharp} \mid y^{\sharp} \sim \operatorname{Normal}_{N^{\sharp}}\left(\bar{m}^{\sharp}, \bar{v}^{\sharp \sharp}\right) \\
& f^{\star} \mid f^{\sharp} \sim \operatorname{Normal}_{N^{\star}}\left(m^{\star}+v^{\star \sharp}\left(v^{\sharp \sharp}\right)^{-1}\left(f^{\sharp}-m^{\sharp}\right), v^{\star \star}-v^{\star \sharp}\left(v^{\sharp ⿱}\right)^{-1} v^{\sharp \star}\right)
\end{aligned}
$$

Finally, this gives

$$
f^{\star} \mid y^{\#} \sim \operatorname{Normal}_{N^{\star}}\left(\bar{m}^{\star}, \bar{v}^{\star \star}\right)
$$

with the hyper-parameters given by

$$
\begin{aligned}
\bar{m}^{\star} & =m^{\star}+v^{\star \sharp}\left(v^{\# \#}\right)^{-1}\left(\bar{m}^{\#}-m^{\#}\right), \\
\bar{v}^{\star \star} & =v^{\star \sharp}\left(v^{\# \#}\right)^{-1} \bar{v}^{\# \#}\left(v^{\# \#}\right)^{-1} v^{\# \star}+v^{\star \star}-v^{\star \sharp}\left(v^{\# \#}\right)^{-1} v^{\# \star} \\
& =v^{\star \sharp}\left[\left(v^{\# \sharp}\right)^{-1} \bar{v}^{\# \sharp}\left(v^{\# \sharp}\right)^{-1}-\left(v^{\# \sharp}\right)^{-1}\right] v^{\sharp \star}+v^{\star \star} \\
& =v^{\star \sharp}\left(v^{\# \sharp}\right)^{-1}\left[\bar{v}^{\# \sharp}\left(v^{\sharp \sharp}\right)^{-1}-I^{\sharp \sharp}\right] v^{\sharp \star}+v^{\star \star}
\end{aligned}
$$

## Kernels

To conduct kernel regression, we need a mean and a kernel

$$
\begin{aligned}
m: \mathbb{X} & \mapsto \mathbb{R} \\
v: \mathbb{X} \times \mathbb{X} & \mapsto \mathbb{R}
\end{aligned}
$$

The kernel must be symmetric

$$
v\left(x^{\prime}, x^{\prime \prime}\right)=v\left(x^{\prime \prime}, x^{\prime}\right), \quad \forall x^{\prime}, x^{\prime \prime} \in \mathbb{X}
$$

and positive semi-definite, this means that

$$
\sum_{n^{\prime}=1}^{N} \sum_{n^{\prime \prime}=1}^{N} \gamma_{n^{\prime}} \gamma_{n^{\prime \prime}} v\left(x_{n^{\prime}}, x_{n^{\prime \prime}}\right) \geq 0
$$

for any choice of $x_{1}, \ldots, x_{N} \in \mathbb{X}, \gamma_{1}, \ldots, \gamma_{N} \in \mathbb{R}$ and $N=1,2, \ldots$

- Having a symmetric positive semi-definite kernel $v_{0}$, new kernels can be obtained by
$$
\begin{aligned}
v\left(x^{\prime}, x^{\prime \prime}\right) & =c v_{0}\left(x^{\prime}, x^{\prime \prime}\right), & & c>0 \\
v\left(x^{\prime}, x^{\prime \prime}\right) & =c+v_{0}\left(x^{\prime}, x^{\prime \prime}\right), & & c>0
\end{aligned}
$$
- Having symmetric positive semi-definite kernels $v_{1}$ and $v_{2}$, new kernels can be obtained by
$$
\begin{aligned}
& v\left(x^{\prime}, x^{\prime \prime}\right)=v_{1}\left(x^{\prime}, x^{\prime \prime}\right)+v_{2}\left(x^{\prime}, x^{\prime \prime}\right) \\
& v\left(x^{\prime}, x^{\prime \prime}\right)=v_{1}\left(x^{\prime}, x^{\prime \prime}\right) v_{2}\left(x^{\prime}, x^{\prime \prime}\right)
\end{aligned}
$$

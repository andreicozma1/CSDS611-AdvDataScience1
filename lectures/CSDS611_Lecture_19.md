## Implementation of Gaussian processes regression

- Numerical implementation
- Non-standard kernels

## GP regression

We have data $\left\{\left(x_{n}^{\sharp}, y_{n}^{\sharp}, \epsilon_{n}^{\sharp}\right)\right\}_{n=1}^{N^{\sharp}} \subset \mathbb{X} \times \mathbb{R} \times \mathbb{R}$ and seek an unknown function

$$
f: \mathbb{X} \mapsto \mathbb{R}
$$

- Our regression model consists of
$$
\begin{aligned}
f & \sim \operatorname{GP}_{\mathbb{X}}(m, v) \\
y_{n}^{\sharp} \mid f & \sim \operatorname{~Normal}\left(f\left(x_{n}^{\sharp}\right), v_{n}^{\sharp}\right), \quad n=1, \ldots, N^{\sharp}
\end{aligned}
$$
- To obtain predictions at some $x^{\star} \in \mathbb{X}$, we apply the predictive distribution
$$
\begin{array}{rlrl}
f^{\star} \mid Y^{\#} & \sim \operatorname{Normal}_{1}\left(\mu^{\star}, v^{\star}\right) & f^{\star} & \equiv f\left(x^{\star}\right) \\
\mu^{\star} & =m^{\star}+V^{\star \sharp}\left(P^{\# \#}+V^{\sharp \sharp}\right)^{-1}\left(Y^{\#}-m^{\sharp}\right) & \mu^{\star} \equiv \mu\left(x^{\star}\right) \\
v^{\star} & =V^{\star \star}-V^{\star \sharp}\left(P^{\# \#}+V^{\sharp \sharp}\right)^{-1} V^{\sharp \star} & v^{\star} \equiv v\left(x^{\star}\right)
\end{array}
$$

## Implementation of the predictive statistics

Our predictive statistics, at input $x^{\star} \in \mathbb{X}$, are determined by

$$
\begin{aligned}
& \mu^{\star}=m^{\star}+V^{\star \sharp}\left(P^{\# \#}+V^{\# \#}\right)^{-1}\left(Y^{\#}-m^{\#}\right) \\
& v^{\star}=V^{\star \star}-V^{\star \sharp}\left(P^{\# \#}+V^{\# \#}\right)^{-1} V^{\sharp \star}
\end{aligned}
$$

$$
\begin{aligned}
& \mu^{\star} \equiv \mu\left(x^{\star}\right) \\
& v^{\star} \equiv v\left(x^{\star}\right)
\end{aligned}
$$

Evaluation of $\mu^{*}, v^{*}$ starts with the (lower) Cholesky factor
...which is computed in time $O\left(\left(N^{\sharp}\right)^{3}\right)$

$$
\left(L^{\sharp \sharp}\right)\left(L^{\sharp \sharp}\right)^{t}=P^{\sharp \sharp}+V^{\sharp \sharp}
$$

and proceeds via the vector
...which is computed in time $O\left(\left(N^{\sharp}\right)^{2}\right)$

$$
\alpha^{\sharp}=\left(P^{\sharp \sharp}+V^{\sharp \sharp}\right)^{-1}\left(Y^{\sharp}-m^{\sharp}\right) \Longleftrightarrow\left(P^{\sharp \sharp}+V^{\sharp \sharp}\right) \alpha^{\sharp}=Y^{\sharp}-m^{\sharp} \Longleftrightarrow\left(L^{\sharp \sharp}\right)\left(L^{\sharp \sharp}\right)^{t} \alpha^{\sharp}=Y^{\sharp}-m^{\sharp}
$$

and the matrix

$$
V^{\star \sharp}\left(P^{\sharp \sharp}+V^{\sharp \sharp}\right)^{-1} V^{\sharp \star}=V^{\star \sharp}\left(\left(L^{\sharp \sharp}\right)\left(L^{\sharp \sharp}\right)^{t}\right)^{-1} V^{\sharp \star}=V^{\star \sharp}\left(L^{\sharp \sharp}\right)^{-t}\left(L^{\sharp \sharp}\right)^{-1} V^{\sharp \star}=\left(\left(L^{\sharp \sharp}\right)^{-1} V^{\sharp \star}\right)^{t}\left(\left(L^{\sharp \sharp}\right)^{-1} V^{\sharp \star}\right)
$$

...given $\alpha^{\sharp}$, the predictive mean $\mu^{\star}$ is obtained in time $O\left(N^{\#}\right)$
...given $L^{\sharp \sharp}$, the predictive variance $v^{\star}$ is obtained in time $O\left(\left(N^{\sharp}\right)^{2}\right)$

## Implementation of the Cholesky factor

We consider the (lower) Cholesky factor

$$
\left(L^{\sharp \sharp}\right)\left(L^{\sharp \sharp}\right)^{t}=P^{\sharp \sharp}+V^{\sharp \sharp}
$$

Our $L^{\sharp \sharp}$ is based on the discretization

$$
x^{\sharp}=\left(\begin{array}{c}
x_{1}^{\sharp} \\
\vdots \\
x_{N^{\sharp}}^{\sharp}
\end{array}\right)
$$

The direct computation of $L^{\sharp \sharp}$ is achieved in time $O\left(\left(N^{\sharp}\right)^{3}\right)$

We partition $x^{\sharp}$ like this

$$
x^{\sharp}=\left(\begin{array}{c}
x_{1}^{\sharp} \\
\vdots \\
x_{N^{\sharp}}^{\sharp}
\end{array}\right) \equiv\binom{x_{\text {old }}}{x_{\text {add }}}=x_{\text {new }}
$$

and consider the corresponding Cholesky factors

$$
\begin{aligned}
N^{\sharp} \leftrightarrow x^{\sharp} \leftrightarrow L^{\sharp \sharp} \equiv & L_{\text {new }} \leftrightarrow x_{\text {new }} \leftrightarrow N_{\text {new }} \\
& L_{\text {old }} \leftrightarrow x_{\text {old }} \leftrightarrow N_{\text {old }}
\end{aligned}
$$

According to this scheme, $L_{\text {new }}$ can be obtained sequentially

## Implementation of the Cholesky factor

Our partitioned discretization and sequential discretization scheme is

$$
x_{\text {new }}=\binom{x_{\text {old }}}{x_{\text {add }}} \quad L_{\text {old }} \leftrightarrow x_{\text {old }} \leftrightarrow N_{\text {old }} \quad L_{\text {new }} \leftrightarrow x_{\text {new }} \leftrightarrow N_{\text {new }} \quad N_{\text {new }}=N_{\text {old }}+N_{\text {add }}
$$

The (lower) Cholesky factors are defined by the decompositions

$$
L_{\text {old }} L_{\text {old }}^{t}=P_{\text {old }}+V_{\text {old }} \quad L_{\text {new }} L_{\text {new }}^{t}=P_{\text {new }}+V_{\text {new }}
$$

and are obtained by

$$
P_{\text {new }}=\left[\begin{array}{cc}
P_{\text {old }} & 0 \\
0 & P_{\text {add }}
\end{array}\right] \quad V_{\text {new }}=\left[\begin{array}{cc}
V_{\text {old }} & V_{\text {old }, \text { add }} \\
V_{\text {add }, \text { old }} & V_{\text {add }}
\end{array}\right]
$$

Accordingly, the updated Cholesky factor is

$$
L_{\text {new }} L_{\text {new }}^{t}=\left[\begin{array}{cc}
P_{\text {old }}+V_{\text {old }} & V_{\text {old }, \text { add }} \\
V_{\text {add }, \text { old }} & P_{\text {add }}+V_{\text {add }}
\end{array}\right]
$$

This indicates that

$$
L_{\text {new }}=\left(\begin{array}{cc}
L_{\text {old }} & 0 \\
\Lambda_{1} & \Lambda_{2}
\end{array}\right), \quad \quad \Lambda_{2} \Lambda_{2}^{t}=P_{\text {add }}+V_{\text {add }}-\Lambda_{1} \Lambda_{1}^{t}, \quad \Lambda_{1}=v_{\text {add }, \text { old }} L_{\text {old }}^{-t}
$$

...this way the computation of $L_{\text {new }}$ requires only time $O\left(N_{\text {add }} N_{\text {old }}\right)$

## The squared exponential kernel

The square exponential kernel is

$$
v\left(x^{\prime}, x^{\prime \prime}\right)=\sigma^{2} \exp \left(-\frac{1}{2}\left(\frac{x^{\prime}-x^{\prime \prime}}{\ell}\right)^{2}\right) \quad x^{\prime}, x^{\prime \prime} \in \mathbb{R}
$$

The kernel parameters consist of a strength $\sigma$ and a scale $\ell$
Our prior is

$$
\binom{f\left(x^{\prime}\right)}{f\left(x^{\prime \prime}\right)} \sim \operatorname{Normal}_{2}\left(\binom{m\left(x^{\prime}\right)}{m\left(x^{\prime \prime}\right)},\left[\begin{array}{cc}
v\left(x^{\prime}, x^{\prime}\right) & v\left(x^{\prime}, x^{\prime \prime}\right) \\
v\left(x^{\prime \prime}, x^{\prime}\right) & \left(x^{\prime \prime}, x^{\prime \prime}\right)
\end{array}\right]\right)
$$

Our correlation is given by

$$
C\left(x^{\prime}, x^{\prime \prime}\right)=\frac{v\left(x^{\prime}, x^{\prime \prime}\right)}{\sqrt{v\left(x^{\prime}, x^{\prime}\right)} \sqrt{v\left(x^{\prime \prime}, x^{\prime \prime}\right)}}=\exp \left(-\frac{1}{2}\left(\frac{x^{\prime}-x^{\prime \prime}}{\ell}\right)^{2}\right)
$$

![](https://cdn.mathpix.com/cropped/f91aa640-eaf9-4c5b-848e-e95ec34948af-07.jpg?height=702&width=1410&top_left_y=91&top_left_x=74)

## The white noise kernel

The white noise kernel is

$$
v\left(x^{\prime}, x^{\prime \prime}\right)=\sigma^{2} \cdot\left\{\begin{array}{ll}
1, & x^{\prime}=x^{\prime \prime} \\
0, & x^{\prime} \neq x^{\prime \prime}
\end{array} \quad x^{\prime}, x^{\prime \prime} \in \mathbb{R}\right.
$$

The only kernel parameter consist of a strength $\sigma$
Our prior is

$$
\binom{f\left(x^{\prime}\right)}{f\left(x^{\prime \prime}\right)} \sim \operatorname{Normal}_{2}\left(\binom{m\left(x^{\prime}\right)}{m\left(x^{\prime \prime}\right)},\left[\begin{array}{cc}
v\left(x^{\prime}, x^{\prime}\right) & v\left(x^{\prime}, x^{\prime \prime}\right) \\
v\left(x^{\prime \prime}, x^{\prime}\right) & \left(x^{\prime \prime}, x^{\prime \prime}\right)
\end{array}\right]\right)
$$

Our correlation is given by

$$
C\left(x^{\prime}, x^{\prime \prime}\right)=\frac{v\left(x^{\prime}, x^{\prime \prime}\right)}{\sqrt{v\left(x^{\prime}, x^{\prime}\right)} \sqrt{v\left(x^{\prime \prime}, x^{\prime \prime}\right)}}= \begin{cases}1, & x^{\prime}=x^{\prime \prime} \\ 0, & x^{\prime} \neq x^{\prime \prime}\end{cases}
$$

![](https://cdn.mathpix.com/cropped/f91aa640-eaf9-4c5b-848e-e95ec34948af-09.jpg?height=701&width=1410&top_left_y=92&top_left_x=74)

## The constant kernel

The constant kernel is

$$
v\left(x^{\prime}, x^{\prime \prime}\right)=\sigma^{2} \quad x^{\prime}, x^{\prime \prime} \in \mathbb{R}
$$

The only kernel parameter consist of a strength $\sigma$
Our prior is

$$
\binom{f\left(x^{\prime}\right)}{f\left(x^{\prime \prime}\right)} \sim \operatorname{Normal}_{2}\left(\binom{m\left(x^{\prime}\right)}{m\left(x^{\prime \prime}\right)},\left[\begin{array}{cc}
v\left(x^{\prime}, x^{\prime}\right) & v\left(x^{\prime}, x^{\prime \prime}\right) \\
v\left(x^{\prime \prime}, x^{\prime}\right) & \left(x^{\prime \prime}, x^{\prime \prime}\right)
\end{array}\right]\right)
$$

Our correlation is given by

$$
C\left(x^{\prime}, x^{\prime \prime}\right)=\frac{v\left(x^{\prime}, x^{\prime \prime}\right)}{\sqrt{v\left(x^{\prime}, x^{\prime}\right)} \sqrt{v\left(x^{\prime \prime}, x^{\prime \prime}\right)}}=1
$$

![](https://cdn.mathpix.com/cropped/f91aa640-eaf9-4c5b-848e-e95ec34948af-11.jpg?height=703&width=1411&top_left_y=90&top_left_x=72)

## The exponential sine squared kernel

The constant kernel is

$$
v\left(x^{\prime}, x^{\prime \prime}\right)=\sigma^{2} \exp \left(-\frac{2}{\ell^{2}} \sin ^{2}\left(\frac{\pi}{p}\left(x^{\prime}-x^{\prime \prime}\right)\right)\right) \quad x^{\prime}, x^{\prime \prime} \in \mathbb{R}
$$

The kernel parameters consist of a strength $\sigma$, a scale $\ell$, and a period $p$
Our prior is

$$
\binom{f\left(x^{\prime}\right)}{f\left(x^{\prime \prime}\right)} \sim \operatorname{Normal}_{2}\left(\binom{m\left(x^{\prime}\right)}{m\left(x^{\prime \prime}\right)},\left[\begin{array}{cc}
v\left(x^{\prime}, x^{\prime}\right) & v\left(x^{\prime}, x^{\prime \prime}\right) \\
v\left(x^{\prime \prime}, x^{\prime}\right) & \left(x^{\prime \prime}, x^{\prime \prime}\right)
\end{array}\right]\right)
$$

Our correlation is given by

$$
C\left(x^{\prime}, x^{\prime \prime}\right)=\frac{v\left(x^{\prime}, x^{\prime \prime}\right)}{\sqrt{v\left(x^{\prime}, x^{\prime}\right)} \sqrt{v\left(x^{\prime \prime}, x^{\prime \prime}\right)}}=\exp \left(-\frac{2}{\ell^{2}} \sin ^{2}\left(\frac{\pi}{p}\left(x^{\prime}-x^{\prime \prime}\right)\right)\right)
$$

![](https://cdn.mathpix.com/cropped/f91aa640-eaf9-4c5b-848e-e95ec34948af-13.jpg?height=702&width=1412&top_left_y=91&top_left_x=73)

## The diffusion kernel

The diffusion kernel is

$$
v\left(x^{\prime}, x^{\prime \prime}\right)=2 D \min \left\{\left|x^{\prime}\right|,\left|x^{\prime \prime}\right|\right\} \quad x^{\prime}, x^{\prime \prime} \in \mathbb{R}
$$

The only kernel parameter consists of a diffusivity $D$
Our prior is

$$
\binom{f\left(x^{\prime}\right)}{f\left(x^{\prime \prime}\right)} \sim \operatorname{Normal}_{2}\left(\binom{m\left(x^{\prime}\right)}{m\left(x^{\prime \prime}\right)},\left[\begin{array}{cc}
v\left(x^{\prime}, x^{\prime}\right) & v\left(x^{\prime}, x^{\prime \prime}\right) \\
v\left(x^{\prime \prime}, x^{\prime}\right) & \left(x^{\prime \prime}, x^{\prime \prime}\right)
\end{array}\right]\right)
$$

Our correlation is given by

$$
C\left(x^{\prime}, x^{\prime \prime}\right)=\frac{v\left(x^{\prime}, x^{\prime \prime}\right)}{\sqrt{v\left(x^{\prime}, x^{\prime}\right)} \sqrt{v\left(x^{\prime \prime}, x^{\prime \prime}\right)}}=\frac{\min \left\{\left|x^{\prime}\right|,\left|x^{\prime \prime}\right|\right\}}{\sqrt{\left|x^{\prime} x^{\prime \prime}\right|}}
$$

![](https://cdn.mathpix.com/cropped/f91aa640-eaf9-4c5b-848e-e95ec34948af-15.jpg?height=704&width=1412&top_left_y=89&top_left_x=72)

## The anchored diffusion kernel

The anchored diffusion kernel is

$$
v\left(x^{\prime}, x^{\prime \prime}\right)=2 D \cdot\left\{\begin{array}{ll}
\min \left\{\left|x^{\prime}-X\right|,\left|x^{\prime \prime}-X\right|\right\}, & x^{\prime}>X, x^{\prime \prime}>X \\
\min \left\{\left|x^{\prime}-X\right|,\left|x^{\prime \prime}-X\right|\right\}, & x^{\prime}<X, x^{\prime \prime}<X \\
0, & x^{\prime}>X, x^{\prime \prime}<X \\
0, & x^{\prime}<X, x^{\prime \prime}>X
\end{array} \quad x^{\prime}, x^{\prime \prime} \in \mathbb{R}\right.
$$

The kernel parameters consist of a diffusivity $D$ and an anchor $X$
Our prior is

$$
\binom{f\left(x^{\prime}\right)}{f\left(x^{\prime \prime}\right)} \sim \operatorname{Normal}_{2}\left(\binom{m\left(x^{\prime}\right)}{m\left(x^{\prime \prime}\right)},\left[\begin{array}{cc}
v\left(x^{\prime}, x^{\prime}\right) & v\left(x^{\prime}, x^{\prime \prime}\right) \\
v\left(x^{\prime \prime}, x^{\prime}\right) & \left(x^{\prime \prime}, x^{\prime \prime}\right)
\end{array}\right]\right)
$$

Our correlation is given by

$$
C\left(x^{\prime}, x^{\prime \prime}\right)=\frac{v\left(x^{\prime}, x^{\prime \prime}\right)}{\sqrt{v\left(x^{\prime}, x^{\prime}\right)} \sqrt{v\left(x^{\prime \prime}, x^{\prime \prime}\right)}}= \begin{cases}\frac{\min \left\{\left|x^{\prime}-X\right|,\left|x^{\prime \prime}-X\right|\right\}}{\sqrt{\left(x^{\prime}-X\right)\left(x^{\prime \prime}-X\right)}}, & x^{\prime}>X, x^{\prime \prime}>X \\ \frac{\min \left\{\left|x^{\prime}-X\right|,\left|x^{\prime \prime}-X\right|\right\}}{\sqrt{\left(x^{\prime}-X\right)\left(x^{\prime \prime}-X\right)}}, & x^{\prime}<X, x^{\prime \prime}<X \\ 0, & x^{\prime}>X, x^{\prime \prime}<X \\ 0, & x^{\prime}<X, x^{\prime \prime}>X\end{cases}
$$

![](https://cdn.mathpix.com/cropped/f91aa640-eaf9-4c5b-848e-e95ec34948af-17.jpg?height=704&width=1413&top_left_y=89&top_left_x=72)


## Gaussian random vectors

- Multivariate normal distributions

## Multivariate normal

A multivariate normal random variable is denoted with

$$
w \sim \operatorname{Normal}_{D}(\mu, V)
$$

This variable attains real vectorial values in $\mathbb{R}^{D}$
The probability density function is given by

$$
p(w)=\operatorname{Normal}_{D}(w ; \mu, V)=\frac{1}{\sqrt{(2 \pi)^{D}|V|}} \exp \left(-\frac{(w-\mu)^{t} V^{-1}(w-\mu)}{2}\right)
$$

The parameters are $\mu \in \mathbb{R}^{D}$ and $V \in \mathbb{R}_{\text {sym },+}^{D \times D} \quad \ldots \mathbb{R}_{\text {sym },+}^{D \times D}$ denotes symmetric, strictly positive definite matrices By convention:

- vectors in $\mathbb{R}^{D}$ are column arrays
- the transpose $v^{t}$ is a row array $\quad \ldots$ this is a linear map $\mathbb{R}^{D} \mapsto \mathbb{R}$
- $V^{-1}$ denotes the inverse matrix ...this is a linear map $\mathbb{R}^{D} \mapsto \mathbb{R}^{D}$
- $(w-\mu)^{t} V^{-1}(w-\mu)$ is an inner product on $\mathbb{R}^{D}$
- $|V|$ denotes the determinant on $\mathbb{R}^{D \times D} \ldots$ for scalars $c$, the determinant follows $|c V|=c^{D}|V|$

## Special cases

We consider a variable

$$
w \sim \operatorname{Normal}_{D}(\mu, V), \quad \mu \in \mathbb{R}^{D}, \quad V \in \mathbb{R}_{\text {sym },+}^{D \times D}
$$

- In 1D, this is a univariate normal and reduces to the usual normal
$$
\operatorname{Normal}_{1}(\mu, V) \equiv \operatorname{Normal}(\mu, V) \quad \mu \in \mathbb{R}^{1} \equiv \mathbb{R}, \quad V \in \mathbb{R}_{\text {sym },+}^{1 \times 1} \equiv(0, \infty)
$$
- In 2D, this is a bivariate normal
$$
\operatorname{Normal}_{2}(\mu, V) \quad \mu \in \mathbb{R}^{2}, \quad V \in \mathbb{R}_{\text {sym },+}^{2 \times 2}
$$
This is often parametrized by
$$
\mu=\binom{\mu_{1}}{\mu_{2}}, \quad V=\left[\begin{array}{cc}
v_{1} & \rho \sqrt{v_{1} v_{2}} \\
\rho \sqrt{v_{1} v_{2}} & v_{2}
\end{array}\right]=\underbrace{\left[\begin{array}{cc}
\sqrt{v_{1}} & 0 \\
0 & \sqrt{v_{2}}
\end{array}\right]}_{\substack{\text { diagonal with } \\
\text { scales }}} \underbrace{\left[\begin{array}{cc}
1 & \rho \\
\rho & 1
\end{array}\right]}_{\substack{\text { square with } \\
\text { correlations }}} \underbrace{\left[\begin{array}{cc}
\sqrt{v_{1}} & 0 \\
0 & \sqrt{v_{2}}
\end{array}\right]}_{\substack{\text { diagonal with } \\
\text { scales }}}
$$
for $\mu_{1}, \mu_{2} \in \mathbb{R}$ and $v_{1}, v_{2} \in(0, \infty)$ and $\rho \in(-1,+1)$

## Simulation

To generate a multivariate normal variate

$$
w \sim \operatorname{Normal}_{D}(\mu, V)
$$

- First, find a square-root $L$ such that
$$
L L^{t}=V
$$
- Then, generate standard normal variates
$$
\zeta_{d} \sim \operatorname{Normal}(0,1), \quad d=1, \ldots, D
$$
- Finally, transform
$$
w=\mu+L \zeta, \quad \zeta=\left(\begin{array}{c}
\zeta_{1} \\
\vdots \\
\zeta_{D}
\end{array}\right)
$$

The algorithm works because of the de-whitening property

$$
\left.\begin{array}{rl}
\zeta & \sim \operatorname{Normal}_{K}(0, I) \\
w & =\mu+L \zeta
\end{array}\right\} \Rightarrow w \sim \operatorname{Normal}\left(\mu, L L^{t}\right)
$$

for any $L \in \mathbb{R}^{D \times K}$

In this algorithm, we have many choices

- dimension $K$...clear-cut decision $K \geq D$
- square-root $L$...not a clear-cut decision

## Transformation properties

De-whitening property

$$
\left.\begin{array}{c}
\zeta \sim \operatorname{Normal}_{K}(0, l) \\
w=\mu+L \zeta
\end{array}\right\} \Rightarrow w \sim \operatorname{Normal}_{D}\left(\mu, L L^{t}\right)
$$

Whitening property

$$
\left.\begin{array}{l}
x \sim \operatorname{Normal}_{D}\left(\mu, L L^{t}\right) \\
y=L^{-1}(x-\mu)
\end{array}\right\} \Rightarrow y \sim \operatorname{Normal}_{D}(0, I)
$$

General transformation property

$$
\left.\begin{array}{l}
x \sim \operatorname{Normal}_{K}(m, V) \\
y=a+B x
\end{array}\right\} \Longrightarrow y \sim \operatorname{Normal}_{D}\left(a+B m, B V B^{t}\right)
$$

Here, the dimensions are

$$
m \in \mathbb{R}^{K} \quad V \in \mathbb{R}^{K \times K} \quad a \in \mathbb{R}^{D \times 1} \quad B \in \mathbb{R}^{D \times K}
$$

## Other properties

Addition property

$$
\left.\begin{array}{rl}
x_{1} & \sim \operatorname{Normal}_{D}\left(m_{1}, V_{1}\right) \\
x_{2} & \sim \operatorname{Normal}_{D}\left(m_{2}, V_{2}\right) \\
y & =x_{1}+x_{2}
\end{array}\right\} \Longrightarrow y \sim \operatorname{Normal}_{D}\left(m_{1}+m_{2}, V_{1}+V_{2}\right)
$$

Magnitude properties

$$
\begin{aligned}
& x \sim \operatorname{Normal}_{D}(0, I) \\
& \left.\begin{array}{l}
y=\|x\|_{2}^{2} \\
x \sim \operatorname{Normal}_{D}(0, I) \\
z=\|x\|_{2}
\end{array}\right\} \Longrightarrow y \sim \chi_{D}^{2} \\
& \Longrightarrow z \sim \chi_{D}
\end{aligned}
$$

here $\|\cdot\|_{2}$ is the Euclidean norm on $\mathbb{R}^{D}$

## Covariance factorizations

A covariance matrix $V \in \mathbb{R}_{\text {sym },+}^{D \times D}$ attains three important decompositions:

- Lower Cholesky decomposition ...in Matlab this is L = chol (V, 'lower') ; Our matrix is factorized like this ...runs in $\approx \frac{1}{3} D^{3}$ flops
$$
V=L L^{t}
$$
where $L \in \mathbb{R}^{D \times D}$ is lower triangular
- Eigen-decomposition ...in Matlab this is $[\mathrm{U}, \mathrm{S}]=\operatorname{eig}(\mathrm{V})$; Our matrix is factorized like this ...runs in $\approx 9 D^{3}$ flops
$$
V=U S U^{t}
$$
where $S \in \mathbb{R}^{D \times D}$ is diagonal and $U \in \mathbb{R}^{D \times D}$ is orthogonal
- Singular-value decomposition ...in Matlab this is $[\mathrm{W}, \mathrm{S}, \sim]=\operatorname{svd}(\mathrm{V})$; Our matrix is factorized like this ...runs in $\approx 22 D^{3}$ flops
$$
V=W S W^{t}
$$
where $S \in \mathbb{R}^{D \times D}$ is diagonal and $W \in \mathbb{R}^{D \times D}$ is orthogonal

## Covariance square-roots

We consider a covariance matrix $V \in \mathbb{R}_{\text {sym },+}^{D \times D}$ and its three important decompositions:

Lower Cholesky decomposition

$$
V=L L^{t}
$$

we have our square-root directly

Eigen-decomposition

$$
V=U S U^{t}
$$

we derive our square-root by

$$
L=U \sqrt{S}
$$

Singular-value decomposition

$$
V=W S W^{t}
$$

we derive our square-root by

$$
L=W \sqrt{S}
$$

This method:

- is little expensive
- usually fails

This method:

- is moderately expensive
- often fails

This method:

- is very expensive
- never fails

## Bayesian considerations

In BO, we will consider multivariate normals in this form

$$
\begin{aligned}
m & \sim \operatorname{Normal}_{D}(M, C) \\
w \mid m & \sim \operatorname{Normal}_{K}(a+B m, V)
\end{aligned}
$$

This is a Bayesian model which is conjugate
The posterior is

$$
m \mid w \sim \operatorname{Normal}_{D}\left(M^{\prime}, C^{\prime}\right)
$$

and the hyper-parameters are

$$
\begin{aligned}
C^{\prime} & =\left(C^{-1}+B^{t} V^{-1} B\right)^{-1} \\
M^{\prime} & =C^{\prime}\left(C^{-1} M+B^{t} V^{-1}(w-a)\right)
\end{aligned}
$$


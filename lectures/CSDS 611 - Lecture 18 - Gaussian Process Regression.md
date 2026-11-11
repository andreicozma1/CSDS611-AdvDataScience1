## Gaussian processes regression

- Formulation
- GP regression
- Squared exponential kernel

## GP regression

We have data $\left\{\left(x_{n}^{\sharp}, y_{n}^{\sharp}, \epsilon_{n}^{\sharp}\right)\right\}_{n=1}^{N^{\sharp}} \subset \mathbb{X} \times \mathbb{R} \times \mathbb{R}$ and seek an unknown function

$$
f: \mathbb{X} \mapsto \mathbb{R}
$$

Our regression model consists of

$$
\begin{aligned}
f & \sim \operatorname{GP}_{\mathbb{X}}(m, v) \\
y_{n}^{\sharp} \mid f & \sim \text { Normal }\left(f\left(x_{n}^{\sharp}\right),\left(\epsilon_{n}^{\sharp}\right)^{2}\right), \quad n=1, \ldots, N^{\sharp}
\end{aligned}
$$

Our model's "hyper-parameters" consist of

- a mean
…this is a function
$$
m: \mathbb{X} \mapsto \mathbb{R}
$$
- a symmetric positive semi-definite kernel
...this is also a function
$$
v: \mathbb{X} \times \mathbb{X} \mapsto \mathbb{R}
$$

## GP posterior

Our regression model consists of

$$
\begin{aligned}
f & \sim \operatorname{GP}_{\mathbb{X}}(m, v) \\
y_{n}^{\sharp} \mid f & \sim \operatorname{Normal}\left(f\left(x_{n}^{\sharp}\right),\left(\epsilon_{n}^{\sharp}\right)^{2}\right),
\end{aligned}
$$

$$
n=1, \ldots, N^{\sharp}
$$

- To obtain predictions at some $x^{\star} \in \mathbb{X}$
...we discretize the prior on $\left\{x_{n}^{\sharp}\right\}_{n=1}^{N^{\sharp}} \cup\left\{x^{\star}\right\}$
$$
\mathbb{X}^{N^{\sharp}+1} \ni\left(\begin{array}{c}
x_{1}^{\sharp} \\
x_{2}^{\sharp} \\
\vdots \\
x_{N^{\sharp}}^{\sharp} \\
x^{\sharp}
\end{array}\right) \equiv\binom{x^{\sharp}}{x^{\star}} \in \mathbb{X}^{N^{\sharp}} \oplus \mathbb{X}^{1}
$$
...and investigate the statistics of
$$
\mathbb{R}^{N^{\sharp}+1} \ni\left(\begin{array}{c}
f_{1}^{\sharp} \\
f_{2}^{\sharp} \\
\vdots \\
f_{N^{\sharp}}^{\sharp} \\
f^{\star}
\end{array}\right) \equiv\binom{f^{\sharp}}{f^{\star}} \in \mathbb{R}^{N^{\sharp}} \oplus \mathbb{R}^{1}
$$

## GP posterior

Our original regression model consists of

$$
\begin{aligned}
f & \sim \operatorname{GP}_{\mathbb{X}}(m, v) \\
y_{n}^{\sharp} \mid f & \sim \text { Normal }\left(f\left(x_{n}\right), \epsilon_{n}^{2}\right), \quad n=1, \ldots, N^{\sharp}
\end{aligned}
$$

Our discretized regression model takes the form

$$
\begin{aligned}
& \binom{f^{\sharp}}{f^{\star}} \sim \operatorname{Normal}_{N \sharp+1}\left(\binom{m^{\sharp}}{m^{\star}},\left[\begin{array}{cc}
V^{\sharp \sharp} & V^{\sharp \star} \\
V^{\star \sharp} & V^{\star \star}
\end{array}\right]\right) \\
& Y^{\sharp} \mid f^{\sharp} \sim \operatorname{Normal}_{N \sharp}\left(f^{\sharp}, P^{\sharp \sharp}\right)
\end{aligned}
$$

Our discretized regression model decomposes like this

$$
\begin{aligned}
& \quad f^{\sharp} \sim \operatorname{Normal}_{N \sharp}\left(m^{\sharp}, V^{\sharp \sharp}\right) \\
& f^{\star} \mid f^{\sharp} \sim \operatorname{Normal}_{1}\left(m^{\star}+V^{\star \sharp}\left(V^{\sharp \sharp}\right)^{-1}\left(f^{\sharp}-m^{\sharp}\right), V^{\star \star}-V^{\star \sharp}\left(V^{\sharp \sharp}\right)^{-1} V^{\sharp \star}\right) \\
& Y^{\sharp} \mid f^{\sharp} \sim \operatorname{Normal}_{N \sharp}\left(f^{\sharp}, P^{\sharp \sharp}\right)
\end{aligned}
$$

## GP posterior

Our discretized regression model decomposes like this

$$
\begin{aligned}
& f^{\sharp} \sim \operatorname{Normal}_{N \sharp}\left(m^{\sharp}, V^{\sharp \sharp}\right) \\
& f^{\star} \mid f^{\sharp} \sim \operatorname{Normal}_{1}\left(m^{\star}+V^{\star \sharp}\left(V^{\sharp \sharp}\right)^{-1}\left(f^{\sharp}-m^{\sharp}\right), V^{\star \star}-V^{\star \sharp}\left(V^{\sharp \sharp}\right)^{-1} V^{\sharp \star}\right) \\
& Y^{\sharp} \mid f^{\sharp} \sim \operatorname{Normal}_{N}\left(f^{\sharp}, P^{\sharp \sharp}\right)
\end{aligned}
$$

Our decomposed discretized regression model recomposes like this

$$
\begin{aligned}
& f^{\sharp} \sim \operatorname{Normal}_{N \sharp}\left(m^{\sharp}, V^{\sharp \sharp}\right) \\
& \binom{f^{\star}}{Y^{\sharp}} \left\lvert\, f^{\sharp} \sim \operatorname{Normal}_{1+N}\left(\binom{m^{\star}+V^{\star \sharp}\left(V^{\sharp \sharp}\right)^{-1}\left(f^{\sharp}-m^{\sharp}\right)}{f^{\sharp}},\left[\begin{array}{cc}
V^{\star \star}-V^{\star \sharp}\left(V^{\sharp \sharp}\right)^{-1} V^{\sharp \star} & 0^{\star \sharp} \\
0^{\star \sharp} & P^{\sharp \sharp}
\end{array}\right]\right)\right.
\end{aligned}
$$

## GP posterior

Our decomposed discretized regression model recomposes like this

$$
\begin{aligned}
& f^{\sharp} \sim \operatorname{Normal}_{N \sharp}\left(m^{\sharp}, V^{\sharp \sharp}\right) \\
& \binom{f^{\star}}{Y^{\sharp}} \left\lvert\, f^{\sharp} \sim \operatorname{Normal}_{1+N^{\sharp}}\left(\binom{m^{\star}+V^{\star \sharp}\left(V^{\sharp \sharp}\right)^{-1}\left(f^{\sharp}-m^{\sharp}\right)}{f^{\sharp}},\left[\begin{array}{cc}
V^{\star \star}-V^{\star \sharp}\left(V^{\sharp \sharp}\right)^{-1} V^{\sharp \star} & 0^{\star \sharp} \\
0^{\star \sharp} & P^{\sharp \sharp}
\end{array}\right]\right)\right.
\end{aligned}
$$

Our recomposed discretized regression model marginalizes like this

$$
\binom{f^{\star}}{Y^{\#}} \sim \operatorname{Normal}_{1+N \sharp}\left(\binom{m^{\star}}{m^{\#}},\left[\begin{array}{cc}
V^{\star \star} & V^{\star \sharp} \\
V^{\star \sharp} & P^{\# \#}+V^{\# \#}
\end{array}\right]\right)
$$

Our marginalized recomposed discretized regression model conditions like this

$$
f^{\star} \mid Y^{\sharp} \sim \operatorname{Normal}_{1}\left(m^{\star}+V^{\star \sharp}\left(P^{\sharp \sharp}+V^{\sharp \sharp}\right)^{-1}\left(Y^{\sharp}-m^{\sharp}\right), V^{\star \star}-V^{\star \sharp}\left(P^{\sharp \sharp}+V^{\sharp \sharp}\right)^{-1} V^{\sharp \star}\right)
$$

## GP posterior

We have data $\left\{\left(x_{n}^{\sharp}, y_{n}^{\sharp}, \epsilon_{n}^{\sharp}\right)\right\}_{n=1}^{N^{\sharp}} \subset \mathbb{X} \times \mathbb{R} \times \mathbb{R}$ and seek an unknown function

$$
f: \mathbb{X} \mapsto \mathbb{R}
$$

- Our regression model consists of
$$
\begin{aligned}
f & \sim \operatorname{GP}_{\mathbb{X}}(m, v) \\
y_{n}^{\sharp} \mid f & \sim \operatorname{Normal}\left(f\left(x_{n}^{\sharp}\right),\left(\epsilon_{n}^{\sharp}\right)^{2}\right), \quad n=1, \ldots, N^{\sharp}
\end{aligned}
$$
- To obtain predictions at some $x^{\star} \in \mathbb{X}$, we apply the predictive
$$
\begin{aligned}
f^{\star} \mid Y^{\#} & \sim \operatorname{Normal}_{1}\left(\mu^{\star},\left(\sigma^{\star}\right)^{2}\right) & f^{\star} & \equiv f\left(x^{\star}\right) \\
\mu^{\star} & =m^{\star}+V^{\star \sharp}\left(P^{\# \#}+V^{\# \#}\right)^{-1}\left(Y^{\#}-m^{\#}\right) & \mu^{\star} & \equiv \mu\left(x^{\star}\right) \\
\sigma^{\star} & =\sqrt{V^{\star \star}-V^{\star \sharp}\left(P^{\# \#}+V^{\# \#}\right)^{-1} V^{\sharp \star}} & \sigma^{\star} & \equiv \sigma\left(x^{\star}\right)
\end{aligned}
$$

## Example

![](https://cdn.mathpix.com/cropped/a417adf9-9ef4-467f-8f94-9279b4717b67-08.jpg?height=645&width=1229&top_left_y=129&top_left_x=165)
We have scalar inputs $\mathbb{X}=\mathbb{R}$ and $N^{\sharp}=7$ points with $m(x)=0$ and $v\left(x^{\prime}, x^{\prime \prime}\right)=\exp \left(-2\left(x^{\prime}-x^{\prime \prime}\right)^{2}\right)$

## Example

![](https://cdn.mathpix.com/cropped/a417adf9-9ef4-467f-8f94-9279b4717b67-09.jpg?height=579&width=1381&top_left_y=131&top_left_x=94)
We have scalar inputs $\mathbb{X}=\mathbb{R}$ and $N^{\sharp}=7$ points with $m(x)=0$ and $v\left(x^{\prime}, x^{\prime \prime}\right)=\exp \left(-2\left(x^{\prime}-x^{\prime \prime}\right)^{2}\right)$

## The squared exponential kernel

The square exponential kernel is given by $\quad$...this is symmetric and positive semi-definite $v: \mathbb{R} \times \mathbb{R} \mapsto \mathbb{R}$

$$
v\left(x^{\prime}, x^{\prime \prime}\right)=\sigma^{2} \exp \left(-\frac{1}{2}\left(\frac{x^{\prime}-x^{\prime \prime}}{\ell}\right)^{2}\right) \quad x^{\prime}, x^{\prime \prime} \in \mathbb{R}
$$

The kernel parameters consist of a strength $\sigma$ and a scale $\ell$
We consider a Gaussian process
...for some mean $m: \mathbb{R} \mapsto \mathbb{R}$

$$
f \sim \mathrm{GP}_{\mathbb{R}}(m, v)
$$

and two inputs $x^{\prime}, x^{\prime \prime} \in \mathbb{R}$
Our prior is

$$
\binom{f\left(x^{\prime}\right)}{f\left(x^{\prime \prime}\right)} \sim \operatorname{Normal}_{2}\left(\binom{m\left(x^{\prime}\right)}{m\left(x^{\prime \prime}\right)},\left[\begin{array}{cc}
v\left(x^{\prime}, x^{\prime}\right) & v\left(x^{\prime}, x^{\prime \prime}\right) \\
v\left(x^{\prime \prime}, x^{\prime}\right) & \left(x^{\prime \prime}, x^{\prime \prime}\right)
\end{array}\right]\right)
$$

## The squared exponential kernel

The square exponential kernel is

$$
v\left(x^{\prime}, x^{\prime \prime}\right)=\sigma^{2} \exp \left(-\frac{1}{2}\left(\frac{x^{\prime}-x^{\prime \prime}}{\ell}\right)^{2}\right) \quad x^{\prime}, x^{\prime \prime} \in \mathbb{R}
$$

Our prior is

$$
\binom{f\left(x^{\prime}\right)}{f\left(x^{\prime \prime}\right)} \sim \operatorname{Normal}_{2}\left(\binom{m\left(x^{\prime}\right)}{m\left(x^{\prime \prime}\right)},\left[\begin{array}{cc}
v\left(x^{\prime}, x^{\prime}\right) & v\left(x^{\prime}, x^{\prime \prime}\right) \\
v\left(x^{\prime \prime}, x^{\prime}\right) & \left(x^{\prime \prime}, x^{\prime \prime}\right)
\end{array}\right]\right)
$$

Our correlation is given by
![](https://cdn.mathpix.com/cropped/a417adf9-9ef4-467f-8f94-9279b4717b67-11.jpg?height=324&width=354&top_left_y=166&top_left_x=1074)

$$
C\left(x^{\prime}, x^{\prime \prime}\right)=\frac{v\left(x^{\prime}, x^{\prime \prime}\right)}{\sqrt{v\left(x^{\prime}, x^{\prime}\right)} \sqrt{v\left(x^{\prime \prime}, x^{\prime \prime}\right)}}=\exp \left(-\frac{1}{2}\left(\frac{x^{\prime}-x^{\prime \prime}}{\ell}\right)^{2}\right)
$$

The limiting correlation is

$$
\begin{aligned}
& \left|\frac{x^{\prime}-x^{\prime \prime}}{\ell}\right| \gg 1 \\
& C\left(x^{\prime}, x^{\prime \prime}\right) \rightarrow 0
\end{aligned}
$$

$$
\begin{aligned}
& \left|\frac{x^{\prime}-x^{\prime \prime}}{\ell}\right| \ll 1 \\
& C\left(x^{\prime}, x^{\prime \prime}\right) \rightarrow 1
\end{aligned}
$$

![](https://cdn.mathpix.com/cropped/a417adf9-9ef4-467f-8f94-9279b4717b67-11.jpg?height=326&width=321&top_left_y=541&top_left_x=1091)

## The squared exponential kernel

The square exponential kernel is

$$
v\left(x^{\prime}, x^{\prime \prime}\right)=\sigma^{2} \exp \left(-\frac{1}{2}\left(\frac{x^{\prime}-x^{\prime \prime}}{\ell}\right)^{2}\right) \quad x^{\prime}, x^{\prime \prime} \in \mathbb{R}
$$

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

The limiting correlation is

$$
\begin{aligned}
& \left|\frac{x^{\prime}-x^{\prime \prime}}{\ell}\right| \gg 1 \\
& C\left(x^{\prime}, x^{\prime \prime}\right) \rightarrow 0
\end{aligned}
$$

$$
\begin{aligned}
& \left|\frac{x^{\prime}-x^{\prime \prime}}{\ell}\right| \ll 1 \\
& C\left(x^{\prime}, x^{\prime \prime}\right) \rightarrow 1
\end{aligned}
$$

![](https://cdn.mathpix.com/cropped/a417adf9-9ef4-467f-8f94-9279b4717b67-12.jpg?height=309&width=304&top_left_y=540&top_left_x=1099)


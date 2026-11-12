# CSDS 611 transcription glossary

This is the Scribe v3 keyterm list for the Fall 2026 lecture recordings. It draws from all 18 [Markdown slide decks](README.md#slides-by-lecture), lectures 02–19, including their equations and examples. Each bullet under **Keyterms** is one literal entry to send, in the order shown.

Use the current course-wide list for each recording because the [recording-to-deck mapping](README.md#recordings-by-date) is still unverified. The glossary covers slide vocabulary, plausible spoken forms of notation, and terms added after reviewing transcripts. The dated additions below preserve the order of earlier versions. Each transcript identifies the version it used by term count and hash.

## Keyterms

### Bayesian optimization and probability (02–04)

- acquisition function
- Bayesian optimization
- BO
- Newton-Raphson
- Nelder-Mead
- stochastic gradient descent
- probabilistic surrogate
- objective function
- optimization policy
- query point
- search space
- global optimum
- global optimizer
- termination criterion
- exploration versus exploitation
- surrogate model
- nonparametric model
- stochastic process
- quantity of interest
- probability mass function
- probability density function
- probability measure
- joint distribution
- marginal distribution
- conditional distribution
- Bayes' theorem
- Bayes' rule
- Bayesian updating
- prior distribution
- likelihood function
- posterior distribution
- normalizing constant
- marginalization
- probabilistic inference
- inverse problem
- data assimilation
- active learning
- experiment design
- supervised learning
- unsupervised learning
- PMF
- PDF

### Random variables and Gaussian models (05–08)

- Bernoulli
- binomial distribution
- Poisson
- geometric distribution
- uniform distribution
- beta distribution
- von Mises
- exponential distribution
- gamma distribution
- gamma function
- Weibull
- beta-prime
- chi distribution
- chi-squared distribution
- Student's t distribution
- degrees of freedom
- memorylessness
- heavy tails
- Euclidean norm
- Gaussian random variable
- Gaussian random vector
- univariate normal
- bivariate normal
- multivariate normal
- standard normal variate
- independent normal variates
- cumulative distribution function
- CDF
- quantile function
- error function
- erf
- inverse error function
- credible set
- credible interval
- credible ellipse
- standard deviation
- precision parameter
- inverse variance
- gamma shape parameter
- gamma scale parameter
- normal-gamma model
- covariance matrix
- covariance square root
- symmetric positive definite
- Cholesky decomposition
- lower Cholesky factor
- eigendecomposition
- singular value decomposition
- SVD
- orthogonal matrix
- lower triangular matrix
- matrix transpose
- matrix inverse
- matrix determinant
- inner product
- MATLAB
- whitening transformation
- de-whitening
- conditional independence
- block diagonal matrix
- covariance partition
- conditional mean
- conditional covariance
- sequential update

### Hypothesis tests and decisions (09–12)

- categorical distribution
- exchangeability
- spam detection
- spam versus ham
- null hypothesis
- alternative hypothesis
- binary hypothesis test
- Bayes factor
- prior odds
- posterior odds
- odds statistic
- likelihood ratio
- marginal likelihood
- marginal posterior
- maximum a posteriori
- MAP estimate
- maximum likelihood
- ML criterion
- exponential family
- natural parameter
- log partition function
- conjugate prior
- conjugacy
- hyperparameter
- sufficient statistic
- pseudo-measurement
- Gamma-Poisson model
- Poisson likelihood
- gamma prior
- signal detection
- intensity-dependent noise
- noisy channel
- Bayesian decision theory
- Bayes action
- Bayes estimator
- posterior expected loss
- decision rule
- state space
- action space
- point estimation
- posterior mean
- posterior median
- posterior mode
- squared deviation loss
- absolute deviation loss
- zero-one loss
- clinical patient management
- diagnostic outcome
- missing diagnostic information
- recommendation system
- noninformative prior
- probability simplex
- Dirichlet
- Dirichlet prior
- preferential reaction
- Ioannis
- The Manchurian Candidate
- Bride of Chucky
- Se7en
- Blues Brothers 2000
- The Fugitive
- The Conjuring
- Good Will Hunting
- Die Hard with a Vengeance
- Halloween: Resurrection
- The Departed
- John Wick

### Regression, model selection, and prediction (13–16)

- ill-posed problem
- basis function
- feature expansion
- polynomial basis
- design matrix
- ordinary least squares
- OLS
- normal equations
- Moore-Penrose pseudoinverse
- Gram matrix
- ridge regression
- ridge regularization
- ridge normal equations
- Bayesian linear regression
- coefficient vector
- nested models
- model selection
- model uncertainty
- model prior
- model-specific hyperparameters
- posterior model probability
- model evidence
- predictive distribution
- posterior predictive distribution
- joint predictive distribution
- Bayesian model averaging
- posterior mixture
- posterior mixture prediction
- kernel regression
- discretization
- covariance function
- positive semidefinite kernel

### Gaussian process regression and kernels (17–19)

- Gaussian process
- GP regression
- Gaussian process prior
- Gaussian process posterior
- mean function
- covariance kernel
- latent function
- finite-dimensional distribution
- finite-dimensional marginal
- observation noise
- noise covariance
- noise variance
- predictive mean
- predictive variance
- predictive covariance
- cross-covariance
- squared exponential kernel
- white noise kernel
- constant kernel
- exponential sine squared kernel
- periodic kernel
- diffusion kernel
- anchored diffusion kernel
- diffusivity
- length scale
- kernel strength
- Cholesky update
- triangular solve
- Schur complement
- block covariance matrix
- forward substitution
- back substitution
- cubic time
- quadratic time

### Spoken notation

These entries are plausible readings of notation in the slides. The speaker's preferred readings still need to be checked against the audio.

- mu
- alpha
- beta
- gamma
- lambda
- pi
- chi
- sigma squared
- tau
- theta
- epsilon
- zeta
- eta
- kappa
- xi
- nu
- rho
- phi
- psi
- omega
- theta hat
- mu star
- f star
- f sharp
- epsilon sharp
- x prime
- x double prime
- x star
- x sharp
- y sharp
- V sharp sharp
- V star sharp
- H zero
- H naught
- H sub A
- empty set
- two pi
- raised to the power
- proportional to
- distributed as
- conditioned on
- L transpose
- L inverse transpose
- big O of N cubed
- argmin
- argmax

### Additions from the August 20 transcript

- queries

### Additions from the August 25 transcript

- capital J
- indicator function

### Additions from the September 1 transcript

- von Mises distribution
- modified Bessel function
- rand
- conjugate

### Additions from the September 10 transcript

- normal distribution

### Additions from the September 29 transcript

- Tikhonov regularization

### Additions from the October 8 transcript

- high-dimensional

### Additions from the October 13 transcript

- Mercer's theorem
- Woodbury's identity

### Additions from the October 27 transcript

- ell

### Additions from the November 10 transcript

- UCB
- LCB

## Terms to check against the audio

- **Bayes factor and posterior odds.** The Bayes factor multiplies the prior odds to give the posterior odds. See [lecture 09](<CSDS 611 - Lecture 09 - Bayesian Hypothesis Tests.md>).
- **Precision, variance, and standard deviation.** In the scalar Gaussian model, precision is inverse variance. Check what the speaker says before converting it to notation. See [lecture 06](<CSDS 611 - Lecture 06 - Gaussian Random Scalars.md>).
- **Positive definite and positive semidefinite.** A covariance matrix being factored and a kernel required to give valid covariance matrices appear in different contexts. See [lectures 07](<CSDS 611 - Lecture 07 - Gaussian Vectors - Transformations and Covariance Factors.md>) and [16](<CSDS 611 - Lecture 16 - Kernel Regression.md>).
- **Sharp, star, and prime.** Listen for the suffixes on variables. In GP regression, the slides use sharp for observed inputs and star for prediction locations. See [lecture 18](<CSDS 611 - Lecture 18 - Gaussian Process Regression.md>).
- **Ioannis and Se7en.** Use the printed spelling when discussing the recommendation example. The text conversion sometimes reads `Ioannis` as `loannis`. See [lecture 12 PDF](<CSDS 611 - Lecture 12 - Applied Decision Problems.pdf>).

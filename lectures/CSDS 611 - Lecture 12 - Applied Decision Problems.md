## Applied decision problems

- Examples
- Decisions under missing information
- Recommendation systems

## Decision and Bayesian decision problems

A decision problem involves three spaces

- a state-space $\mathcal{Q}$...states live here, $q \in \mathcal{Q}$
- a data-space $\mathcal{W} \quad \ldots$ data live here, $w \in \mathcal{W}$
- an action-space $\mathcal{A} \quad \ldots$ actions live here, $\alpha \in \mathcal{A}$

A Bayesian decision problem consists of

- a Bayesian model
$$
\begin{aligned}
q & \sim Q \\
w \mid q & \sim P_{q}
\end{aligned}
$$
- a loss function
$$
L: \mathcal{A} \times \mathcal{Q} \mapsto(-\infty,+\infty)
$$

The posterior expected loss is

$$
\rho(\alpha, w)=\underbrace{\mathbb{E}_{q \mid w} L(\alpha, q)}_{\begin{array}{c}
\text { posterior } \\
\text { expectation }
\end{array}}
$$

The Bayes rule is

$$
D^{*}(w)=\operatorname{argmin}_{\alpha \in \mathcal{A}} \rho(\alpha, w)
$$

## Clinical patient management

A suspected patient shows ambiguous symptoms
Based on demographics and historical data, there is

- 20\% chance our patient has condition A
- 15\% chance our patient has condition B
- 65\% chance our patient has no condition
On a different facility, the patient ran one of two diagnostics:
- A costly test with no side effects This test identifies $C_{A}$ with 90\% success rate and $C_{B}$ with only 50\% success rate
- A costless test with severe side effects This test identifies both $C_{A}$ and $C_{B}$ with 85\% success rate

We lost record of which diagnostic the patient ran, but we maintain the diagnostic's outcome
Our goal is to come up with a treatment plan

## Clinical patient management

We form and solve a Bayesian decision problem

- Our problem's states are
$$
c \in\left\{C_{A}, C_{B}, C_{\emptyset}\right\}
$$
- Our problem's data are
$$
w \in\{A, B, \emptyset\}
$$
- Our problem's actions are
$$
t \in\left\{T_{A}, T_{B}, T_{\emptyset}\right\}
$$
...patient's actual condition
...diagnostic's outcome
...treatment plans

## Clinical patient management

Our Bayesian model consists of

$$
\begin{aligned}
c & \sim \text { Categorical }_{C_{A}, C_{B}, C_{\emptyset}}(0.20,0.15,0.65) \\
d & \sim \text { Categorical }_{D_{1}, D_{2}}\left(\psi_{D_{1}}, \psi_{D_{2}}\right) \\
w \mid c, d & \sim \text { Categorical }_{A, B, \emptyset}\left(f_{d}(c)\right)
\end{aligned}
$$

- To model our diagnostics, we use
$$
\begin{aligned}
& f_{D_{1}}\left(C_{A}\right)=(0.90,0.00,0.10) \\
& f_{D_{1}}\left(C_{B}\right)=(0.00,0.50,0.50) \\
& f_{D_{1}}\left(C_{\emptyset}\right)=(0.00,0.00,1.00)
\end{aligned}
$$
$$
\begin{aligned}
& f_{D_{2}}\left(C_{A}\right)=(0.85,0.00,0.15) \\
& f_{D_{2}}\left(C_{B}\right)=(0.00,0.85,0.15) \\
& f_{D_{2}}\left(C_{\emptyset}\right)=(0.00,0.00,1.00)
\end{aligned}
$$

## Clinical patient management

Our Bayesian model consists of

$$
\begin{aligned}
c & \sim \text { Categorical }_{C_{A}, C_{B}, C_{\emptyset}}(0.20,0.15,0.65) \\
d & \sim \text { Categorical }_{D_{1}, D_{2}}\left(\psi_{D_{1}}, \psi_{D_{2}}\right) \\
w \mid c, d & \sim \text { Categorical }_{A, B, \emptyset}\left(f_{d}(c)\right)
\end{aligned}
$$

- Our posterior is
$$
\begin{aligned}
p(c \mid w)=\sum_{d} p(c, d \mid w) & \propto \sum_{d} p(w \mid c, d) p(c, d) \\
& =\sum_{d} p(w \mid c, d) p(c) p(d) \\
& =p(c) \sum_{d} p(w \mid c, d) p(d) \\
& =p(c)\left(p\left(w \mid c, d=D_{1}\right) p\left(d=D_{1}\right)+p\left(w \mid c, d=D_{2}\right) p\left(d=D_{2}\right)\right) \\
& =\operatorname{Cat}(c ; \cdots)\left(\operatorname{Cat}\left(w ; f_{D_{1}}(c)\right) \psi_{D_{1}}+\operatorname{Cat}\left(w ; f_{D_{2}}(c)\right) \psi_{D_{2}}\right) \\
& =\operatorname{Cat}(c ; \cdots) \operatorname{Cat}\left(w ; \psi_{D_{1}} f_{D_{1}}(c)+\psi_{D_{2}} f_{D_{2}}(c)\right)=\operatorname{Cat}(c ; \cdots)
\end{aligned}
$$

## Clinical patient management

Our loss function is

$$
L(t, c)= \begin{cases}0, & c=C_{A}, t=T_{A} \\ 0.8, & c=C_{B}, t=T_{A} \\ 1.0, & c=C_{\emptyset}, t=T_{A} \\ 0.6, & c=C_{A}, t=T_{B} \\ 0, & c=C_{B}, t=T_{B} \\ 0.9, & c=C_{\emptyset}, t=T_{B} \\ 0.3, & c=C_{A}, t=T_{\emptyset} \\ 0.4, & c=C_{B}, t=T_{\emptyset} \\ 0, & c=C_{\emptyset}, t=T_{\emptyset}\end{cases}
$$

## A recommendation system

We own rights to a movie database with five genres ...we ignore multi-genre movies and movie attributes 'horror', 'thriller', 'action', 'drama', 'comedy'

Our platform streams movies and records reactions ...we ignore time-stamps and viewer attributes Q, B, O, 0

We aim to develop an automated recommendation algorithm
...good recommendations will make viewers happy and maintain our subscription …bad recommendations will make viewers unhappy and leave our subscription

We will form and solve a decision problem

## A recommendation system

We consider a single viewer. Our viewer has engaged in past viewing rounds which we index with

$$
n=1, \ldots, N
$$

- Our problem's states are the viewer's actual preferences ...encoded as a vector in the probability simplex
$$
\pi=\left(\pi_{\text {'horror }}{ }^{\prime}, \pi_{\text {'thriller }}^{\prime}, \pi_{\text {'action' }}^{\prime}, \pi_{\text {'drama }}^{\prime}, \pi_{\text {'comedy }}^{\prime}\right) \in \mathbb{R}_{\text {prob }}^{5}
$$
- Our problem's data are the viewer's past movies and reactions ...encoded as two sequences
$$
\begin{aligned}
& \mu_{n} \in\{\text { 'horror', 'thriller', 'action', 'drama', 'comedy' }\} \\
& \omega_{n} \in\{\mathfrak{V}, \mathbb{B}, \mathcal{V}, \emptyset\}
\end{aligned}
$$
- Our problem's actions are the recommendations
$$
\alpha \in\{\text { 'horror', 'thriller', 'action', 'drama', 'comedy'\} }
$$
for the $(N+1)^{\text {th }}$ viewing round

## A recommendation system

Our Bayesian model consists of
$\pi \sim$ Dirichlet 'horror', 'thriller', 'action', 'drama', 'comedy' $\left(\gamma^{\prime}\right.$ 'horror',$\gamma^{\prime}$ thriller',$\gamma^{\prime}$ action',$\gamma^{\prime}$ drama',$\gamma^{\prime}$ comedy' $)$

$$
\mu_{n} \mid \pi \sim \text { Categorical }{ }_{\text {'horror', 'thriller', 'action', 'drama', 'comedy' }}(\pi),
$$

$$
n=1, \ldots, N
$$

$$
\omega_{n} \mid \mu_{n}, \pi \sim \text { Categorical }{ }_{\mathfrak{D}, \mathcal{B}, \mathcal{O}, \emptyset}\left(f_{\mathcal{Q}}^{\mu_{n}}(\pi), f_{\mathcal{B}}^{\mu_{n}}(\pi), f_{\circlearrowleft}^{\mu_{n}}(\pi), f_{\emptyset}^{\mu_{n}}(\pi)\right),
$$

$$
n=1, \ldots, N
$$

- To model non-informative priors, we use
$$
\gamma_{\text {'horror }}^{\prime}=\gamma_{\text {'thriller }}^{\prime}=\gamma_{\text {'action }}^{\prime}=\gamma_{\text {'drama }}^{\prime}=\gamma_{\text {'comedy }}^{\prime}=1
$$
- To model preferential reactions, we use
$$
\begin{aligned}
f_{\circlearrowleft}^{\mu}(\pi) & =\frac{6}{10}\left(1-\pi_{\mu}\right)+\frac{1}{10} \\
f_{0}^{\mu}(\pi) & =\frac{5}{10} \pi_{\mu}+\frac{1}{10} \\
f_{\circlearrowright}^{\mu}(\pi) & =\frac{1}{10} \pi_{\mu} \\
f_{\emptyset}^{\mu_{n}}(\pi) & =\frac{2}{10}
\end{aligned}
$$

## A recommendation system

Our loss function is

$$
L(\alpha, \pi)=1-\pi_{\alpha}
$$

this way:

- good recommendations agree with our viewer's preference ...high preference $\pi_{\alpha}$ and low loss $L(\alpha, \pi)$
- bad recommendations disagree with our viewer's preference ...low preference $\pi_{\alpha}$ and high loss $L(\alpha, \pi)$

Our loss assumes all genres are equally valuable/costful to our platform

Alternative losses

$$
L(\alpha, \pi)=\left(\max _{\alpha^{\prime}} R_{\alpha^{\prime}}\right)-R_{\alpha} \pi_{\alpha}
$$

$$
L(\alpha, \pi)=\left(\left(\max _{\alpha^{\prime}} R_{\alpha^{\prime}}\right)-R_{\alpha} \pi_{\alpha}\right)^{2}
$$

Assumes genres have unequal rewards/costs
Avoids over-saturation

## A recommendation system

- loannis engages with $N=11$ movies
Our posterior is given by
$$
\begin{aligned}
p\left(\pi \mid \mu_{1: N}, \omega_{1: N}\right) & \propto p\left(\mu_{1: N}, \omega_{1: N} \mid \pi\right) p(\pi) \\
& =p\left(\omega_{1: N} \mid \mu_{1: N}, \pi\right) \\
& \times p\left(\mu_{1: N} \mid \pi\right) p(\pi) \\
& =\left[\prod_{n=1}^{N} p\left(\omega_{n} \mid \mu_{1: N}, \pi\right)\right] \\
& \times\left[\prod_{n=1}^{N} p\left(\mu_{n} \mid \pi\right)\right] p(\pi) \\
& =\left[\prod_{n=1}^{N} \operatorname{Cat}\left(\omega_{n} ; f^{\mu_{n}}(\pi)\right)\right] \\
& \times \underbrace{\left[\prod_{n=1}^{N} \operatorname{Cat}\left(\mu_{n} ; \pi\right)\right] \operatorname{Dir}(\pi ; \gamma)}_{\propto \operatorname{Dir}\left(\pi ; \gamma^{\prime}\right)}
\end{aligned}
$$

| $n$ | $\mu_{n}$ | $\omega_{n}$ |  |
| :--- | :--- | :--- | :--- |
| 1 | 'comedy' | Q | Blues Brothers 2000 |
| 2 | 'thriller' | $\emptyset$ | The Fugitive |
| 3 | 'horror' | 3 | The Conjuring |
| 4 | 'drama' | Q | Good Will Hunting |
| 5 | 'action' | $\emptyset$ | Die Hard with a Vengeance |
| 6 | 'horror' | 3 | Halloween: Resurrection |
| 7 | 'thriller' | 3 | Se7en |
| 8 | 'drama' | $\emptyset$ | The Departed |
| 9 | 'horror' | 0 | Bride of Chucky |
| 10 | 'thriller' | 3 | The Manchurian Candidate |
| 11 | 'action' | Q | John Wick |

## A recommendation system

| - loannis engages with $N=11$ movies |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- |
| Our posterior is given by $p\left(\pi \mid \mu_{1: N}, \omega_{1: N}\right) \propto\left[\prod_{n=1}^{N} \operatorname{Cat}\left(\omega_{n} ; f^{\mu_{n}}(\pi)\right)\right] \operatorname{Dir}\left(\pi ; \gamma^{\prime}\right) \approx \operatorname{Dir}\left(\pi ; \gamma^{\prime \prime}\right)$ | $n$ | $\mu_{n}$ | $\omega_{n}$ |  |
|  | 1 | 'comedy' | Q | Blues Brothers 2000 |
|  | 2 | 'thriller' | $\emptyset$ | The Fugitive |
|  | 3 | 'horror' | 3 | The Conjuring |
|  | 4 | 'drama' | Q | Good Will Hunting |
| With posterior weights given by | 5 | 'action' | $\emptyset$ | Die Hard with a Vengeance |
| $\gamma_{\text {'horror }}^{\prime}=\gamma^{\prime}$ horror $^{\prime}+3$ | 6 | 'horror' | B | Halloween: Resurrection |
| $\gamma_{\text {'thriller' }}^{\prime}=\gamma_{\text {'thriller }}^{\prime}+3$ | 7 | 'thriller' | 3 | Se7en |
| $\gamma_{\text {'action' }}^{\prime}=\gamma_{\text {'action' }}^{\prime}+2$ | 8 | 'drama' | $\emptyset$ | The Departed |
| $\gamma_{\text {'drama }}^{\prime}=\gamma_{\text {'drama }}^{\prime}+2$ | 9 | 'horror' | 0 | Bride of Chucky |
| $\gamma_{\text {comedy }}^{\prime}=\gamma_{\text {'comedy }}^{\prime}+1$ | 10 | 'thriller' | 3 | The Manchurian Candidate |
|  | 11 | 'action' | Q | John Wick |

## A recommendation system

| - loannis engages with $N=11$ movies |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- |
| Our posterior is given by <br> $p\left(\pi \mid \mu_{1: N}, \omega_{1: N}\right) \approx \operatorname{Dir}\left(\pi ; \gamma^{\prime \prime}\right)$ | $n$ | $\mu_{n}$ | $\omega_{n}$ |  |
|  | 1 | 'comedy' | Q | Blues Brothers 2000 |
|  | 2 | 'thriller' | $\emptyset$ | The Fugitive |
| With posterior weights given by <br> $\gamma^{\prime \prime}$ horror $^{\prime}=8.7$ <br> $\gamma^{\prime \prime}{ }_{\text {thriller }}$ ' = 6.3 <br> $\gamma^{\prime \prime}{ }_{\text {action }}{ }^{\prime}=2.1$ <br> $\gamma^{\prime \prime}{ }_{\text {drama }}{ }^{\prime}=2.2$ <br> $\gamma^{\prime \prime}{ }_{\text {comedy }}^{\prime}=0.9$ | 3 | 'horror' | 3 | The Conjuring |
|  | 4 | 'drama' | Q | Good Will Hunting |
|  | 5 | 'action' | $\emptyset$ | Die Hard with a Vengeance |
|  | 6 | 'horror' | 3 | Halloween: Resurrection |
|  | 7 | 'thriller' | 3 | Se7en |
|  | 8 | 'drama' | $\emptyset$ | The Departed |
| Our expected posterior loss is | 9 | 'horror' | 0 | Bride of Chucky |
| $\rho(\alpha) \approx \int d \pi\left(1-\pi_{\alpha}\right) \operatorname{Dir}\left(\pi ; \gamma^{\prime \prime}\right)$ | 10 | 'thriller' | 3 | The Manchurian Candidate |
| $=1-\int d \pi \pi_{\alpha} \operatorname{Dir}\left(\pi ; \gamma^{\prime \prime}\right)=1-\frac{\gamma_{\alpha}^{\prime \prime}}{\sum_{\alpha^{\prime}} \gamma_{\alpha^{\prime}}^{\prime \prime}}$ | 11 | 'action' | Q | John Wick |


A recommendation system
| - loannis engages with $N=11$ movies |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- |
| Our posterior is given by $p\left(\pi \mid \mu_{1: N}, \omega_{1: N}\right) \approx \operatorname{Dir}\left(\pi ; \gamma^{\prime \prime}\right)$ | $n$ | $\mu_{n}$ | $\omega_{n}$ |  |
|  | 1 | 'comedy' | Q | Blues Brothers 2000 |
|  | 2 | 'thriller' | $\emptyset$ | The Fugitive |
| Our expected posterior losses are <br> $\rho($ 'horror' $) \approx 0.57$ <br> $\rho($ 'thriller' $) \approx 0.69$ <br> $\rho($ 'action' $) \approx 0.90$ <br> $\rho($ 'drama' $) \approx 0.89$ <br> $\rho($ 'comedy' $) \approx 0.96$ | 3 | 'horror' | 3 | The Conjuring |
|  | 4 | 'drama' | Q | Good Will Hunting |
|  | 5 | 'action' | $\emptyset$ | Die Hard with a Vengeance |
|  | 6 | 'horror' | 3 | Halloween: Resurrection |
|  | 7 | 'thriller' | B | Se7en |
|  | 8 | 'drama' | $\emptyset$ | The Departed |
| Our Bayes recommendation is <br> $\alpha^{*}=$ 'horror' | 9 | 'horror' | 0 | Bride of Chucky |
|  | 10 | 'thriller' | 3 | The Manchurian Candidate |
|  | 11 | 'action' | Q | John Wick |



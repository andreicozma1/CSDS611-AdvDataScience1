# Lower bounds on the Lotka–Volterra fit

For the instructor’s CSV, the strongest bound obtained for the continuous
Lotka–Volterra model is **249.53 SSE** over the full assignment rate box.
The best checked fit has an SSE of **495.69**, giving a gap of **246.16 SSE**
between the lower bound and the observed fit. Any rate vector must score
at least the lower bound, while the checked fit shows an attainable score.
[Checked fit](../benchmarks/2026-11-13/adaptive-phase-scan/README.md)

## Model and objective

The objective sums the squared prey and predator errors at all 27 CSV
timestamps. The model starts at $(x(0),y(0))=(2.11,1.35)$ with rates
$(a,b,c,d)=(\theta_1,\theta_2,\theta_3,\theta_4)$:

$$
\dot x=x(a-by), \qquad \dot y=y(dx-c).
$$

The inclusive assignment intervals are $[0.10,50]$, $[0.01,2]$,
$[0.10,5]$, and $[0.01,2]$, respectively. The bound applies to the
continuous ODE with these inputs. [Step 1 handout](../project_step_1.pdf) · [Assignment data](../LV_data.csv)

## Partitioning the sampling phase

Each positive non-equilibrium trajectory is periodic. Write $P$ for its period
and $\phi$ for the fractional part of $5000/P$. All observation times have the
form $t_i=5000n_i$ with integer $n_i$. The phase at $t_i$, measured in cycles
from the initial point, is the fractional part of $n_i\phi$.

Two sample phases can exchange their order only when
$(n_i-n_j)\phi$ is an integer. This includes crossings of phase zero by taking
$n_j=0$. Enumerating all such fractions gives **25,412 intervals** covering
$[0,1]$. The sample order is fixed inside each interval. At an endpoint, tied
phases have identical predictions and satisfy the weak ordering from either
side. The partition allows every fractional phase, which can include phases
outside the range attainable within the assignment box. [Phase partition and exact arithmetic](../benchmarks/2026-11-13/phase-rate-bounds/README.md#global-lower-bound)

## Relaxing the trajectory constraints

For each phase interval, enumerate the possible positions of the population
extrema between samples. Retain the following conditions on a single set of
predicted values.

| Condition | Restriction on the predictions |
| --- | --- |
| Monotonicity | Each species has an increasing arc and a decreasing arc. The extrema alternate as prey maximum, predator maximum, prey minimum, predator minimum. |
| Initial state | The point at time zero is fixed at $(2.11,1.35)$. Weak inequalities also cover constant equilibria. |
| Nullclines | Predator decreases when prey is below $c/d$, and prey increases when predator is below $a/b$. The assignment bounds imply $c/d\in[0.05,500]$ and $a/b\in[0.05,5000]$. |
| Convexity in time | Prey is convex on predator-decreasing arcs, and predator is convex on prey-increasing arcs. |

For example, $x''=x(a-by)^2-bx\dot y$ is nonnegative when $\dot y\le0$.
On such an arc, a prey prediction at an intermediate time is at most the
elapsed-time-weighted interpolation of two surrounding prey predictions.
The allowable weights are bounded over the phase interval and rounded
outward to preserve the inequality for every phase in the interval.
[Derivation of the restrictions](../benchmarks/2026-11-13/shared-orbit-bounds/README.md#constraints)

### Certifying a bound within an interval

The monotonicity pass uses **isotonic regression**, which minimizes the
squared error of a sequence constrained to increase or decrease. The joint
pass adds the nullcline and time inequalities to the same predicted values.
Write these inequalities as $Az\le b$, with the fixed initial values moved
to the right-hand side, and let $v$ be the observation vector. For any
$\lambda\ge0$, a lower bound on the relaxed SSE is

$$
2\lambda^{\mathsf T}(Av-b)-\|A^{\mathsf T}\lambda\|_2^2.
$$

This follows by adding $2\lambda^{\mathsf T}(Az-b)$ to the objective and
minimizing the resulting quadratic over unrestricted $z$. The added term is
nonpositive at every feasible $z$. The calculation searches for multipliers
numerically, evaluates their certificate with integer arithmetic, and
subtracts an allowance for rounding the observations to six decimal places.
Each valid multiplier gives a bound even if the search stops early.
The global bound is the minimum over turning-point assignments and phase
intervals. [Integer evaluation of the certificate](../benchmarks/2026-11-13/shared-orbit-bounds/joint_timing.py)

## Removing the prey RMSE cap

The original calculation used a prey RMSE cap of $r=2.447581572956998$ and
reached **247.960675934056** after 283 rational subdivisions. To extend this
bound to the full assignment box, consider fits whose prey RMSE exceeds $r$.
Their prey SSE exceeds $27r^2\approx161.7477$. In each original phase interval,
let $L_x$ and $L_y$ be the saved species-specific lower bounds before filtering
by the cap. The total SSE for a fit above the cap is at least

$$
\max(L_x,27r^2)+L_y.
$$

The minimum of this expression across all 25,412 intervals is approximately
**329.1899**. Therefore the lower bound for the full box is the smaller of
the two case bounds, **247.960675934056**. [Saved subdivisions](../benchmarks/2026-11-13/shared-orbit-bounds/subdivision.json) · [Saved species-specific bounds](../benchmarks/2026-11-13/phase-rate-bounds/bound.json)

## Tightening the bound to 249.53

The refinement recomputed the **287 phase intervals** in the subdivided
partition with existing bounds below 270. Higher-bound intervals kept their
certificates. The computation used an interpolation-weight grid of
$1/1024$ instead of $1/64$ and up to 72 multiplier sweeps instead of 12.
The recomputed relaxation allowed any prey RMSE. The larger of the saved
and new bounds was retained for the at-or-below-cap case. The above-cap
case kept its separate **329.1899** bound.

The recomputation raised the global floor to **249.510105835641**.
Splitting the weakest interval into eight equal subintervals and recalculating
its bound raised the floor to **249.531080704188**. This gained about 1.57 SSE
and closed about 0.6% of the gap from 247.96 to the checked fit.

### Why the gap remains

Some sample sequences that satisfy these inequalities violate the full
Lotka–Volterra equations. The earlier interval
enclosures of the full trajectories and periods left **664 of 721 rate regions**
at the previous floor. In one such region the period enclosure spanned about
**13.4 to 209.9** time units, so it allowed every fractional sampling phase.
Tighter bounds on the orbit shape and its feasible speed would constrain which
predicted values can occur together. [Trajectory and period enclosures](../benchmarks/2026-11-13/trajectory-period-bounds/README.md) · [Saved rate-region results](../benchmarks/2026-11-13/trajectory-period-bounds/results.json)

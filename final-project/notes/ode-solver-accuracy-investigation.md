# ODE solver accuracy investigation

Investigation snapshot: November 12, 2026. Findings describe the code and runs inspected at that time.

**There is a real numerical accuracy problem, but I did not find a mistake in the equations, RK4 stages, or SciPy wrappers that explains it.** The main cause is accumulated **phase drift and artificial changes in oscillation amplitude** over an exceptionally long integration.

### 1. The actual equilibrium test passes

These are two different cases:

| Case | Rates \(\theta\) | Initial derivative |
|---|---|---|
| Equilibrium | \((1.35,1,2.11,1)\) | \((0,0)\) |
| Current benchmark | \((1.62,1,2.11,1)\) | \((0.5697,0)\) |

- **RK45, DOP853, and both LSODA interfaces preserved the true equilibrium exactly** in the full-interval check.
- The current benchmark intentionally starts away from equilibrium.
- Some numerical solutions subsequently approach equilibrium because they **artificially damp the oscillations**.

That last behavior is an integration error—not the expected solution.

### 2. Why the long interval makes this difficult

For the current rates, the oscillation period is approximately

\[
T=3.406293934576513.
\]

Integrating through \(2{,}960{,}000\) therefore covers approximately **869,000 oscillations**.

- A period error of just **one part per million** would accumulate to roughly **0.87 cycles** by the end.
- Two predictions can consequently have similar amplitudes but place the population near opposite points of its oscillation.
- SciPy’s tolerances control estimated **local error**, not the total accumulated prediction error over this interval. [SciPy documentation](https://docs.scipy.org/doc/scipy-1.17.0/reference/generated/scipy.integrate.solve_ivp.html)

This explains why a solver can finish successfully and still disagree substantially with another solver.

### 3. Evidence that separates phase error from amplitude error

The assignment’s equations conserve

\[
H(x,y)=\theta_4x-\theta_3\ln x+\theta_2y-\theta_1\ln y.
\]

Differentiating this expression along the equations gives \(dH/dt=0\), so changes in it expose numerical drift independently of the CSV observations.

For DOP853 at \((\mathrm{rtol},\mathrm{atol})=(10^{-8},10^{-10})\):

| Comparison over the 27 CSV times | Prey discrepancy | Predator discrepancy |
|---|---:|---:|
| Compare at the same times | \(0.653\) | \(0.522\) |
| Allow each point to shift along the reference orbit | \(0.000327\) | \(0.000176\) |

**The large DOP853 discrepancy is predominantly a timing/phase error.** The second row is only a diagnostic; it is not an acceptable replacement for comparing predictions at the requested times.

Other configurations also have substantial amplitude errors:

- RK45 at \((10^{-6},10^{-9})\) loses almost all of the initial oscillation energy.
- Both LSODA interfaces at \((10^{-8},10^{-10})\) lose approximately **20%** by the final time.
- DOP853 at that pair loses approximately **0.19%**, yet its accumulated phase error is still large.

### 4. How I checked the reference independently

#### Shih’s orbit and period calculation

Shagi-Di Shih’s 2005 note, *Comments on “A New Method for the Explicit Integration of Lotka–Volterra Equations”*, separates the shape of the orbit from the time it takes to traverse it. The initial state fixes a level of the conserved quantity \(H\). For positive populations away from equilibrium, that level is a closed orbit. [Shih, *Divulgaciones Matemáticas* 13(2), pp. 99–106](https://www.maths.tcd.ie/EMIS/journals/DM/v13-2/art3.pdf)

1. **Find the orbit.** Shih rearranges the equation for \(H\) into the form \(we^w=z\), which Lambert \(W\) inverts. Its two real branches, \(W_0\) and \(W_{-1}\), give the lower and upper predator populations for a given prey population between the turning points. [Shih, Eqs. 2.1–2.4](https://www.maths.tcd.ie/EMIS/journals/DM/v13-2/art3.pdf#page=5)
2. **Find the period.** The prey equation gives the time spent traversing each branch through \(dt=dx/x'(t)\). Adding both travel times gives one period. The resulting integral has integrable square-root singularities at its endpoints, which Shih handles using Gauss–Chebyshev quadrature. His ten-node example gives a period of approximately \(5.270242858\). [Shih, Eqs. 2.5–2.7](https://www.maths.tcd.ie/EMIS/journals/DM/v13-2/art3.pdf#page=6)

The branch formulas give the possible predator populations at a given prey population. To predict both populations at a given time, we also need the position along the orbit at that time.

#### What the diagnostic script did

The [archived script](benchmarks/2026-11-12/ode-solver-accuracy-investigation/period_check.py) uses the same branch travel-time idea as Shih’s Eq. 2.5. It uses log prey relative to equilibrium, \(u=\ln(x/x_*)\) with \(x_*=\theta_3/\theta_4\), and evaluates the two predator branches using Lambert \(W\). If \(u_-\) and \(u_+\) are the turning points, the script substitutes

\[
u=\frac{u_-+u_+}{2}+\frac{u_+-u_-}{2}\sin\phi,
\qquad -\frac{\pi}{2}\le\phi\le\frac{\pi}{2}.
\]

The cosine factor from this substitution cancels the endpoint behavior. The script then uses **Gauss–Legendre quadrature** on the transformed integral, where Shih uses **Gauss–Chebyshev quadrature** on a weighted form. For the benchmark rates and initial state, the 64- and 128-node runs at 55-digit working precision differed by about \(7.8\times10^{-51}\) and gave \(T\approx3.406293934576513\). [Saved period and predictions](benchmarks/2026-11-12/ode-solver-accuracy-investigation/period_result.json)

To get predictions, the script integrated one orbit from the benchmark initial state with DOP853. It used the high-precision period to reduce each CSV time \(t_i\) to \(t_i\bmod T\), then evaluated the one-orbit solution at those 27 phases. It cross-checked the orbit by halving DOP853’s maximum step from \(T/100\) to \(T/200\) and comparing with Radau at \(T/200\). DOP853 and Radau predictions differed by at most about \(1.2\times10^{-14}\) across both populations and all 27 phases.

#### Period accuracy over 868,979 cycles

At a CSV time \(t_i\), let \(N_i=\lfloor t_i/T\rfloor\) be the number of complete cycles. The time within the cycle is \(t_i-N_iT\). Changing the period by \(\Delta T\) shifts that time by \(-N_i\Delta T\) as long as the cycle count stays the same. At the last CSV time, \(t_i=2{,}960{,}000\), there are 868,979 complete cycles. A period error of \(10^{-12}\) time units would therefore shift the final phase by about \(8.7\times10^{-7}\) time units.

The later benchmark verification recomputed the period with 64 nodes at 55 decimal digits and 96 nodes at 75 digits. The largest observed period difference across those runs and the original calculation was \(9.69\times10^{-51}\). Multiplying by 868,979 gives an implied phase shift of about \(8.42\times10^{-45}\) time units at the last CSV time. For this orbit, the conserved quantity confines the prey to \([1.7,2.6]\) and the predator to \([1.3,2.0]\). Substituting those ranges into the ODE gives \(|x'|,|y'|<1\), so the implied shift corresponds to less than \(9\times10^{-45}\) population units in either component. [Reference verification](benchmarks/2026-11-12/direct-ode-comparison-expanded-300s/diagnostic-reference/README.md)

The one-cycle DOP853 and Radau predictions differed by at most \(1.2\times10^{-14}\) population units at the 27 phases. The smallest errors in the main benchmark were \(1.65\times10^{-6}\) for prey and \(2.18\times10^{-6}\) for predator, both from Numba RK4 at \(h=1/1024\). Those errors are more than eight orders of magnitude larger than the observed one-cycle solver disagreement, and the change implied by period refinement is smaller still. The two checks measure empirical agreement, with the orbit solvers sharing the computed period. The benchmarked RK4 solves advance directly from zero through the last CSV time. [Scored benchmark](benchmarks/2026-11-12/direct-ode-comparison-expanded-300s/diagnostic-reference/scored-summary.json)

Against that diagnostic reference, the saved full-interval RK4 predictions give:

| RK4 step \(h\) | \(\|e_x\|_\infty\) | \(\|e_y\|_\infty\) |
|---|---:|---:|
| \(1/128\) | \(6.70\times10^{-2}\) | \(7.86\times10^{-2}\) |
| \(1/256\) | \(1.85\times10^{-3}\) | \(2.42\times10^{-3}\) |
| \(1/512\) | \(5.59\times10^{-5}\) | \(7.35\times10^{-5}\) |
| \(1/1024\) | \(1.65\times10^{-6}\) | \(2.18\times10^{-6}\) |
| \(1/2048\) | \(5.14\times10^{-8}\) | \(6.87\times10^{-8}\) |

These are differences from the diagnostic reference—not from observed populations in the CSV.

#### Period helper checks at four other rate vectors

All four cases start at the assignment's initial populations \((2.11,1.35)\). I computed each period with 32, 64, and 96 Gauss–Legendre nodes at 40, 55, and 75 decimal digits of working precision, respectively. The period changed less on the second refinement in every case. The table shows the absolute change from the 64-node result to the 96-node result.

| Case | Rates \((\theta_1,\theta_2,\theta_3,\theta_4)\) | Period \(T\) | Final change in \(T\) | Max. return error |
|---|---|---:|---:|---:|
| Near equilibrium | \((1.351,1,2.11,1)\) | 3.721439666870 | \(9.25\times10^{-47}\) | \(1.07\times10^{-14}\) |
| Interior | \((4,0.5,1,0.8)\) | 4.491910322351 | \(9.84\times10^{-42}\) | \(6.71\times10^{-14}\) |
| All lower bounds | \((0.10,0.01,0.10,0.01)\) | 83.999783442405 | \(4.79\times10^{-38}\) | \(4.97\times10^{-14}\) |
| All upper bounds | \((50,2,5,2)\) | 1.015413676138 | \(8.77\times10^{-29}\) | \(1.69\times10^{-12}\) |

I separately integrated the ODE in log-population coordinates with Radau. Tightening its tolerances from \((2\times10^{-11},2\times10^{-13})\) to \((2\times10^{-13},2\times10^{-15})\) and halving its maximum step from \(T/100\) to \(T/200\) reduced the return error in all four cases. The table reports the tighter solve's larger absolute difference between the starting and ending populations at \(t=T\), in population units. I also checked the first return to the starting prey level in the same direction. Its time agreed with \(T\) within \(2.7\times10^{-13}\) time units in all four cases. These checks measure numerical agreement for the four orbits tested.

### 5. A controlled change greatly improves DOP853

I repeated a direct DOP853 integration through \(t=100{,}000\), keeping tolerances fixed and changing only its maximum internal step.

| DOP853 setting | Prey discrepancy at endpoint | Predator discrepancy at endpoint |
|---|---:|---:|
| Automatic steps, no imposed maximum | \(3.41\times10^{-3}\) | \(1.44\times10^{-3}\) |
| `max_step=0.125` | \(1.54\times10^{-8}\) | \(6.62\times10^{-9}\) |

Both used \((10^{-8},10^{-10})\).

- The uncapped solver commonly took steps around \(0.33\), approximately ten per oscillation.
- The cap substantially reduced accumulated drift.
- **This validates the mechanism and a promising remedy through \(100{,}000\); it does not yet validate that setting through \(2{,}960{,}000\).**

### 6. Code review findings

| Area | Finding |
|---|---|
| Equations and parameter order | Match the assignment |
| Coupled RK4 stages | Correct |
| Python versus Numba | Same algorithm; matching completed predictions |
| Initial conditions and output times | Correct |
| SciPy callback conventions | Correct; checked against independently written equations |
| SciPy maximum-step control | Currently not exposed by the wrapper |
| Plot markers | Confirmed unrelated formatting bug |

The plot generator used at the time has only three marker shapes in its loop, so later settings lose their individual markers when a method has four or five configurations.

### What I recommend

1. **Keep the existing direct RK4 implementation.** The investigation supports its correctness and shows clear improvement under refinement.
2. **Do not treat the existing full-interval DOP853 run as ground truth.** Its phase drift is substantial.
3. **Validate a capped DOP853 configuration over the full interval**, including a smaller-cap comparison, before using it as a direct reference.
4. **Use the conserved quantity as an additional diagnostic**, alongside prediction differences.
5. **Keep the 27 CSV times unchanged.** More output points, longer timeouts, or larger `mxstep` limits alone do not resolve numerical accuracy.

### Saved scripts and evidence

The [evidence bundle](benchmarks/2026-11-12/ode-solver-accuracy-investigation/README.md) preserves the four diagnostic scripts, three JSON result files, and two benchmark-input snapshots outside the code and Overleaf repositories.

- [Period and reference predictions](benchmarks/2026-11-12/ode-solver-accuracy-investigation/period_result.json).
- [Direct solver comparisons](benchmarks/2026-11-12/ode-solver-accuracy-investigation/direct_results.json).
- [DOP853 maximum-step check](benchmarks/2026-11-12/ode-solver-accuracy-investigation/step_cap_result.json).
- [File inventory and checksums](benchmarks/2026-11-12/ode-solver-accuracy-investigation/manifest.json).

The bundle README records original paths, input dependencies, and missing terminal-only output. The scripts are preserved unchanged; their original hard-coded paths must be redirected in separate working copies before replay. The originals in `/tmp` were retained, and no experiments were rerun during archival.

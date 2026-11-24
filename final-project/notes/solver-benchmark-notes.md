# Lotka–Volterra solver benchmark

Step 1 asks us to implement a Runge–Kutta integrator and time one evaluation of
the least-squares objective. The objective starts at `t = 0` with populations
`[2.11; 1.35]` and uses both populations at all 27 observation times, through
`t = 2,960,000`.
[Assignment handout](project_step_1.pdf)

## Benchmark setting

Use `h = 0.15` for the benchmark rates `[0.12, 0.08, 0.15, 0.07]`.
The reference sum of squared residuals was `1395.57677581`.

| RK4 maximum step | Time | Largest absolute population error | Relative loss error |
| ---: | ---: | ---: | ---: |
| 0.25 | 4.68 s | 5.81e-3 | 0.00830% |
| 0.1875 | 5.95 s | 1.32e-3 | 0.00203% |
| 0.15 | 7.92 s | 4.15e-4 | 0.000680% |
| 0.125 | 9.01 s | 1.59e-4 | 0.000280% |
| 0.0625 | 18.02 s | 3.50e-6 | 0.00000994% |

At four times the benchmark rates, the maximum population error was
`0.309` at `h = 0.125` and `0.102` at `h = 0.0625`. For
`[1.2, 0.7, 1.1, 0.6]`, it was `0.697` at `h = 0.125`.
At the allowed corner `[50, 0.01, 5, 2]`, RK4 with that step produced a
nonfinite state near `t = 0.375`. A future solver for fitting needs accuracy
checks across the search box, including faster and larger-amplitude orbits.
Recheck the leading candidates with tighter settings when solver error is
large enough to affect their ordering by loss.

## Direct comparison with MATLAB `ode45`

Both solvers used MATLAB R2025b on an Apple silicon Mac, the same
right-hand side, initial state, observation times, and sum of squared
residuals. These wall times include the solve and loss calculation. CSV
loading, reference generation, plotting, and printing were outside the timed
calls. Each sweep row is one evaluation.

| `ode45` RelTol | `ode45` AbsTol | Time | Largest absolute population error | Relative loss error |
| ---: | ---: | ---: | ---: | ---: |
| 1e-6 | 1e-8 | 0.87 s | 3.74e-1 | 0.672% |
| 1e-8 | 1e-10 | 1.95 s | 2.74e-1 | 0.0241% |
| 1e-9 | 1e-11 | 3.42 s | 2.77e-2 | 0.0322% |
| 1e-10 | 1e-12 | 5.33 s | 2.85e-3 | 0.00334% |
| 3e-11 | 3e-13 | 6.33 s | 8.57e-4 | 0.00101% |
| 2e-11 | 2e-13 | 6.78 s | 5.72e-4 | 0.000671% |
| 1.5e-11 | 1.5e-13 | 7.86 s | 4.29e-4 | 0.000503% |
| 1e-11 | 1e-13 | 8.60 s | 2.86e-4 | 0.000336% |

At looser tolerances, the loss and the population errors varied independently.
The tolerances control estimated error per
step, and phase error can accumulate over roughly 63,000 cycles.
[MATLAB tolerance documentation](https://www.mathworks.com/help/matlab/ref/odeset.html)

Three alternating repeats at the settings below gave the following
times and work counts. The median favored `ode45` by about 5%, and the
timing ranges overlapped.

| Solver | Median time (range) | Successful steps | Right-hand-side calls |
| --- | ---: | ---: | ---: |
| Custom RK4, `h = 0.15` | 7.62 s (7.61–7.66 s) | 19.73 million | 78.93 million |
| MATLAB `ode45`, `RelTol = 1.5e-11`, `AbsTol = 1.5e-13` | 7.22 s (7.16–7.83 s) | 10.71 million | 64.27 million |

`ode45` reported one rejected step in a separate statistics run.

## Reproduce the comparison

Run `benchmark_objective` from the [MATLAB directory](code/matlab/) for the default
RK4 timing. Pass a different third argument to repeat the step-size sweep.
Run `validate_rk4` for the half-step, equilibrium, and short `ode45` checks.
The corresponding direct `ode45` evaluation uses the observation times as
requested outputs. [MATLAB output-time documentation](https://www.mathworks.com/help/matlab/ref/ode45.html)

```matlab
data = load_lv_data();
theta = [0.12, 0.08, 0.15, 0.07];
times = [0; data(:, 1)];
rhs = @(t, state) lotka_volterra_rhs(t, state, theta);
options = odeset('RelTol', 1.5e-11, 'AbsTol', 1.5e-13);

timer = tic;
[returned_times, states] = ode45(rhs, times, [2.11; 1.35], options);
assert(isequal(returned_times, times));
residuals = states(2:end, :) - data(:, 2:3);
loss = sum(residuals(:).^2);
elapsed_seconds = toc(timer);
```

For the accuracy reference, integrate a few cycles with `ode113` at
`RelTol = 5e-14` and `AbsTol = 5e-15`. Estimate the period between consecutive
upward crossings of the equilibrium prey level `theta(3)/theta(4)`. Use that
period to evaluate the interpolant at each observation time modulo the period.
The benchmark period was about `46.870805758684` time units. A second
`ode113` tolerance pair and a separate `ode45` calculation agreed with the
reference to within `5.5e-8` in the benchmark populations. The timed calls
integrated the full interval. [MATLAB event location](https://www.mathworks.com/help/matlab/math/ode-event-location.html)

Use the same numerical reference for each setting. For repeated timings,
alternate solver order and report the median and range. If needed,
collect successful steps, rejected steps, and right-hand-side call counts in
a separate diagnostic run with `ode45` statistics enabled.

## Python comparison

The Python runs used CPython 3.12.12, NumPy 2.3.5, SciPy 1.17.0, and
Numba 0.62.1 on the same Apple silicon Mac. They used the same initial state,
benchmark rates, 27 timestamps, and objective as MATLAB.
The independently reconstructed Python reference agreed with the MATLAB
reference within `9.6e-9` population units across the three checked cases.
The comparison below scores Python against the same MATLAB reference.

The Python RK4 updates the two populations as scalars and uses the same
four stages and interval subdivisions as MATLAB. CPython and Numba run
the same Python function, with ordinary double precision and Numba fast
math disabled. Numba compilation and a one-step warm-up took 0.35 s before
the timed calls. The MATLAB RK4 implementation uses a generic vector right-hand
side, so the timings compare these implementations on this machine.
[Numba compilation](https://numba.readthedocs.io/en/stable/user/jit.html)

### Repeated timings at selected settings

Python medians are from three sequential runs with the order reversed on
the second run. MATLAB values are from the earlier MATLAB comparison.
Each time covers the full solve and loss. The error is the largest
absolute error over both populations and all observation times.

| Solver | Step or relative/absolute tolerances | Median (range), s | Population error |
| --- | --- | ---: | ---: |
| Numba RK4 | `h=0.15` | 0.261 (0.260–0.267) | 0.000415 |
| SciPy LSODA (`odeint`) | `3e-11/3e-13` | 3.407 (3.352–3.602) | 0.00027 |
| SciPy DOP853 (Fortran) | `1e-10/1e-12` | 4.956 (4.855–5.634) | 0.000481 |
| CPython RK4 | `h=0.15` | 6.459 (6.162–6.525) | 0.000415 |
| MATLAB ode45 | `1.5e-11/1.5e-13` | 7.22 (7.16–7.83) | 0.000429 |
| MATLAB RK4 | `h=0.15` | 7.62 (7.61–7.66) | 0.000415 |
| SciPy Dormand–Prince 5(4) (Fortran) | `1e-11/1e-13` | 20.985 (20.459–21.161) | 0.000488 |

On this case, warm Numba RK4 was about 29 times as fast as MATLAB RK4.
LSODA had the lowest median runtime among the SciPy solvers in this table.
Its measured population error varied nonmonotonically across the tolerance sweep. Numba reproduced
the fixed-step failures from MATLAB at the faster rates, the different
orbit, and the nonfinite corner. Accuracy and runtime depend on the rates as well as the step size.

### Full sweeps

Each row below is a single timed objective call. RK4 population and loss
errors agreed with MATLAB at all five steps to the precision shown. For
SciPy, the same eight tolerance pairs were tested on each compiled solver.
The Fortran Dormand–Prince and DOP853 interfaces advanced sequentially to
the observation times. LSODA used `odeint` with the full vector of output
times. [SciPy compiled ODE solvers](https://docs.scipy.org/doc/scipy/reference/generated/scipy.integrate.ode.html)
· [SciPy LSODA](https://docs.scipy.org/doc/scipy/reference/generated/scipy.integrate.odeint.html)

| RK4 maximum step | MATLAB, s | CPython, s | Numba, s | Population error | Relative loss error |
| ---: | ---: | ---: | ---: | ---: | ---: |
| 0.25 | 4.68 | 3.852 | 0.156 | 0.00581 | 8.3e-05 |
| 0.1875 | 5.95 | 4.967 | 0.202 | 0.00132 | 2.03e-05 |
| 0.15 | 7.92 | 6.097 | 0.245 | 0.000415 | 6.8e-06 |
| 0.125 | 9.01 | 7.543 | 0.303 | 0.000159 | 2.8e-06 |
| 0.0625 | 18.02 | 14.768 | 0.590 | 3.5e-06 | 9.94e-08 |

| SciPy solver | Relative/absolute tolerances | Time, s | Population error | Relative loss error |
| --- | --- | ---: | ---: | ---: |
| `lsoda` | `1e-06/1e-08` | 1.440 | 0.359 | 0.002 |
| `lsoda` | `1e-08/1e-10` | 2.010 | 0.295 | 0.0099 |
| `lsoda` | `1e-09/1e-11` | 2.479 | 0.0963 | 0.00094 |
| `lsoda` | `1e-10/1e-12` | 2.955 | 0.00914 | 0.000108 |
| `lsoda` | `3e-11/3e-13` | 3.290 | 0.00027 | 2.67e-06 |
| `lsoda` | `2e-11/2e-13` | 3.439 | 0.000516 | 6.04e-06 |
| `lsoda` | `1.5e-11/1.5e-13` | 3.655 | 0.00026 | 2.94e-06 |
| `lsoda` | `1e-11/1e-13` | 3.448 | 9.15e-05 | 1.06e-06 |
| `dop853` | `1e-06/1e-08` | 1.784 | 0.389 | 0.00413 |
| `dop853` | `1e-08/1e-10` | 3.378 | 0.0535 | 0.000591 |
| `dop853` | `1e-09/1e-11` | 3.761 | 0.00527 | 6.14e-05 |
| `dop853` | `1e-10/1e-12` | 4.768 | 0.000481 | 5.61e-06 |
| `dop853` | `3e-11/3e-13` | 5.403 | 0.000155 | 1.81e-06 |
| `dop853` | `2e-11/2e-13` | 5.850 | 0.000109 | 1.27e-06 |
| `dop853` | `1.5e-11/1.5e-13` | 6.495 | 9.23e-05 | 1.08e-06 |
| `dop853` | `1e-11/1e-13` | 6.523 | 6.45e-05 | 7.54e-07 |
| `dopri5` | `1e-06/1e-08` | 5.842 | 0.254 | 0.000102 |
| `dopri5` | `1e-08/1e-10` | 6.197 | 0.254 | 0.000103 |
| `dopri5` | `1e-09/1e-11` | 8.321 | 0.0461 | 0.000527 |
| `dopri5` | `1e-10/1e-12` | 13.128 | 0.00485 | 5.69e-05 |
| `dopri5` | `3e-11/3e-13` | 16.565 | 0.00146 | 1.71e-05 |
| `dopri5` | `2e-11/2e-13` | 17.796 | 0.000975 | 1.14e-05 |
| `dopri5` | `1.5e-11/1.5e-13` | 19.307 | 0.000731 | 8.58e-06 |
| `dopri5` | `1e-11/1e-13` | 21.001 | 0.000488 | 5.73e-06 |

### SciPy's `solve_ivp` interface

I timed the usual `solve_ivp` call with its default method, RK45, and
the same objective, observation times, and numerical reference. Each row
is one full evaluation. I set the tolerances explicitly for the comparison.
The `dopri5` sweep uses the same Runge–Kutta formula through SciPy's
`ode` interface and has its own timings.
[SciPy `solve_ivp`](https://docs.scipy.org/doc/scipy/reference/generated/scipy.integrate.solve_ivp.html)

| Method | Relative/absolute tolerances | Time, s | Population error | Relative loss error |
| --- | ---: | ---: | ---: | ---: |
| RK45 | `1e-11/1e-13` | 153.243 | 6.48e-4 | 7.60e-6 |
| RK45 | `5e-12/5e-14` | 173.684 | 3.24e-4 | 3.80e-6 |
| DOP853 | `1e-10/1e-12` | 28.745 | 6.94e-4 | 8.10e-6 |
| DOP853 | `3e-11/3e-13` | 33.182 | 1.94e-4 | 2.27e-6 |

The [archived Python sweep](code/archive/benchmark_python_solvers.py)
reproduces the single-vector timings above. Run it from the code directory.
It can reconstruct its reference without MATLAB. An optional
`--matlab-reference` CSV provides the reference used in the original
timings, with one pair of population columns per tested rate vector.

```sh
cd code
PYTHONPATH=python python3 -m archive.benchmark_python_solvers
PYTHONPATH=python python3 -m archive.benchmark_python_solvers --solve-ivp-only RK45
PYTHONPATH=python python3 -m archive.benchmark_python_solvers --solve-ivp-only DOP853
```

## ODE solve only

Each timing covers one solve at the benchmark rates from time zero to
2,960,000, returning both populations at the 27 CSV timestamps. Data loading,
Numba compilation, and error and loss calculations are outside the timer.
For `solve_ivp`, set `t_span=(0, t[-1])` and `t_eval=t` using the CSV
time column. For `odeint`, pass `[0, *t]` and drop the initial row.
For Python, component errors were verified in separate runs with the
same settings as the timing runs.

Let `eₓ` and `eᵧ` be the solver predictions minus the numerical reference
at the 27 timestamps. **‖eₓ‖∞** is the largest absolute prey error,
**‖eᵧ‖∞** is the largest absolute predator error, and **‖e‖∞** is the
larger of those two. All errors are in population units.

### Python RK4

The same scalar RK4 function runs in plain Python and with Numba.
The maximum step `h` uses the CSV time units. The benchmark default is
shown in bold.

| h | Python (s) | Numba (s) | ‖eₓ‖∞ | ‖eᵧ‖∞ | ‖e‖∞ |
| ---: | ---: | ---: | ---: | ---: | ---: |
| 0.10 | 9.363 | 0.388 | 4.82e-05 | 4.57e-05 | 4.82e-05 |
| **0.15** | 6.117 | 0.244 | 0.000415 | 0.000391 | 0.000415 |
| 0.25 | 3.684 | 0.151 | 0.00581 | 0.00546 | 0.00581 |
| 0.50 | 1.848 | 0.077 | 0.189 | 0.17 | 0.189 |

### Python adaptive solvers

`rtol` and `atol` are the relative and absolute local error tolerances.

| Solver | rtol / atol | Time (s) | ‖eₓ‖∞ | ‖eᵧ‖∞ | ‖e‖∞ |
| --- | --- | ---: | ---: | ---: | ---: |
| RK45 (`solve_ivp`) | `1e-3 / 1e-6` (default) | 5.982 | 0.915 | 0.7 | 0.915 |
| RK45 (`solve_ivp`) | `1e-8 / 1e-10` | 38.661 | 0.381 | 0.302 | 0.381 |
| RK45 (`solve_ivp`) | `3e-11 / 3e-13` | 122.640 | 0.00194 | 0.00181 | 0.00194 |
| RK45 (`solve_ivp`) | `5e-12 / 5e-14` | 175.454 | 0.000324 | 0.000303 | 0.000324 |
| DOP853 (`solve_ivp`) | `1e-3 / 1e-6` (default) | 1.795 | 0.201 | 0.159 | 0.201 |
| DOP853 (`solve_ivp`) | `1e-8 / 1e-10` | 18.808 | 0.0816 | 0.0713 | 0.0816 |
| DOP853 (`solve_ivp`) | `3e-11 / 3e-13` | 34.161 | 0.000194 | 0.000182 | 0.000194 |
| LSODA (`solve_ivp`) | `1e-3 / 1e-6` (default) | 3.940 | 1.54 | 1.2 | 1.54 |
| LSODA (`solve_ivp`) | `1e-8 / 1e-10` | 7.197 | 0.295 | 0.207 | 0.295 |
| LSODA (`solve_ivp`) | `3e-11 / 3e-13` | 12.324 | 0.00027 | 0.000251 | 0.00027 |
| LSODA (`solve_ivp`) | `1e-11 / 1e-13` | 12.992 | 9.16e-05 | 8.54e-05 | 9.16e-05 |
| LSODA (`odeint`) | `1.49e-8 / 1.49e-8` (default¹) | 1.758 | 0.378 | 0.268 | 0.378 |
| LSODA (`odeint`) | `1e-3 / 1e-6` | 1.122 | 1.51 | 1.19 | 1.51 |
| LSODA (`odeint`) | `1e-8 / 1e-10` | 1.871 | 0.295 | 0.207 | 0.295 |
| LSODA (`odeint`) | `3e-11 / 3e-13` | 3.293 | 0.00027 | 0.000251 | 0.00027 |
| LSODA (`odeint`) | `1e-11 / 1e-13` | 3.383 | 9.16e-05 | 8.55e-05 | 9.16e-05 |

¹ The `solve_ivp` defaults are `1e-3 / 1e-6`. The `odeint` tolerance
defaults are approximately `1.49e-8 / 1.49e-8`. All reported `odeint` times
use an internal step limit of 20 million. The stock limit stopped the
default run with an excess-work error.
[SciPy solve_ivp](https://docs.scipy.org/doc/scipy-1.17.0/reference/generated/scipy.integrate.solve_ivp.html)
· [SciPy odeint](https://docs.scipy.org/doc/scipy-1.17.0/reference/generated/scipy.integrate.odeint.html)

### MATLAB RK4

| h | Time (s) | ‖eₓ‖∞ | ‖eᵧ‖∞ | ‖e‖∞ |
| ---: | ---: | ---: | ---: | ---: |
| 0.10 | 12.046 | 4.82e-05 | 4.57e-05 | 4.82e-05 |
| **0.15** | 7.862 | 0.000415 | 0.000391 | 0.000415 |
| 0.25 | 4.778 | 0.00581 | 0.00546 | 0.00581 |
| 0.50 | 2.397 | 0.189 | 0.17 | 0.189 |

### MATLAB adaptive solver

| Solver | RelTol / AbsTol | Time (s) | ‖eₓ‖∞ | ‖eᵧ‖∞ | ‖e‖∞ |
| --- | --- | ---: | ---: | ---: | ---: |
| `ode45` | `1e-3 / 1e-6` (default) | 0.342 | 0.472 | 0.347 | 0.472 |
| `ode45` | `1e-8 / 1e-10` | 2.019 | 0.274 | 0.219 | 0.274 |
| `ode45` | `3e-11 / 3e-13` | 7.027 | 0.000857 | 0.000801 | 0.000857 |
| `ode45` | `1.5e-11 / 1.5e-13` | 8.218 | 0.000429 | 0.0004 | 0.000429 |

The `ode45` defaults are `1e-3 / 1e-6`.
[MATLAB odeset](https://www.mathworks.com/help/matlab/ref/odeset.html)

All three RK4 implementations agree to the precision shown. At the shared
pair `3e-11 / 3e-13`, the two LSODA interfaces called the model equations
8,753,928 times each and agreed to the precision shown. `odeint` took
3.29 s and `solve_ivp` took 12.3 s.

## Eight-case Python solver comparison

The current report uses the eight-case study, with the single-vector timings
above retained for context. All eight vectors come from one seeded Latin
hypercube (seed 611) mapped linearly to the assignment's four rate ranges.
The same vectors and 27 CSV output times are used by each setting. The
timed interval is the ODE solve from zero through the final CSV time.
The DOP853 and Radau short-orbit integrations in log populations are
reference calculations outside the timer.

The definitive run is in
[`benchmarks/2026-11-12/python-ode-v02`](benchmarks/2026-11-12/python-ode-v02/).
Its manifest contains the exact rates, settings, output times, and library
versions. The solve records include completed predictions and losses,
numerical errors where the reference passed its checks, and explicit failure
or timeout records. The reference records contain the period and agreement
checks. The sibling `python-ode` directory is a superseded pilot that passed
NumPy scalar rates into the timed code. The definitive run uses native
Python floats.

From the course repository root, run the following with a fresh output
directory. The second command regenerates the report table and figure.

```sh
PYTHONPATH=final-project/code:final-project/code/python python3 -B -m archive.benchmark_python_sample path/to/new-output
MPLBACKEND=Agg PYTHONPATH=final-project/code:final-project/code/python python3 -B -m archive.plot_python_ode_benchmark \
    path/to/new-output final-project/report
```

The definitive matrix contains 64 attempts: 7 completed, 44 invalid, and
13 timed out. Seven of eight numerical references passed the checks.
Case 3 was unresolved and had no completed solver runs. The largest
DOP853–Radau population difference among checked references was
`2.33e-4`, which was small relative to the observed RK4 errors.
The completed RK4 runs cover two distinct rate vectors (cases 2 and 7).
At `h = 0.15`, both implementations ranked case 7 ahead of case 2
by least-squares loss, reversing the reference ordering. LSODA had
zero completions under the tested settings and time caps.

## Log-population follow-up

I repeated three Numba RK4 settings and the two tight LSODA settings on
the same eight saved rate vectors. The log-state right-hand side evolves
the natural logs of prey and predator. The solver converts its predictions
back to population units at the same 27 CSV times, and the benchmark
computes the same least-squares loss. The numerical references and per-solve
time caps were the same as in the direct-population benchmark.

The numerical LSODA tolerance pair is the same in both runs
(`rtol = 3e-11`, `atol = 3e-13`). It controls error in the coordinates
being integrated, so it does not specify equal population-space error
in the two runs. The RK4 maximum steps are `0.10`, `0.15`, and `0.25`.

The run records are in
[`benchmarks/2026-11-12/python-ode-log`](benchmarks/2026-11-12/python-ode-log/).
To repeat from the course repository root, use a new output directory:

```sh
PYTHONPATH=final-project/code:final-project/code/python python3 -B -m archive.benchmark_python_sample path/to/new-output \
  --log-baseline final-project/benchmarks/2026-11-12/python-ode-v02
```

| Setting | Direct completed | Log completed | Log invalid | Log timed out |
| --- | ---: | ---: | ---: | ---: |
| Numba RK4, `h = 0.10` | 2/8 | 2/8 | 6 | 0 |
| Numba RK4, `h = 0.15` | 2/8 | 2/8 | 6 | 0 |
| Numba RK4, `h = 0.25` | 1/8 | 1/8 | 7 | 0 |
| LSODA via `odeint`, tight | 0/8 | 0/8 | 3 | 5 |
| LSODA via `solve_ivp`, tight | 0/8 | 0/8 | 0 | 8 |

Exactly the same five Numba runs completed in both coordinate systems.
Their errors in population units were essentially unchanged. At
`h = 0.15`, the log-state runs took 1.00 and 1.04 seconds versus 0.27
and 0.29 seconds in the direct-state run. Each time is a single solve.
Both formulations reversed the reference least-squares ordering of cases
2 and 7 at `h = 0.10` and `h = 0.15`.

Of the 19 invalid log-state Numba attempts, 13 returned a zero
population after exponentiation and six produced a nonfinite RK4 state.
All three invalid `odeint` attempts reached its internal work limit.
These outcomes give no reason to carry the tested full-horizon log-state
settings into fitting.

## One-cycle RK4 pilot

I reused the custom Numba RK4 stepper in log population coordinates.
A same-direction return to the starting section determines the period.
Cubic Hermite interpolation locates that return and evaluates the orbit
at each of the 27 CSV times reduced modulo the estimated period. The
timed objective includes the period search, interpolation, and
least-squares sum, with the CSV loaded and Numba warmed up beforehand.

I used cases 2 and 7 from the original eight-case design. Both rate
vectors are inside the assignment bounds. At a maximum RK4 step of
0.0003125, case 2 had loss 1354.889465 versus the reference's 1354.889466,
and case 7 had loss 1479.762785 versus 1479.762834. The maximum absolute
population errors over both species and all 27 times were 3.57e-7 and
6.77e-6, respectively. Each complete objective call took about 1.7–1.9 ms
in one warmed run. The reference ranking was recovered for both cases
at all seven tested step sizes, even though the coarsest runs still had
large prediction errors. This pilot covers two cases.

[Summary](benchmarks/2026-11-12/periodic-rk4-pilot/summary.json) ·
[Predictions at every CSV time](benchmarks/2026-11-12/periodic-rk4-pilot/predictions.csv)

Run from the course repository root with a new output directory:

~~~sh
PYTHONPATH=final-project/code:final-project/code/python python3 -B -m archive.benchmark_periodic_rk4 \
  final-project/benchmarks/2026-11-12/python-ode-v02 path/to/new-output
~~~

The Step 1 handout asks for a Runge–Kutta implementation and a timed
objective evaluation. It gives no periodicity hint and does not specify
how the integrator must cover the model interval. Periodic reuse follows
from the model equations and should be confirmed with the instructor
before relying on it for submission.

## Early short RK4 verification

An earlier report draft compared plain Python RK4, Numba RK4, DOP853 and LSODA through
`solve_ivp`, and LSODA through `odeint` on a controlled trajectory.
The equilibrium vector is derived from the given initial state. Increasing
only the prey growth rate by 20% produces the moving case on `[0, 8]`.
See the [measured comparison](benchmarks/2026-11-12/rk4-verification-v02.json)
and the [reproduction script](code/archive/benchmark_rk4_verification.py).
The [prior report assets](benchmarks/2026-11-12/full-interval-report-assets/)
belong to the full-interval experiments documented below.

## Full-interval solver comparisons

These campaigns used the given initial populations `(2.11, 1.35)` and the
27 CSV times through `2,960,000`. For the moving case, set `theta2 = theta4 = 1`
and use the equilibrium relations `theta1 = theta2*y0` and
`theta3 = theta4*x0`. Increasing `theta1` by 20% gives
`theta = (1.62, 1, 2.11, 1)`.

- [Initial campaign](benchmarks/2026-11-12/direct-ode-comparison-300s/manifest.json):
  Python and Numba RK4 at `1/256`, `1/512`, and `1/1024`; RK45, DOP853,
  and LSODA through `solve_ivp`, plus LSODA through `odeint`. The adaptive
  settings were each API's defaults plus shared `(rtol, atol)` pairs
  `(1e-8, 1e-10)` and `(1e-10, 1e-12)`. The plan allowed three warmed calls
  per setting, with mean and sample SD for complete triplets, and a 300 s
  limit per call. The `odeint` campaign override was 200 million internal
  steps per output interval; the [project wrapper](code/python/scipy_solvers.py)
  defaults to 20 million. Neither setting is a wall-clock limit.
- [Direct reference attempt](benchmarks/2026-11-12/direct-ode-comparison-300s/summary.json):
  DOP853 reference settings were `(1e-11, 1e-13)` and `(1e-12, 1e-14)`,
  with a planned Numba RK4 cross-check through `h = 1/2048`. The direct
  reference did not pass the campaign's checks.
- [Moderate sweep](benchmarks/2026-11-12/direct-ode-comparison-moderate-300s/manifest.json)
  and [expanded sweep](benchmarks/2026-11-12/direct-ode-comparison-expanded-300s/summary.json):
  the expanded comparison uses single timings, adds coarser RK4 steps, and
  keeps the 300 s limit. The saved summaries identify the exact settings and
  source run for each timing. The [periodic reference verification](benchmarks/2026-11-12/direct-ode-comparison-expanded-300s/diagnostic-reference/README.md)
  shows agreement within about `1.2e-14` at the 27 times after period and
  integration refinement and a DOP853–Radau comparison.

### SciPy and MATLAB drift checks

- [SciPy investigation](ode-solver-accuracy-investigation.md): For DOP853 at
  `1e-8 / 1e-10`, the maximum error was `0.653` at matching times and
  `0.000327` after matching to the nearest point on the reference orbit.
  Extended DOP853 runs took about 372 s and 443 s at `1e-8 / 1e-10` and
  `1e-9 / 1e-11`, with maximum errors of `0.653` and `0.245`.
  A step cap of `0.125` improved the endpoint error through `t = 100,000`
  at unchanged tolerances in that diagnostic. Some RK45 and LSODA settings
  also damped the oscillations.
- [MATLAB cross-check](benchmarks/2026-11-12/ode-solver-accuracy-investigation/matlab-cross-check/README.md):
  At `RelTol = 1e-8, AbsTol = 1e-10`, single warmed solves took 31.348 s
  for `ode45` and 78.410 s for `ode113`. Maximum prey/predator errors were
  `0.640 / 0.556` and `0.628 / 0.541`, respectively. Nearest-orbit
  matching reduced the largest differences to `0.014` and `0.022`.
  At `1e-11 / 1e-13` both reached the 180 s process limit including
  startup, with no predictions returned.

Same-time error measures prediction accuracy. Nearest-orbit matching helps
isolate timing drift, and the conserved quantity helps detect changes in
orbit size. These checks describe the documented rates and settings.

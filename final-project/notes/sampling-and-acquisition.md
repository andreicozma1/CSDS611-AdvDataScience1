# Sampling rates and representing them in the GP

The assignment has four bounded physical rates and asks for approximately
50 space-filling initial queries. Current code uses 50 scrambled Halton points;
physical-versus-log mapping and the final GP representation remain open choices.
The [BO method note](bayesian-optimization.md) owns the loop, configuration,
acquisition search, failure handling, and staged comparisons.

## Initial sampling space

Let `u` be a Halton point in `[0,1]^4`, and let `L,U` be the assignment bounds.

| Mapping | Physical rates returned | Coverage interpretation |
| --- | --- | --- |
| Physical | `L + u*(U-L)` | Equal absolute changes |
| Log | `exp(log(L) + u*(log(U)-log(L)))` | Equal proportional changes |

Physical mapping puts relatively few queries near the small ends of wide rate
ranges. Log mapping allocates more queries there and leaves larger absolute
gaps near the upper bounds. Neither guarantees a better fit. Compare coverage
in a named coordinate system and judge BO performance with measured SSE.

`sampling.initial_rates(seed, count, mapping=...)` implements both mappings.
Larger counts retain the same Halton prefix. The default initial mapping is
physical and the current seed is 612. Each returned point is a physical rate
vector passed unchanged to the selected solver.

## GP input representation

The GP can use physical rates, bound-scaled physical rates, natural-log rates,
or bound-scaled log rates. Changing this representation transforms existing
rate vectors for the kernel; it does not choose a different initial design.

A constant rescaling can be absorbed into corresponding kernel length scales.
With fixed numerical length-scale initializations and bounds, however, the
implemented GP fits can differ. Log coordinates change distances nonlinearly,
so they are a separate modeling choice. Current length-scale settings are
expressed in the selected GP input units and saved with each policy.

Acquisition optimization uses a normalized unit box even when the GP inputs
are unscaled. The map back to physical rates follows the selected physical or
log coordinates. It does not restrict the search to a fixed candidate pool.

## GP target and objective

The objective remains raw SSE over both populations at the observation times.
The GP can model that SSE or its natural logarithm. GP centering and scaling
apply to these measured objective targets, not to the CSV populations or the
physical rates. They affect the surrogate and its acquisition scores while
leaving the underlying least-squares definition unchanged.

See [GP settings](bayesian-optimization.md#what-each-choice-belongs-to) and
[acquisition rules](bayesian-optimization.md#acquisition-search-policy) for the
implemented options, units, and defaults.

## Fair comparisons

- A sampling-space comparison shares Halton unit points and changes only their physical/log mapping.
- A GP-input or GP-target comparison shares physical initial points and their compatible measured scores.
- An acquisition-search comparison holds the GP, evaluator, and acquisition rule fixed while varying search effort.
- A compatible initialization checkpoint supplies shared scores through `--initial-results`, with reused timings labeled.

Keep rates, observations, solver settings, attempt budgets, and seeds matched
where the named comparison requires them. The
[staged acquisition-search plan](bayesian-optimization.md#staged-acquisition-search-comparison)
starts at 50 Halton samples; later expansions require review. Its acquisition
sample count is separate from the 50 initial objective queries.

The [decision ledger](decision-ledger.md) records the remaining choices.
The [synthetic recovery study](../benchmarks/archived-synthetic-recovery/README.md)
and fixed-pool rankings remain archived.

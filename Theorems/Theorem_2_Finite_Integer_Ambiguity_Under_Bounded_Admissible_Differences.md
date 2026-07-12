# Theorem 2 — Finite Integer Ambiguity Under Bounded Admissible Differences

```text
Document ID: AWC-THM-2-0.7
Version: Theorem Draft 0.7
Status: Conditional mathematical result
Applies to: AIRS Draft 0.1 and AWC-THM-1-0.5
Normative status: Informative and non-normative
Validation status: Not independently validated
Supersedes: Image-only aWc Theorem 2 — Finite Ambiguity Theorem
```

## 1. Purpose

This theorem states sufficient conditions under which integer-cycle ambiguity produced by a finite collection of bounded wrapped-phase observations reduces to a finite discrete search space. Exact enumeration is available when endpoint decisions are certified; otherwise, verified outward-rounded enclosures provide a finite conservative enumeration domain.

The theorem concerns the finiteness of **integer-cycle hypotheses**. It does not establish that:

- the continuous physical-state set is finite;
- any jointly consistent hypothesis exists;
- one hypothesis is unique;
- the retained model is physically correct;
- or a search procedure has examined the finite set exhaustively.

The essential condition is not absolute source-range boundedness. It is that every modeled propagation-time difference used by the wrapped observations has finite lower and upper bounds over each retained hypothesis branch.

---

## 2. Relationship to Theorem 1

Theorem 1 produces, for a declared observer pair, event, frequency, and path branch, a family of propagation-time-difference hypotheses indexed by an integer cycle variable.

For a scalar corrected phase, Theorem 1 gives intervals of the form:

```text
Δpₐ
∈
[
  (nₐ + qₐ)/fₐ − δₐ,
  (nₐ + qₐ)/fₐ + δₐ
]
```

where:

```text
qₐ = φ̃ₐ/(2π)
```

and, in the bounded scalar case:

```text
δₐ = ε_φ,ₐ/(2πfₐ)
```

Theorem 2 also permits a compact, set-valued corrected-phase support. Circular supports that cross the principal-branch boundary must first be represented as a finite union of non-wrapping intervals. Those intervals are treated as separate finite branches.

---

## 3. Indexing and Notation

Let:

- `B` be a finite set of retained discrete hypothesis branches;
- `b ∈ B` identify a declared combination of event association, propagation path, calibration branch, phase-support branch, and other discrete alternatives;
- `Ω_b` be the nonempty continuous admissible state set for branch `b`;
- `A_b` be the finite set of wrapped observations retained in branch `b`;
- `a ∈ A_b` index one observer-pair/event/frequency observation;
- `fₐ > 0` be its declared analysis frequency on the applicable physical or working-frequency coordinate;
- `gₐ,b(θ)` be the propagation-time-difference predicted by state `θ ∈ Ω_b`;
- `L̲ₐ,b ∈ ℝ` and `Ūₐ,b ∈ ℝ` be declared certified lower and upper bounds for `gₐ,b(θ)`;
- `Qₐ,b = [q⁻ₐ,b, q⁺ₐ,b]` be one compact, non-wrapping corrected-phase support expressed in cycles;
- `δₐ,b ≥ 0` be a finite additional timing-domain uncertainty half-width;
- `nₐ ∈ ℤ` be the corresponding integer-cycle hypothesis;
- `n_b = (nₐ)_{a∈A_b}` be the integer vector for branch `b`;
- and `C_b(θ,n_b)` be the predicate representing all other declared branch-consistency constraints.

The phase-cycle support satisfies:

```text
−1/2 < q⁻ₐ,b ≤ q⁺ₐ,b ≤ 1/2
```

except that an endpoint convention equivalent to Theorem 1 may be used consistently.

A singleton phase estimate is represented by:

```text
q⁻ₐ,b = q⁺ₐ,b
```

The state `θ` may include, as applicable:

- source coordinates;
- observer coordinates;
- event times;
- clock parameters;
- propagation parameters;
- environmental parameters;
- path parameters;
- and other bounded continuous nuisance variables.

---

## 4. Assumptions

### A1 — Finite discrete branch set

`B` is finite.

Every retained event-association, path, calibration, phase-support, and other discrete alternative relevant to this theorem is either included in `B` or explicitly excluded with justification.

### A2 — Finite observation set per branch

For every `b ∈ B`, the observation index set `A_b` is finite.

### A3 — Certified finite predicted-difference bounds

For every `b ∈ B` and `a ∈ A_b`, declared finite numbers:

```text
L̲ₐ,b ∈ ℝ
```

and:

```text
Ūₐ,b ∈ ℝ
```

are available such that:

```text
L̲ₐ,b
≤
gₐ,b(θ)
≤
Ūₐ,b
```

for every `θ ∈ Ω_b`, with:

```text
L̲ₐ,b ≤ Ūₐ,b
```

The bounds may be exact extrema or conservative certified enclosures. A bound is **certified** when its construction guarantees the enclosure for every `θ ∈ Ω_b` under the declared model, parameter domain, and numerical-arithmetic treatment. Sampled minima, sampled maxima, or unverified optimizer outputs do not constitute certified bounds.

A numerical solver limit is not a certified model bound merely because it is finite.

### A4 — Bounded observation support

For every `b ∈ B` and `a ∈ A_b`:

- `fₐ` is finite and strictly positive;
- `Qₐ,b` is compact and non-wrapping;
- and `δₐ,b` is finite.

The phase support and timing uncertainty must include all declared measurement, correction, calibration, and residual-model uncertainty used at this stage. Uncertainty must not be omitted or counted twice.

### A5 — Common coordinates and units

`gₐ,b(θ)` and `δₐ,b` are expressed in the same physical or declared working-time units. `fₐ` is expressed in cycles per that time unit, and `Qₐ,b` is dimensionless and expressed in cycles.

Device-recorded timing and frequency coordinates must be transformed through the applicable clock model before combination.

### A6 — No hidden unbounded nuisance direction

Any nuisance parameter that could otherwise prevent a finite certified bound on `gₐ,b(θ)` is handled by at least one of the following:

- it is bounded within `Ω_b`;
- it is removed by a declared gauge;
- it is analytically shown not to affect `gₐ,b`;
- its induced variation is separately proven finite and included in the certified enclosure required by A3;
- or it is excluded from the declared model and theorem scope with an explicit limitation.

No finite-ambiguity claim applies outside that declared scope. A numerically imposed solver limit is not, by itself, a physical or mathematical bound.

### D1 — Downstream dependency condition

Shared clocks, shared acquisition chains, derivative recordings, common calibration, and other dependencies do not affect the elementary finiteness proof, but they must be represented when candidate hypotheses are scored, combined, or assigned an AIRS integrity status.

---

## 5. Bound-Construction Note

Compactness of `Ω_b` and continuity of `gₐ,b` are sufficient to establish the existence of finite extrema. Practical enumeration additionally requires certified numerical enclosures or another verified bound-construction procedure.

A noncompact state set is permitted when finite bounds on every relevant `gₐ,b` are established by another justified argument.

---

## 6. Lifted Interval for One Integer Hypothesis

For branch `b`, observation `a`, and integer `n ∈ ℤ`, define the timing interval generated by the phase-support interval and timing uncertainty:

```text
Jₐ,b(n)
=
[
  (n + q⁻ₐ,b)/fₐ − δₐ,b,
  (n + q⁺ₐ,b)/fₐ + δₐ,b
]
```

An integer `n` is individually compatible with the bounded predicted-difference range when:

```text
Jₐ,b(n) ∩ [L̲ₐ,b, Ūₐ,b] ≠ ∅
```

Define the corresponding per-observation candidate set:

```text
Nₐ,b
=
{
  n ∈ ℤ :
  Jₐ,b(n) ∩ [L̲ₐ,b, Ūₐ,b] ≠ ∅
}
```

---

## 7. Theorem Statement

### Theorem 2 — Finite Integer Ambiguity

Under Assumptions A1–A6, every per-observation candidate set `Nₐ,b` is finite.

More precisely:

```text
Nₐ,b
=
ℤ ∩
[
  fₐ(L̲ₐ,b − δₐ,b) − q⁺ₐ,b,
  fₐ(Ūₐ,b + δₐ,b) − q⁻ₐ,b
]
```

Therefore:

```text
|Nₐ,b|
=
max{
  0,
  floor[fₐ(Ūₐ,b + δₐ,b) − q⁻ₐ,b]
  − ceil[fₐ(L̲ₐ,b − δₐ,b) − q⁺ₐ,b]
  + 1
}
```

and in particular:

```text
|Nₐ,b| < ∞
```

The displayed cardinality is exact when the derived real endpoints and their ceiling/floor decisions are known exactly or certified sufficiently to resolve their relation to neighboring integers.

For finite-precision implementation, define:

```text
Aₐ,b
=
fₐ(L̲ₐ,b − δₐ,b) − q⁺ₐ,b
```

```text
Bₐ,b
=
fₐ(Ūₐ,b + δₐ,b) − q⁻ₐ,b
```

Suppose finite verified outward-rounded endpoints `A⁻ₐ,b ∈ ℝ` and `B⁺ₐ,b ∈ ℝ` satisfy:

```text
A⁻ₐ,b ≤ Aₐ,b
```

and:

```text
Bₐ,b ≤ B⁺ₐ,b
```

Then the safely enumerable set:

```text
N̂ₐ,b
=
ℤ ∩
[
  ceil(A⁻ₐ,b),
  floor(B⁺ₐ,b)
]
```

is finite and satisfies:

```text
Nₐ,b ⊆ N̂ₐ,b
```

When:

```text
ceil(A⁻ₐ,b) > floor(B⁺ₐ,b)
```

the interval is empty and:

```text
N̂ₐ,b = ∅
```

If exact ceiling and floor decisions are not certified, `N̂ₐ,b` must be treated as a conservative candidate superset rather than claimed to equal `Nₐ,b`.

For each branch, define the integer vector:

```text
n_b = (nₐ)_{a∈A_b}
```

The empty product is defined as `1` when a branch contains no wrapped observations.

Define the exact raw finite discrete search space:

```text
H_raw
=
⋃_{b∈B}
{
  b
}
×
∏_{a∈A_b} Nₐ,b
```

Because each component is tagged by a distinct branch `b`, the union is disjoint. Therefore:

```text
|H_raw|
=
Σ_{b∈B}
∏_{a∈A_b}
|Nₐ,b|
<
∞
```

Define the conservative raw search space:

```text
Ĥ_raw
=
⋃_{b∈B}
{
  b
}
×
∏_{a∈A_b} N̂ₐ,b
```

Then:

```text
H_raw ⊆ Ĥ_raw
```

and:

```text
|Ĥ_raw|
=
Σ_{b∈B}
∏_{a∈A_b}
|N̂ₐ,b|
<
∞
```

When exact endpoint decisions are certified, `N̂ₐ,b` may be replaced by `Nₐ,b`. Otherwise, complete conservative enumeration means enumerating or admissibly pruning `Ĥ_raw`.

For every candidate `(b,n_b) ∈ Ĥ_raw`, define the compatible continuous state set:

```text
S_b,n_b
=
{
  θ ∈ Ω_b :
  gₐ,b(θ) ∈ Jₐ,b(nₐ)
  for every a ∈ A_b
  and C_b(θ,n_b)
}
```

Define the exact jointly consistent set:

```text
H_cons
=
{
  (b,n_b) ∈ H_raw :
  S_b,n_b ≠ ∅
}
```

Define the conservatively enumerated jointly consistent set:

```text
Ĥ_cons
=
{
  (b,n_b) ∈ Ĥ_raw :
  S_b,n_b ≠ ∅
}
```

Then:

```text
Ĥ_cons = H_cons
```

and therefore:

```text
|Ĥ_cons|
=
|H_cons|
<
∞
```

Extra candidates introduced by outward rounding must be retained until certified feasibility or consistency analysis proves their compatible state set empty. Under complete certified filtering of `Ĥ_raw`, the surviving set equals `H_cons`.

Thus, bounded predicted propagation-time differences transform the otherwise unbounded integer-cycle ambiguity into a finite discrete hypothesis search.

---

## 8. Proof

Fix one branch `b ∈ B` and one observation `a ∈ A_b`.

By Assumption A3, certified finite bounds satisfy:

```text
L̲ₐ,b
≤
gₐ,b(θ)
≤
Ūₐ,b
```

for every `θ ∈ Ω_b`.

The interval:

```text
Jₐ,b(n)
=
[
  (n + q⁻ₐ,b)/fₐ − δₐ,b,
  (n + q⁺ₐ,b)/fₐ + δₐ,b
]
```

intersects `[L̲ₐ,b, Ūₐ,b]` if and only if both:

```text
(n + q⁻ₐ,b)/fₐ − δₐ,b ≤ Ūₐ,b
```

and:

```text
(n + q⁺ₐ,b)/fₐ + δₐ,b ≥ L̲ₐ,b
```

hold.

Because `fₐ > 0`, these inequalities are equivalent to:

```text
n ≤ fₐ(Ūₐ,b + δₐ,b) − q⁻ₐ,b
```

and:

```text
n ≥ fₐ(L̲ₐ,b − δₐ,b) − q⁺ₐ,b
```

Therefore:

```text
Nₐ,b
=
ℤ ∩
[
  fₐ(L̲ₐ,b − δₐ,b) − q⁺ₐ,b,
  fₐ(Ūₐ,b + δₐ,b) − q⁻ₐ,b
]
```

The interval on the right has finite endpoints, so it contains only finitely many integers. The stated cardinality formula follows from counting the integers between its ceiling and floor.

When `L̲ₐ,b` and `Ūₐ,b` are conservative certified enclosures rather than exact extrema, `Nₐ,b` is the exact candidate set relative to those declared bounds and may retain integers that later joint-consistency analysis rejects.

For a fixed branch `b`, `A_b` is finite and every `Nₐ,b` is finite. Therefore the Cartesian product:

```text
∏_{a∈A_b} Nₐ,b
```

is finite.

The outward-rounded endpoints are finite, so every `N̂ₐ,b` is also finite. Therefore:

```text
∏_{a∈A_b} N̂ₐ,b
```

is finite for every branch.

Because `B` is finite, both finite unions defining `H_raw` and `Ĥ_raw` are finite. Since `H_cons ⊆ H_raw`, the exact jointly consistent set is finite.

It remains to prove conservative-domain equivalence.

Because:

```text
H_raw ⊆ Ĥ_raw
```

every candidate in `H_cons` also belongs to `Ĥ_raw`, has a nonempty compatible state set, and therefore belongs to `Ĥ_cons`. Thus:

```text
H_cons ⊆ Ĥ_cons
```

Conversely, suppose:

```text
(b,n_b) ∈ Ĥ_raw \ H_raw
```

Then for at least one observation `a ∈ A_b`:

```text
nₐ ∉ Nₐ,b
```

By the definition of `Nₐ,b`:

```text
Jₐ,b(nₐ)
∩
[L̲ₐ,b, Ūₐ,b]
=
∅
```

Assumption A3 guarantees that:

```text
gₐ,b(θ)
∈
[L̲ₐ,b, Ūₐ,b]
```

for every `θ ∈ Ω_b`. Therefore no state can satisfy:

```text
gₐ,b(θ) ∈ Jₐ,b(nₐ)
```

for that observation, and hence:

```text
S_b,n_b = ∅
```

Thus no candidate in `Ĥ_raw \ H_raw` can belong to `Ĥ_cons`, so:

```text
Ĥ_cons ⊆ H_cons
```

Combining both inclusions gives:

```text
Ĥ_cons = H_cons
```

Therefore conservative outward-rounded enumeration may add candidates requiring examination, but complete certified feasibility and consistency filtering recovers exactly the same jointly consistent discrete set. ∎

---

## 9. What “Finite Ambiguity” Means

The theorem establishes finiteness only for the retained **discrete integer-cycle and branch hypotheses**.

The compatible continuous state set `S_b,n_b` is defined for every candidate in `Ĥ_raw`.

For candidates introduced solely by conservative outward rounding:

```text
(b,n_b) ∈ Ĥ_raw \ H_raw
```

the proof establishes:

```text
S_b,n_b = ∅
```

For `(b,n_b) ∈ H_raw`, the set `S_b,n_b` may be:

- empty;
- a single state up to gauge;
- finitely many disconnected states;
- a continuum;
- or a higher-dimensional non-identifiable region.

For:

```text
(b,n_b) ∈ H_cons = Ĥ_cons
```

the set `S_b,n_b` is nonempty, but it may still be a singleton up to gauge, a finite disconnected set, a continuum, or a higher-dimensional non-identifiable region.

Therefore:

```text
|H_cons| < ∞
```

does not imply:

```text
|S_b,n_b| < ∞
```

and does not imply unique localization or resolution.

---

## 10. Useful Corollaries

### Corollary 1 — Shrinking valid bounds cannot add integers

Suppose valid replacements satisfy:

```text
[L̲′ₐ,b, Ū′ₐ,b]
⊆
[L̲ₐ,b, Ūₐ,b]
```

```text
Q′ₐ,b ⊆ Qₐ,b
```

and:

```text
0 ≤ δ′ₐ,b ≤ δₐ,b
```

Then:

```text
N′ₐ,b ⊆ Nₐ,b
```

This is a search-space monotonicity result, not a claim that tighter bounds are automatically better calibrated or more physically correct.


### Corollary 2 — Direct-path constant-speed baseline bound

For known observer positions `sᵢ` and `sⱼ`, a direct-path constant-speed model gives:

```text
gᵢⱼ(x)
=
(||x − sᵢ|| − ||x − sⱼ||)/c
```

with `c > 0`.

By the reverse triangle inequality:

```text
|gᵢⱼ(x)|
≤
||sᵢ − sⱼ||/c
```

for every source position `x`.

Therefore, the pairwise propagation-time difference has finite bounds even when the source-location region itself is not compact.

This corollary does not apply automatically to reflected, diffracted, relayed, public-address, moving-medium, or otherwise path-specific propagation models.

### Corollary 3 — Global consistency can only reduce the raw set

Any exact physical, geometric, timing, multi-frequency, cycle-closure, or other joint-consistency test selects a subset of `H_raw`. Such tests cannot make the discrete candidate set infinite.

They may, however, leave zero, one, or multiple candidates.

---

## 11. Search Completeness

Finiteness of `H_raw` or `Ĥ_raw` does not establish that a particular implementation searched the applicable domain completely.

A completeness claim must identify whether enumeration used the exact domain `H_raw` or the conservative domain `Ĥ_raw`. When exact floor or ceiling decisions are unresolved, completeness requires coverage of `Ĥ_raw`, not an unsupported claim of exact coverage of `H_raw`. Extra candidates introduced by outward rounding must be retained until certified feasibility or consistency analysis proves `S_b,n_b = ∅`. Under complete certified filtering of `Ĥ_raw`, the surviving set equals `H_cons`.

A feasibility or emptiness determination is **certified** when it proves, under the declared model, parameter domain, constraints, tolerances, and numerical-arithmetic treatment, either that:

```text
S_b,n_b ≠ ∅
```

or that:

```text
S_b,n_b = ∅
```

Failure of a local optimizer, failure to find a feasible point, iteration limits, timeouts, or numerical divergence do not by themselves certify emptiness.

A completeness claim requires, as applicable:

- explicit enumeration bounds for every `Nₐ,b`;
- certified outward rounding for all derived enumeration endpoints;
- documentation of unresolved near-integer endpoint cases;
- conservative retention when exact floor or ceiling decisions cannot be certified;
- documented branch generation;
- complete discrete enumeration or admissible pruning;
- documented pruning rules;
- proof that pruning is admissible;
- complete feasibility determination for every retained candidate;
- certified exclusion of every outward-rounding-only candidate before it is discarded;
- deterministic or reproducible traversal;
- solver termination criteria;
- retained rejected-candidate records or sufficient audit summaries;
- and treatment of numerical tolerances.

If only part of the applicable domain (`H_raw` or `Ĥ_raw`) is enumerated, if any outward-rounding-only candidate is discarded without certified emptiness, or if feasibility and branch-consistency testing is incomplete for any retained candidate, the result must use the AIRS classification appropriate to an incomplete bounded search.

---

## 12. Failure and Non-Applicability Conditions

The theorem does not establish a finite search space when any material requirement below is unresolved:

- an infinite or continuously unenumerated discrete branch family;
- an unbounded observation count;
- an unbounded state direction that can change a predicted difference without a certified finite enclosure;
- no justified certified finite bounds on `gₐ,b`;
- zero, undefined, or unbounded analysis frequency;
- unbounded phase, timing, calibration, or model uncertainty;
- circular phase support represented incorrectly as one line interval across the wrapping boundary;
- device-frequency coordinates compared without required clock-scale transformation;
- hidden path, event, or calibration alternatives;
- or numerical search limits substituted for model bounds.

If a branch lacks justified finite bounds, that branch must not be declared covered by this theorem.

---

## 13. Claims Not Established

Theorem 2 does **not** establish:

- that `H_cons` is nonempty;
- that one integer vector is correct;
- that one integer vector is unique;
- that continuous parameters are identifiable;
- that a source location is unique;
- that event association is correct;
- that a selected path is the physical path;
- that the model is compatible with the evidence;
- that uncertainty bounds are calibrated;
- that observers are statistically independent;
- that the search was exhaustive;
- that the surviving region satisfies a resolution criterion;
- authenticity;
- forensic validity;
- or certified performance.

A finite search space is a computational property of the declared bounded model, not proof that the model or any surviving hypothesis is physically correct.

---

## 14. Relationship to AIRS Draft 0.1

This theorem is an informative specialization of AIRS requirements concerning:

- bounded hypothesis spaces;
- event and path branching;
- phase prerequisites;
- integer-cycle ambiguity;
- clock-scale transformation;
- propagation modeling;
- uncertainty support;
- observability and gauge;
- dependency handling;
- search completeness;
- inference classification;
- and integrity reporting.

Where this theorem conflicts with AIRS Draft 0.1, AIRS Draft 0.1 controls.

Theorem 2 supplies a finite candidate domain for later global-consistency analysis. It does not perform that analysis and does not establish the conclusion of Theorem 3.

---

## 15. Validation Requirements

Before implementation claims are made, Theorem 2 should be exercised with cases covering at least:

1. one scalar phase observation with a known integer count;
2. set-valued phase support;
3. phase support crossing the principal wrapping boundary;
4. multiple observer-pair observations;
5. multiple frequencies with frequency-indexed integers;
6. multiple event-association branches;
7. multiple path branches;
8. compact uncertain observer geometry;
9. compact uncertain propagation parameters;
10. the direct-path baseline-bound corollary;
11. an empty candidate set;
12. one surviving integer vector;
13. multiple surviving integer vectors;
14. a finite integer set with a continuous non-identifiable state region;
15. unbounded nuisance parameters that invalidate the theorem;
16. incomplete branch generation;
17. exact verification of the cardinality formula;
18. brute-force comparison against enumerated small cases;
19. numerical-boundary cases at integer ceilings and floors;
20. and independent review of pruning and completeness claims.

Evaluation must distinguish:

- independent mathematical review of the theorem statement, assumptions, and proof;
- correctness and certification of bound construction;
- correctness of candidate enumeration;
- correctness of joint-consistency filtering;
- numerical robustness near interval boundaries;
- search completeness;
- and empirical applicability of the declared model bounds.

---

## 16. Revision History

| Version | Date | Change |
|---|---|---|
| 0.7 | 2026-07-11 | Required finite verified outward-rounded endpoints and defined the empty conservative integer interval explicitly; added an operational definition of certified feasibility and emptiness; and clarified that optimizer failure, timeouts, iteration limits, and numerical divergence do not certify infeasibility. |
| 0.6 | 2026-07-11 | Reordered exact and conservative search-domain definitions; removed the unnecessary separate conservative integer-vector symbol; defined compatible state sets over `Ĥ_raw`; introduced `Ĥ_cons`; proved `Ĥ_cons = H_cons`; and required outward-rounding-only candidates to be retained until certified feasibility or consistency analysis proves their compatible state sets empty. |
| 0.5 | 2026-07-11 | Added the conservative branch-level search domain `Ĥ_raw`; distinguished exact from conservative completeness claims; required conservative-domain coverage when endpoint decisions remain unresolved; clarified rejection of outward-rounding candidates; refined the purpose statement; and corrected the treatment of nuisance parameters that could otherwise prevent certified finite bounds. |
| 0.4 | 2026-07-11 | Distinguished exact mathematical cardinality from conservative finite-precision enumeration; added verified outward-rounded endpoint enclosures and near-integer handling; tightened the treatment of unbounded nuisance directions and theorem scope; and moved the bound-construction note into its own section. |
| 0.3 | 2026-07-11 | Defined certified bounds operationally and required ordered finite enclosures; moved sufficient bound-construction conditions outside the theorem assumptions; corrected the continuous compatible-set logic by defining it over `H_raw`; and strengthened search-completeness requirements for enumeration, pruning, and feasibility testing. |
| 0.2 | 2026-07-11 | Replaced exact-extrema computability with certified finite predicted-difference enclosures; separated existence of bounds from verified numerical construction; made the raw-space cardinality exact; formalized branch integer vectors and consistency predicates; corrected units for dimensionless phase-cycle support; and strengthened the monotonicity result using set inclusion. |
| 0.1 | 2026-07-11 | Replaced the image-only absolute wrapped-range theorem with an AIRS-compatible finite integer-ambiguity result based on bounded pairwise propagation-time differences, finite branches, compact continuous state sets, set-valued phase support, explicit cardinality bounds, and separate raw versus jointly consistent hypothesis sets. |

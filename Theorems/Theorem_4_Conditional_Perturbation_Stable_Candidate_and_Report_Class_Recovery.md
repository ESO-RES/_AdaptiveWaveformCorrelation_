# Theorem 4 — Conditional Perturbation-Stable Candidate and Report-Class Recovery

```text
Document ID: AWC-THM-4-1.0
Version: Frozen 1.0
Status: Conditional mathematical result
Applies to: AIRS Draft 0.1, AWC-THM-1-0.5, AWC-THM-2-0.7, and AWC-THM-3-1.0
Normative status: Informative and non-normative
Validation status: Not independently validated
Supersedes: Image-only aWc Theorem 4 — Robust Recovery / Integrity Theorem
Repository status: Final frozen release
```

## 1. Purpose

This theorem states sufficient conditions under which a predeclared objective-based candidate or report-class selection remains unchanged for every perturbation in a declared uncertainty set.

It also gives separate sufficient conditions for:

- uniform candidate-score separation;
- uniform report-class-score separation;
- conversion of a nominal score gap into a perturbation-stability certificate;
- local gauge-fixed state stability;
- and preservation of a predeclared report class under a certified physical-displacement bound.

The theorem does **not** identify the physically true hypothesis merely because one candidate has the lowest objective value. It does not convert objective separation into authenticity, causality, calibrated confidence, evidence integrity, or forensic validity.

The theorem separates five questions:

1. whether the complete candidate and perturbation domains were declared;
2. whether globally optimized candidate or class scores were bounded under every declared perturbation;
3. whether the winning candidate or report class is uniformly separated from all alternatives;
4. whether the recovered continuous state is locally stable after gauge treatment;
5. and whether any resulting report class remains unchanged at the predeclared reporting resolution.

---

## 2. Relationship to Theorems 1–3

Theorem 1 forms bounded, set-valued, same-event relative measurement hypotheses under declared measurement assumptions.

Theorem 2 converts integer-cycle ambiguity into a finite exact or conservative candidate domain.

Theorem 3 establishes the complete admissible report-class image when certified inner and outer report-class bounds agree.

Theorem 4 adds a separate perturbation-stability layer. It asks whether a predeclared score-based decision remains unchanged when measurements, calibration quantities, environmental parameters, admissible masks, or other declared inputs vary over a certified perturbation set.

The roles are distinct:

```text
Theorem 1:
form bounded relative measurements

Theorem 2:
construct a finite candidate domain

Theorem 3:
establish the complete admissible report-class image

Theorem 4:
certify stability of a declared score-based candidate,
report-class, or local-state decision under perturbation
```

A score-minimizing candidate selected by Theorem 4 need not be the only admissible candidate under Theorem 3.

Likewise, report-class stability under Theorem 4 does not by itself establish candidate-level closure, exact state-set closure, or an AIRS primary inference classification.

---

## 3. Perturbation Domain and Candidate Domain

Let:

```text
U
```

be a nonempty, predeclared perturbation set.

Let:

```text
u₀ ∈ U
```

denote the nominal or reference instance.

A perturbation element `u ∈ U` may include, when explicitly modeled:

- bounded measurement changes;
- interval-valued phase or timing observations;
- calibration uncertainty;
- environmental or propagation uncertainty;
- clock uncertainty;
- geometry uncertainty;
- declared missing-data patterns;
- predeclared sensor masks;
- predeclared contamination or outlier branches;
- or other bounded model inputs.

Let:

```text
D ≠ ∅
```

be one finite nonempty candidate domain that covers every candidate relevant to every `u ∈ U`.

If the exact candidate domain varies with `u`, then `D` must be a certified finite union or conservative superset covering all perturbation-dependent domains. A candidate absent at a particular `u` is represented by an empty compatible set.

For each:

```text
h = (b,n_b) ∈ D
```

and each:

```text
u ∈ U
```

let:

```text
S_h(u) ⊆ Ω_b
```

be the exact compatible continuous state set under the perturbed instance `u` and all declared constraints.

Define:

```text
H_adm(u)
=
{
  h ∈ D :
  S_h(u) ≠ ∅
}
```

The perturbation-dependent exact report-class image is:

```text
C_rep(u)
=
⋃_{h∈D}
{
  ψ_h(θ) :
  θ ∈ S_h(u)
}
```

where the total report-class maps `ψ_h` are predeclared as in Theorem 3.

Define the perturbation-union report-class domain:

```text
C_U
=
⋃_{u∈U} C_rep(u)
```

Theorem 4 does not assume that `C_rep(u)` is constant over `U`.

Unless stated otherwise, this theorem uses the extended-real convention:

```text
inf ∅ = +∞
```

Expressions involving a maximum over competing alternatives are used only when the alternative set is nonempty. Singleton-domain cases are handled separately.

---

## 4. Objective, Optimized Candidate Scores, and Minimizers

For every candidate `h ∈ D`, let:

```text
J_h : Ω_b × U → [0,+∞)
```

be a finite-valued, predeclared objective or discrepancy function.

The objective may be a weighted least-squares loss, robust loss, interval-consistency penalty, likelihood-derived score, or another declared decision functional. Its semantics, units, weighting, dependencies, and treatment of missing or contaminated observations must be specified before final evaluation.

For every `h ∈ D` and `u ∈ U`, define the optimized candidate score:

```text
V_h(u)
=
inf {
  J_h(θ;u) :
  θ ∈ S_h(u)
}
```

with the convention:

```text
inf ∅ = +∞
```

so that, because `J_h` is finite-valued and nonnegative:

```text
V_h(u) = +∞
⇔
S_h(u) = ∅
```

and:

```text
S_h(u) ≠ ∅
⇒
V_h(u) < +∞
```

Define the candidate minimizer set:

```text
M_h(u)
=
{
  θ ∈ S_h(u) :
  J_h(θ;u) = V_h(u)
}
```

and the globally winning candidate set:

```text
H_min(u)
=
arg min_{h∈D} V_h(u)
```

Because `D` is finite and nonempty, the globally optimized candidate score:

```text
V_min(u)
=
min_{h∈D} V_h(u)
```

always exists as an extended-real value, and the winning candidate-index set satisfies:

```text
H_min(u) ≠ ∅
```

Candidate-index attainment does not imply that any compatible continuous state attains `V_h(u)`. Continuous-state attainment is a separate condition governed by Assumption A9.

If every candidate is infeasible at `u`, then:

```text
V_min(u) = +∞
```

and:

```text
H_min(u) = D
```

even though no compatible continuous state exists.

A local optimizer output is not, by itself, a certificate of `V_h(u)`.

Failure to find a feasible point does not establish:

```text
V_h(u) = +∞
```

unless emptiness of `S_h(u)` is independently certified.

---

## 5. Report-Class-Restricted Scores

For every candidate `h ∈ D`, report class `c ∈ C_U`, and perturbation `u ∈ U`, define:

```text
S_h,c(u)
=
{
  θ ∈ S_h(u) :
  ψ_h(θ) = c
}
```

Define the optimized score restricted to report class `c`:

```text
V_c^rep(u)
=
inf {
  J_h(θ;u) :
  h ∈ D,
  θ ∈ S_h,c(u)
}
```

with:

```text
inf ∅ = +∞
```

Because `J_h` is finite-valued:

```text
V_c^rep(u) = +∞
⇔
⋃_{h∈D} S_h,c(u) = ∅
```

Define the winning report-class index set by:

```text
C_min(u)
=
arg min_{c∈C_U} V_c^rep(u)
```

when:

```text
C_U ≠ ∅
```

Even when `C_U ≠ ∅`, the set `C_min(u)` may be empty if the infimum of the report-class scores is not attained by any class index.

Proposition 4A excludes this nonattainment case for its designated class by supplying a finite upper bound for `c★` together with strict separation from every alternative class.

If:

```text
C_U = ∅
```

define:

```text
C_min(u) = ∅
```

If:

```text
C_U ≠ ∅
```

but:

```text
C_rep(u) = ∅
```

then:

```text
V_c^rep(u) = +∞
```

for every `c ∈ C_U`, and therefore:

```text
C_min(u) = C_U
```

as a pure score-index tie. This tie must not be interpreted as a selected physical report class because no compatible report class exists at that perturbation.

Whenever a globally minimizing compatible candidate-state pair exists:

```text
V_min(u)
=
min_{c∈C_U} V_c^rep(u)
```

and the report class of every attained global minimizer belongs to:

```text
C_min(u)
```

Whenever a globally minimizing compatible state exists, it must therefore map to a winning report class. Conversely, a winning report class need not identify one discrete candidate or one continuous state.

Candidate-score separation and report-class-score separation are therefore different certification targets.

---

## 6. Certified Score Envelopes

### 6.1 Candidate-score envelopes

For every candidate `h ∈ D`, let certified extended-real bounds satisfy:

```text
V̲_h
≤
V_h(u)
≤
V̄_h
```

for every:

```text
u ∈ U
```

The bounds must account for:

- complete global optimization over `S_h(u)`;
- perturbation of the observations and constraints;
- perturbation-dependent feasibility;
- numerical and arithmetic error;
- all predeclared branch alternatives;
- and any perturbation-dependent objective weights or loss parameters.

### 6.2 Report-class-score certificates

For a report-class separation claim designating:

```text
c★ ∈ C_U
```

let a certified upper bound satisfy:

```text
V_{c★}^rep(u)
≤
V̄_{c★}^rep
```

for every:

```text
u ∈ U
```

For every alternative class:

```text
c ∈ C_U \ {c★}
```

let a certified lower bound satisfy:

```text
V̲_c^rep
≤
V_c^rep(u)
```

for every:

```text
u ∈ U
```

Upper bounds for alternative classes are not required for Proposition 4A. Lower bounds for the designated class may be computed but are not required for the strict-separation conclusion.

Every class in:

```text
C_U \ {c★}
```

must be covered by a certified uniform lower bound.

One certificate may cover an entire declared family of alternative classes when it establishes the required uniform lower bound for every member of that family.

No alternative class may be excluded from the strict-separation infimum.

A finite upper bound on `V_c^rep(u)` certifies that report class `c` is nonempty for the covered perturbation.

A claim that an attained score is no greater than `V̄_c^rep` additionally requires either:

- a certified candidate-state witness in class `c` with objective value at most `V̄_c^rep`;
- or an independent attainment result for the class-restricted infimum.

A report-class lower bound must apply to every candidate and every compatible state mapping to that class.

### 6.3 Finite bounds and feasibility

A finite certified upper bound:

```text
V̄_h < +∞
```

establishes that:

```text
S_h(u) ≠ ∅
```

for every covered perturbation. It does not, by itself, provide a certified feasible witness or establish an attained score at or below `V̄_h`; either conclusion additionally requires a witness or an attainment result.

A finite report-class upper bound:

```text
V̄_c^rep < +∞
```

establishes that report class `c` is nonempty for every covered perturbation. It does not, by itself, establish an attained score at or below that bound unless a witness or attainment result is also certified.

Because the objective is finite-valued:

```text
V̲_h = +∞
```

certifies:

```text
S_h(u) = ∅
```

for every perturbation covered by that lower bound.

Likewise:

```text
V̲_c^rep = +∞
```

certifies that no compatible state maps to class `c` for every perturbation covered by that lower bound.

---

## 7. Assumptions

### A1 — Valid upstream scope

All measurement-formation, integer-domain, branch-scope, gauge, and report-map requirements inherited from Theorems 1–3 are satisfied for the declared perturbation family.

### A2 — Declared perturbation set

The set `U` is specified before final evaluation.

Its coordinates, units, dependency structure, boundary conventions, and inclusion or exclusion of contamination, missingness, calibration, and environmental alternatives are documented.

### A3 — Complete finite candidate coverage

The finite domain `D` covers every material discrete candidate that can arise for any `u ∈ U` within the declared theorem scope.

Candidates may not be silently added, removed, or redefined after observing the winning result.

### A4 — Exact perturbation-dependent compatible sets

For every `h ∈ D` and `u ∈ U`, `S_h(u)` includes all applicable inherited and perturbation-dependent constraints.

A perturbation that changes feasibility must be represented in `S_h(u)` or by an explicitly declared branch.

### A5 — Predeclared total report maps

For every candidate, the quotient, claim, and resolution maps are total on the relevant domains and fixed before final evaluation:

```text
ψ_h
=
ρ ∘ r_h ∘ q_b
:
Ω_b → C
```

The reporting space, units, gauge treatment, cell boundaries, and materially reportable branch distinctions are common and semantically consistent across `D` and `U`.

### A6 — Predeclared objective

Every `J_h` is specified before final evaluation.

The report states:

- the residual or discrepancy definition;
- weights and units;
- dependency and covariance treatment;
- robust-loss parameters;
- missing-data treatment;
- mask or outlier treatment;
- regularization;
- and whether objective values are comparable across candidates and branches.

A score may not be used across candidates unless its scale and additive terms have consistent decision semantics.

### A7 — Certified candidate-score envelopes

For the candidate-separation path, certified bounds satisfy:

```text
V̲_h
≤
V_h(u)
≤
V̄_h
```

for every `h ∈ D` and every `u ∈ U`.

### A8 — Certified report-class-score separation bounds

For any report-class separation claim designating:

```text
c★ ∈ C_U
```

a certified upper bound satisfies:

```text
V_{c★}^rep(u)
≤
V̄_{c★}^rep
```

for every `u ∈ U`.

For every alternative:

```text
c ∈ C_U \ {c★}
```

a certified lower bound satisfies:

```text
V̲_c^rep
≤
V_c^rep(u)
```

for every `u ∈ U`.

Every alternative class in:

```text
C_U \ {c★}
```

must be covered by a certified lower bound.

One certificate may cover an entire declared family of alternative classes, provided it establishes the required uniform lower bound for every member of that family.

No alternative class may be excluded from the strict-separation infimum:

```text
V̄_{c★}^rep
<
inf_{c∈C_U, c≠c★} V̲_c^rep
```

Alternative-class upper bounds are not required for Proposition 4A.

### A9 — Global attainment or certified attainment argument

For every perturbation to which a selected-state conclusion is applied, the global minimum is attained by at least one compatible candidate-state pair, or another certified attainment argument establishes existence, such as compactness of the feasible domain together with lower semicontinuity of the objective.

Candidate-score separation alone does not establish uniqueness of the continuous minimizer within the winning candidate.

### A10 — Reproducible global certification

All score bounds, feasibility conclusions, perturbation traversals, and optimization certificates are deterministic or reproducible.

Local optimization alone is insufficient unless accompanied by a valid global lower-bound or exhaustiveness certificate.

### A11 — Gauge-fixed local-state conditions

Any local continuous-state stability claim is made only in a justified gauge-fixed representation of the relevant quotient state.

The gauge-fixed coordinate domains, optimization-complete coordinate-realization maps `χ_u`, the common comparison domain `X̃`, the uniformly defined maps `Φ_u`—identity maps in the common-domain form and certified bijections otherwise—complete quotient coverage, preservation of feasibility, exact optimized values, physical minimizer sets modulo gauge, gauge-consistent objective semantics, claim semantics, the fixed norm `||·||_X`, the predeclared metric or pseudometric `d_Z`, the local convex region, global-minimum attainment, minimizer confinement, convexity conditions, and claim-map regularity are independently certified.

### D1 — Separate admissibility, classification, and integrity status

Objective-based selection is reported separately from:

- Theorem 3 admissibility and report-class closure;
- AIRS primary inference classification;
- evidence-integrity status;
- authenticity;
- causality;
- and forensic conclusions.

A stable score winner is not automatically the only admissible solution.

---

## 8. Theorem Statement

### Theorem 4 — Uniform Candidate-Score Separation

Under Assumptions A1–A7 and A10, let:

```text
h★ ∈ D
```

be a designated candidate.

Suppose:

```text
V̄_{h★}
<
inf_{h∈D, h≠h★} V̲_h
```

Then, for every:

```text
u ∈ U
```

candidate `h★` is the unique globally score-minimizing candidate:

```text
H_min(u) = {h★}
```

Equivalently:

```text
V_{h★}(u)
<
V_h(u)
```

for every:

```text
h ∈ D \ {h★}
```

and every:

```text
u ∈ U
```

The certified uniform candidate gap is:

```text
Δ_cand
=
inf_{h∈D, h≠h★} V̲_h
-
V̄_{h★}
>
0
```

This conclusion establishes **perturbation-stable candidate selection under the declared objective**.

Under the convention:

```text
inf ∅ = +∞
```

the separation condition includes the singleton case:

```text
D = {h★}
```

whenever `V̄_{h★} < +∞`. No competing-candidate lower bound needs to be computed.

It does not establish:

- that `h★` is physically true;
- that all other candidates are inadmissible;
- that the minimizer inside `h★` is unique;
- that one report class is selected;
- or that AIRS requires a resolved classification.

---

## 9. Proof of Theorem 4

For every `u ∈ U`, Assumption A7 gives:

```text
V_{h★}(u)
≤
V̄_{h★}
```

For every alternative `h ≠ h★`:

```text
V̲_h
≤
V_h(u)
```

By the strict separation assumption:

```text
V̄_{h★}
<
V̲_h
```

for every `h ≠ h★`.

Therefore:

```text
V_{h★}(u)
≤
V̄_{h★}
<
V̲_h
≤
V_h(u)
```

for every `h ≠ h★` and every `u ∈ U`.

Thus `h★` has strictly smaller globally optimized score than every alternative candidate under every declared perturbation:

```text
H_min(u) = {h★}
```

The result concerns candidate-level score ordering only. ∎

---

## 10. Report-Class Recovery

### Proposition 4A — Uniform Report-Class-Score Separation

Under Assumptions A1–A6, A8, and A10, let:

```text
c★ ∈ C_U
```

be a designated report class.

Suppose:

```text
V̄_{c★}^rep
<
inf_{c∈C_U, c≠c★} V̲_c^rep
```

Then, for every:

```text
u ∈ U
```

the unique score-minimizing report-class index is:

```text
C_min(u) = {c★}
```

If Assumption A9 additionally holds for the selected-state conclusion, then every globally score-minimizing compatible candidate-state pair maps to `c★`.

The certified uniform report-class gap is:

```text
Δ_rep
=
inf_{c∈C_U, c≠c★} V̲_c^rep
-
V̄_{c★}^rep
>
0
```

The score-level conclusion permits multiple candidate indices to achieve the globally minimal candidate score while the unique minimizing report-class index remains `c★`.

If Assumption A9 additionally holds, multiple attained continuous minimizers may exist, but every globally minimizing compatible candidate-state pair maps to `c★`.

Under the convention:

```text
inf ∅ = +∞
```

the separation condition includes the singleton case:

```text
C_U = {c★}
```

whenever `V̄_{c★}^rep < +∞`. No competing-class lower bound needs to be computed.

It establishes **perturbation-stable report-class selection under the declared objective and resolution map**.

It does not establish one candidate, one branch, one exact state, or physical truth.

#### Proof

For every `u ∈ U`:

```text
V_{c★}^rep(u)
≤
V̄_{c★}^rep
```

For every alternative class `c ≠ c★`:

```text
V̲_c^rep
≤
V_c^rep(u)
```

Strict envelope separation gives:

```text
V_{c★}^rep(u)
<
V_c^rep(u)
```

for every:

```text
c ∈ C_U \ {c★}
```

and therefore:

```text
C_min(u) = {c★}
```

If Assumption A9 additionally holds, let:

```text
(h_u,θ_u)
```

be any globally minimizing compatible candidate-state pair, and define:

```text
c_u
=
ψ_{h_u}(θ_u)
```

Its objective value equals the attained global minimum:

```text
J_{h_u}(θ_u;u)
=
min_{c∈C_U} V_c^rep(u)
=
V_{c★}^rep(u)
```

If:

```text
c_u ≠ c★
```

then:

```text
V_{c_u}^rep(u)
≤
J_{h_u}(θ_u;u)
=
V_{c★}^rep(u)
```

contradicting strict class separation.

Hence every globally minimizing compatible candidate-state pair maps to `c★`.

Therefore the score-level conclusion holds under A1–A6, A8, and A10, while the attained state-level mapping conclusion additionally requires A9. ∎

### Corollary 1 — Candidate stability plus within-candidate class stability

Assume Theorem 4 establishes:

```text
H_min(u) = {h★}
```

for every `u ∈ U`.

If, in addition, every minimizer of the winning candidate maps to one common class:

```text
{
  ψ_{h★}(θ) :
  θ ∈ M_{h★}(u)
}
=
{c★}
```

for every `u ∈ U`, then every global minimizer maps to `c★`.

Candidate stability alone does not imply this corollary without the within-candidate report-class condition.

---

## 11. Nominal Gap and the `2B` Corollary

Let the nominal optimized scores be:

```text
V_h(u₀)
```

and let `h₀` be the unique nominal score winner.

Define the nominal candidate gap:

```text
G₀
=
min_{h∈D, h≠h₀}
V_h(u₀)
-
V_{h₀}(u₀)
```

so that:

```text
G₀ > 0
```

This nominal competitor-gap construction is used only when:

```text
D \ {h₀} ≠ ∅
```

When:

```text
D = {h₀}
```

candidate uniqueness is trivial once `h₀` is certified feasible and globally minimizing. The `G₀` and competing-candidate `max` formulas are not used.

### Corollary 2 — Candidate stability from optimized-value perturbation bounds

This corollary applies only when:

```text
V_h(u₀) < +∞
```

and:

```text
V_h(u) < +∞
```

for every `h ∈ D` and every covered `u ∈ U`.

A candidate having an infinite optimized value at the nominal or any covered perturbed instance lies outside the scope of Corollary 2.

Such candidates must instead be handled through Theorem 4's direct certified score-envelope path. A combined argument must state the absolute-difference and direct-envelope paths separately.

Suppose certified finite constants satisfy:

```text
0 ≤ B_h < +∞
```

for every `h ∈ D`, and:

```text
|V_h(u) - V_h(u₀)|
≤
B_h
```

for every `h ∈ D` and every `u ∈ U`.

If:

```text
G₀
>
B_{h₀}
+
max_{h∈D, h≠h₀} B_h
```

then:

```text
H_min(u) = {h₀}
```

for every `u ∈ U`.

#### Uniform-bound form

If one common finite bound satisfies:

```text
0 ≤ B < +∞
```

and:

```text
|V_h(u) - V_h(u₀)|
≤
B
```

for every candidate and perturbation, then the sufficient condition becomes:

```text
G₀ > 2B
```

This is the rigorous form of the common ambiguity-gap rule.

The quantity `B` must bound changes in the **globally optimized candidate values** `V_h`, not merely raw observation errors, individual residuals, or one fixed-state objective evaluation.

### Fit-consistency threshold

Let:

```text
0 ≤ τ_fit < +∞
```

be a finite, predeclared score threshold with declared units and interpretation.

If:

```text
V̄_{h★} ≤ τ_fit
```

then:

```text
V_{h★}(u)
≤
V̄_{h★}
≤
τ_fit
```

for every `u ∈ U`.

Thus the winning candidate's optimized score infimum satisfies the declared threshold for every perturbation. An attained compatible state with objective value at or below `τ_fit` additionally requires a certified witness or an attainment result.

This fit-consistency statement is separate from score separation.

A candidate may be uniformly best but still fit poorly:

```text
V̄_{h★} > τ_fit
```

A candidate may also fit within threshold without being uniquely separated from alternatives.

---

## 12. From Pointwise Objective Bounds to Optimized-Value Bounds

### Proposition 4B — Fixed-feasible-set objective perturbation

Fix a candidate `h`.

Suppose there is one common nonempty feasible set:

```text
S_h ≠ ∅
```

such that:

```text
S_h(u) = S_h
```

for every `u ∈ U`.

Because `S_h` is nonempty and `J_h` is finite-valued and nonnegative:

```text
V_h(u) < +∞
```

for every `u ∈ U`.

Suppose a certified finite constant satisfies:

```text
0 ≤ B_h < +∞
```

and:

```text
|J_h(θ;u) - J_h(θ;u₀)|
≤
B_h
```

for every:

```text
θ ∈ S_h
```

and every:

```text
u ∈ U
```

Then:

```text
|V_h(u) - V_h(u₀)|
≤
B_h
```

for every `u ∈ U`.

#### Proof

The pointwise upper inequality gives:

```text
J_h(θ;u)
≤
J_h(θ;u₀) + B_h
```

for every `θ ∈ S_h`.

Taking infima over the same feasible set gives:

```text
V_h(u)
≤
V_h(u₀) + B_h
```

The same absolute-value bound also gives the reverse inequality:

```text
V_h(u₀)
≤
V_h(u) + B_h
```

Therefore:

```text
|V_h(u) - V_h(u₀)|
≤
B_h
```

∎

When `S_h(u)` changes with `u`, a pointwise objective bound on a fixed state does not by itself bound the optimized values. Perturbation-dependent feasibility must be handled by direct value envelopes or a certified correspondence between feasible sets.

### Weighted least-squares example

Let `W` be a fixed symmetric positive-semidefinite weighting matrix, and let:

```text
||·||_W
```

denote its associated seminorm.

If `W` varies with `u`, its perturbation must be included in the objective-difference bound.

Suppose on a common feasible set:

```text
J_h(θ;u)
=
||ℓ_h(θ;u)||_W²
```

and:

```text
ℓ_h(θ;u)
=
ℓ_h(θ;u₀) + δ_h(θ;u)
```

with certified finite constants:

```text
0 ≤ K_h < +∞
```

and:

```text
0 ≤ ε_h < +∞
```

satisfying:

```text
||ℓ_h(θ;u₀)||_W ≤ K_h
```

and:

```text
||δ_h(θ;u)||_W ≤ ε_h
```

for every relevant `θ` and `u`.

Then:

```text
|J_h(θ;u) - J_h(θ;u₀)|
≤
2K_h ε_h + ε_h²
```

and Proposition 4B permits:

```text
B_h
=
2K_h ε_h + ε_h²
```

This bound is valid only when the stated residual, feasible-set, weighting, and dependency assumptions are certified.

A bound on raw wrapped-phase error alone does not automatically produce this optimized-score bound.

---

## 13. Local Gauge-Fixed State Stability

Candidate-score separation does not establish continuous-state stability.

For a local state-stability claim, fix the uniformly selected candidate:

```text
h★ = (b★,n★)
```

and use a justified gauge-fixed representation.

For every:

```text
u ∈ U
```

let:

```text
X̃_u
```

denote a complete gauge-fixed coordinate domain for the winning candidate under perturbation `u`.

Let:

```text
χ_u : X̃_u → S_{h★}(u)
```

be a certified coordinate-realization map into the exact compatible state set.

The realization must be complete over the entire exact compatible set at the quotient level:

```text
q_{b★}(χ_u(X̃_u))
=
q_{b★}(S_{h★}(u))
```

No gauge-equivalence class in `S_{h★}(u)` may be excluded merely because it was not initially considered claim-relevant.

The winning-candidate objective must be gauge-consistent on the represented compatible set. In particular, either:

```text
q_{b★}(θ₁) = q_{b★}(θ₂)
⇒
J_{h★}(θ₁;u) = J_{h★}(θ₂;u)
```

for all represented `θ₁,θ₂ ∈ S_{h★}(u)`, or another certified representative rule must establish that the chosen gauge-fixed realization preserves the exact optimized value and minimizer semantics.

Coordinate points representing the same gauge-fixed physical state must also have identical claim semantics.

Define the perturbation-specific gauge-fixed claim map:

```text
g_u
=
r_{h★} ∘ q_{b★} ∘ χ_u
:
X̃_u → Z
```

Let:

```text
X̃ ⊆ ℝ^p
```

be the common coordinate domain used for cross-perturbation comparison.

Fix one norm:

```text
||·||_X
```

on the ambient vector space:

```text
ℝ^p
```

and use its restriction to differences of points in `X̃`.

Proposition 4C applies only under one of the following two certified domain conditions.

### Common-domain form

For every `u ∈ U`:

```text
X̃_u = X̃
```

and define:

```text
Φ_u = id_X̃
```

### Certified reparameterized-domain form

For every `u ∈ U`, there is a certified bijection:

```text
Φ_u : X̃_u → X̃
```

with certified inverse:

```text
Φ_u⁻¹ : X̃ → X̃_u
```

For every `u ∈ U`, the common-coordinate norm `||·||_X` must have a certified physical interpretation after application of `Φ_u`.

When a native metric or norm is used on `X̃_u`, the report must provide a certified conversion or distortion bound connecting that native geometry to displacement measured in `||·||_X`.

Under either domain form, the correspondence must preserve:

- feasibility and coordinate realization in both directions;
- exact objective values and global minimizers;
- gauge-equivalence semantics;
- the claim-relevant physical state represented in the common coordinates;
- and the certified physical interpretation of displacement measured in the common-coordinate norm `||·||_X`.

After defining `Φ_u` for either path, define the common-coordinate objective once by:

```text
F_u(y)
=
J_{h★}(
  χ_u(Φ_u⁻¹(y));
  u
)
```

for every:

```text
y ∈ X̃
```

The coordinate construction must preserve the exact winning-candidate optimized value:

```text
inf_{y∈X̃} F_u(y)
=
V_{h★}(u)
```

for every `u ∈ U`.

Let:

```text
g : X̃ → Z
```

be the common gauge-fixed physical claim map. Require:

```text
g(Φ_u(x))
=
g_u(x)
=
r_{h★}(
  q_{b★}(χ_u(x))
)
```

for every `x ∈ X̃_u`.

The fixed norm `||·||_X` must represent the declared common comparison metric after coordinate realization and reparameterization. Any native source-domain geometry must be linked to this norm by a certified conversion or distortion bound.

Let:

```text
X ⊆ X̃
```

be a common nonempty convex region.

The reparameterization-preservation requirement, strong-convexity constant, displacement result, and claim-map Lipschitz bound all use `||·||_X`.

Define the global minimizer set:

```text
M_u
=
arg min_{x∈X̃} F_u(x)
```

and let:

```text
M₀ = M_{u₀}
```

for the nominal instance.

Whenever both the coordinate and original winning-candidate minima are attained, the realization and reparameterization must preserve the physical minimizer set modulo gauge:

```text
q_{b★}(
  χ_u(
    Φ_u⁻¹(M_u)
  )
)
=
q_{b★}(M_{h★}(u))
```

where maps applied to sets denote their set-valued images.

### Proposition 4C — Strong-convexity stability bound

Under Assumption A11 and the optimization-complete coordinate construction specified above, assume:

1. for every `u ∈ U`, `F_u` attains a global minimum over `X̃`;
2. every global minimizer lies in `X`:

```text
M_u ⊆ X
```

3. one common finite constant satisfies:

```text
0 < μ < +∞
```

and every restriction `F_u|_X` is `μ`-strongly convex on `X` with respect to `||·||_X`, meaning that for every `x,y ∈ X` and every `t ∈ [0,1]`:

```text
F_u(tx+(1-t)y)
≤
tF_u(x)
+
(1-t)F_u(y)
-
(μ/2)t(1-t)||x-y||_X²
```

4. and one certified finite constant satisfies:

```text
0 ≤ η < +∞
```

together with:

```text
sup_{x∈X}
|F_u(x) - F_{u₀}(x)|
≤
η
```

for every `u ∈ U`.

Then, for every `u ∈ U`, the global minimizer set is a singleton:

```text
M_u = {x_u}
```

and the nominal minimizer set is:

```text
M₀ = {x₀}
```

The unique minimizers satisfy:

```text
||x_u - x₀||_X
≤
2√(η/μ)
```

for every `u ∈ U`.

#### Proof

Because every global minimizer lies in `X`, and `F_u|_X` is strongly convex, there can be at most one global minimizer in `X`.

Assumption 1 guarantees existence of a global minimizer over `X̃`, and Assumption 2 places that minimizer in `X`.

Therefore:

```text
M_u = {x_u}
```

for every `u ∈ U`, including:

```text
M₀ = {x₀}
```

Applying the strong-convexity inequality to `x₀` and `x_u`, using the minimality of `x₀`, and letting the interpolation parameter tend to zero gives the quadratic-growth bound:

```text
F_{u₀}(x_u)
≥
F_{u₀}(x₀)
+
(μ/2)||x_u-x₀||_X²
```

The uniform objective perturbation bound gives:

```text
F_{u₀}(x_u)
≤
F_u(x_u) + η
≤
F_u(x₀) + η
≤
F_{u₀}(x₀) + 2η
```

Combining the inequalities yields:

```text
(μ/2)||x_u-x₀||_X²
≤
2η
```

and therefore:

```text
||x_u-x₀||_X
≤
2√(η/μ)
```

∎

### Claim-space displacement

Let:

```text
d_Z
```

be a predeclared metric or pseudometric on the physical claim space `Z`.

If `d_Z` is a pseudometric, distinct physical claims may have zero distance. In that case the resolution-cell margin may be zero and the margin test below cannot certify class preservation.

Let:

```text
g|_X : X → Z
```

denote the restriction of the previously declared common claim map `g : X̃ → Z`.

Suppose one finite constant satisfies:

```text
0 ≤ L < +∞
```

and `g|_X` is `L`-Lipschitz with respect to the same `d_Z` and `||·||_X`:

```text
d_Z(g|_X(x),g|_X(y))
≤
L||x-y||_X
```

for every `x,y ∈ X`.

Then:

```text
d_Z(g|_X(x_u),g|_X(x₀))
≤
2L√(η/μ)
```

for every `u ∈ U`.

### Corollary 3 — Report-class preservation by cell margin

Let:

```text
z₀ = g|_X(x₀)
```

and define the resolution-cell margin:

```text
m_ρ(z₀)
=
inf {
  d_Z(z₀,z) :
  ρ(z) ≠ ρ(z₀)
}
```

using:

```text
m_ρ(z₀) = +∞
```

when no alternative report class exists.

If:

```text
2L√(η/μ)
<
m_ρ(z₀)
```

then:

```text
ρ(g|_X(x_u))
=
ρ(z₀)
```

for every `u ∈ U`.

Thus the local state may move while the report class remains perturbation-stable.

If:

```text
m_ρ(z₀) = 0
```

—for example because the nominal claim lies on a report-cell boundary, because distinct report classes have zero pseudometric separation, or because alternative classes approach arbitrarily closely—this margin test cannot certify class preservation.

### Jacobian and geometry note

A positive smallest singular value of one Jacobian at one point:

```text
σ_min(A(x₀)) > 0
```

is not, by itself, a global uniqueness or perturbation-stability certificate.

It may contribute to a local strong-convexity or inverse-function argument only when:

- the gauge has been removed;
- the singular-value bound is valid on a declared neighborhood;
- nonlinear remainder terms are controlled;
- the correct norm and weighting are used;
- and competing minima outside the neighborhood are excluded.

A condition number or geometry score is a diagnostic unless connected to a proved state or claim-space bound.

---

## 14. Outliers, Masks, Robust Losses, and Contamination

Outlier handling must be declared before the final result.

Permitted approaches include:

- a predeclared robust loss;
- a predeclared finite family of sensor masks;
- a bounded-contamination uncertainty set;
- a mixture or alternate-model branch;
- or a certified adversarial corruption budget.

If sensor removal, down-weighting, or masking can change the candidate or report-class winner, that choice must be included in `U`, in `D`, or in another declared branch domain.

The following are not certified by this theorem:

- deleting sensors after inspecting residuals without branching over the deletion rule;
- tuning thresholds until one candidate wins;
- treating every large residual as evidence corruption;
- assuming retained sensors are independent after selection;
- or calling a heuristic robustness score an integrity probability.

Residual thresholds may support a declared consistency check, but consistency is not authenticity.

---

## 15. Certificate Status and Interpretation

### 15.1 Candidate certificate

If:

```text
V̄_{h★}
<
inf_{h≠h★} V̲_h
```

then candidate selection is uniformly certified over `U`.

If the certified envelopes overlap or touch:

```text
V̄_{h★}
≥
inf_{h≠h★} V̲_h
```

then the candidate-separation certificate is inconclusive.

An inconclusive certificate does not prove that the candidate changes under perturbation. It means the selected bounds do not establish invariance.

### 15.2 Report-class certificate

If:

```text
V̄_{c★}^rep
<
inf_{c≠c★} V̲_c^rep
```

then the score-minimizing report-class index is uniformly certified over `U`.

A claim that every attained globally minimizing compatible state maps to `c★` additionally requires Assumption A9.

If the class envelopes overlap or touch, report-class recovery remains pending under this certificate.

### 15.3 Local-state certificate

A candidate or class may be uniformly selected while the continuous state remains broad, disconnected, or unstable.

Local state stability is established only when the separate conditions of Proposition 4C or another valid certified stability argument hold.

### 15.4 Relationship to Theorem 3 closure

For each `u`:

```text
C_rep(u) ≠ ∅
⇒
C_min(u) ⊆ C_rep(u)
```

This score-index inclusion does not require Assumption A9. When `C_rep(u) ≠ ∅`, at least one report-class score is finite; therefore every minimizing class index also has finite score and corresponds to a nonempty report class.

Assumption A9 is needed only for the further conclusion that an attained globally minimizing compatible candidate-state pair exists and maps to a member of `C_min(u)`.

If `C_rep(u) = ∅`, any all-`+∞` score-index tie over `C_U` is not a selected physical report class.

Uniform score selection does not establish the full set `C_rep(u)`.

Conversely, Theorem 3 report-class closure does not establish an objective winner unless the score comparison required by Theorem 4 is separately certified.

---

## 16. Search and Perturbation Completeness

A perturbation-stability claim requires, as applicable:

- complete finite coverage of `D` over all `u ∈ U`;
- complete material branch generation;
- a predeclared perturbation set;
- explicit perturbation dependencies and correlations;
- total claim and report maps;
- comparable objective semantics across candidates;
- global optimized-value bounds;
- certified perturbation-dependent feasibility;
- complete class coverage for a class-separation claim;
- conservative numerical and interval arithmetic;
- treatment of score ties and boundary equality;
- declared handling of missingness and contamination;
- reproducible optimization and traversal;
- retained audit records for rejected bounds and branches;
- and disclosure of perturbations or model families outside `U`.

The report must distinguish:

- nominal winner;
- uniformly certified candidate winner;
- uniformly certified report-class winner;
- fit-threshold consistency;
- local continuous-state stability;
- resolution-cell stability;
- Theorem 3 admissibility and report closure;
- AIRS inference classification;
- and evidence-integrity status.

---

## 17. Certificate Failure and Non-Applicability Conditions

The candidate, report-class, or local-state conclusions are not established through the selected path when any applicable condition below is unresolved:

- incomplete candidate coverage over `U`;
- an empty candidate domain;
- use of an objective that can take `+∞` while absolute-difference expressions are applied;
- an undeclared perturbation that can affect feasibility or score ordering;
- hidden branch, mask, contamination, calibration, path, or association alternatives;
- incomparable objective scales across candidates;
- post-hoc objective, weight, threshold, mask, or resolution selection;
- local minima treated as global optimized values;
- failure to certify perturbation-dependent feasible sets;
- raw measurement-error bounds treated directly as optimized-score bounds without a valid derivation;
- score envelopes that omit numerical or interval error;
- omission of an alternative report class without a certified lower bound participating in the strict separation condition;
- non-strict candidate or class separation presented as a uniqueness certificate;
- failure of global-minimum attainment where a selected-state claim is made;
- application of Proposition 4C without Assumption A11, complete gauge-fixed coordinate domains, optimization-complete coordinate-realization maps, one common comparison domain, and uniformly defined identity or bijective maps `Φ_u`;
- coordinate realization that fails to cover the complete quotient image `q_{b★}(S_{h★}(u))`;
- a coordinate realization or reparameterization that fails to preserve feasibility, exact optimized values, physical minimizer sets modulo gauge, gauge-consistent objective semantics, claim semantics, or a certified physical interpretation of displacement in `||·||_X`;
- use of a native source-domain metric without a certified conversion or distortion bound into the common-coordinate norm;
- mixing the Corollary 2 absolute-difference path with infinite optimized candidate values without a separately stated direct-envelope argument;
- use of an undeclared or inconsistent claim-space metric or pseudometric;
- use of an undeclared, inconsistent, or infinite perturbation, Lipschitz, fit-threshold, residual, or optimized-value certificate constant;
- defining a point-valued minimizer before existence and uniqueness are certified;
- unfixed or unquotiented gauge in a state-stability claim;
- one-point Jacobian rank treated as global observability;
- strong convexity claimed only at one point;
- no exclusion of lower minima outside the local stability region;
- report-cell boundary margin equal to zero or uncertified;
- post-hoc outlier deletion without a declared branch or robust model;
- unmodeled covariance or shared dependencies;
- or excluded perturbations presented as disproven.

---

## 18. Prohibited Interpretations and Claims Not Established

Theorem 4 does **not** establish:

- that the score-minimizing candidate is physically true;
- that non-winning candidates are inadmissible;
- that the declared perturbation set contains all real-world errors;
- exact continuous-state uniqueness from candidate separation alone;
- report-class stability from candidate stability alone;
- global stability from local strong convexity alone;
- observability from one Jacobian singular value alone;
- a calibrated probability of correctness;
- a calibrated confidence level;
- evidence authenticity;
- absence of editing;
- malicious or non-malicious intent;
- causality;
- forensic validity;
- or certified real-world performance.

The labels “robust,” “stable,” and “recovered” are valid only relative to:

- the declared candidate domain;
- the declared perturbation set;
- the declared objective;
- the certified global score bounds;
- the declared gauge;
- and the declared reporting resolution.

A heuristic score combining separation, fit, and geometry may be reported as a diagnostic index only when clearly labeled as uncalibrated. It must not be presented as an integrity probability or posterior confidence without an independent calibration theorem and validation evidence.

---

## 19. Relationship to AIRS Draft 0.1

This theorem is an informative mathematical specialization of AIRS provisions concerning:

- declared hypothesis spaces;
- retained and admissible solutions;
- uncertainty and dependency;
- global versus local optimization;
- perturbation analysis;
- observability and gauge;
- report resolution;
- multiple admissible solutions;
- non-resolvable outcomes;
- searched-space versus exhaustive conclusions;
- inference classification;
- integrity status;
- and prohibited output styles.

A uniformly stable score winner does not automatically justify:

- **Resolved Within the Declared Model**;
- **Provisionally Resolved Within the Searched Hypothesis Space**;
- or any other AIRS primary inference classification.

AIRS classification additionally depends on admissibility, search completeness, surviving-hypothesis structure, separability at the required resolution, and the controlling AIRS definitions.

Where this theorem conflicts with AIRS Draft 0.1, AIRS Draft 0.1 controls.

---

## 20. Validation Requirements

Before implementation claims are made, Theorem 4 should be exercised with cases covering at least:

1. one uniformly separated candidate;
2. two candidates with overlapping certified score envelopes;
3. equality at the candidate-separation boundary;
4. a nominal winner that changes under an allowed perturbation;
5. a nominal winner that remains stable with `G₀ > 2B`;
6. failure of the `2B` condition despite actual empirical stability;
7. candidate stability with multiple continuous minimizers;
8. candidate stability with multiple report classes inside the winning candidate;
9. report-class stability with multiple winning candidates;
10. one candidate changing while the winning report class remains fixed;
11. one report class changing while the discrete candidate remains fixed;
12. a finite perturbation set;
13. an interval or continuum perturbation set;
14. perturbation-dependent candidate feasibility;
15. a conservative union candidate domain over `U`;
16. a candidate infeasible for some perturbations and feasible for others;
17. certified `+∞` lower bounds from emptiness;
18. an uncertified optimizer failure incorrectly treated as infeasibility;
19. fixed-feasible-set pointwise objective perturbation;
20. variable-feasible-set failure of Proposition 4B;
21. weighted least-squares score perturbation with a valid residual bound;
22. raw measurement-error bounds that do not yield a finite optimized-score bound;
23. correlated residual perturbations;
24. perturbation-dependent objective weights;
25. incomparable objective normalization across branches;
26. a uniformly best candidate that fails the fit threshold;
27. multiple candidates that all pass the fit threshold;
28. a score threshold selected post hoc;
29. a valid gauge-fixed strong-convexity example;
30. an unfixed gauge producing a flat direction;
31. a one-point positive singular value without a uniform neighborhood bound;
32. a lower competing minimum outside the local stability region;
33. verification of the bound `2√(η/μ)`;
34. a Lipschitz claim map and certified claim-space displacement;
35. report-class preservation with positive cell margin;
36. failure of the margin test at a resolution boundary;
37. a disconnected state set;
38. a robust loss declared before evaluation;
39. a post-hoc outlier deletion that changes the winner;
40. a predeclared finite sensor-mask family;
41. bounded adversarial contamination;
42. hidden contamination alternatives outside `U`;
43. a stable winner with incomplete candidate search;
44. a stable score winner that is not the only Theorem 3 admissible candidate;
45. Theorem 3 report closure without a stable objective winner;
46. a stable report class without candidate-level closure;
47. a heuristic separation-fit-geometry index correctly labeled uncalibrated;
48. an invalid conversion of that index into a probability;
49. separate evidence-integrity and inference-classification reporting;
50. reproducibility of global lower and upper score bounds;
51. conservative numerical treatment of strict gap boundaries;
52. auditability of all masks, branches, and perturbation bounds;
53. confirmation that candidate-envelope overlap is inconclusive rather than proof of instability;
54. confirmation that report-class-envelope overlap is inconclusive rather than proof of class change;
55. a strongly convex objective on an open domain with no attained minimum, confirming that strong convexity alone does not prove existence;
56. explicit global-minimum attainment over `X̃` with all minimizers confined to `X`;
57. a singleton candidate domain in which the nominal `G₀` and competing-candidate `max` formulas are not used;
58. a report-class infimum upper bound without attainment, distinguished from a witness-based attained-score certificate;
59. a finite candidate infimum upper bound without a witness, distinguished from certified nonemptiness and attained-score claims;
60. an empty alternative report-class set producing `m_ρ(z₀) = +∞`;
61. singleton candidate and report-class domains handled through `inf ∅ = +∞`;
62. a candidate with `V_h(u₀) = +∞` or `V_h(u) = +∞`, confirming that the absolute-difference `B_h` formulation is inapplicable;
63. a nonempty common feasible set for Proposition 4B;
64. an empty common feasible set demonstrating why `|+∞-(+∞)|` is not used;
65. a changing perturbation-dependent feasible domain that fails Proposition 4C without a certified common-domain representation;
66. certified bijections `Φ_u : X̃_u → X̃` preserving feasibility, objective values, global minimizers, gauge semantics, and claims, together with a certified physical interpretation of displacement in `||·||_X`;
67. a reparameterization that distorts native geometry without a certified conversion or distortion bound, making the state-displacement conclusion inapplicable;
68. verification of `V_min(u) = min_{c∈C_U} V_c^rep(u)` under attained global minimization;
69. a finite nonempty candidate domain with candidate-index attainment but no attained continuous-state minimizer;
70. an all-infeasible perturbation instance with `V_min(u) = +∞` and `H_min(u) = D`;
71. a finite-valued objective confirming `V_h(u) = +∞` exactly when `S_h(u) = ∅`;
72. modular Proposition 4A testing in which `C_min(u) = {c★}` holds without A9, followed by a separate attained-state test using A9;
73. alternative-class lower-bound coverage without unnecessary alternative-class upper bounds;
74. an omitted alternative class lacking a certified lower bound, making class separation inapplicable;
75. one fixed norm `||·||_X` used consistently for strong convexity, reparameterization, displacement, and Lipschitz bounds;
76. a fixed positive-semidefinite weighting matrix and associated seminorm;
77. a perturbation-dependent weighting matrix whose effect is included in the objective-difference bound;
78. notation review confirming unambiguous indexed forms such as `ψ_{h_u}`, `J_{h_u}`, and `V_{c_u}^rep`;
79. an empty global report-class domain `C_U = ∅` with `C_min(u) = ∅`;
80. a nonempty `C_U` with `C_rep(u) = ∅`, producing an all-`+∞` score-index tie that is not interpreted as a physical report-class selection;
81. a finite designated-class upper bound confirming that Proposition 4A excludes the all-infeasible perturbation case;
82. a certified coordinate-realization map `χ_u : X̃_u → S_{h★}(u)` with complete gauge-fixed physical-state coverage;
83. a coordinate realization that fails to preserve objective or claim semantics, making Proposition 4C inapplicable;
84. a predeclared metric `d_Z` used consistently in the Lipschitz and resolution-margin conditions;
85. a pseudometric with distinct zero-distance claims and a zero resolution-cell margin;
86. a fit-threshold result at the optimized-infimum level without an attained compatible state;
87. an attained fit-threshold witness or attainment result;
88. a family-level lower-bound certificate covering every member of a declared alternative-class family;
89. confirmation that no alternative class is excluded from the strict-separation infimum;
90. quotient-complete coordinate realization satisfying `q_{b★}(χ_u(X̃_u)) = q_{b★}(S_{h★}(u))`;
91. a coordinate realization that omits a feasible gauge class affecting the global optimum;
92. gauge-consistent objective values on equivalent states or a certified objective-preserving representative rule;
93. verification that `inf_{y∈X̃} F_u(y) = V_{h★}(u)`;
94. verification that attained coordinate minimizers map onto `M_{h★}(u)` modulo gauge;
95. declaration of `||·||_X` before every use in reparameterization and stability conditions;
96. a nonempty `C_rep(u)` confirming `C_min(u) ⊆ C_rep(u)` without A9;
97. a nonempty `C_U` for which the report-class score infimum is not attained and `C_min(u) = ∅`;
98. Proposition 4A preventing report-class-index nonattainment through a finite designated-class upper bound and strict separation;
99. a separate A9 test establishing an attained globally minimizing compatible state;
100. one common comparison domain `X̃` and norm `||·||_X` declared before the common-domain and reparameterized-domain alternatives;
101. the common-domain path with `Φ_u = id_X̃`;
102. the reparameterized-domain path with certified bijective `Φ_u`;
103. one common definition of `F_u` used after both domain paths;
104. explicit application of Assumption A11 in Proposition 4C;
105. finite constants `B_h`, `B`, `τ_fit`, `K_h`, `ε_h`, `η`, and `L`;
106. a certified conversion or distortion bound from a native source-domain metric into the common-coordinate norm `||·||_X`;
107. consistent indexed notation including `V_{h★}`, `V_{h₀}`, `B_{h₀}`, `ψ_{h★}`, `M_{h★}`, and `S_{h★}`;
108. direct verification of the stated `μ`-strong-convexity inequality with `0 < μ < +∞`;
109. use of the restricted claim map `g|_X` in the Lipschitz and displacement conclusions;
110. zero report-cell margin caused respectively by a cell boundary, zero pseudometric separation, and arbitrarily close alternative classes;
111. a norm defined on the ambient vector space `ℝ^p` and restricted to differences of points in `X̃`;
112. direct verification of the quadratic-growth step used in Proposition 4C;
113. separate treatment of finite-score candidates through Corollary 2 and infinite-score candidates through the direct-envelope path;
114. confirmation that a stable winner does not establish physical truth;
115. and independent review of mathematical correctness, optimization certification, perturbation completeness, numerical robustness, classification use, repository control, release control, and empirical applicability.

Evaluation must distinguish:

- correctness of the candidate-separation theorem;
- correctness of the report-class-separation proposition;
- correctness of optimized-value perturbation bounds;
- validity of global optimization certificates;
- completeness of `D`;
- completeness of `U`;
- gauge treatment;
- local-state stability;
- resolution-cell stability;
- fit-threshold semantics;
- AIRS classification correctness;
- evidence-integrity reporting;
- and real-world validation.

---

## 21. Revision History

| Version | Date | Change |
|---|---|---|
| 1.0 | 2026-07-11 | Frozen final release. Defined `||·||_X` on the ambient vector space `ℝ^p`; made the quadratic-growth derivation in Proposition 4C explicit; aligned validation items with the certified conversion-or-distortion treatment of source-domain geometry; clarified that candidates with infinite optimized values lie outside Corollary 2 and must be handled through a separately stated direct-envelope path; changed repository metadata from freeze-candidate review to final frozen release; and superseded the prior image-only Theorem 4. |
| 0.9 | 2026-07-11 | Advanced the document to freeze-candidate review; replaced the undefined source-domain norm-preservation requirement with a certified physical interpretation and conversion-or-distortion requirement for the common-coordinate norm; standardized indexed notation throughout; made the finite `μ`-strong-convexity convention explicit; used the restriction `g|_X` consistently in claim-space displacement; expanded the zero-margin explanation to include cell boundaries, pseudometric degeneracy, and arbitrarily close alternative classes; renamed A9 to reflect certified attainment arguments; and expanded failure and validation provisions. |
| 0.8 | 2026-07-11 | Moved the common comparison domain and norm outside the two coordinate-domain alternatives; defined `Φ_u` uniformly as the identity in the common-domain path or a certified bijection in the reparameterized path; defined the common-coordinate objective `F_u` once after both paths; stated that `C_min(u)` may be empty when a report-class score infimum is not attained and explained why Proposition 4A prevents that case; made Proposition 4C explicitly depend on A11 and the optimization-complete coordinate construction; standardized the winning branch as `h★ = (b★,n★)` with indexed notation `q_{b★}`, `r_{h★}`, `J_{h★}`, and `M_{h★}`; required all perturbation, Lipschitz, fit-threshold, residual, and optimized-value certificate constants to be finite; and expanded failure and validation provisions. |
| 0.7 | 2026-07-11 | Made the gauge-fixed coordinate realization optimization-complete by requiring full quotient coverage, gauge-consistent objective semantics or an equivalent certified representative rule, exact optimized-value preservation, and attained minimizer-set preservation modulo gauge; harmonized Section 6.2 with A8 so every alternative class participates in the strict-separation certificate; simplified the Theorem 3 relationship to show `C_min(u) ⊆ C_rep(u)` whenever `C_rep(u) ≠ ∅` without requiring A9; moved declaration of the common norm `||·||_X` before its first use; separated score-level and attained-minimizer interpretations in Proposition 4A; clarified A9 as one of several sufficient attainment routes; and expanded failure and validation provisions. |
| 0.6 | 2026-07-11 | Added explicit handling for `C_U = ∅` and perturbation-specific `C_rep(u) = ∅`, including the distinction between an all-`+∞` score-index tie and a physical report-class selection; introduced certified coordinate-realization maps `χ_u` to type the gauge-fixed objective and claim constructions correctly; declared a common claim-space metric or pseudometric `d_Z`; qualified fit-threshold conclusions as optimized-infimum claims unless a witness or attainment result is certified; tightened alternative-class coverage so no class is excluded from the strict-separation infimum while permitting family-level lower-bound certificates; removed a duplicate Proposition 4A conclusion; corrected Section 6 and A8 spacing; refined Theorem 3 relationship wording; and expanded failure and validation provisions. |
| 0.5 | 2026-07-11 | Made every objective `J_h` finite-valued so that `V_h(u) = +∞` exactly represents an empty compatible set; required `D` to be finite and nonempty and separated candidate-index attainment from continuous-state attainment; removed A9 from the candidate-score theorem and modularized Proposition 4A so score-level class selection does not require A9 while attained state-level mapping does; replaced the omitted-class provision with explicit designated-class upper and alternative-class lower bounds; fixed one common norm `||·||_X` for reparameterization, strong convexity, displacement, and Lipschitz claims; clarified Proposition 4B finiteness and reverse-inequality wording; standardized indexed notation; and expanded failure and validation provisions. |
| 0.4 | 2026-07-11 | Restricted the `B_h` absolute-difference corollary to finite optimized values and directed infinite-value candidates to direct score envelopes; required a common nonempty feasible set in Proposition 4B; formalized perturbation-dependent gauge-fixed domains and certified bijections into one common domain for Proposition 4C, including preservation of feasibility, objective values, global minimizers, gauge semantics, claim semantics, and the displacement metric; stated the identity `V_min(u) = min_{c∈C_U} V_c^rep(u)` under attained global minimization; corrected singleton validation wording; changed draft repository metadata from `Supersedes` to `Draft replacement for`; and expanded failure and validation provisions. |
| 0.3 | 2026-07-11 | Harmonized candidate and report-class upper-bound semantics by separating certified nonemptiness from witness and attained-score claims; rewrote the Proposition 4A proof to use global attainment explicitly; required one common complete gauge-fixed feasible domain, or a certified reparameterization into one, for Proposition 4C; removed a redundant local-state assumption; harmonized singleton candidate and report-class cases through the convention `inf ∅ = +∞`; specified a fixed symmetric positive-semidefinite weighting matrix and associated seminorm for the weighted least-squares example, with perturbation-dependent weights included in the objective-difference bound; corrected Section 13 spacing; and expanded failure and validation provisions. |
| 0.2 | 2026-07-11 | Corrected Proposition 4C by separating the complete gauge-fixed feasible domain from the common convex stability region, requiring global-minimum attainment and minimizer confinement before defining unique point minimizers, and retaining the certified `2√(η/μ)` displacement bound; renamed weighted least-squares residual symbols to avoid collision with the claim map `r_h` and report set `R_h`; clarified that a finite report-class value upper bound establishes nonemptiness but requires a witness or attainment result for an attained-score claim; added extended-real and empty-alternative conventions, singleton-domain handling, and an infinite report-cell margin when no alternative class exists; and expanded failure and validation provisions. |
| 0.1 | 2026-07-11 | Initial AIRS-compatible theorem draft replacing the image-only robust-recovery/integrity claim with separate certified results for uniform candidate-score separation, report-class-score separation, nominal-gap stability, optimized-value perturbation bounds, local gauge-fixed state stability, and resolution-cell preservation; formalized the `G₀ > 2B` rule as a corollary requiring bounds on globally optimized scores; separated fit consistency, admissibility, AIRS classification, and evidence-integrity status; and prohibited post-hoc outlier handling and uncalibrated integrity claims. |

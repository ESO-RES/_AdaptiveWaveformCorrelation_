# Theorem 3 — Conditional Resolution-Level Report Closure and Classification

```text
Document ID: AWC-THM-3-1.0
Version: Frozen 1.0
Status: Conditional mathematical result
Applies to: AIRS Draft 0.1, AWC-THM-1-0.5, and AWC-THM-2-0.7
Normative status: Informative and non-normative
Validation status: Not independently validated
Supersedes: AWC-THM-3-0.9
Repository status: Final frozen release
Obsoletes: Prior 1.0 freeze-candidate working artifact, repository alias AWC-THM-3-1.0-rc1
```

## 1. Purpose

This theorem states sufficient conditions under which a finite exact or conservative hypothesis domain can be evaluated to establish the complete report-class image of the admissible solution set at a predeclared resolution.

Resolution-level report closure is weaker than candidate-level closure and exact state-set constraint closure. Full constraint closure may be claimed only when the corresponding stronger conditions are independently satisfied.

Report-class cardinality is also distinct from AIRS inference classification. AIRS classification additionally depends on search completeness, the number and structure of surviving hypotheses, boundedness, separability, and the required resolution.

The theorem separates four distinct questions:

1. whether the applicable discrete hypothesis domain was covered completely;
2. whether each candidate's exact report-class image was enclosed with certification and, when state-level claims are made, whether its continuous state set was characterized or bounded;
3. whether gauge-equivalent parameterizations were identified as one physical outcome;
4. and whether the resulting physical outcomes are distinguishable at the declared reporting resolution.

The theorem does **not** convert model compatibility into physical truth, authenticity, absence of editing, causality, or forensic validity.

---

## 2. Relationship to Theorems 1 and 2

Theorem 1 conditionally forms bounded-error, same-event, pairwise propagation-time-difference hypotheses indexed by integer cycles.

Theorem 2 converts the unbounded integer-cycle ambiguity into:

- an exact declared-bound raw domain `H_raw`;
- a conservative finite-precision domain `Ĥ_raw`;
- exact compatible continuous state sets `S_b,n_b`;
- and the equality:

```text
Ĥ_cons = H_cons
```

under complete certified filtering.

Theorem 3 begins after those measurement-formation and finite-domain conditions have been satisfied. It addresses complete global constraint evaluation, physical equivalence, and resolution-safe reporting.

---

## 3. Candidate and State-Set Notation

Let the applicable finite enumeration domain be:

```text
D =
H_raw
```

when exact endpoint decisions are certified, or:

```text
D =
Ĥ_raw
```

when conservative outward-rounded enumeration is required.

Let the jointly consistent discrete set established by Theorem 2 be denoted:

```text
H_cons^(2)
```

For each candidate:

```text
h = (b,n_b) ∈ D
```

let:

```text
S_h^(2)
```

denote its compatible continuous state set under the constraints inherited from Theorem 2.

Let:

```text
S_h
=
{
  θ ∈ Ω_b :
  all inherited Theorem 2 constraints hold,
  together with all declared timing, propagation,
  geometry, calibration, branch, dependency,
  and other Theorem 3 model constraints,
  including any explicitly declared
  evidence-validity, acquisition-history,
  or alternate-model branch assumptions
}
```

be its exact compatible continuous state set for Theorem 3.

Define the Theorem 3 admissible discrete set:

```text
H_adm
=
{
  h ∈ D :
  S_h ≠ ∅
}
```

Under Assumption A2a:

```text
S_h ⊆ S_h^(2)
```

for every `h ∈ D`, and therefore:

```text
H_adm ⊆ H_cons^(2)
```

When:

```text
h ∈ Ĥ_raw \ H_raw
```

Theorem 2 gives:

```text
S_h^(2) = ∅
```

and hence:

```text
S_h = ∅
```

Equality:

```text
H_adm = H_cons^(2)
```

holds only when Theorem 3 adds no constraints beyond those already represented in Theorem 2.

---

## 4. Gauge and Physical Equivalence

For each branch `b`, let `G_b` denote the declared gauge action on `Ω_b`.

Gauge directions may include, when justified:

- additive event-time shift;
- working-time origin;
- unconstrained clock reference;
- global spatial translation;
- global spatial rotation;
- reflection or handedness;
- and scale when neither the time scale, propagation scale, nor spatial scale is fixed independently.

Every transformation in `G_b` must preserve:

- the admissible domain `Ω_b`;
- all modeled observables;
- all declared constraints;
- and all claim-relevant physical content.

A transformation that changes a reportable physical outcome is an ambiguity or branch alternative, not a gauge. Reflection, handedness, and scale are therefore not automatically gauges.

Let:

```text
q_b : Ω_b → Ω̄_b = Ω_b/G_b
```

be the quotient map from parameter states to gauge-equivalence classes.

Two parameter vectors that differ only by the declared gauge represent one physical state for this theorem.

Gauge freedom must be removed or quotiented before uniqueness, multiplicity, separation, diameter, or resolution is assessed.

---

## 5. Claim Map and Declared Resolution

Let `Z` be the declared physical reporting space. Examples include:

- source location in a declared coordinate frame;
- observer geometry;
- event-time differences;
- clock parameters;
- propagation parameters;
- or a declared tuple of claim-relevant quantities.

For each candidate `h = (b,n_b)`, define a claim map on the full quotient domain:

```text
r_h : Ω̄_b → Z
```

that reports only the quantities relevant to the stated conclusion.

Different branches or parameterizations may map to the same physical reported outcome.

Before examining the final result, declare a resolution map:

```text
ρ : Z → C
```

where `C` is the set of reportable resolution classes.

Define the total report-class map:

```text
ψ_h
=
ρ ∘ r_h ∘ q_b
:
Ω_b → C
```

The map `ρ` must specify:

- which physical quantities are being resolved;
- the coordinate system and units;
- gauge treatment;
- the required spatial, temporal, propagation, or parameter resolution;
- boundary conventions;
- and which branch distinctions are materially reportable.

A post-hoc resolution chosen to force uniqueness does not satisfy this assumption.

---

## 6. Exact Report Sets and Certificate Paths

For every candidate:

```text
h = (b,n_b) ∈ D
```

the exact compatible state set `S_h` is defined in Section 3, and the exact per-candidate report-class set is:

```text
R_h
=
{
  ψ_h(θ) :
  θ ∈ S_h
}
```

The exact report-class image of the admissible solution set is defined independently of the selected certificate path:

```text
C_rep
=
⋃_{h∈D} R_h
```

### 6.1 Full-domain certificate

For every candidate `h ∈ D`, let certified class-level bounds satisfy:

```text
R_h⁻ ⊆ R_h ⊆ R_h⁺
```

When state-level certificates are used, let:

```text
W_h ⊆ S_h ⊆ O_h ⊆ Ω_b
```

where:

- `W_h` is a certified feasible witness set;
- `O_h` is a certified outer state enclosure;
- `W_h ⊆ S_h` is guaranteed under the declared model and arithmetic treatment;
- `S_h ⊆ O_h` is guaranteed under the declared model and arithmetic treatment;
- and `O_h ⊆ Ω_b` ensures that the quotient, claim, and resolution maps are defined on the entire outer enclosure.

`W_h` may be empty even when `S_h` is nonempty if no feasible witness has yet been certified.

`O_h = ∅` certifies:

```text
S_h = ∅
```

A finite collection of isolated optimizer outputs is not, by itself, a certified outer enclosure. It may serve as an outer enclosure only when an independent exhaustiveness proof establishes that it contains the complete compatible state set. Failure to find a point does not certify emptiness.

A sufficient inner construction is:

```text
R_h⁻
=
{
  ψ_h(θ) :
  θ ∈ W_h
}
```

A sufficient outer construction is any certified set `R_h⁺` satisfying:

```text
{
  ψ_h(θ) :
  θ ∈ O_h
}
⊆
R_h⁺
```

This permits conservative report-image computation without claiming that a numerically computed outer image is exact.

For the full-domain certificate, define:

```text
C⁻
=
⋃_{h∈D} R_h⁻
```

and:

```text
C⁺
=
⋃_{h∈D} R_h⁺
```

### 6.2 Retained-domain certificate

When pruning is used, let `D_ret` and `D_pr` be the retained and pruned domains defined in Section 10.

For every retained candidate `k ∈ D_ret`, certified bounds satisfy:

```text
R_k⁻ ⊆ R_k ⊆ R_k⁺
```

For every pruned candidate `h ∈ D_pr`, a certified outer report-class enclosure satisfies:

```text
R_h ⊆ R_h⁺
```

No `W_h`, `O_h`, or `R_h⁻` need be constructed for a pruned candidate unless required by the selected certification method.

The retained-domain aggregate sets `C_ret⁻` and `C_ret⁺` are defined in Section 10.

---

## 7. Assumptions

### A1 — Valid upstream measurement formation

Every wrapped-phase observation used by this theorem satisfies the applicable conditions of Theorem 1 or is represented by a separately justified AIRS-compatible measurement model.

### A2 — Finite applicable discrete domain

The applicable candidate domain `D` is finite and is constructed under Theorem 2.

The report identifies whether:

```text
D = H_raw
```

or:

```text
D = Ĥ_raw
```

### A2a — Upstream compatible-set inheritance

For every candidate `h ∈ D`, the Theorem 3 admissible state set retains all applicable Theorem 2 compatibility requirements:

```text
S_h ⊆ S_h^(2)
```

Consequently:

```text
H_adm ⊆ H_cons^(2)
```

and, when:

```text
h ∈ Ĥ_raw \ H_raw
```

Theorem 2 gives:

```text
S_h^(2) = ∅
```

so:

```text
S_h = ∅
```

### A3 — Complete branch scope

Every material event-association, propagation-path, calibration, phase-support, source-class, explicitly declared evidence-validity, acquisition-history, alternate-model, and other discrete alternative within the declared theorem scope is:

- included in `D`;
- independently proven inadmissible;
- or explicitly excluded from the theorem scope with a stated limitation.

### A4 — Complete declared constraint model

Every constraint used to define `S_h` is declared before final classification, including applicable:

- timing observations;
- wrapped-phase intervals;
- clock offset, scale, and drift;
- event-dependent latency;
- propagation paths and environmental bounds;
- source and observer geometry;
- calibration;
- covariance and dependency;
- cycle closure;
- explicitly declared evidence-validity, acquisition-history, and alternate-model branches;
- and branch-consistency conditions.

Unmodeled dependencies must not be counted as independent evidence.

### A5 — Gauge treatment

All material gauge freedoms are fixed by justified references or represented by the quotient `Ω̄_b`.

Every declared gauge transformation preserves `Ω_b`, all modeled observables, all declared constraints, and all claim-relevant physical content.

### A6 — Predeclared total claim and resolution maps

For every candidate `h = (b,n_b) ∈ D`, including every candidate that is subsequently retained or pruned under the selected certificate path, the physical claim map:

```text
r_h : Ω̄_b → Z
```

and the report-class map:

```text
ψ_h
=
ρ ∘ r_h ∘ q_b
:
Ω_b → C
```

are defined before final classification.

All candidates use a common physical reporting space `Z`, a common resolution-class space `C`, and the common resolution map:

```text
ρ : Z → C
```

Branch-specific claim maps must have consistent report semantics across the complete domain `D`.

### A7 — Certified full-domain bounds

For the full-domain certificate, every candidate `h ∈ D` has certified report-class bounds satisfying:

```text
R_h⁻ ⊆ R_h ⊆ R_h⁺
```

under the declared parameter domain, constraints, tolerances, maps, and numerical-arithmetic treatment.

When state-level certificates are used for a candidate, they satisfy:

```text
W_h ⊆ S_h ⊆ O_h ⊆ Ω_b
```

The retained-domain path uses the candidate-specific requirements in A8 instead of requiring `R_h⁻` for every pruned candidate.

### A8 — Complete retained-domain certificate

When pruning is used, the complete domain is partitioned as:

```text
D = D_ret ∪ D_pr
```

with:

```text
D_ret ∩ D_pr = ∅
```

For every retained candidate `k ∈ D_ret`, certified bounds satisfy:

```text
R_k⁻ ⊆ R_k ⊆ R_k⁺
```

For every pruned candidate `h ∈ D_pr`, a certified outer report-class enclosure satisfies:

```text
R_h ⊆ R_h⁺
```

Every candidate in `D` is assigned to exactly one of `D_ret` or `D_pr`. No candidate may be omitted.

When `D = Ĥ_raw`, every outward-rounding-only candidate is assigned to exactly one of `D_ret` or `D_pr`. A candidate certified empty may be assigned to `D_pr` with:

```text
R_h⁺ = ∅
```

This assumption does not itself establish that pruning preserves `C_rep`. Report preservation follows only when the conditions of Proposition 3A are satisfied.

### A9 — Reproducible applicable certificate construction

For the full-domain certificate, every `R_h⁻` and `R_h⁺` used to construct `C⁻` and `C⁺` is deterministic or reproducible.

For the retained-domain certificate:

- every `R_k⁻` and `R_k⁺` for `k ∈ D_ret`;
- and every `R_h⁺` for `h ∈ D_pr`

is deterministic or reproducible.

All applicable constructions treat:

- numerical boundaries;
- interval or set arithmetic;
- resolution-cell boundaries;
- disconnected regions;
- branch overlap;
- and conservative outer-image approximation

conservatively.

The retained-domain path does not require construction of `R_h⁻` for every pruned candidate.

### D1 — Separate integrity status

Constraint compatibility, resolution-level report closure, report-class cardinality, and AIRS inference classification are reported separately from evidence-integrity status.

Branching over evidence-validity or acquisition-history assumptions is part of model evaluation. It does not itself assign an evidence-integrity status or establish authenticity, editing, or intent.

A compatible solution does not establish authenticity. An integrity exception does not automatically establish malicious editing.

---

## 8. Theorem Statement

### Theorem 3 — Certified Report-Class Closure Sandwich

Under Assumptions A1, A2, A2a, A3–A7, and A9, with certified `R_h⁻` and `R_h⁺` available for every `h ∈ D`:

```text
C⁻ ⊆ C_rep ⊆ C⁺
```

Therefore, when:

```text
C⁻ = C⁺
```

it follows that:

```text
C_rep = C⁻ = C⁺
```

and the complete report-class image of the admissible solution set is established relative to:

- the declared model;
- the declared candidate domain;
- the declared gauge;
- the declared claim map;
- and the declared resolution map.

This condition establishes **resolution-level report closure** even when the exact continuous sets `S_h` are not represented point for point, provided the certified inner and outer report-class images agree.

Resolution-level report closure does not by itself establish candidate-by-candidate feasibility, emptiness, or exact state-set characterization. Candidate-level closure requires every candidate to be:

- certified empty;
- certified nonempty with its exact report-class image established;
- or removed by a certified candidate-equivalence proof preserving admissible states and report classes.

Ordinary report-preserving pruning may establish resolution-level report closure, but it does not establish candidate-level closure.

Exact state-set closure is stronger and requires the admissible continuous sets themselves to be characterized, not merely their report-class images.

When pruning occurs before full-domain class bounds are constructed, closure must be established through the retained-domain sandwich in Section 10 rather than through `C⁻` and `C⁺`.

---

## 9. Proof

For every candidate `h ∈ D`, Assumption A7 gives:

```text
R_h⁻ ⊆ R_h ⊆ R_h⁺
```

Taking the union over the complete finite domain `D` gives:

```text
⋃_{h∈D} R_h⁻
⊆
⋃_{h∈D} R_h
⊆
⋃_{h∈D} R_h⁺
```

By definition:

```text
C⁻ ⊆ C_rep ⊆ C⁺
```

If:

```text
C⁻ = C⁺
```

then the squeeze relation implies:

```text
C_rep = C⁻ = C⁺
```

When the state-level constructions in Section 6.1 are used, they follow from:

```text
W_h ⊆ S_h ⊆ O_h ⊆ Ω_b
```

because the total map:

```text
ψ_h : Ω_b → C
```

preserves set inclusion of images:

```text
ψ_h(W_h)
⊆
ψ_h(S_h)
⊆
ψ_h(O_h)
```

The theorem itself requires only the certified class-level sandwich:

```text
R_h⁻ ⊆ R_h ⊆ R_h⁺
```

for every `h ∈ D`.

Theorem 2 guarantees that conservative enumeration does not change its jointly consistent discrete set when outward-rounding-only candidates are filtered correctly. Theorem 3 may impose additional declared constraints, so its admissible set satisfies:

```text
H_adm ⊆ H_cons^(2)
```

The conclusion is relative to the declared model and reporting maps because `S_h`, `q_b`, `r_h`, `ρ`, and `ψ_h` are all model- and claim-dependent. ∎

---

## 10. Retained-Domain Report Closure

Let:

```text
D_ret ⊆ D
```

be the retained candidate domain, and define the pruned domain:

```text
D_pr = D \ D_ret
```

with:

```text
D = D_ret ∪ D_pr
```

and:

```text
D_ret ∩ D_pr = ∅
```

Define the retained-domain certified inner and outer report-class sets:

```text
C_ret⁻
=
⋃_{k∈D_ret} R_k⁻
```

and:

```text
C_ret⁺
=
⋃_{k∈D_ret} R_k⁺
```

### Proposition 3A — Retained-Domain Report Closure

Under Assumptions A1, A2, A2a, A3–A6, A8, and A9, suppose every pruned candidate satisfies:

```text
R_h⁺ ⊆ C_ret⁻
```

for every:

```text
h ∈ D_pr
```

Then:

```text
C_ret⁻
⊆
C_rep
⊆
C_ret⁺
```

The lower inclusion follows because every retained inner class belongs to the exact admissible union:

```text
C_ret⁻ ⊆ C_rep
```

For every retained candidate `k ∈ D_ret`:

```text
R_k
⊆
R_k⁺
⊆
C_ret⁺
```

For every pruned candidate `h ∈ D_pr`:

```text
R_h
⊆
R_h⁺
⊆
C_ret⁻
⊆
C_ret⁺
```

Therefore every exact report class from either the retained or pruned domain lies in `C_ret⁺`, giving:

```text
C_rep ⊆ C_ret⁺
```

Consequently, if:

```text
C_ret⁻ = C_ret⁺
```

then:

```text
C_rep
=
C_ret⁻
=
C_ret⁺
```

This establishes resolution-level report closure through the retained-domain certificate after the report-preservation condition has been certified.

When:

```text
C_ret⁻ ≠ C_ret⁺
```

the retained-domain certificate is inconclusive regarding the exact value and cardinality of `C_rep`; certificate status is governed by Section 11.1.

When pruning occurs before full-domain class bounds are constructed, closure must be established through this retained-domain sandwich rather than through `C⁻` and `C⁺`.

### Report-level pruning

A pruning rule is **admissible for report-level closure** when it certifies that removing every candidate in `D_pr` cannot change `C_rep`.

A sufficient exact condition is that, for every `h ∈ D_pr`:

```text
R_h
⊆
⋃_{k∈D_ret} R_k
```

which implies:

```text
C_rep
=
⋃_{k∈D_ret} R_k
```

A certified sufficient condition is:

```text
R_h⁺ ⊆ C_ret⁻
```

for every `h ∈ D_pr`.

This proves that pruning cannot change the report-class union. It does not prove that a pruned candidate is infeasible, physically equivalent to a retained candidate, or characterized at the candidate level.

Sufficient report-level pruning cases include:

- certified emptiness represented by `R_h⁺ = ∅`;
- exact report-image containment;
- or certified outer-to-inner report-image containment through `R_h⁺ ⊆ C_ret⁻`.

### Candidate-equivalence pruning

Candidate-equivalence pruning requires a stronger certified correspondence.

For a pruned candidate `h ∈ D_pr` and retained candidate `k ∈ D_ret`, a sufficient condition is a certified inverse pair:

```text
T_hk : S_h → S_k
```

and:

```text
T_kh : S_k → S_h
```

satisfying:

```text
T_kh ∘ T_hk = id_{S_h}
```

and:

```text
T_hk ∘ T_kh = id_{S_k}
```

together with:

```text
ψ_h(θ)
=
ψ_k(T_hk(θ))
```

for every `θ ∈ S_h`.

The correspondence must preserve:

- gauge equivalence;
- all declared constraints;
- branch semantics;
- and claim-relevant physical content.

Ordinary report-level pruning may establish resolution-level report closure, but only certified candidate equivalence can support candidate-level closure for a removed nonempty candidate.

---

## 11. Certificate Status, Report-Class Cardinality, and AIRS Classification

### 11.1 Certificate status

For the full-domain path, if:

```text
C⁻ = C⁺
```

then Theorem 3 establishes:

```text
C_rep = C⁻ = C⁺
```

If instead:

```text
C⁻ ≠ C⁺
```

then the full-domain sandwich certificate alone does not establish `C_rep` or its cardinality.

For the retained-domain path, if:

```text
C_ret⁻ = C_ret⁺
```

then Proposition 3A establishes:

```text
C_rep = C_ret⁻ = C_ret⁺
```

If instead:

```text
C_ret⁻ ≠ C_ret⁺
```

then the retained-domain sandwich certificate alone does not establish `C_rep` or its cardinality.

In either unequal-sandwich case, resolution-level report-closure status remains **pending under this theorem** unless another independent certified argument establishes the exact report-class image `C_rep`. A valid AIRS inference classification may still follow from other certified information, but it does not establish `C_rep`, close the unequal sandwich, or convert the certificate into resolution-level report closure.

`Resolution-level report closure pending` is the certificate status used by this theorem when the applicable sandwich remains unequal. `Classification pending`, where used in an AIRS workflow, is an informative workflow status and is not itself an AIRS primary inference classification.

A singleton certified inner set does not establish that `C_rep` is a singleton when the corresponding certified outer set contains additional unresolved classes.

### 11.2 Report-Class Cardinality After Closure

Assume resolution-level report closure has been established by either Theorem 3 or Proposition 3A.

Then the following report-class cardinality cases are mutually exclusive and exhaustive.

### Corollary 1 — Empty report-class image

If:

```text
|C_rep| = 0
```

then:

```text
C_rep = ∅
```

and every compatible state set is empty:

```text
S_h = ∅
```

for every `h ∈ D`.

Thus no admissible state exists under the declared theorem scope.

This mathematical result does not by itself distinguish an incomplete searched-space no-solution result from model incompatibility within exhaustively declared bounds.

### Corollary 2 — Singleton report-class image

If:

```text
|C_rep| = 1
```

then there exists one reportable class `c` such that:

```text
C_rep = {c}
```

Exactly one reportable resolution class remains for the declared claim map.

This does not establish:

- one admissible discrete hypothesis;
- one branch;
- one integer vector;
- one connected admissible state region;
- one exact parameter vector;
- one exact geometry;
- one source point;
- or an AIRS-resolved inference classification.

Several materially distinct hypotheses or disconnected admissible state regions may map to the same report class.

### Corollary 3 — Finite report-class image

If:

```text
|C_rep| = k
```

for an integer:

```text
k ≥ 2
```

then exactly `k` distinct reportable resolution classes remain under the declared model, claim map, and resolution map.

This cardinality result does not by itself determine whether AIRS requires Multiple Admissible Solutions, Non-Resolvable, or another inference classification.

### Corollary 4 — Infinite report-class image

If:

```text
|C_rep| = ∞
```

then an infinite report-class image remains at the declared resolution.

A continuum, an unbounded countable family, or any other infinite set of report classes must not be converted into a preferred point estimate or a finite alternative list.

An infinite report-class image alone does not establish the AIRS Non-Resolvable classification. AIRS classification also depends on the structure, boundedness, separability, and reportability of the surviving hypotheses.

An unresolved gauge violates Assumption A5 and makes this theorem inapplicable rather than producing a valid classification.

### 11.3 Relationship to AIRS Inference Classification

Resolution-level report closure establishes the exact set `C_rep`. AIRS inference classification additionally depends on:

- search completeness;
- the number and structure of surviving hypotheses;
- whether surviving regions are bounded;
- whether materially distinct hypotheses can be separated;
- whether alternatives can be reported individually;
- and whether the required resolution has been met.

No AIRS primary inference classification follows from `|C_rep|` alone.

This subsection is an informative classification crosswalk. Theorem 3 and Proposition 3A establish report-class closure only; they do not independently establish an AIRS primary inference classification.

Subject to the controlling definitions and requirements of AIRS Draft 0.1:

- **Resolved Within the Declared Model** requires one admissible region or solution, separation from competing hypotheses, and exhaustive evaluation within declared bounds or independent proof that omitted regions are inadmissible.
- **Provisionally Resolved Within the Searched Hypothesis Space** applies when one admissible region or solution remains only within an incomplete or restricted search.
- **Multiple Admissible Solutions** applies when more than one materially distinct, individually reportable hypothesis remains.
- **Non-Resolvable** applies when surviving hypotheses cannot be distinguished, bounded, or separated at the required resolution.
- **No Admissible Solution Found in the Searched Hypothesis Space** applies when no tested hypothesis survives but unsearched or heuristically excluded alternatives may remain.
- **Model-Incompatible Within Declared Bounds** applies when no admissible solution remains after exhaustive evaluation within the declared bounds or independent exclusion of omitted regions.

A singleton report-class image may coexist with multiple admissible hypotheses:

```text
|C_rep| = 1
```

while:

```text
|H_adm| > 1
```

or while multiple disconnected admissible state regions survive. Such a result must not be reported as AIRS-resolved solely because the selected report quantity occupies one resolution class.

Where this subsection conflicts with AIRS Draft 0.1, AIRS Draft 0.1 controls.

---

## 12. Search-Completeness Requirements

A resolution-level report-closure claim requires, as applicable:

- complete coverage of `D` before admissible pruning;
- total claim and report-class maps for every candidate in `D`;
- explicit definitions of `D_ret` and `D_pr` when pruning is used;
- explicit construction of `C_ret⁻` and `C_ret⁺` when the retained-domain path is used;
- certified outer report-class enclosures for all pruned candidates;
- report-preservation proofs when a pruning claim is made;
- complete material branch generation;
- certified feasibility witnesses when inner occupancy is claimed;
- certified outer state enclosures when state-level outer certificates are used;
- certified inner and outer report-class sets required by the selected certificate path;
- certified emptiness for candidates rejected as infeasible;
- correct gauge treatment;
- complete dependency representation;
- predeclared total claim and resolution maps;
- conservative set-image evaluation;
- explicit treatment of resolution boundaries;
- reproducible traversal and solver configuration;
- retained audit records for rejected, pruned, and unresolved candidates;
- unique repository identifiers for released, candidate, obsolete, and superseded artifacts;
- and disclosure of all excluded model families.

Resolution-level report closure, report-class cardinality, AIRS inference classification, candidate-level closure, and exact state-set closure must be reported separately.

Candidate-level closure requires every candidate to be:

- certified empty;
- certified nonempty with its exact report-class image established;
- or removed by a certified candidate-equivalence proof preserving admissible states and report classes.

A report must distinguish:

- complete resolution-level report closure within the declared model family;
- the cardinality and structure of `C_rep`;
- the AIRS inference classification and its search-completeness basis;
- complete candidate-level closure;
- exact state-set constraint closure;
- characterization only within a searched subset;
- and unresolved alternatives outside the theorem scope.

---

## 13. Certificate Failure, Non-Applicability, and Prohibited Interpretation

### 13.1 Certificate Failure and Non-Applicability Conditions

The resolution-level report-closure and report-class-cardinality conclusions of Theorem 3 or Proposition 3A are not established through the selected certificate path when any applicable condition below is unresolved:

- incomplete candidate-domain coverage;
- hidden event, path, source, calibration, evidence-validity, acquisition-history, or alternate-model branches within the declared theorem scope;
- heuristic pruning without a report-preserving or candidate-equivalence proof;
- use of the full-domain sandwich after pruning when full-domain class bounds were not constructed;
- requiring or implying full-domain inner certificates for pruned candidates when only the retained-domain path was certified;
- missing report-class bounds required by the selected certificate path;
- undefined, inconsistent, or partially defined claim or report maps across candidates or branches;
- candidate-equivalence claims without certified inverse mappings preserving gauge, constraints, branch semantics, and report classes;
- local-optimizer failure treated as emptiness;
- uncertified isolated feasible points treated as complete state regions;
- non-conservative outer enclosures;
- unfixed or unquotiented gauge;
- post-hoc resolution selection;
- unmodeled covariance or shared dependencies;
- unresolved numerical boundary cases;
- failure to provide the state-level or report-class certificate required by the selected closure path;
- or uncertified emptiness when a candidate is rejected as infeasible.

### 13.2 Prohibited Interpretations and Reporting Uses

Even when resolution-level report closure has been established, the following interpretations are not licensed by Theorem 3 or Proposition 3A:

- assigning an AIRS inference classification from `|C_rep|` alone;
- treating `|C_rep| = 1` as proof of one surviving hypothesis or one connected admissible region;
- treating `|C_rep| = ∞` as sufficient by itself for the AIRS Non-Resolvable classification;
- presenting excluded model alternatives as disproven;
- presenting resolution-level report closure as physical truth;
- presenting resolution-level report closure as proof of authenticity or absence of editing;
- presenting resolution-level report closure as proof of causality or intent;
- or presenting resolution-level report closure as forensic validity.

---

## 14. Claims Not Established

Theorem 3 does **not** establish:

- that the declared model is physically true;
- that a surviving branch is causally correct;
- that event association is correct outside the tested branch scope;
- that a selected path is the actual propagation path;
- exact continuous-state uniqueness unless separately proven;
- resolution finer than the declared resolution map;
- calibrated probability for any surviving class;
- one surviving hypothesis from `|C_rep| = 1`;
- an AIRS primary inference classification from report-class cardinality alone;
- statistical independence of observations;
- authenticity;
- absence of editing;
- intent;
- forensic validity;
- or certified real-world performance.

Resolution-level report closure establishes the complete report-class image of the admissible result **within the declared model, domain, gauge, claim map, and resolution map**. It does not establish that no materially different model could explain the evidence.

---

## 15. Relationship to AIRS Draft 0.1

This theorem is an informative mathematical specialization of AIRS provisions concerning:

- retained hypothesis sets;
- admissible solution sets;
- resolution-level report closure and stronger constraint-closure distinctions;
- separation of report-class cardinality from AIRS primary inference classification;
- event and path branching;
- clock and spatial gauge;
- observability;
- uncertainty and covariance;
- multiple admissible solutions;
- non-resolvable outcomes;
- searched-space versus exhaustive no-solution results;
- inference classification;
- integrity status;
- and prohibited output styles.

Where this theorem conflicts with AIRS Draft 0.1, AIRS Draft 0.1 controls.

---

## 16. Validation Requirements

Before implementation claims are made, Theorem 3 should be exercised with cases covering at least:

1. one exact feasible candidate with one physical state;
2. one candidate with a continuum of gauge-equivalent parameterizations;
3. one candidate with a broad non-identifiable physical region;
4. several discrete candidates mapping to one report class;
5. several candidates mapping to distinct report classes;
6. exact no-solution closure;
7. searched-space no solution with unsearched branches;
8. conservative enumeration containing outward-rounding-only candidates;
9. certified empty outer enclosures;
10. feasible witnesses with loose outer enclosures;
11. equality `C⁻ = C⁺` without exact pointwise state reconstruction;
12. inequality `C⁻ ≠ C⁺`;
13. one inner class with additional unresolved outer classes;
14. multiple bounded reportable alternatives;
15. an infinite or continuous report-class image without presuming the AIRS Non-Resolvable classification;
16. unfixed timing gauge;
17. unfixed spatial gauge;
18. hidden reflection or public-address branches;
19. correlated observations treated incorrectly as independent;
20. resolution-cell boundary cases;
21. post-hoc resolution manipulation;
22. local optimizer failure;
23. incomplete pruning;
24. branch overlap mapping to the same physical claim;
25. strict inclusion `S_h ⊂ S_h^(2)` from additional Theorem 3 constraints;
26. outward-rounding-only candidates with `S_h^(2) = ∅`;
27. report-level pruning by certified outer-to-inner containment;
28. candidate-equivalence pruning by a certified report-preserving inverse pair;
29. all four report-class cardinality cases `0`, `1`, finite `≥ 2`, and infinite;
30. retained-domain closure with `C_ret⁻ ⊆ C_rep ⊆ C_ret⁺`;
31. equality `C_ret⁻ = C_ret⁺` under Proposition 3A after report-preserving pruning;
32. inequality `C_ret⁻ ≠ C_ret⁺` with certificate status pending under the retained-domain path;
33. pruning before full-domain class bounds are constructed;
34. report-preserving pruning that does not establish candidate-level closure;
35. candidate-equivalence pruning with a certified inverse pair;
36. a failed equivalence claim caused by non-preservation of branch semantics or gauge;
37. retained-domain certification with `R_h ⊆ R_h⁺` but without report preservation;
38. confirmation that A8 alone does not imply `C_rep` preservation;
39. full-domain and retained-domain closure paths yielding the same report-class cardinality;
40. a pruned candidate with no constructed `W_h`, `O_h`, or `R_h⁻`;
41. a certified-empty pruned candidate represented by `R_h⁺ = ∅`;
42. total and semantically consistent report maps for retained and pruned candidates;
43. verification that retained-domain symbols are defined before classification uses them;
44. confirmation that unequal sandwich bounds produce certificate-status pending rather than a closed-set cardinality result;
45. a singleton `C_rep` with multiple surviving hypotheses or disconnected admissible state regions;
46. a finite multi-class `C_rep` whose AIRS classification depends on hypothesis separability;
47. an infinite `C_rep` that is not automatically labeled AIRS Non-Resolvable;
48. searched-space no-solution versus model-incompatible classification under different search-completeness conditions;
49. resolved versus provisionally resolved classification under exhaustive and restricted searches;
50. confirmation that `resolution-level report closure pending` is a theorem certificate status;
51. confirmation that `classification pending` is an AIRS workflow status rather than a primary inference classification;
52. separation of certificate-invalidating conditions from prohibited downstream interpretations;
53. a correct closure certificate accompanied by an invalid AIRS interpretation, without treating the certificate itself as mathematically invalid;
54. repository-control review confirming that the prior 1.0 freeze candidate is obsolete and uniquely identified as `AWC-THM-3-1.0-rc1`;
55. verification that no two active released artifacts share the formal identifier `AWC-THM-3-1.0`;
56. and independent review of report closure, report-class cardinality, stronger closure claims, AIRS classification, and document control.

Evaluation must distinguish:

- mathematical correctness of the sandwich theorem;
- correctness of candidate-domain construction;
- correctness of gauge quotienting;
- certification of inner witnesses;
- certification of outer enclosures;
- correctness of report-class images;
- search completeness;
- numerical robustness;
- classification correctness;
- and empirical applicability of the declared model.

---

## 17. Revision History

| Version | Date | Change |
|---|---|---|
| 1.0 | 2026-07-11 | Frozen release. Updated version continuity to supersede `AWC-THM-3-0.9`; identified the AIRS classification crosswalk as informative rather than a theorem conclusion; standardized terminology separating report closure, report-class cardinality, AIRS inference classification, and evidence-integrity status; clarified that an AIRS classification cannot close an unequal report-class sandwich; distinguished `resolution-level report closure pending` from AIRS workflow-level `classification pending`; removed the forward reference to `D_pr` from A6; separated certificate-invalidating conditions from prohibited downstream interpretations; qualified isolated optimizer outputs so they count as outer enclosures only with an independent exhaustiveness proof; corrected the Section 13.2 spacing; designated the prior freeze-candidate artifact obsolete under repository alias `AWC-THM-3-1.0-rc1`; required unique repository identifiers; and retained the limitation that the theorem is not independently validated. |
| 0.9 | 2026-07-11 | Renamed the exact report-class image from `C_adm` to `C_rep` to avoid collision with AIRS admissible-solution terminology; made the cardinality results mathematically neutral; separated certificate status, report-class cardinality, and AIRS inference classification; stated that no AIRS primary classification follows from `|C_rep|` alone; added explicit AIRS mapping criteria based on search completeness, surviving-hypothesis structure, boundedness, separability, and required resolution; identified `classification pending` as a workflow status; and expanded failure, claims, reporting, and validation provisions. |
| 0.8 | 2026-07-11 | Separated certificate status from classification after closure; removed the contradiction between assuming closure and testing unequal sandwich bounds; renamed the retained-domain result as Proposition 3A because it is independent of the full-domain theorem; revised the purpose so retained-domain pruning does not imply universal state-level certification; replaced universal feasibility/infeasibility certification language with path-specific certificate requirements; and updated corollary numbering, validation cases, and cross-references. |
| 0.7 | 2026-07-11 | Made Section 6 certificate-path dependent by defining exact report sets universally while separating full-domain and retained-domain bounds; required total and semantically consistent report maps for every candidate, including pruned candidates; placed certified-empty candidates inside the retained/pruned partition through `R_h⁺ = ∅`; moved and formalized the retained-domain result before resolution classification; separated search-completeness requirements into their own section; renumbered corollaries and later sections; and expanded failure and validation coverage for path-specific certification. |
| 0.6 | 2026-07-11 | Replaced the circular pruning assumption with a complete retained-domain certificate; revised A9 to support distinct full-domain and retained-domain certificate paths; added the complete assumption set to Corollary 6; made the resolution classification apply after either closure path; clarified that A8 alone does not prove report preservation; strengthened retained-domain search requirements; and corrected the failure wording to distinguish report-level, candidate-level, and exact state-set closure. |
| 0.5 | 2026-07-11 | Renamed the theorem to resolution-level report closure to avoid overstating full constraint closure; separated the full-domain theorem from the A8 pruning result; required full-domain class bounds for the central sandwich; formalized a retained-domain report-closure corollary; qualified classification-pending conclusions for both sandwiches; strengthened candidate equivalence to a certified inverse pair preserving gauge, constraints, branch semantics, and report classes; and expanded failure and validation requirements. |
| 0.4 | 2026-07-11 | Explicitly included A2a in the theorem assumptions; corrected candidate-level closure so ordinary report-preserving pruning does not qualify; retitled A8 as complete report-level domain evaluation; introduced retained-domain sets `C_ret⁻` and `C_ret⁺`; proved `C_ret⁻ ⊆ C_adm ⊆ C_ret⁺` and equality under retained-domain closure; completed integrity-branch terminology; and made the finite-multiplicity corollary exact in `k`. |
| 0.3 | 2026-07-11 | Added explicit upstream compatible-set inheritance `S_h ⊆ S_h^(2)` and formalized `H_adm ⊆ H_cons^(2)`; defined retained and pruned domains; distinguished report-preserving pruning from candidate-equivalence pruning; added a certified report-preserving bijection condition; replaced descriptive resolution outcomes with an exhaustive cardinality classification; and separated evidence-validity and acquisition-history branches from evidence-integrity status. |
| 0.2 | 2026-07-11 | Distinguished Theorem 2 consistency from Theorem 3 admissibility; replaced reused consistency notation with `H_cons^(2)`, `H_adm`, and `C_adm`; required gauge actions to preserve observables, constraints, and claim-relevant content; made claim and report maps total on the outer domain; separated state enclosures from certified report-class enclosures; distinguished resolution-level report closure from candidate-level closure; defined admissible pruning; and removed unresolved gauge from valid non-resolvable outcomes. |
| 0.1 | 2026-07-11 | Initial AIRS-compatible theorem draft establishing a certified inner/exact/outer report-class sandwich; resolution-level constraint closure when inner and outer images agree; gauge-safe uniqueness; explicit multiple-solution, non-resolvable, no-solution, and classification-pending outcomes; and separation of model-relative closure from authenticity or physical truth. |

# Theorem 6 — Conditional Witness-Cloud Error Control and Scaling

```text
Document ID: AWC-THM-6
Version: Mathematical Draft 3.0.0-beta1
Date: 2026-07-12
Status: Conditional mathematical scaling result

Required direct dependency:
    • Theorem 5 — Conditional End-to-End Inference Composition
      Required version: AWC-THM-5 version 3.6.0-beta1

Required inherited chain:
    • Theorem 1 — Conditional Relative Same-Event Measurement Formation
    • Theorem 2 — Finite Integer Ambiguity Under Bounded Admissible Differences
    • Interface AWC-IF-C23 version 0.1
    • Theorem 3 — Conditional Resolution-Level Report Closure and Classification

Optional inherited interfaces:
    • Theorem 4 — Conditional Perturbation-Stable Candidate and Report-Class Recovery
    • E0 — Certified Raw Observation Interface

Normative status:
    Non-normative research specification

Validation status:
    Not independently validated

Supersedes:
    AWC-THM-6 version 2.0.0-beta1
```

---

## 1. Purpose

### 1.1 Objective

Theorem 6 states conditional bounds for combining multiple certified witness-level inference outputs into a common witness-cloud decision.

The theorem distinguishes four different quantities that must not be collapsed into one generic notion of “reliability”:

1. retention of an incorrect target;
2. rejection of the correct target;
3. survival of at least one incorrect target across the full target family;
4. unique retention of the correct target.

The theorem provides:

- target-wise false-retention bounds;
- correct-target retention bounds;
- family-wise false-retention bounds;
- empty-set risk bounds;
- ambiguity bounds;
- unique-correct-recovery bounds;
- conditional-independence factorizations;
- explicit dependence-aware alternatives;
- and asymptotic conditions under which unique recovery is justified.

The theorem does not assert that adding witnesses automatically improves total inference reliability.

Under a strict all-witness intersection rule:

```text
additional witnesses can reduce false-target survival
```

while simultaneously:

```text
additional witnesses can increase correct-target rejection.
```

A valid scaling claim must account for both effects.

---

### 1.2 Fundamental principle

The governing principle is:

```text
Witness scaling is an error trade-off,
not an automatic confidence amplifier.
```

Consequently:

```text
rejection of false targets
does not by itself establish correct recovery;
```

```text
low target-wise false acceptance
does not by itself establish low family-wise error;
```

```text
more witnesses
do not by themselves preserve the correct target;
```

```text
pairwise independence
does not imply mutual factorization;
```

```text
correlation summaries
do not by themselves define an effective witness count;
```

```text
model-based probability
does not establish empirical calibration;
```

```text
mathematical error control
does not establish physical truth, authenticity, or legal reliability.
```

---

### 1.3 Scope

Theorem 6 concerns mathematical error control and scaling for a finite common target space.

Its scope includes:

- witness-level retained-target sets;
- common target-space alignment;
- cloud aggregation rules;
- false-retention and false-rejection events;
- correct-target retention;
- family-wise false-retention risk;
- empty retained-set risk;
- ambiguity and wrong-singleton risk;
- unique-correct-recovery bounds;
- conditional independence;
- block independence;
- latent-variable dependence;
- certified joint-probability envelopes;
- report-class and candidate-level scaling;
- and request-relative scaling records.

The theorem does not establish:

- that a designated target is physically true;
- that the probability model is empirically calibrated;
- witness independence from sensor count alone;
- sensor correctness;
- calibration validity;
- preprocessing correctness;
- communication reliability;
- source authenticity;
- evidence integrity;
- chain of custody;
- implementation correctness;
- computational complexity;
- operational utility;
- or legal admissibility.

---

### 1.4 Two theorem modes

Theorem 6 has two distinct modes.

#### Mode A — Truth-free alternative-survival analysis

This mode requires no designated correct target.

It requires a declared alternative family:

```text
X_alt(u) ⊆ X
```

for each scenario:

```text
u ∈ U_6.
```

Define the alternative-survival event:

```text
ALT_m
=
{C_m ∩ X_alt(u) ≠ ∅}.
```

Mode A may establish statements such as:

```text
the probability that declared alternative x survives
is at most q_m(x,u)
```

or:

```text
P_u(ALT_m)
≤
δ_m^alt(u).
```

This mode establishes survival or rejection behavior for the declared alternative family only.

It does not establish correctness.

#### Mode B — Truth-indexed error-control analysis

This mode assumes a declared data-generating scenario and a designated correct target:

```text
x_*(u)
```

for each scenario:

```text
u ∈ U_6.
```

The incorrect-target family is:

```text
X_-(u)
=
X \ {x_*(u)}.
```

Truth-indexed analysis specializes the alternative family to:

```text
X_alt(u)
=
X_-(u).
```

It may establish:

- correct-target retention;
- false rejection;
- family-wise false retention;
- empty-set risk;
- wrong-singleton risk;
- ambiguity risk;
- and unique-correct-recovery bounds.

The designation of `x_*(u)` is an assumption of the probabilistic model. T6 does not prove that designation physically true.

## 2. Position in the AWC theorem series

The intended architecture is:

```text
Per witness or certified witness group:

(Optional E0)
      │
      ▼
T1 → T2 → C23 → T3 → T5
                         │
                         ▼
                    witness-level
                    certified output
                         │
            ┌────────────┴────────────┐
            │                         │
       other certified           other certified
       witness outputs           witness outputs
            │                         │
            └────────────┬────────────┘
                         ▼
                        T6
          witness-cloud error control and scaling
```

Optional T4 conclusions may be included in a witness-level T5 certificate, but T4 is not required for the core T6 result.

T6 does not:

- form T1 measurements;
- enumerate T2 candidates;
- execute C23 compatibility evaluation;
- construct T3 report images;
- perform T4 optimization or stability analysis;
- or replace T5 composition.

T6 consumes one or more valid T5-certified witness-level outputs and analyzes their joint retained-target behavior.

---

## 3. Mathematical setting

### 3.1 Scenario space and probability model

Let:

```text
U_6
```

be the declared scenario domain for the T6 request.

For each:

```text
u ∈ U_6,
```

let:

```text
(Ω_u, 𝔽_u, P_u)
```

be the probability space governing the declared observation perturbations, witness randomness, randomized preprocessing, or other modeled uncertainty relevant to the T6 analysis.

All probabilities in this theorem are conditional on the declared scenario and model.

A pointwise statement has the form:

```text
P_u(·).
```

A uniform certificate over `U_6` must explicitly bound:

```text
sup_{u∈U_6} P_u(·).
```

A pointwise bound may not be reported as uniform.

---

### 3.2 Common finite target space

Let:

```text
X
```

be a finite common target space.

`X` may represent:

- T2 candidate identities;
- T3 report classes;
- declared claim classes;
- or another finite target family preserved by valid T5 certificates.

Every witness-level output must map into the same `X` through an identity-preserving or certified semantics-preserving map.

The theorem does not permit silent aggregation across incompatible candidate, claim, report, gauge, or resolution semantics.

---

### 3.3 Alternative family and designated correct target

For every T6 request, declare an alternative family:

```text
X_alt(u) ⊆ X.
```

In truth-free mode, `X_alt(u)` is the family whose survival probability is to be bounded. No correct target is required.

In truth-indexed mode, each scenario has a designated correct target:

```text
x_*(u) ∈ X.
```

When the target is scenario-invariant over the request domain, write:

```text
x_*.
```

The set of incorrect targets is:

```text
X_-(u)
=
X \ {x_*(u)}.
```

Truth-indexed mode requires:

```text
X_alt(u)
=
X_-(u).
```

T6 does not establish that `x_*(u)` is empirically correct. It conditions its correctness statements on that designation.

### 3.4 Witness set and stochastic decision maps

Let:

```text
W_m
=
{w_1, …, w_m}
```

be the selected witness set.

Each witness must be represented by a certified witness contract:

```text
J_i^(6)
=
(
  witness_id_i,
  T5_certificate_id_i,
  T5_version_i,
  target_space_i,
  target_map_i,
  decision_map_i,
  certificate_scope_i,
  scenario_domain_i,
  probability_model_i,
  dependence_metadata_i,
  assumptions_i,
  result_status_i,
  completeness_i,
  provenance_i
)
```

Let the witness-specific target space be:

```text
X_i.
```

For each scenario `u`, the witness decision map is:

```text
D_{i,u}
:
Ω_u → 2^{X_i}.
```

The certified target map is:

```text
φ_i
:
X_i → X.
```

The common-space retained set is the random set:

```text
A_{i,u}(ω)
=
φ_i
(
  D_{i,u}(ω)
).
```

When the scenario is fixed, write:

```text
A_i
=
A_{i,u}.
```

For each target `x ∈ X`, define the witness acceptance event:

```text
E_i(x)
=
{x ∈ A_i}.
```

The witness contract must state whether T5 coverage is:

```text
POINTWISE
```

meaning that for `P_u`-almost every `ω`, the realized output `D_{i,u}(ω)` is covered by a valid T5 certificate; or:

```text
UNIFORM
```

meaning that one valid T5 conformance certificate covers the entire declared stochastic family over the stated scenario and probability domain.

The map `D_{i,u}` must be measurable, `φ_i` must preserve the declared target semantics, and unresolved or failed realizations must remain represented rather than being silently dropped.

### 3.5 Witness-cloud aggregation rule

A witness-cloud aggregation rule is:

```text
G_m
:
(2^X)^m → 2^X.
```

The cloud-retained set is:

```text
C_m
=
G_m(A_1, …, A_m).
```

The aggregation rule must be declared before its scaling properties are certified.

The baseline conjunction rule is:

```text
G_m^∩(A_1,…,A_m)
=
⋂_{i=1}^m A_i,
```

so that:

```text
C_m^∩
=
⋂_{i=1}^m A_i.
```

T6 also permits another aggregation rule only when its semantic meaning and error bounds are separately certified.

A majority rule, threshold rule, weighted vote, score fusion, or learned aggregator is not certified merely because it can be computed.

---

### 3.6 Core survival and error events

For every declared alternative family, define:

#### Alternative-family survival

```text
ALT_m
=
{C_m ∩ X_alt(u) ≠ ∅}.
```

In truth-indexed mode, where:

```text
X_alt(u)
=
X_-(u),
```

define the following additional events.

#### Correct-target false rejection

```text
FR_m
=
{x_*(u) ∉ C_m}.
```

#### Any false retention

```text
FA_m
=
{C_m ∩ X_-(u) ≠ ∅}.
```

Under the truth-indexed specialization:

```text
FA_m = ALT_m.
```

#### Empty retained set

```text
EMP_m
=
{C_m = ∅}.
```

#### Ambiguous retained set

```text
AMB_m
=
{|C_m| > 1}.
```

#### Wrong singleton

```text
WS_m
=
{
  C_m = {x}
  for some x ∈ X_-(u)
}.
```

#### Unique correct recovery

```text
UC_m
=
{C_m = {x_*(u)}}.
```

These events are distinct.

### 3.7 Error-bound objects

Every T6 request may supply or derive:

```text
δ_m^alt(u)
```

such that:

```text
P_u(ALT_m)
≤
δ_m^alt(u).
```

In truth-indexed mode, because:

```text
FA_m = ALT_m,
```

define:

```text
δ_m^+(u)
=
δ_m^alt(u)
```

as the family-wise false-retention bound.

Truth-indexed mode may also supply or derive:

```text
δ_m^-(u)
```

such that:

```text
P_u(FR_m)
≤
δ_m^-(u).
```

Uniform bounds are:

```text
\bar δ_m^alt
≥
sup_{u∈U_6} P_u(ALT_m),
```

and, in truth-indexed mode:

```text
\bar δ_m^-
≥
sup_{u∈U_6} P_u(FR_m)
```

and:

```text
\bar δ_m^+
=
\bar δ_m^alt.
```

A bound must be labeled pointwise or uniform.

## 4. Request and interface model

### 4.1 T6 request

A T6 scaling request is:

```text
R_6
=
(
  request_id,
  analysis_mode,
  target_level,
  target_space,
  alternative_family,
  scenario_domain,
  selected_witnesses,
  aggregation_rule,
  dependence_model,
  requested_error_bounds,
  uniformity_scope,
  unresolved_policy
)
```

where:

- `analysis_mode` is truth-free or truth-indexed;
- `target_level` identifies candidate, claim, report, or another declared level;
- `target_space` identifies `X`;
- `alternative_family` identifies `X_alt(u)`;
- `scenario_domain` identifies `U_6`;
- `selected_witnesses` identifies the witness contracts used;
- `aggregation_rule` identifies `G_m`;
- `dependence_model` identifies the joint model or certified dependence envelope;
- `requested_error_bounds` identifies target-wise, alternative-family, or truth-indexed quantities requested;
- `uniformity_scope` identifies pointwise or uniform certification;
- and `unresolved_policy` states how unresolved inputs are recorded.

In truth-indexed mode, the request must also declare `x_*(u)` and satisfy:

```text
X_alt(u)
=
X \ {x_*(u)}.
```

### 4.2 Required direct inputs

T6 directly consumes:

1. one or more successful T5 certificates;
2. a measurable witness decision map `D_{i,u}` for each selected witness;
3. a declared pointwise or uniform T5 certificate scope for each decision map;
4. the retained-target output or certified retained-target bound produced by each decision map;
5. a certified common target-space mapping `φ_i`;
6. the declared alternative family `X_alt(u)`;
7. the request scenario domain;
8. a declared aggregation rule;
9. a declared probability or joint-error-bound model;
10. dependence metadata;
11. assumptions and limitations;
12. completeness and unresolved statuses;
13. and provenance.

T6 does not infer probability models from retained sets alone.

A single realized T5 certificate does not, by itself, define or certify a random retained-set map over `Ω_u`.

### 4.3 Witness-level eligibility

A witness may support a T6 semantic conclusion only when its measurable decision map is covered pointwise or uniformly by valid T5 composition certification over the declared probability domain.

For pointwise coverage, for `P_u`-almost every `ω`, the realized witness output must have T5 certificate status:

```text
COMPOSABLE
```

or:

```text
COMPOSABLE_WITH_UNRESOLVED_OUTPUTS
```

and the selected semantic retained-target output itself must be eligible.

For uniform coverage, one valid T5 conformance certificate must certify the entire declared stochastic family and its output contract over the stated domain.

An unresolved T5 output may be preserved as metadata but may not support a substantive probabilistic T6 conclusion.

A heuristic artifact may not serve as a certified witness acceptance set or a certified probability bound.

Failed or unresolved realizations may not be silently removed from the probability space.

### 4.4 Common semantic alignment

Every selected witness must preserve or certify compatibility of:

- target identity;
- target level;
- report resolution;
- claim semantics;
- branch semantics;
- gauge treatment;
- event identity;
- scenario interpretation;
- coordinates and units;
- aggregation meaning;
- and probability conditioning.

A witness mapped from a different target space requires an explicit certified map:

```text
φ_i
:
X_i → X.
```

The map must preserve the semantic proposition being aggregated.

---

## 5. Compatibility and certification conditions

The following conditions are sufficient for a T6 certificate.

### C1 — Valid stochastic T5 witness contracts

Every selected witness is generated by a measurable witness decision map whose retained-set outputs are covered pointwise or uniformly by valid T5 composition certification over the declared probability domain.

Every selected semantic retained-target output must be eligible under the applicable T5 certificate scope.

### C2 — Common target and alternative spaces

All selected outputs are aligned to the same finite target space `X`, and the request declares a common alternative family `X_alt(u) ⊆ X`.

In truth-indexed mode:

```text
X_alt(u)
=
X \ {x_*(u)}.
```

### C3 — Common scenario interpretation

All probability statements refer to compatible scenarios in `U_6`.

### C4 — Declared aggregation

The aggregation rule `G_m` is explicit and fixed for the requested certificate.

### C5 — Measurability

For every selected witness and scenario, `D_{i,u}` is measurable, the mapped retained set `A_{i,u}` is measurable, and every requested aggregation or error event is measurable under `P_u`.

### C6 — Correct-target designation for correctness claims

Any claim involving correctness, false rejection, empty-set risk relative to truth, or unique recovery requires a declared `x_*(u)`.

### C7 — Mode-appropriate survival and error quantities

In truth-free mode, target-wise alternative survival and alternative-family survival are explicitly defined and bounded.

In truth-indexed mode, false-target retention and correct-target rejection are separately defined and separately bounded.

### C8 — Family-wise accounting

A claim about any incorrect target surviving must account for the full declared alternative family, not only one target.

### C9 — Dependence declaration

The request must identify one of:

- unrestricted dependence with direct joint bounds;
- mutual conditional independence;
- block independence;
- conditional independence given a declared latent variable;
- or another separately certified dependence model.

Pairwise correlations alone are insufficient for product factorization.

### C10 — Aggregation-specific bounds

Every scaling formula must correspond to the declared aggregation rule.

A conjunction formula may not be applied to a majority or score-fusion rule.

### C11 — Assumption preservation

All assumptions required by the witness contracts, probability model, dependence model, and aggregation rule remain attached.

### C12 — Domain preservation

Every conclusion remains restricted to the common certified domain.

### C13 — Status preservation

Conservative, unresolved, heuristic, pointwise, and uniform statuses may not be silently upgraded.

### C14 — Provenance preservation

Every bound remains traceable to the witness contracts, probability model, aggregation rule, dependence basis, target space, and scenario domain.

---

## 6. Deterministic set relations

### Lemma 6.1 — Conjunction nesting

For conjunction aggregation:

```text
C_{m+1}^∩
=
C_m^∩ ∩ A_{m+1}.
```

Therefore:

```text
C_{m+1}^∩
⊆
C_m^∩
```

for every realization.

Consequently, for every target `x`:

```text
{x ∈ C_{m+1}^∩}
⊆
{x ∈ C_m^∩}.
```

Thus target survival under conjunction is non-increasing with added witnesses, without requiring independence.

This applies to both false and correct targets.

---

### Lemma 6.2 — No automatic total-reliability monotonicity

Under conjunction, adding a witness can reduce:

```text
P_u(FA_m)
```

but can increase:

```text
P_u(FR_m).
```

Therefore no scalar “reliability improves with witness count” conclusion follows without:

- a declared loss or success event;
- control of both error directions;
- and an aggregation-specific proof.

---

### Lemma 6.3 — Empty-set implication

Because:

```text
C_m = ∅
```

implies:

```text
x_*(u) ∉ C_m,
```

we have:

```text
EMP_m ⊆ FR_m.
```

Therefore:

```text
P_u(EMP_m)
≤
P_u(FR_m).
```

Any valid false-rejection bound is also an upper bound on empty-set risk.

---

### Lemma 6.4 — Ambiguity and wrong-singleton implications

When there is one designated correct target:

```text
AMB_m ⊆ FA_m
```

and:

```text
WS_m ⊆ FA_m.
```

Therefore:

```text
P_u(AMB_m)
≤
P_u(FA_m)
```

and:

```text
P_u(WS_m)
≤
P_u(FA_m).
```

---

### Lemma 6.5 — Unique-correct complement

The complement of unique correct recovery is:

```text
UC_m^c
=
FR_m ∪ FA_m.
```

Therefore:

```text
P_u(UC_m)
=
1 - P_u(FR_m ∪ FA_m)
```

and by the union bound:

```text
P_u(UC_m)
≥
1 - P_u(FR_m) - P_u(FA_m).
```

---

## 7. General probabilistic bounds

### 7.1 Target-wise alternative-survival bounds

For each declared alternative target:

```text
x ∈ X_alt(u),
```

let:

```text
q_m(x,u)
```

be a certified upper bound satisfying:

```text
P_u(x ∈ C_m)
≤
q_m(x,u).
```

No independence is required when `q_m` is established directly from a valid joint model or enclosure.

---

### 7.2 Alternative-family survival bound

Because:

```text
ALT_m
=
⋃_{x∈X_alt(u)}
{x ∈ C_m},
```

the union bound gives:

```text
P_u(ALT_m)
≤
Σ_{x∈X_alt(u)}
q_m(x,u).
```

Define:

```text
δ_m^alt(u)
=
min
{
  1,
  Σ_{x∈X_alt(u)} q_m(x,u)
}.
```

Then:

```text
P_u(ALT_m)
≤
δ_m^alt(u).
```

This is the truth-free alternative-family survival result.

Target-wise decay alone is insufficient when the alternative family grows too quickly.

---

### 7.3 Truth-indexed false-retention specialization

In truth-indexed mode:

```text
X_alt(u)
=
X_-(u)
```

and:

```text
FA_m
=
ALT_m.
```

Define:

```text
δ_m^+(u)
=
δ_m^alt(u).
```

Then:

```text
P_u(FA_m)
≤
δ_m^+(u).
```

This is family-wise false-retention control.

---

### 7.4 Correct-target retention bound

In truth-indexed mode, let:

```text
r_m(u)
```

be a certified lower bound satisfying:

```text
P_u(x_*(u) ∈ C_m)
≥
r_m(u).
```

Define:

```text
δ_m^-(u)
=
1 - r_m(u).
```

Then:

```text
P_u(FR_m)
≤
δ_m^-(u).
```

---

### 7.5 Unique-correct-recovery bound

In truth-indexed mode, combining the previous bounds gives:

```text
P_u(UC_m)
≥
max
{
  0,
  1 - δ_m^-(u) - δ_m^+(u)
}.
```

Equivalently:

```text
P_u(UC_m)
≥
max
{
  0,
  r_m(u) - δ_m^+(u)
}.
```

This bound explicitly accounts for both correct-target rejection and false-target retention.

---

### 7.6 Empty, ambiguity, and wrong-singleton bounds

In truth-indexed mode, the same certificate yields:

```text
P_u(EMP_m)
≤
δ_m^-(u),
```

```text
P_u(AMB_m)
≤
δ_m^+(u),
```

and:

```text
P_u(WS_m)
≤
δ_m^+(u).
```

## 8. Conjunction aggregation

### 8.1 Per-witness error quantities

For conjunction aggregation, define for each incorrect target:

```text
α_i(x,u)
=
P_u(x ∈ A_i),
```

and define the correct-target false-rejection probability:

```text
β_i(u)
=
P_u(x_*(u) ∉ A_i).
```

Thus:

```text
P_u(x_*(u) ∈ A_i)
=
1 - β_i(u).
```

These are model-based probabilities, not automatically empirical error rates.

---

### 8.2 General dependence

Under arbitrary dependence:

```text
P_u(x ∈ C_m^∩)
=
P_u
(
  ⋂_{i=1}^m E_i(x)
).
```

This probability may not be replaced by:

```text
∏_{i=1}^m α_i(x,u)
```

without the required mutual or conditional independence.

A valid certificate must instead provide a direct joint upper bound:

```text
q_m(x,u)
≥
P_u
(
  ⋂_{i=1}^m E_i(x)
).
```

For correct-target retention, the union bound gives:

```text
P_u(FR_m)
=
P_u
(
  ⋃_{i=1}^m E_i(x_*)^c
)
≤
min
{
  1,
  Σ_{i=1}^m β_i(u)
}.
```

This bound requires no independence.

---

### 8.3 Mutual conditional independence

Assume that for a fixed scenario `u`, the events:

```text
E_1(x), …, E_m(x)
```

are mutually independent for each requested target `x`.

Then for every incorrect target:

```text
P_u(x ∈ C_m^∩)
=
∏_{i=1}^m α_i(x,u).
```

For the correct target:

```text
P_u(x_*(u) ∈ C_m^∩)
=
∏_{i=1}^m
(
  1 - β_i(u)
).
```

Therefore:

```text
δ_m^+(u)
≤
min
{
  1,
  Σ_{x∈X_-(u)}
  ∏_{i=1}^m α_i(x,u)
}
```

and:

```text
δ_m^-(u)
=
1 -
∏_{i=1}^m
(
  1 - β_i(u)
).
```

Consequently:

```text
P_u(UC_m)
≥
max
{
  0,
  ∏_{i=1}^m(1-β_i(u))
  -
  Σ_{x∈X_-(u)}
  ∏_{i=1}^m α_i(x,u)
}.
```

---

### 8.4 Exponential false-target rejection

Suppose:

```text
α_i(x,u)
≤
α
<
1
```

for every selected witness, incorrect target, and scenario in the declared scope.

Under mutual conditional independence:

```text
P_u(x ∈ C_m^∩)
≤
α^m.
```

If:

```text
|X_-(u)|
≤
N_-,
```

then:

```text
P_u(FA_m)
≤
min
{
  1,
  N_- α^m
}.
```

This establishes exponential family-wise false-retention decay only when `N_-` is fixed or grows slowly enough that:

```text
N_-(m) α^m → 0.
```

---

### 8.5 Correct-target attrition under fixed per-witness false rejection

Suppose under mutual conditional independence:

```text
β_i(u)
≥
β
>
0.
```

Then:

```text
P_u(x_*(u) ∈ C_m^∩)
≤
(1-β)^m
→
0.
```

Thus strict conjunction with a fixed nonzero per-witness false-rejection floor eventually rejects the correct target with probability approaching one.

Therefore exponential rejection of false targets does not imply asymptotically reliable recovery.

---

### 8.6 Zero-false-rejection special case

If every selected witness satisfies:

```text
β_i(u) = 0,
```

then:

```text
P_u(x_*(u) ∈ C_m^∩) = 1.
```

In that special case:

```text
P_u(UC_m)
≥
1 - δ_m^+(u).
```

If the family-wise false-retention bound tends to zero, unique correct recovery tends to one.

---

## 9. Dependence-aware scaling

### 9.1 Direct joint certificates

The most general admissible dependence treatment is a direct certified bound:

```text
q_m(x,u)
≥
P_u
(
  x ∈ C_m
).
```

The certificate must identify:

- the joint probability model;
- the aggregation rule;
- the scenario domain;
- the target;
- assumptions;
- approximation direction;
- and provenance.

---

### 9.2 Block independence

Let the witness set be partitioned into blocks:

```text
B_1, …, B_K.
```

Dependence may be arbitrary within each block.

Suppose the block-level target-survival events are mutually independent across blocks.

For each incorrect target, let:

```text
a_k(x,u)
```

satisfy:

```text
P_u
(
  x survives every witness in block B_k
)
≤
a_k(x,u).
```

Then under conjunction:

```text
P_u(x ∈ C_m^∩)
≤
∏_{k=1}^K a_k(x,u).
```

Similarly, if:

```text
r_k(u)
```

is a certified lower bound on correct-target retention within block `B_k`, then:

```text
P_u(x_*(u) ∈ C_m^∩)
≥
∏_{k=1}^K r_k(u).
```

The scaling unit is the certified independent block, not the physical witness count.

---

### 9.3 Conditional independence given a latent variable

Let:

```text
Z
```

be a declared latent variable.

If witness events are conditionally independent given `(u,Z)`, then:

```text
P_u(x ∈ C_m^∩)
=
E_u
[
  ∏_{i=1}^m
  P_u
  (
    E_i(x) | Z
  )
].
```

In general:

```text
E
[
  ∏_i p_i(Z)
]
≠
∏_i E[p_i(Z)].
```

Therefore marginal acceptance probabilities may not be multiplied.

---

### 9.4 Effective witness count

An effective witness count may be reported only when derived from a certified bound of the form:

```text
q_m(x,u)
≤
a(x,u)^{m_eff(x,u)}
```

with:

```text
0 < a(x,u) < 1.
```

The certificate must state:

- the reference rate `a`;
- the target and scenario scope;
- the dependence model;
- the derivation of `m_eff`;
- and whether the bound is pointwise or uniform.

`m_eff` may not be inferred solely from:

- witness count;
- average pairwise correlation;
- geometric proximity;
- shared hardware;
- or a heuristic diversity score.

---

## 10. General aggregation rules

### 10.1 Aggregation-specific certification

For an aggregation rule other than conjunction, T6 does not reuse conjunction formulas.

The request must provide aggregation-specific bounds:

```text
q_m(x,u)
≥
P_u(x ∈ C_m)
```

and, in truth-indexed mode:

```text
r_m(u)
≤
P_u(x_*(u) ∈ C_m).
```

The general family-wise and unique-recovery bounds in Section 7 then apply.

---

### 10.2 Threshold and vote aggregation

A threshold, majority, or weighted-vote rule may improve correct-target retention relative to strict conjunction, but may also increase false-target retention.

Such a rule is eligible only when the request declares:

- the threshold or weights;
- witness-level score or vote semantics;
- the joint distribution or certified tail bounds;
- target-family accounting;
- and the resulting `q_m` and `r_m` bounds.

T6 does not certify voting from witness count alone.

---

### 10.3 Learned aggregation

A learned aggregator may be transported as a heuristic artifact.

It may support a theorem-certified T6 conclusion only if a separate mathematical certificate establishes the requested error bounds over the declared domain.

Training performance, validation accuracy, or calibration plots alone are not T6 certificates.

---

## 11. Principal theorem

### Theorem 6 — Sound Witness-Cloud Error-Control Composition

Let:

```text
R_6
```

be a declared T6 request with common finite target space `X`, declared alternative family `X_alt(u)`, scenario domain `U_6`, selected stochastic witness contracts, and aggregation rule `G_m`.

Assume C1–C14.

Assume that for every:

```text
u ∈ U_6
```

and every:

```text
x ∈ X_alt(u),
```

there is a certified bound:

```text
P_u(x ∈ C_m)
≤
q_m(x,u).
```

Define:

```text
δ_m^alt(u)
=
min
{
  1,
  Σ_{x∈X_alt(u)} q_m(x,u)
}.
```

#### Part A — Truth-free alternative-family survival

Without assuming any designated correct target:

```text
P_u(ALT_m)
≤
δ_m^alt(u).
```

This conclusion establishes only the survival probability of the declared alternative family.

It does not establish correctness.

#### Part B — Truth-indexed error control and recovery

Additionally assume truth-indexed mode with designated correct target:

```text
x_*(u) ∈ X,
```

and:

```text
X_alt(u)
=
X_-(u)
=
X \ {x_*(u)}.
```

Assume a certified false-rejection bound:

```text
P_u(FR_m)
≤
δ_m^-(u).
```

Define:

```text
δ_m^+(u)
=
δ_m^alt(u).
```

Then:

##### 1. Family-wise false retention

```text
P_u(FA_m)
≤
δ_m^+(u).
```

##### 2. Correct-target false rejection

```text
P_u(FR_m)
≤
δ_m^-(u).
```

##### 3. Empty-set risk

```text
P_u(EMP_m)
≤
δ_m^-(u).
```

##### 4. Ambiguity risk

```text
P_u(AMB_m)
≤
δ_m^+(u).
```

##### 5. Wrong-singleton risk

```text
P_u(WS_m)
≤
δ_m^+(u).
```

##### 6. Unique-correct recovery

```text
P_u(UC_m)
≥
max
{
  0,
  1 - δ_m^-(u) - δ_m^+(u)
}.
```

All conclusions remain conditional on:

- the declared alternative family;
- the designated target, when used;
- the measurable witness decision maps;
- the pointwise or uniform T5 certificate scope;
- the probability model;
- the selected witnesses;
- the aggregation rule;
- the dependence model;
- the target family;
- the scenario domain;
- and all inherited upstream assumptions.

The theorem establishes no scalar reliability improvement solely from increasing `m`.

## 12. Proof

Fix:

```text
u ∈ U_6.
```

By C1 and C5, each witness retained set is induced by a measurable decision map covered pointwise or uniformly by valid T5 composition certification, and the requested aggregation events are measurable.

### Part A — Truth-free alternative-family survival

By definition:

```text
ALT_m
=
⋃_{x∈X_alt(u)}
{x ∈ C_m}.
```

By the union bound:

```text
P_u(ALT_m)
≤
Σ_{x∈X_alt(u)}
P_u(x ∈ C_m)
≤
Σ_{x∈X_alt(u)}
q_m(x,u).
```

Truncating at one yields:

```text
P_u(ALT_m)
≤
δ_m^alt(u).
```

No designated correct target is used.

### Part B — Truth-indexed recovery

Under truth-indexed mode:

```text
X_alt(u)
=
X_-(u)
```

and therefore:

```text
FA_m
=
ALT_m.
```

Hence:

```text
P_u(FA_m)
≤
δ_m^+(u).
```

The false-rejection inequality is assumed from the certified correct-target retention analysis.

Because:

```text
EMP_m ⊆ FR_m,
```

we have:

```text
P_u(EMP_m)
≤
δ_m^-(u).
```

Because there is one designated correct target:

```text
AMB_m ⊆ FA_m
```

and:

```text
WS_m ⊆ FA_m.
```

Therefore both probabilities are bounded by `δ_m^+(u)`.

Finally:

```text
UC_m^c
=
FR_m ∪ FA_m.
```

Thus:

```text
P_u(UC_m)
=
1 - P_u(FR_m ∪ FA_m)
```

and by the union bound:

```text
P_u(UC_m)
≥
1 - P_u(FR_m) - P_u(FA_m)
≥
1 - δ_m^-(u) - δ_m^+(u).
```

Probability is nonnegative, so the lower bound may be truncated at zero.

No independence assumption is required for the principal theorem because the supplied `q_m` and `δ_m^-` may arise from any valid joint certificate.

Independence is required only for the product factorizations in Section 8.

∎

## 13. Corollaries

### Corollary 6.1 — Uniform certificate

If:

```text
\bar δ_m^-
≥
sup_{u∈U_6} δ_m^-(u)
```

and:

```text
\bar δ_m^+
≥
sup_{u∈U_6} δ_m^+(u),
```

then uniformly over `U_6`:

```text
P_u(UC_m)
≥
max
{
  0,
  1 - \bar δ_m^- - \bar δ_m^+
}.
```

---

### Corollary 6.2 — Independent conjunction

Under the mutual conditional-independence assumptions of Section 8.3:

```text
q_m(x,u)
=
∏_{i=1}^m α_i(x,u)
```

and:

```text
δ_m^-(u)
=
1 -
∏_{i=1}^m
(
  1 - β_i(u)
).
```

The principal theorem then yields the independent-conjunction bounds.

---

### Corollary 6.3 — Family-wise exponential false-retention decay

If:

```text
α_i(x,u) ≤ α < 1
```

and:

```text
|X_-(u)| ≤ N_-,
```

then:

```text
P_u(FA_m)
≤
min
{
  1,
  N_- α^m
}.
```

This is a family-wise result, not merely a target-wise result.

---

### Corollary 6.4 — No asymptotic recovery from false-target rejection alone

Even when:

```text
δ_m^+(u) → 0,
```

unique correct recovery need not tend to one unless:

```text
δ_m^-(u) → 0.
```

In particular, strict conjunction with a fixed nonzero independent per-witness false-rejection floor does not yield asymptotic correct recovery.

---

### Corollary 6.5 — Sufficient condition for asymptotic unique recovery

If uniformly over the declared domain:

```text
\bar δ_m^- → 0
```

and:

```text
\bar δ_m^+ → 0,
```

then:

```text
inf_{u∈U_6}
P_u(UC_m)
→
1.
```

This is the required two-sided asymptotic condition.

---

### Corollary 6.6 — Report-class scaling

Let `X` be the finite T3 report-class space.

Then all theorem statements apply to report-class retention.

A report-class certificate does not imply candidate-level or state-level recovery.

---

### Corollary 6.7 — Candidate-level scaling

Let `X` be the finite T2/C23 candidate space.

Then all theorem statements apply to candidate retention only when candidate identity and coverage are preserved through T5.

Candidate-level unique recovery does not imply unique physical state unless separately established.

---

### Corollary 6.8 — Block-independent scaling

Under the block model of Section 9.2, target-wise joint bounds factorize across certified independent blocks, not necessarily across individual witnesses.

---

## 14. T6 evaluation record and certificate

### 14.1 Evaluator

Define:

```text
Evaluate_6
:
WitnessCloudRequests
→
Record_6.
```

`Evaluate_6` returns an audit record for every syntactically evaluable T6 request.

A successful semantic certificate is issued only when the requested bounds satisfy the theorem conditions.

---

### 14.2 Certificate

A successful T6 certificate is:

```text
Cert_6
=
(
  Q_sem^(6),
  M_meta^(6)
).
```

`Q_sem^(6)` contains only certified mathematical bound statements.

`M_meta^(6)` contains:

- selected witness identities;
- T5 certificate references;
- witness decision maps;
- T5 certificate scope by witness;
- target-space mappings;
- target level;
- alternative family;
- scenario domain;
- designated-target status;
- probability-model status;
- aggregation rule;
- dependence model;
- pointwise or uniform scope;
- assumptions;
- completeness;
- unresolved items;
- limitations;
- and provenance.

---

### 14.3 Evaluation statuses

`Record_6` assigns one status:

```text
CERTIFIED
```

when the requested exact or explicitly stated bounds are established;

```text
CERTIFIED_CONSERVATIVE
```

when only valid conservative bounds are established;

```text
UNRESOLVED
```

when a required joint, dependence, target-alignment, or correct-retention bound is not established;

```text
NONCOMPOSABLE
```

when witness contracts, target semantics, probability models, or aggregation semantics are incompatible;

and:

```text
NOT_APPLICABLE
```

when the requested correctness or scaling claim lies outside the declared target or scenario domain.

Only `CERTIFIED` and `CERTIFIED_CONSERVATIVE` permit `Cert_6`.

---

### 14.4 Required record fields

`Record_6` must identify:

```text
record_id
certificate_id_if_any
T6_document_id
T6_version
request_id
analysis_mode
target_level
target_space
alternative_family
scenario_domain
selected_witnesses
T5_certificate_references
witness_decision_maps
T5_certificate_scope_by_witness
target_space_mappings
designated_correct_target_if_any
aggregation_rule
dependence_model
probability_model
pointwise_or_uniform_scope
per_target_alternative_survival_bounds
alternative_family_survival_bound
per_target_false_retention_bounds_if_truth_indexed
family_wise_false_retention_bound_if_truth_indexed
correct_target_retention_bound_if_any
false_rejection_bound_if_any
empty_set_risk_bound_if_any
ambiguity_bound_if_any
wrong_singleton_bound_if_any
unique_correct_recovery_bound_if_any
assumption_ledger
completeness_ledger
unresolved_items
limitations
provenance
evaluation_status
```

---

## 15. Failure and unresolved conditions

### F1 — Missing or invalid stochastic T5 witness coverage

A selected witness lacks a measurable decision map, lacks declared pointwise or uniform T5 certificate scope, or has retained-set realizations not covered by valid T5 composition certification.

### F2 — Target-space or alternative-family mismatch

Witness outputs cannot be mapped to one common semantic target space, or the request does not define one common alternative family over that space.

### F3 — Scenario or stochastic-family mismatch

Witness probability statements, decision maps, or T5 certificate scopes refer to incompatible scenarios, probability domains, or conditioning events.

### F4 — Undeclared truth assumption

A correctness or false-rejection claim is made without a designated correct target.

### F5 — Undeclared aggregation rule

The cloud-retained set is formed by an unspecified or changing aggregation rule.

### F6 — Wrong aggregation formula

A conjunction, voting, threshold, or score-fusion formula is applied to a different aggregation rule.

### F7 — Unsupported independence

A product factorization is used without mutual or valid conditional independence.

### F8 — Pairwise-independence substitution

Pairwise independence or pairwise correlation is treated as sufficient for full joint factorization.

### F9 — Missing family-wise accounting

Target-wise false-retention bounds are reported as whole-family error without accounting for all alternatives.

### F10 — Correct-target attrition suppressed

False-target rejection is reported as reliability improvement while correct-target rejection is omitted.

### F11 — Empty-set risk suppressed

An aggregation rule can reject all targets, but empty-set risk is not recorded.

### F12 — Heuristic effective witness count

`m_eff` is asserted without a certified dependence-based envelope.

### F13 — Pointwise-to-uniform upgrade

A scenario-specific bound is reported as uniform.

### F14 — Model probability interpreted as empirical calibration

A model-based probability is reported as observed frequency or calibrated confidence without separate validation.

### F15 — Unresolved witness output used semantically

An unresolved or heuristic upstream output is used as a certified T6 premise.

### F16 — Assumption or provenance suppression

A required model, domain, dependence, aggregation, or witness-contract assumption is omitted.

### F17 — Candidate/report-level conflation

A report-class scaling result is interpreted as candidate-level or state-level recovery.

### F18 — Unsupported asymptotic claim

Asymptotic recovery is claimed without both:

```text
δ_m^- → 0
```

and:

```text
δ_m^+ → 0.
```

---

## 16. Claims not established

Theorem 6 does not establish:

- that the designated correct target is physically true;
- that witness errors are empirically calibrated;
- that witnesses are independent because they are distinct devices;
- that more witnesses always improve a chosen utility;
- that false-target rejection alone establishes correct recovery;
- that a nonempty retained set is correct;
- that a singleton retained set is correct;
- that report-class recovery implies candidate or state recovery;
- that candidate recovery implies unique physical-state recovery;
- source authenticity;
- recording integrity;
- legal reliability;
- implementation correctness;
- computational efficiency;
- or operational readiness.

---

## 17. Relationship to T5, T4, and E0

### 17.1 T5

T5 is the required direct dependency.

T6 consumes T5-certified witness-level semantic outputs and preserved metadata.

T6 does not repair a noncomposable or unresolved T5 request.

### 17.2 T4

T4 is optional.

A T4 stability conclusion may be included only when preserved by the supporting T5 certificate and relevant to the selected T6 target or probability model.

T4 stability does not establish witness independence or probabilistic calibration.

### 17.3 E0

E0 is optional.

Without E0, T6 conclusions begin no earlier than the certified-measurement scope preserved by T5.

With E0, provenance may extend to certified raw observations only over the E0-qualified domain.

---

## 18. Validation requirements

Before T6 is treated as independently validated, the project should provide:

1. independent mathematical review of the principal theorem and proof;
2. target-space alignment tests;
3. scenario-conditioning tests;
4. truth-free versus truth-indexed mode tests;
5. measurable retained-set and aggregation-event tests;
6. per-target false-retention tests;
7. correct-target false-rejection tests;
8. family-wise union-bound tests;
9. empty-set risk tests;
10. ambiguity and wrong-singleton tests;
11. unique-correct-recovery tests;
12. mutual-independence factorization tests;
13. negative tests showing pairwise independence is insufficient;
14. arbitrary-dependence joint-bound tests;
15. block-independence tests;
16. latent-variable conditional-independence tests;
17. conjunction attrition tests;
18. fixed nonzero false-rejection asymptotic counterexamples;
19. two-sided asymptotic recovery tests;
20. growing-target-family tests;
21. report-class versus candidate-level tests;
22. effective-witness certificate tests;
23. pointwise versus uniform bound tests;
24. heuristic-isolation tests;
25. T5-to-T6 integration tests;
26. and negative tests for every failure condition in Section 15.

Passing implementation tests validates an implementation profile, not this theorem by itself.

---

## 19. Revision history

| Version | Date | Summary |
|---|---:|---|
| 3.0.0-beta1 | 2026-07-12 | Rewrote T6 as a conditional witness-cloud error-control and scaling theorem; corrected the dependency order so T6 consumes T5-certified witness outputs; formally separated truth-free alternative-family survival from truth-indexed correctness analysis; introduced false retention, false rejection, family-wise error, empty-set risk, ambiguity, wrong-singleton, and unique-correct-recovery events; proved general union-bound and two-sided recovery bounds; restricted product factorization to mutual or valid conditional independence; added arbitrary-dependence, block-independence, latent-variable, and aggregation-specific profiles; prohibited heuristic effective-witness claims; replaced automatic reliability-growth claims with explicit two-sided asymptotic conditions; added measurable stochastic decision maps with pointwise or uniform T5 certificate coverage; made C7 mode-relative; and aligned certificate metadata and record fields with both truth-free and truth-indexed modes. |
| 2.0.0-beta1 | 2026-07-12 | Prior witness-cloud scaling draft centered primarily on incorrect-hypothesis survival and independence-based factorization. Superseded because it did not adequately control correct-hypothesis rejection, empty-set risk, family-wise error, aggregation dependence, or two-sided recovery. |

---

## 20. Summary

T6 analyzes the retained-target set:

```text
C_m
=
G_m(A_1,…,A_m)
```

formed from measurable witness decision maps:

```text
D_{i,u}
:
Ω_u → 2^{X_i}
```

whose mapped retained-set outputs are covered pointwise or uniformly by valid T5 composition certification.

In truth-free mode, T6 uses a declared alternative family:

```text
X_alt(u) ⊆ X
```

and establishes:

```text
P_u
(
  C_m ∩ X_alt(u) ≠ ∅
)
≤
δ_m^alt(u).
```

This does not establish correctness.

In truth-indexed mode:

```text
X_alt(u)
=
X_-(u)
=
X \ {x_*(u)},
```

and T6 distinguishes:

```text
false rejection:
FR_m = {x_* ∉ C_m}
```

from:

```text
false retention:
FA_m = {C_m ∩ X_- ≠ ∅}.
```

Given valid bounds:

```text
P_u(FR_m) ≤ δ_m^-(u)
```

and:

```text
P_u(FA_m) ≤ δ_m^+(u),
```

T6 establishes:

```text
P_u(C_m = {x_*(u)})
≥
max
{
  0,
  1 - δ_m^-(u) - δ_m^+(u)
}.
```

For conjunction under mutual conditional independence:

```text
P_u(x ∈ C_m)
=
∏_{i=1}^m α_i(x,u)
```

for an incorrect target, while:

```text
P_u(x_* ∈ C_m)
=
∏_{i=1}^m (1-β_i(u)).
```

Thus more witnesses can suppress false targets while also rejecting the correct target.

Asymptotic unique recovery requires both:

```text
δ_m^- → 0
```

and:

```text
δ_m^+ → 0.
```

T6 does not infer independence, calibration, correctness, or reliability from witness count alone.

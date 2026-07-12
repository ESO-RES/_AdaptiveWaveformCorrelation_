# Theorem 5 — Conditional End-to-End Inference Composition

```text
Document ID: AWC-THM-5
Version: Mathematical Draft 3.6.0-beta1
Date: 2026-07-12
Status: Internally frozen research draft

Required dependencies:
    • Theorem 1 — Conditional Relative Same-Event Measurement Formation
    • Theorem 2 — Finite Integer Ambiguity Under Bounded Admissible Differences
    • Theorem 3 — Conditional Resolution-Level Report Closure and Classification

Required bridge interface:
    • Interface ID: AWC-IF-C23
    • Version: 0.1
    • Title: Candidate-State Compatibility Evaluation Interface
    • Repository file: Interfaces/AWC-IF-C23_Candidate-State_Compatibility_Evaluation.md

Optional consumed interfaces:
    • Theorem 4 — Conditional Perturbation-Stable Candidate and Report-Class Recovery
    • E0 — Certified Raw Observation Interface

Normative status:
    Non-normative research specification

Validation status:
    Not independently validated

Change policy:
    Reopen only for proof-breaking, dependency-breaking,
    or semantic-contract defects.

Freeze baseline:
    This document is feature-complete for internal review.
    Further schema, audit, serialization, implementation,
    and conformance refinements belong in supporting specifications.

Supersedes:
    AWC-THM-5 version 3.5.0-beta1
```

---

## 1. Purpose

### 1.1 Objective

Theorem 5 states sufficient conditions under which valid outputs from Theorems 1–3, together with a declared candidate-state compatibility interface and an optional Theorem 4 stability interface, may be composed into one end-to-end mathematical inference contract.

The theorem is exclusively a **composition and contract-preservation result**.

It does not:

- form measurements;
- enumerate integer-cycle candidates;
- construct compatible state sets;
- optimize an objective;
- select a preferred candidate;
- construct claim or report images;
- prove perturbation stability;
- or establish witness-cloud reliability.

Those functions belong to the theorem or interface that originally establishes them.

The role of Theorem 5 is to verify that the consumed interfaces:

- refer to the same mathematical objects;
- use compatible units, coordinates, gauges, models, and domains;
- preserve candidate and branch identity;
- preserve representation types, certificate types, and result statuses;
- preserve assumptions and limitations;
- preserve completeness and unresolved-status information;
- and do not silently strengthen one another.

When those conditions hold, the interfaces may be composed without changing the meaning or strength of any upstream conclusion.

---

### 1.2 Fundamental principle

The governing principle is:

```text
Valid composition preserves upstream conclusions.

Valid composition establishes no stronger conclusion
than the consumed interfaces establish separately.
```

Consequently:

```text
upstream incompleteness cannot be repaired by composition;
```

```text
finite enumeration does not establish compatibility;
```

```text
compatibility does not establish physical truth;
```

```text
report-level closure does not establish candidate-level closure;
```

```text
objective separation does not establish authenticity or causality;
```

```text
perturbation stability does not establish global identifiability;
```

```text
mathematical correctness does not establish empirical validity.
```

---

### 1.3 Scope

The theorem concerns mathematical interface composition.

Its scope includes:

- measurement-interface identity;
- candidate-domain identity;
- branch and observation indexing;
- state-set and constraint identity;
- gauge and coordinate compatibility;
- claim and report-map identity;
- perturbation-domain compatibility;
- representation-type, certificate-type, and result-status preservation;
- search-completeness preservation;
- unresolved-status preservation;
- optional stability-interface incorporation;
- and production of an auditable composition record and, when eligibility conditions hold, a successful composition certificate.

The theorem does not establish:

- sensor correctness;
- calibration validity;
- preprocessing correctness;
- source authenticity;
- evidence integrity;
- chain of custody;
- forensic or legal admissibility;
- implementation correctness;
- computational complexity;
- empirical performance;
- calibrated probability;
- or operational suitability.

---

## 2. Position in the AWC theorem series

The theorem series is interpreted as:

```text
T1
Conditional pairwise measurement formation
        │
        ▼
T2
Finite exact or conservative candidate construction
        │
        ▼
C23
Candidate-state compatibility evaluation
        │
        ▼
T3
Claim/report closure and classification
        │
        ├───────────────┐
        │               │
        │          optional T4
        │     perturbation-stability certification
        │               │
        └───────┬───────┘
                ▼
T5
End-to-end composition and contract preservation
        │
        ▼
T6
Conditional witness-cloud scaling
```

The bridge `C23` is not a new theorem in this document. It is an explicitly declared interface connecting T2 candidate construction to the state-set and certificate objects consumed by T3.

T5 occurs **after** T3 and optional T4. It does not construct T3’s input and does not replace any upstream theorem.

---

## 3. Composition scope

### 3.1 Certified-measurement-to-report composition

Without an E0 interface, the earliest certified object consumed by the composed inference is a valid T1 measurement interface.

The resulting scope is:

```text
certified measurement
→ finite candidate domain
→ compatible state/report analysis
→ report output
```

This scope shall be described as:

```text
certified-measurement-to-report composition
```

It shall not be described as raw-observation-to-report composition.

---

### 3.2 Raw-observation-to-report composition

When a valid E0 interface is supplied, E0 must certify the transformation from declared raw observations to the exact T1 input objects.

Only then may the composed scope be described as:

```text
certified raw-observation-to-report composition
```

E0 must preserve or explicitly transform:

- recording identity;
- event identity;
- observer identity;
- time and frequency coordinates;
- preprocessing history;
- calibration references;
- uncertainty bounds;
- and provenance required by T1.

The absence of E0 does not invalidate the principal T5 result. It limits only the earliest certified point of the composed chain.

---

### 3.3 Optional T4 branch

T4 is optional.

The principal T5 composition requires valid T1, T2, C23, and T3 interfaces.

When T4 is absent:

- the T1–T3 composition may remain valid;
- no candidate-stability, report-class-stability, or local-state-stability conclusion may be reported as T4-certified;
- and `Record_5` must record that no T4 interface was consumed.

When T4 is present, its conclusions may be appended only if its domain, candidate identities, report maps, objective, gauge treatment, and perturbation semantics are compatible with the T1–T3 chain.

A missing or invalid T4 interface withholds stability conclusions. It does not invalidate an otherwise valid T1–T3 composition.

---

## 4. Interface model

### 4.1 General interface contract and interface slots

A supplied interface is represented abstractly by:

```text
I_k
=
(
  id_k,
  version_k,
  inputs_k,
  outputs_k,
  obligations_k,
  assumptions_k,
  domain_k,
  model_k,
  coordinates_k,
  units_k,
  gauges_k,
  representation_type_k,
  certificate_type_k,
  conformance_k,
  applicability_k,
  result_status_k,
  completeness_k,
  provenance_k
)
```

where:

- `id_k` identifies the theorem or bridge interface;
- `version_k` identifies the exact document or schema revision;
- `inputs_k` and `outputs_k` identify the mathematical objects consumed and produced;
- `obligations_k` identifies the enumeration, pruning, coverage, search, closure, stability, and reporting obligations applicable to the interface;
- `assumptions_k` is the applicable assumption ledger;
- `domain_k` is the domain on which the interface is interpreted;
- `model_k` identifies the equations, constraints, and branch semantics;
- `coordinates_k` and `units_k` identify mathematical coordinates and dimensions;
- `gauges_k` identifies gauge conventions or quotient treatment;
- `representation_type_k` assigns a representation type to each output;
- `certificate_type_k` is a partial map assigning a mathematical certificate type only to outputs that are actually certified;
- `conformance_k` records whether the supplied interface conforms to its declared contract;
- `applicability_k` records whether the supplied conformant interface applies to the declared request;
- `result_status_k` assigns an inference-result status to each output;
- `completeness_k` assigns a completeness status to each declared obligation;
- and `provenance_k` identifies the source objects and transformations required for audit.

The output-indexed maps are:

```text
representation_type_k
:
outputs_k → RepresentationType
```

```text
certificate_type_k
:
outputs_k ⇀ CertificateType
```

```text
result_status_k
:
outputs_k → ResultStatus
```

and:

```text
completeness_k
:
obligations_k → CompletenessStatus
```

The partial map `certificate_type_k` is undefined for an uncertified heuristic artifact.

Because an absent interface cannot carry its own presence field, each theorem or interface position is represented by an interface slot:

```text
Slot_k
=
(
  presence_k,
  interface_k?
)
```

with:

```text
presence_k
∈
{
  PRESENT,
  NOT_SUPPLIED,
  MISSING_REQUIRED
}
```

The slot semantics are:

```text
Slot_k = (PRESENT, I_k)
```

for a supplied interface;

```text
Slot_k = (MISSING_REQUIRED, ∅)
```

for an absent mandatory interface; and:

```text
Slot_k = (NOT_SUPPLIED, ∅)
```

for an absent optional interface.

`NOT_SUPPLIED` is permitted only for optional slots.

For a present interface:

```text
conformance_k
∈
{
  CONFORMANT,
  NONCONFORMANT,
  NOT_EVALUATED
}
```

Conformance is evaluated only when `presence_k = PRESENT`.

For a present conformant interface:

```text
applicability_k
∈
{
  APPLICABLE,
  NOT_APPLICABLE,
  UNRESOLVED
}
```

A supplied interface may be conformant but not applicable to the declared request.

Output result status is output-level:

```text
ResultStatus
=
{
  EXACT,
  CERTIFIED_INNER,
  CERTIFIED_OUTER,
  CERTIFIED_TWO_SIDED,
  CONSERVATIVE,
  HEURISTIC,
  UNRESOLVED,
  FAILED,
  NOT_APPLICABLE
}
```

Obligation completeness is recorded separately:

```text
CompletenessStatus
=
{
  COMPLETE,
  CERTIFIED_PARTIAL,
  INCOMPLETE,
  UNRESOLVED,
  NOT_APPLICABLE
}
```

An interface is not conformant merely because its values can be serialized or numerically evaluated.

### 4.2 Assumption ledger

Let:

```text
A_k
```

be the assumptions required by interface `I_k`.

The mandatory composed assumption ledger is:

```text
A_5
=
A_1
∪
A_2
∪
A_23
∪
A_3
```

Optional assumptions are added only when the corresponding optional output or obligation belongs to:

```text
Used_opt(J,R_5)
```

Thus:

```text
A_5^(4)
=
A_5 ∪ A_4
```

only when a T4 output or obligation is used by the request, and:

```text
A_5^(0)
=
A_5 ∪ A_0
```

only when an E0 output or obligation is used by the request.

`Record_5` must preserve all assumptions in the request-relative ledger, and any successful `Cert_5` must reference that preserved ledger. An assumption may not be omitted merely because a downstream stage does not restate it.

### 4.3 Common composition domain

Let:

```text
U_*
```

be the common scenario space in which the composed inference is interpreted.

Every mandatory interface domain must be represented as a subset of that same scenario space:

```text
U_k ⊆ U_*
```

with shared scenario identity, event identity, observer identity, branch identity, and coordinate semantics.

If an interface is originally expressed in another domain, an injective, identity-preserving embedding into `U_*` must be certified before T5 composition. Distinct source scenarios may not be collapsed into one scenario in `U_*`. After that certification, the interface domain is identified with its image in `U_*`.

The mandatory composition domain is a declared nonempty set:

```text
U_5
⊆
U_1 ∩ U_2 ∩ U_23 ∩ U_3
```

When T4 is consumed, the stability-qualified composition domain is:

```text
U_5^(4)
⊆
U_5 ∩ U_4
```

When E0 is consumed, the raw-observation-qualified composition domain is:

```text
U_5^(0)
⊆
U_5 ∩ U_0
```

No interface conclusion may be extended outside its certified domain by composition.

If the applicable intersection is empty or cannot be certified nonempty, the requested composition is non-applicable or unresolved.

### 4.4 Representation and certificate classes

Representation type, certificate type, and result status are distinct.

#### Representation types

```text
RepresentationType
=
{
  CANDIDATE_DOMAIN,
  STATE_SET,
  REPORT_IMAGE,
  SCALAR_QUANTITY,
  LOGICAL_STATUS,
  HEURISTIC_ARTIFACT
}
```

#### Set certificate types

```text
ExactSet
CertifiedInnerSet
CertifiedOuterSet
CertifiedTwoSidedEnclosure
```

#### Scalar certificate types

```text
ExactScalar
CertifiedLowerBound
CertifiedUpperBound
CertifiedIntervalBound
```

#### Logical and status certificate types

```text
ExactLogicalCertificate
StatusPreservationCertificate
```

A heuristic artifact has:

```text
representation_type = HEURISTIC_ARTIFACT
result_status = HEURISTIC
```

and no `certificate_type`.

The following preservation rules apply:

1. `ExactSet` may be deliberately weakened to a certified inner set, certified outer set, or certified two-sided enclosure.
2. `CertifiedInnerSet` must remain labeled as inner and may not be interpreted as an outer enclosure or exact set.
3. `CertifiedOuterSet` must remain labeled as outer and may not be interpreted as an inner set or exact set.
4. A `CertifiedTwoSidedEnclosure` is valid only when the certified inner and outer objects refer to the same target set and satisfy the declared containment relation.
5. `ExactScalar`, `CertifiedLowerBound`, `CertifiedUpperBound`, and `CertifiedIntervalBound` must preserve the quantity, direction, units, and domain they certify.
6. A heuristic artifact may be transported and audited, but its substantive proposition is not theorem-certified.
7. `UNRESOLVED` and `FAILED` are result statuses, not certificate types.

Certified inner and certified outer objects are generally directionally different and need not be comparable.

Composition may preserve a certificate type or deliberately weaken it. Composition may not upgrade or directionally reinterpret a type without a separate proof.

---

### 4.5 Interface presence, conformance, applicability, and output status

Presence, conformance, applicability, and output-result status are separate dimensions.

For every interface slot `Slot_k`:

```text
presence_k
∈
{
  PRESENT,
  NOT_SUPPLIED,
  MISSING_REQUIRED
}
```

For every supplied interface `I_k`:

```text
conformance_k
∈
{
  CONFORMANT,
  NONCONFORMANT,
  NOT_EVALUATED
}
```

For every supplied conformant interface `I_k` relative to request `R_5`:

```text
applicability_k
∈
{
  APPLICABLE,
  NOT_APPLICABLE,
  UNRESOLVED
}
```

For every output `y ∈ outputs_k`:

```text
result_status_k(y)
∈
{
  EXACT,
  CERTIFIED_INNER,
  CERTIFIED_OUTER,
  CERTIFIED_TWO_SIDED,
  CONSERVATIVE,
  HEURISTIC,
  UNRESOLVED,
  FAILED,
  NOT_APPLICABLE
}
```

A mandatory slot must be `PRESENT`, and its interface must be `CONFORMANT` and `APPLICABLE`, for successful composition.

A supplied conformant interface may contain outputs with different representation types, certificate types, result statuses, and completeness states. Eligibility is determined only for the dependency-closed outputs and obligations actually used by the request.

A missing required slot, a nonconformant mandatory interface, or unresolved mandatory applicability prevents a successful T5 composition certificate, although `Evaluate_5` still produces an audit record.

### 4.6 Composition request, dependency closure, and successful-certificate eligibility

A composition request is:

```text
R_5
=
(
  request_id,
  requested_scope,
  requested_semantic_conclusions,
  requested_meta_statuses,
  selected_outputs,
  required_obligations,
  unresolved_policy
)
```

where:

- `requested_scope` identifies certified-measurement-to-report or certified raw-observation-to-report composition;
- `requested_semantic_conclusions` identifies the mathematical conclusions requested from T5;
- `requested_meta_statuses` identifies requested presence, conformance, applicability, completeness, unresolved-status, provenance, or optional-interface statements;
- `selected_outputs` identifies the upstream outputs proposed as direct support;
- `required_obligations` identifies the upstream completeness obligations explicitly named by the request;
- and `unresolved_policy` states whether unresolved outputs may be preserved as meta-status results.

Define the request-relative dependency closure:

```text
Used(J,R_5)
=
DependencyClosure_J
(
  selected_outputs
  ∪
  required_obligations
)
```

`Used(J,R_5)` is the least dependency-closed set containing the request-selected outputs and obligations.

It must also contain:

- every upstream output required to derive a selected output;
- every supporting assumption;
- every identity, unit, coordinate, gauge, model, and constraint mapping used;
- every coverage and completeness obligation required by a requested conclusion;
- every provenance object required to trace the derivation;
- and every optional output or obligation on which a requested optional conclusion depends.

Partition the closure as:

```text
Used_mand(J,R_5)
```

for items from mandatory interfaces, and:

```text
Used_opt(J,R_5)
```

for items from supplied optional interfaces.

Every item in `Used_mand(J,R_5)` must satisfy mandatory eligibility.

Every item in `Used_opt(J,R_5)` must satisfy the same output-level and obligation-level eligibility rules for every requested conclusion that uses it.

Failure of an unused optional output does not affect mandatory composition. Failure of a used optional output prevents only the requested conclusions that depend on it.

A semantic conclusion may appear in `Cert_5` only when every used supporting output is eligible under the following rule:

| Result status of a used output | Eligibility for a semantic conclusion |
|---|---|
| `EXACT` | Permitted |
| `CERTIFIED_INNER` | Permitted with the original inner certificate type preserved |
| `CERTIFIED_OUTER` | Permitted with the original outer certificate type preserved |
| `CERTIFIED_TWO_SIDED` | Permitted with the original two-sided certificate type preserved |
| `CONSERVATIVE` | Permitted with conservative status preserved |
| `HEURISTIC` | Not permitted as a theorem-certified premise or conclusion; record only |
| `UNRESOLVED` | Not permitted as a premise for a substantive semantic conclusion; may be preserved only as a requested meta-status |
| `FAILED` | Not permitted |
| `NOT_APPLICABLE` | Not permitted |

Every used obligation must have a completeness status sufficient for the specific requested semantic conclusion.

A heuristic artifact may appear in `Record_5` with its representation type, provenance, and status preserved, but it may not support a substantive semantic conclusion.

An unresolved output may appear in the meta-status component of `Cert_5` only when:

1. the request explicitly permits unresolved meta-status results;
2. the unresolved output is not used to support a substantive semantic conclusion;
3. and every requested semantic conclusion is independently supported by eligible outputs.

A used output with status `FAILED`, `NOT_APPLICABLE`, or `HEURISTIC`, or an insufficiently complete used obligation, prevents the affected requested semantic conclusion from being certified.

Optional-interface outputs affect only conclusions that use those outputs, unless the optional interface altered a mandatory object.

## 5. Required interfaces

### 5.1 T1 measurement interface

The T1 interface must identify every consumed observation by the declared tuple or equivalent identifier containing:

- observer pair;
- physical event;
- frequency;
- path or propagation branch;
- calibration branch;
- phase-support branch;
- and dependency metadata.

For each observation, the interface must preserve:

- the corrected pairwise phase support;
- the associated bounded relative propagation-time-difference interpretation;
- timing and frequency coordinates;
- units;
- circular error bounds;
- admissibility status;
- and all T1 assumptions required for downstream use.

A per-observer phase value is not a substitute for the T1 pairwise same-event interface.

---

### 5.2 T2 candidate-domain interface

The T2 interface must identify:

- the finite branch set `B`;
- the observation index sets `A_b`;
- exact cycle sets `Nₐ,b`, when certified;
- conservative outward-rounded cycle sets `N̂ₐ,b`, when required;
- the exact raw domain `H_raw`;
- the conservative raw domain `Ĥ_raw`;
- and the compatible state sets defined by T2.

The branch-aware exact raw domain is:

```text
H_raw
=
⋃_{b∈B}
(
  {b}
  ×
  ∏_{a∈A_b} Nₐ,b
)
```

with:

```text
H_raw ⊆ Ĥ_raw
```

when conservative endpoint handling is required.

Using T2’s declared definitions:

```text
H_cons
=
{
  h ∈ H_raw :
  S_h^(2) ≠ ∅
}
```

and:

```text
Ĥ_cons
=
{
  h ∈ Ĥ_raw :
  S_h^(2) ≠ ∅
}
```

Under T2’s stated assumptions:

```text
Ĥ_cons = H_cons
```

T5 consumes this equality as a T2 result. T5 does not re-prove it and does not reinterpret `Ĥ_cons` as an unresolved implementation queue.

---

### 5.3 C23 candidate-state compatibility interface

The required bridge interface is published separately as:

```text
Interface ID: AWC-IF-C23
Version: 0.1
Title: Candidate-State Compatibility Evaluation Interface
Repository file:
Interfaces/AWC-IF-C23_Candidate-State_Compatibility_Evaluation.md
```

That file is the versioned interface contract. This section summarizes only the C23 objects required by T5.

C23 connects T2 objects to the exact or certified-enclosure objects required by T3.

Let:

```text
D_analysis ⊆ Ĥ_raw
```

be the declared analysis domain.

C23 must provide a coverage certificate showing that every candidate in:

```text
Ĥ_raw \ D_analysis
```

is handled through at least one permitted path:

- certified exclusion from `H_raw`;
- certified compatibility emptiness;
- certified equivalence to an analyzed candidate that preserves the applicable compatible-state, claim-map, resolution-map, and report-image semantics;
- or a T3-valid report-preserving enclosure or pruning certificate.

For every:

```text
h = (b,n_b) ∈ D_analysis
```

let:

```text
S_h^(2)
```

be the compatible state set established by the T2 constraints.

C23 defines only additional declared compatibility constraints through:

```text
F_h^(23)(θ)
```

and:

```text
S_h^(23)
=
{
  θ ∈ S_h^(2) :
  F_h^(23)(θ)
}
```

Therefore:

```text
S_h^(23) ⊆ S_h^(2)
```

C23 may refine but may not enlarge or silently redefine the T2-compatible state set.

C23 may provide certified bounds:

```text
W_h ⊆ S_h^(23) ⊆ O_h
```

where:

- `W_h` is a certified feasible witness set;
- `O_h` is a certified outer state enclosure;
- and `O_h = ∅` certifies `S_h^(23) = ∅`.

T5 consumes the C23 version, candidate coverage, state-refinement relation, pruning bases, per-output representation and certificate types, per-output result statuses, obligation-level completeness, and provenance.

T5 does not define, execute, or replace the C23 compatibility procedure.

### 5.4 T3 report-closure interface

The T3 interface must identify:

- the declared analysis domain `D_analysis` and its coverage certificate;
- exact refined compatible state sets `S_h^(23)` or certified bounds associated with them;
- gauge or physical-equivalence treatment;
- claim maps;
- resolution maps;
- per-candidate exact report images `R_h`, when available;
- certified inner report images `R_h⁻`;
- certified outer report enclosures `R_h⁺`;
- aggregate report-class bounds;
- pruning certificates;
- search-completeness status;
- and closure or unresolved status.

For the full-domain certificate:

```text
C⁻ ⊆ C_rep ⊆ C⁺
```

and when:

```text
C⁻ = C⁺
```

T3 establishes:

```text
C_rep = C⁻ = C⁺
```

at the declared resolution and relative to the declared model, candidate domain, gauge, claim map, and resolution map.

T5 preserves that conclusion. It does not strengthen report-level closure into candidate-level or exact state-set closure.

---

### 5.5 Optional T4 stability interface

When supplied, the T4 interface must identify:

- the perturbation domain `U_4`;
- the candidate domain used by T4;
- the objective or score family;
- candidate-score or report-class-score envelopes;
- report-class maps;
- gauge-fixed local-state conventions, when applicable;
- certified stability radii or domains;
- and the stability conclusion, certificate type, result status, assumptions, and domain established.

The T4 interface must be linked to the same candidate identities and report semantics used by T3.

A T4-selected candidate may coexist with multiple admissible T3 candidates. T5 must preserve that distinction.

---

### 5.6 Optional E0 raw-observation interface

When supplied, E0 must identify:

- raw recording objects;
- preprocessing operations;
- time and frequency transformations;
- event-window selection;
- calibration transformations;
- uncertainty propagation;
- and provenance linking its outputs to T1 inputs.

E0 may be consumed only when its outputs are certified to satisfy the T1 input contract.

---

## 6. Composition compatibility conditions

The following conditions are sufficient for T5 composition.

### C1 — Interface-slot state and request-relative admissibility

Every mandatory slot must satisfy:

```text
Slot_k = (PRESENT, I_k)
```

and every corresponding interface must satisfy:

```text
conformance_k = CONFORMANT
```

and:

```text
applicability_k = APPLICABLE
```

for the declared request.

For the declared pair `(J,R_5)`, each output and obligation in:

```text
Used(J,R_5)
```

must satisfy the eligibility requirements of Section 4.6.

A missing required slot, a nonconformant mandatory interface, a non-applicable mandatory interface, or unresolved mandatory applicability prevents successful composition.

A used output with status `FAILED`, `NOT_APPLICABLE`, or `HEURISTIC`, or a used obligation lacking sufficient completeness, prevents the affected substantive conclusion from appearing in `Cert_5`.

A used `UNRESOLVED` output may be preserved only as a requested meta-status under:

```text
COMPOSABLE_WITH_UNRESOLVED_OUTPUTS
```

and may not support a substantive semantic conclusion.

### C2 — Version identity

The exact theorem and interface versions are declared.

A composition must not silently combine:

- incompatible theorem drafts;
- renamed objects with changed semantics;
- changed endpoint conventions;
- changed report maps;
- or changed branch definitions.

Version translation requires a separately declared compatibility mapping.

---

### C3 — Object identity

Objects passed across interfaces must preserve identity.

In particular:

- each T1 observation must map to the intended T2 observation index;
- each T2 branch must map to the same C23 and T3 branch;
- each candidate `h = (b,n_b)` must retain the same branch and integer-vector identity;
- and each T3 report object must retain the same claim and resolution semantics in T5.

Relabeling is permitted only through an explicit bijection or certified identity-preserving map.

---

### C4 — Unit and coordinate compatibility

All shared quantities must use compatible:

- time coordinates;
- frequency coordinates;
- spatial coordinates;
- angular conventions;
- sign conventions;
- units;
- and clock-scale transformations.

A unit conversion is part of the interface and must be explicit, reproducible, and uncertainty-preserving.

---

### C5 — Model and constraint compatibility

The propagation, clock, geometry, calibration, path, branch, and dependency models used across interfaces must be identical or linked by a certified conservative refinement.

A downstream interface may add declared constraints, producing a subset of an upstream state set.

It may not silently:

- remove an upstream constraint;
- replace a model;
- merge distinct branches;
- or reinterpret an observation.

---

### C6 — Candidate-domain coverage

The T3 analysis domain must be a declared subset:

```text
D_analysis ⊆ Ĥ_raw
```

Every candidate outside `D_analysis` must be covered by a certified path permitted by C23 and T3:

- certified exclusion;
- certified compatibility emptiness;
- certified equivalence preserving the applicable compatible-state, claim-map, resolution-map, and report-image semantics;
- or a report-preserving enclosure or pruning certificate.

A finite domain is not a complete search merely because it is finite.

A successful T5 certificate must preserve the coverage certificate and its completeness status.

### C7 — State-set identity and refinement

For each analyzed candidate, the T3 state set or enclosure must refer to:

```text
S_h^(23)
=
{
  θ ∈ S_h^(2) :
  F_h^(23)(θ)
}
```

or to a certified bound on that same set.

The refinement relation:

```text
S_h^(23) ⊆ S_h^(2)
```

must be preserved.

An optimizer output, sample cloud, or finite collection of points may not replace `S_h^(23)` unless an independent exhaustiveness proof establishes that replacement.

### C8 — Gauge compatibility

Gauge conventions and physical-equivalence relations must be preserved.

A gauge-fixed coordinate estimate must not be interpreted as a unique physical state unless the applicable quotient or gauge conditions establish that conclusion.

---

### C9 — Claim and resolution-map identity

The claim maps, report maps, and resolution maps used by T3 and optional T4 must be identical or linked by an explicit certified mapping.

A change in report resolution constitutes a new reporting contract.

---

### C10 — Target identity, representation, certificate, and result-status preservation

Every output must preserve the identity of its target semantic object or explicitly record the certified derivation from its source object.

Its representation semantics must be preserved under the recorded transformation.

Its certificate type and result status must either:

- be preserved unchanged; or
- be transformed together through an explicit valid weakening relation recorded in `Record_5`.

Write:

```text
(cert_old, status_old)
⪰
(cert_new, status_new)
```

only when both pairs certify or represent the same target claim, set, quantity, or declared image under the recorded transformation, and when the weakening is valid for the applicable domain, assumptions, direction, and semantic meaning.

Examples of valid weakening include:

```text
(ExactSet, EXACT)
⪰
(CertifiedOuterSet, CERTIFIED_OUTER)
```

and:

```text
(ExactSet, EXACT)
⪰
(CertifiedInnerSet, CERTIFIED_INNER)
```

when the required containment relation is certified and the weakening is explicitly recorded.

No composition step may:

- convert a certified inner set into an outer set without a separate proof of the new outer relation;
- convert a certified outer set into an inner set without a separate proof of the new inner relation;
- convert either one-sided certificate into an exact set;
- claim a two-sided enclosure unless both directions refer to the same target object and the required containment relation is certified;
- convert an unresolved status into emptiness, exactness, or closure;
- convert a heuristic artifact into a probability, certified bound, or theorem-certified conclusion;
- convert a local certificate into a global certificate;
- or convert a conditional conclusion into an unconditional one.

Any deliberate weakening must remain explicitly labeled.

### C11 — Completeness preservation

Enumeration, pruning, compatibility, report-image, perturbation, and search-completeness statuses must remain distinct and traceable.

A downstream stage may resolve an upstream unresolved item only by producing the required separate proof or certificate.

Composition alone does not resolve it.

---

### C12 — Assumption preservation

All assumptions required by the consumed conclusions remain attached to the composed conclusion.

An assumption may be discharged only through an explicit proof that establishes it.

---

### C13 — Optional-interface isolation

The absence or failure of an optional interface affects only the conclusions that depend on that interface.

In particular:

- absent T4 means no T4 stability conclusion;
- absent E0 means no raw-observation-to-report claim.

Optional-interface failure must not invalidate independent mandatory conclusions unless the failed interface altered a mandatory object.

---

### C14 — Request, provenance, and audit-record preservation

Define:

```text
AuditPreserved_5
(
  J,
  R_5,
  Record_5
)
```

to mean that `Record_5` faithfully represents:

- the declared request `R_5`;
- every interface-slot presence state;
- consumed interface identifiers and versions;
- interface conformance and applicability states;
- per-output representation types;
- per-output certificate types when applicable;
- per-output result statuses;
- obligation-level completeness statuses;
- input object identifiers;
- dependency-closure membership;
- transformations and derivations;
- assumptions;
- scenario identity;
- domains;
- certificate-type and status transitions;
- and provenance.

`Evaluate_5` must produce an audit record:

```text
Record_5
```

for every syntactically evaluable pair `(J,R_5)`.

A successful composition certificate:

```text
Cert_5
=
(
  Q_sem,
  M_meta
)
```

may be issued only when:

1. every mandatory slot is present;
2. every mandatory interface is conformant and applicable to the request;
3. every output and obligation in `Used(J,R_5)` is eligible under Section 4.6;
4. the common composition domain is certified nonempty;
5. every applicable condition C1–C13 holds;
6. `AuditPreserved_5(J,R_5,Record_5)` holds;
7. every requested semantic conclusion has a valid T5 support derivation;
8. and the certificate status is `COMPOSABLE` or `COMPOSABLE_WITH_UNRESOLVED_OUTPUTS`.

Here:

- `Q_sem` is the set of theorem-certified semantic mathematical conclusions;
- and `M_meta` is the faithful preservation of requested presence, conformance, applicability, completeness, unresolved-status, optional-interface, provenance, and audit conclusions.

## 7. Principal theorem

### 7.1 Interface slots and composition request

Let:

```text
J
=
(
  Slot_1,
  Slot_2,
  Slot_23,
  Slot_3,
  Slot_4,
  Slot_0
)
```

be the supplied interface-slot tuple, and let `R_5` be the declared composition request from Section 4.6.

Define:

```text
InterfaceTuples
```

as the set of syntactically representable interface-slot tuples, and:

```text
CompositionRequests
```

as the set of syntactically valid T5 requests.

---

### 7.2 Evaluation and composition operators

Define the total audit evaluator:

```text
Evaluate_5
:
InterfaceTuples × CompositionRequests
→
Record_5
```

Thus:

```text
Evaluate_5(J,R_5)
```

returns an audit record for every syntactically evaluable request, including missing, nonconformant, non-applicable, failed, noncomposable, and unresolved-evaluation requests.

Define the eligible composition domain:

```text
Eligible_5
⊆
InterfaceTuples × CompositionRequests
```

as the set of pairs `(J,R_5)` for which:

- all mandatory slots are present;
- all mandatory interfaces are `CONFORMANT` and `APPLICABLE`;
- every output and obligation in the dependency-closed set `Used(J,R_5)` is eligible under Section 4.6;
- the common domain `U_5` is certified nonempty;
- every applicable condition C1–C13 holds;
- `AuditPreserved_5(J,R_5,Record_5)` holds for the evaluation record;
- and every requested semantic conclusion has a valid T5 support derivation.

Define the successful composition operator:

```text
Compose_5
:
Eligible_5
→
Cert_5
```

For an eligible pair `(J,R_5)`:

```text
Evaluate_5(J,R_5)
```

returns `Record_5` containing:

```text
Cert_5 = Compose_5(J,R_5)
```

For a pair outside `Eligible_5`, `Evaluate_5` still returns `Record_5`, but `Compose_5` is not defined and no successful `Cert_5` is issued.

---

### 7.3 Upstream theory ledger

Let:

```text
Γ_upstream
```

be the request-relative preserved ledger containing:

- all assumptions in the dependency closure;
- all valid upstream semantic conclusions in the dependency closure;
- all common-domain restrictions;
- all object-identity mappings;
- all model and constraint mappings;
- all interface-slot presence states;
- all interface conformance and applicability states;
- all per-output representation types;
- all per-output certificate types when applicable;
- all per-output result statuses;
- and all obligation-level completeness information

from the interfaces and dependencies in `Used(J,R_5)`.

---

### 7.4 Semantic and meta components of the certificate

A successful certificate is:

```text
Cert_5
=
(
  Q_sem,
  M_meta
)
```

where:

```text
Q_sem
```

contains only theorem-certified semantic mathematical conclusions about candidate domains, state sets, report images, stability objects, or other declared mathematical objects.

The component:

```text
M_meta
```

contains faithful statements about:

- interface-slot presence;
- interface conformance;
- interface applicability;
- result statuses;
- obligation completeness;
- unresolved outputs;
- optional-interface presence or absence;
- provenance;
- transformations;
- dependency closure;
- certificate lineage;
- and certificate status.

Meta-status statements are certified as faithful records of the consumed interfaces and evaluation process. They are not interpreted as physical propositions about every scenario in `U_5`.

---

### 7.5 Entailment on the composition domain

For every:

```text
Q ∈ Q_sem
```

the notation:

```text
Γ_upstream ⊨_{U_5} Q
```

means:

> For every admissible scenario `u ∈ U_5`, if `u` satisfies every preserved assumption and upstream semantic conclusion in `Γ_upstream`, then `u` satisfies `Q`.

This is a conditional semantic entailment relative to the declared model and composition domain. It does not establish that the model or assumptions are empirically true.

Meta-status statements in `M_meta` satisfy a different requirement:

```text
M_meta
=
faithful preservation of the applicable interface metadata,
slot presence, conformance, applicability, statuses, obligations,
request parameters, dependency closure, and provenance.
```

---

### 7.6 Permitted composition operations

`Compose_5` may form a semantic conclusion only through:

1. identity-preserving relabeling;
2. explicit certified unit or coordinate conversion;
3. domain restriction;
4. logical conjunction of preserved semantic conclusions;
5. projection or omission of variables that does not strengthen the projected claim;
6. certified image mapping through a declared claim or resolution map;
7. substitution through a certified identity or purpose-preserving equivalence;
8. preservation of conservative, inner, outer, or two-sided semantic status;
9. explicit valid weakening of a certificate-type and result-status pair;
10. and deliberate weakening of a claim.

`Compose_5` may form `M_meta` only through faithful copying, aggregation, or request-relative classification of preserved metadata, slot presence, conformance, applicability, statuses, obligations, dependency closure, and provenance.

`Compose_5` may not introduce an arbitrary new proposition, enlarge a domain, strengthen a certificate type, upgrade a result status, suppress a completeness limitation, omit a transitive dependency, or attach a semantic interpretation not separately entailed by the upstream ledger.

A heuristic artifact may be included in `Record_5`, but no substantive proposition asserted only by that artifact may be introduced into `Q_sem`.

---

### 7.7 T5 support derivations

For each requested semantic conclusion `Q`, define a T5 derivation object:

```text
D_5(Q)
```

that records:

- the upstream premises used;
- the dependency-closure items used;
- the permitted operation applied at each step;
- every identity, coordinate, unit, gauge, model, or claim-map transformation;
- every certificate-type and result-status transition;
- the domain on which each step is valid;
- and the resulting target semantic object.

Define:

```text
Supports_5
(
  Γ_upstream,
  U_5,
  Q,
  D_5(Q)
)
```

to mean that `D_5(Q)`:

1. begins only from eligible semantic premises in `Γ_upstream`;
2. uses only operations permitted by Section 7.6;
3. preserves all applicable assumptions, domains, identities, and certificate limitations;
4. contains every transitive dependency required by the derivation;
5. and terminates in `Q`.

A requested semantic conclusion is supported by eligible upstream outputs precisely when there exists a valid derivation `D_5(Q)` satisfying `Supports_5`.

---

### Theorem 5 — Sound Request-Relative End-to-End Inference Composition

Let `J` be the supplied interface-slot tuple and `R_5` the declared composition request.

Assume:

1. all mandatory slots are present;
2. all mandatory interfaces are `CONFORMANT` and `APPLICABLE`;
3. every output and obligation in `Used(J,R_5)` satisfies Section 4.6;
4. the common composition domain `U_5` is certified nonempty;
5. every applicable compatibility condition C1–C13 holds;
6. `AuditPreserved_5(J,R_5,Record_5)` holds;
7. and for every requested semantic conclusion `Q`, there exists a valid derivation `D_5(Q)` such that:

```text
Supports_5
(
  Γ_upstream,
  U_5,
  Q,
  D_5(Q)
)
```

Then:

```text
(J,R_5) ∈ Eligible_5
```

and:

```text
Evaluate_5(J,R_5)
```

returns `Record_5` containing:

```text
Cert_5
=
Compose_5(J,R_5)
=
(
  Q_sem,
  M_meta
)
```

The certificate status is:

```text
COMPOSABLE
```

when every requested semantic conclusion is supported and no request-selected meta output is unresolved; or:

```text
COMPOSABLE_WITH_UNRESOLVED_OUTPUTS
```

when every requested semantic conclusion is supported, the request explicitly permits unresolved meta-status results, and one or more selected unresolved outputs are preserved only in `M_meta`.

For every semantic conclusion:

```text
Q ∈ Q_sem
```

the support derivation is sound:

```text
Supports_5
(
  Γ_upstream,
  U_5,
  Q,
  D_5(Q)
)
```

and therefore:

```text
Γ_upstream ⊨_{U_5} Q
```

The meta component `M_meta` faithfully preserves the applicable interface-slot presence, conformance, applicability, metadata, statuses, obligations, request parameters, dependency closure, and provenance.

Moreover, neither `Q_sem` nor `M_meta` introduces a stronger mathematical or meta-level claim than is separately established, faithfully preserved, validly weakened, or entailed by the consumed interfaces and declared request.

If a compatible T4 interface is supplied and used, `Q_sem` may include only stability conclusions supported by eligible T4 outputs and valid derivations, while `M_meta` preserves the T4 slot presence, conformance, applicability, representation type, certificate type, result status, assumptions, domain, and provenance.

If a compatible E0 interface is supplied and used, the requested scope may be raw-observation-to-report only on the E0-qualified domain.

The theorem does not create new candidate, report, stability, truth, authenticity, integrity, probability, or reliability conclusions.

## 8. Proof

The proof is by request-relative, dependency-closed, sound, contract-preserving composition.

### Step 1 — Interface-slot state and request-relative eligibility

By assumption, all mandatory slots are present and their interfaces are conformant and applicable to `R_5`.

Every output and obligation in the dependency-closed set `Used(J,R_5)` satisfies Section 4.6.

Therefore no output used to support a requested semantic conclusion has status `FAILED`, `NOT_APPLICABLE`, `HEURISTIC`, or `UNRESOLVED`, and every used obligation has sufficient completeness.

Any selected unresolved output permitted by the request is reserved for `M_meta` and is not used to support `Q_sem`.

Any used optional output satisfies the same conclusion-specific eligibility requirements.

---

### Step 2 — Common scenario identity and domain

All mandatory domains are subsets of the common scenario space `U_*`, with shared scenario identity.

Any imported domain has already been connected to `U_*` through an injective, identity-preserving embedding.

The certified nonempty set:

```text
U_5 ⊆ U_1 ∩ U_2 ∩ U_23 ∩ U_3
```

therefore contains scenarios on which every mandatory interface applies without collapsing distinct scenarios.

---

### Step 3 — Dependency closure

By definition:

```text
Used(J,R_5)
=
DependencyClosure_J
(
  selected_outputs
  ∪
  required_obligations
)
```

Therefore every transitive upstream output, assumption, mapping, coverage obligation, completeness obligation, provenance object, and optional dependency required by the request is included in the request-relative ledger.

No requested conclusion can become eligible by omitting a required dependency.

---

### Step 4 — Identity of transferred objects

By C2–C4:

- theorem and interface versions are fixed;
- T1 observations map to the intended T2 indices;
- T2 branches and candidates map to C23 and T3 without identity loss;
- and shared units and coordinates are compatible.

Thus no consumed mathematical object changes identity merely by crossing an interface boundary.

---

### Step 5 — Candidate coverage and state refinement

By C5 and C6, the T2, C23, and T3 models are identical where required or connected by an explicit conservative refinement, and every candidate outside `D_analysis` is covered by a permitted certified path.

By C7:

```text
S_h^(23) ⊆ S_h^(2)
```

for every analyzed candidate.

Therefore C23 cannot enlarge or silently redefine the T2-compatible state set.

---

### Step 6 — Preservation of report conclusions

By C8 and C9, gauge meaning, claim maps, report maps, and resolution maps retain their declared semantics.

T3 establishes its report-image sandwich or retained-domain certificate under its own assumptions.

Since the permitted semantic composition operations do not change candidate accounting, refined state sets, mappings, or certificate bounds, every eligible requested T3 conclusion remains valid after composition.

---

### Step 7 — Target identity and valid weakening

By C10, every output preserves the identity of its target semantic object or records the certified derivation from its source object.

Every certificate-type and result-status pair is either preserved or transformed through an explicit valid weakening relation recorded in `Record_5`.

By C11, unresolved or incomplete statuses are not silently converted into resolved statuses.

By C12, all required assumptions remain attached.

Therefore every semantic conclusion in `Q_sem` has strength no greater than the applicable upstream basis.

---

### Step 8 — Optional-interface isolation

By C13, optional interfaces are isolated.

If T4 is absent or unused, no T4 semantic conclusion is added, and its presence or absence may be recorded only in `M_meta`.

If T4 is present, applicable, compatible, and used, eligible stability conclusions may enter `Q_sem`, while T4 status and provenance enter `M_meta`.

If E0 is absent or unused, the earliest certified point remains the T1 measurement interface.

If E0 is present, applicable, compatible, and used, provenance may extend to raw observations only on the E0-qualified domain.

Failure of an unused optional output does not affect mandatory composition.

---

### Step 9 — Audit preservation and eligibility

By assumption:

```text
AuditPreserved_5
(
  J,
  R_5,
  Record_5
)
```

holds.

Steps 1–8 establish every remaining eligibility condition in Section 7.2.

Therefore:

```text
(J,R_5) ∈ Eligible_5
```

and:

```text
Cert_5 = Compose_5(J,R_5)
```

is defined.

`Evaluate_5(J,R_5)` returns `Record_5` containing `Cert_5`.

The certificate status is `COMPOSABLE` or `COMPOSABLE_WITH_UNRESOLVED_OUTPUTS` according to the theorem statement.

---

### Step 10 — Semantic soundness through support derivations

Let:

```text
Q ∈ Q_sem
```

By assumption, there exists a valid support derivation:

```text
D_5(Q)
```

such that:

```text
Supports_5
(
  Γ_upstream,
  U_5,
  Q,
  D_5(Q)
)
```

The derivation begins from eligible upstream semantic premises, contains every transitive dependency, and uses only operations permitted by Section 7.6.

Each permitted operation preserves semantic consequence on `U_5`.

Therefore:

```text
Γ_upstream ⊨_{U_5} Q
```

---

### Step 11 — Meta-status fidelity

Every item in `M_meta` is formed only through faithful copying, aggregation, or request-relative classification of preserved interface-slot presence, conformance, applicability, metadata, statuses, obligations, dependency closure, and provenance.

Therefore `M_meta` accurately records the applicable interface, completeness, unresolved-status, optional-interface, request, and provenance facts.

A heuristic artifact may be faithfully transported in `Record_5`, but it cannot supply a substantive semantic conclusion in `Q_sem`.

Thus `Cert_5` is both semantically sound and meta-status faithful.

This proves the theorem. ∎

## 9. Corollaries

### Corollary 5.1 — Composition without T4

If the mandatory T1, T2, C23, and T3 interfaces satisfy the theorem conditions for request `R_5` and no T4 interface is supplied, then `Evaluate_5(J,R_5)` returns `Record_5` containing a successful `Cert_5 = Compose_5(J,R_5)`.

The meta component `M_meta` must state:

```text
stability interface: not supplied
stability conclusion: not established
```

The absence of T4 does not invalidate valid T1–T3 conclusions.

---

### Corollary 5.2 — Composition with T4

If a T4 interface is present, conformant, applicable, compatible, and used by `R_5`, then an eligible T4 stability conclusion may enter:

```text
Q_sem
```

Its representation type, certificate type, result status, assumptions, domain, and provenance enter:

```text
M_meta
```

The T4 conclusion remains limited to:

- its declared perturbation domain;
- its declared candidate domain;
- its declared objective;
- its declared report map;
- and its declared gauge conditions.

T4 does not alter T3 admissibility or closure unless a separate theorem explicitly establishes that relationship.

### Corollary 5.3 — Conservative and unresolved upstream outputs

A certified conservative semantic conclusion may enter:

```text
Q_sem
```

with its conservative certificate type and result status preserved or validly weakened.

An unresolved output may enter only:

```text
M_meta
```

and only when the request permits unresolved meta-status preservation.

Neither a conservative conclusion nor an unresolved output may be reported as exact without a separate proof.

### Corollary 5.4 — Report closure with incomplete candidate-level classification

Suppose T3 establishes exact report-level closure through a valid full-domain or retained-domain report-image certificate while candidate-level classification remains incomplete.

Then T5 may preserve:

```text
Q_sem:
report-level closure = certified
```

and:

```text
M_meta:
candidate-level closure = not established
```

T5 must not collapse those statuses into one generic “resolved” label.

### Corollary 5.5 — Certified-measurement-to-report scope

Without a present, conformant, applicable, and used E0 interface, a valid T5 certificate establishes at most:

```text
certified-measurement-to-report composition
```

It does not certify preprocessing from raw recordings.

### Corollary 5.6 — Raw-observation-to-report scope

With a present, conformant, applicable, and used E0 interface, a T5 certificate may establish:

```text
certified raw-observation-to-report composition
```

only over the domain and transformations certified by E0.

### Corollary 5.7 — Non-strengthening

Let `Q` be any claim not established by T1, T2, C23, T3, optional T4, or optional E0.

Then T5 does not establish `Q` solely because the interfaces compose validly.

---

## 10. Audit record and composition certificate

### 10.1 Record and certificate distinction

`Record_5` is the audit object returned by:

```text
Evaluate_5(J,R_5)
```

for every syntactically evaluable pair, including:

```text
COMPOSABLE
COMPOSABLE_WITH_UNRESOLVED_OUTPUTS
UNRESOLVED_EVALUATION
NONCOMPOSABLE
NOT_APPLICABLE
```

`Cert_5` is returned by:

```text
Compose_5(J,R_5)
```

only for pairs in `Eligible_5`.

For an eligible pair `(J,R_5)`, `Evaluate_5(J,R_5)` contains:

```text
Cert_5
=
Compose_5(J,R_5)
=
(
  Q_sem,
  M_meta
)
```

A missing, nonconformant, unresolved-applicability, non-applicable, failed, heuristic-dependent, insufficiently complete, or otherwise ineligible request produces `Record_5`, but not a successful `Cert_5`.

---

### 10.2 Required record fields

`Record_5` must identify:

```text
record_id
certificate_id_if_any
T5_document_id
T5_version
composition_request_id
requested_scope
requested_semantic_conclusions
requested_meta_statuses
selected_outputs
required_obligations
unresolved_policy
composition_domain
interface_slot_states
interface_presence
interface_conformance
interface_applicability
optional_interfaces
interface_versions
dependency_closure
scenario_identity_alignment
object_identity_mappings
unit_and_coordinate_mappings
model_and_constraint_mappings
candidate_domain
coverage_certificate
claim_and_resolution_maps
assumption_ledger
representation_type_ledger
certificate_type_ledger
certificate_status_transition_ledger
output_result_status_ledger
obligation_completeness_ledger
support_derivations
semantic_conclusions
meta_statuses
report_closure_status
candidate_closure_status
state_set_closure_status
stability_status
heuristic_artifacts
unresolved_items
non_applicable_items
failure_items
audit_preservation_status
provenance
composition_status
```

The record may be human-readable or machine-readable, provided the mathematical meaning is preserved.

---

### 10.3 Composition scope field

The requested scope must be one of:

```text
CERTIFIED_MEASUREMENT_TO_REPORT
```

or, when E0 is present, conformant, applicable, used, and valid:

```text
CERTIFIED_RAW_OBSERVATION_TO_REPORT
```

The scope must not be inferred from the theorem title alone.

---

### 10.4 Interface-slot presence, conformance, and applicability fields

Each interface slot must receive one presence value:

```text
PRESENT
NOT_SUPPLIED
MISSING_REQUIRED
```

where `NOT_SUPPLIED` applies only to optional slots.

Every present interface must receive one conformance value:

```text
CONFORMANT
NONCONFORMANT
NOT_EVALUATED
```

Every present conformant interface must receive one request-relative applicability value:

```text
APPLICABLE
NOT_APPLICABLE
UNRESOLVED
```

A missing mandatory slot receives `MISSING_REQUIRED` and causes `NONCOMPOSABLE`.

An optional absent slot receives `NOT_SUPPLIED`.

A present interface may be conformant but non-applicable to `R_5`.

Unresolved mandatory applicability yields `UNRESOLVED_EVALUATION`, not a successful certificate.

---

### 10.5 Per-output result-status and obligation-completeness fields

Every output must separately receive one result status:

```text
EXACT
CERTIFIED_INNER
CERTIFIED_OUTER
CERTIFIED_TWO_SIDED
CONSERVATIVE
HEURISTIC
UNRESOLVED
FAILED
NOT_APPLICABLE
```

Every declared obligation must separately receive one completeness status:

```text
COMPLETE
CERTIFIED_PARTIAL
INCOMPLETE
UNRESOLVED
NOT_APPLICABLE
```

Successful-certificate eligibility is evaluated relative to the dependency-closed set:

```text
Used(J,R_5)
```

including used mandatory and used optional outputs, obligations, assumptions, mappings, and provenance dependencies.

A heuristic artifact may be recorded but may not appear as a theorem-certified semantic conclusion.

---

### 10.6 Semantic, meta, and derivation fields

The record must distinguish:

```text
semantic_conclusions = Q_sem
```

from:

```text
meta_statuses = M_meta
```

and must record:

```text
support_derivations
=
{
  D_5(Q) :
  Q ∈ Q_sem
}
```

Semantic conclusions are subject to:

```text
Γ_upstream ⊨_{U_5} Q
```

for each `Q ∈ Q_sem`.

Meta statuses are subject to faithful-preservation requirements rather than scenario-level semantic entailment.

---

### 10.7 Request-relative evaluation status

`Evaluate_5(J,R_5)` assigns one status:

```text
COMPOSABLE
```

when every requested semantic conclusion has a valid support derivation and no request-selected meta output is unresolved;

```text
COMPOSABLE_WITH_UNRESOLVED_OUTPUTS
```

when every requested semantic conclusion has a valid support derivation, the request explicitly permits unresolved meta-status results, and unresolved selected outputs are preserved only in `M_meta`;

```text
UNRESOLVED_EVALUATION
```

when successful-composition eligibility cannot yet be determined, including when mandatory applicability, common-domain nonemptiness, version compatibility, required identity mapping, or required dependency closure cannot yet be certified;

```text
NONCOMPOSABLE
```

when a definite incompatibility, missing required slot, nonconformance, failed used output, heuristic-dependent requested conclusion, insufficiently complete obligation, invalid support derivation, or prohibited unresolved dependency is established;

and:

```text
NOT_APPLICABLE
```

when the requested scope or common domain is definitively outside the applicable domain.

Only `COMPOSABLE` and `COMPOSABLE_WITH_UNRESOLVED_OUTPUTS` permit a successful `Cert_5`.

A composable request need not produce a unique or resolved inference.

---

### 10.8 Stability status

The stability field must distinguish:

```text
NOT_REQUESTED
NOT_SUPPLIED
CERTIFIED
WITHHELD
FAILED
```

No stability claim is implied by `COMPOSABLE`.

## 11. Failure and non-composability conditions

A requested composition may be composable, unresolved at evaluation time, noncomposable, or non-applicable. Unresolved outputs may remain present only as request-permitted meta-status results under `COMPOSABLE_WITH_UNRESOLVED_OUTPUTS`; unresolved eligibility is reported as `UNRESOLVED_EVALUATION`.

Examples include:

### F1 — Missing mandatory interface

One of T1, T2, C23, or T3 is absent.

### F2 — Invalid mandatory interface

A required theorem or bridge interface is missing, `NONCONFORMANT`, or `NOT_APPLICABLE` to the request; a used mandatory or optional output has status `FAILED`, `NOT_APPLICABLE`, or `HEURISTIC`; or a used obligation lacks sufficient completeness for the requested semantic conclusion.

### F3 — Version incompatibility

Interfaces use incompatible theorem versions without a certified translation.

### F4 — Object mismatch

An observation, branch, candidate, state, claim, or report object changes identity across interfaces.

### F5 — Unit or coordinate mismatch

Shared quantities use incompatible units, coordinates, sign conventions, clock scales, or frequency coordinates.

### F6 — Model substitution

A downstream stage changes the propagation, clock, geometry, calibration, path, or branch model without an explicit certified mapping.

### F7 — Candidate-domain omission

Candidates are omitted without a certificate path sufficient for T3.

### F8 — Silent pruning

A candidate is pruned because an optimizer failed, a sample was absent, an inner approximation was empty, or a tolerance was exceeded without a valid emptiness or report-preserving certificate.

### F9 — State-set substitution

A point estimate or sample cloud is used in place of the complete compatible set without an exhaustiveness proof.

### F10 — Gauge mismatch

Gauge-fixed coordinates are compared or composed as though they were unique physical states.

### F11 — Claim-map or resolution mismatch

T3 and optional T4 use different claim or report semantics without a certified mapping.

### F12 — Certificate-type or result-status upgrade

A conservative, heuristic, unresolved, or one-sided result is reported as exact.

### F13 — Completeness suppression

An incomplete search, unresolved candidate, or failed certificate is omitted from the composed status.

### F14 — Assumption suppression

A required upstream assumption is removed from the composed assumption ledger.

### F15 — Unsupported stability claim

A T4 conclusion is reported when T4 is absent, incompatible, or outside its perturbation domain.

### F16 — Unsupported raw-observation scope

Raw-observation-to-report composition is claimed without a valid E0 interface.

### F17 — Request-support mismatch

A requested semantic conclusion is not supported by the selected eligible outputs, or the request requires unresolved meta-status while prohibiting unresolved preservation.

### F18 — Invalid or missing support derivation

A requested semantic conclusion lacks a valid `D_5(Q)`, uses a prohibited operation, omits a transitive dependency, or fails `Supports_5`.

### F19 — Unresolved evaluation

Mandatory applicability, common-domain nonemptiness, version compatibility, required identity mapping, or dependency closure cannot yet be certified.

### F20 — Empty composition domain

The common mandatory domain is certified empty or the request is definitively outside the applicable domain.

---

## 12. Claims not established

Theorem 5 does not establish:

- that any candidate is physically true;
- that any source is authentic;
- that any recording is unedited;
- that evidence integrity is satisfied;
- that a unique candidate exists;
- that a unique physical state exists;
- that an exact state set has been computed;
- that report-level closure implies candidate-level closure;
- that a preferred objective minimizer is admissible or true;
- that a stable result is globally identifiable;
- that adding witnesses improves complete inference reliability;
- that a score is a calibrated probability;
- that the underlying model is empirically correct;
- that an implementation is correct;
- that computation terminates efficiently;
- or that the result is forensically or legally admissible.

---

## 13. Relationship to AIRS

AIRS may provide:

- procedural context;
- audit requirements;
- event-association records;
- calibration records;
- branch declarations;
- integrity-status reporting;
- and inference-classification terminology.

AIRS is not automatically a mathematical premise of T5.

Any AIRS object used as a theorem input must enter through a declared mathematical interface whose assumptions, units, coordinates, uncertainty, and semantics are explicit.

T5 composition status must remain separate from:

- AIRS evidence-integrity status;
- AIRS acquisition-history status;
- and legal or operational interpretation.

---

## 14. Implementation-profile note

The theorem does not standardize software architecture.

An implementation may use non-normative bookkeeping objects such as:

```text
H_cert
H_work
```

to track certified and unresolved computation.

Such objects are not T2 or T3 theorem interfaces unless formally incorporated into those documents.

If used, the implementation profile must define them explicitly and preserve the theorem-defined meanings of:

```text
H_raw
Ĥ_raw
H_cons
Ĥ_cons
S_h^(2)
S_h^(23)
C_rep
```

Software conformance, serialization, APIs, orchestration, security, storage, and performance requirements should be specified in a separate implementation or composition-conformance document.

They are not part of the principal mathematical theorem.

---

## 15. Validation requirements

Before T5 is treated as independently validated, the project should provide:

1. an independent mathematical review of the principal theorem and proof;
2. a machine-readable interface registry for T1–T4, AWC-IF-C23 version 0.1, and E0;
3. unit and dimensional-consistency checks;
4. candidate and branch identity tests;
5. representation-type, certificate-type, result-status, valid-weakening, and directional-containment tests;
6. tests that unresolved and incomplete statuses cannot be silently upgraded;
7. composition tests with and without T4;
8. composition tests with and without E0;
9. negative tests for every failure condition in Section 11;
10. report-level versus candidate-level closure tests;
11. version-compatibility and migration tests;
12. reproducible request-specific `Evaluate_5(J,R_5)` audit-record examples and `Compose_5(J,R_5)` certificate examples;
13. tests proving that heuristic artifacts cannot become theorem-certified conclusions;
14. scenario-identity and injective-domain-alignment tests;
15. tests separating semantic entailment from meta-status preservation;
16. request-relative eligibility and selected-output tests;
17. independent conformance tests for `AWC-IF-C23` version 0.1;
18. used-mandatory versus used-optional dependency tests;
19. independent presence, conformance, and applicability tests;
20. interface-slot tests for present, missing-required, and not-supplied cases;
21. dependency-closure and omitted-transitive-dependency tests;
22. unresolved-evaluation classification tests;
23. `AuditPreserved_5` predicate tests;
24. target-identity and certified-derivation tests;
25. and `Supports_5` derivation-soundness tests.

Passing implementation tests would validate an implementation profile, not the theorem by itself.

---

## 16. Revision history

| Version | Date | Summary |
|---|---:|---|
| 3.6.0-beta1 | 2026-07-12 | Removed the stale combined conformance model; introduced interface slots so absent interfaces are represented without nonexistent interface objects; made `Used(J,R_5)` the least dependency-closed support set; added `UNRESOLVED_EVALUATION`; extracted the `AuditPreserved_5` predicate; clarified target-semantic-object preservation and certified derivation; introduced `D_5(Q)` and `Supports_5`; made optional assumptions request-relative; corrected E0 scope corollaries; and expanded record, failure, proof, validation, and summary requirements. |
| 3.5.0-beta1 | 2026-07-12 | Generalized `Used(R_5)` to request-relative `Used(J,R_5)` over mandatory and optional interfaces; added `Used_mand` and `Used_opt`; required used optional outputs to satisfy conclusion-specific eligibility; separated interface presence, conformance, and applicability; introduced recorded certificate-type/result-status weakening relations; limited the principal theorem to successful certificate statuses; moved noncomposable and non-applicable outcomes to `Evaluate_5`; clarified T4, conservative, unresolved, and report-closure corollaries; and updated record fields, failures, validation requirements, metadata, and summary terminology. |
| 3.4.0-beta1 | 2026-07-12 | Parameterized evaluation and composition by a declared request `R_5`; defined request-relative `Used(R_5)` and `Eligible_5`; separated theorem-certified semantic conclusions `Q_sem` from faithful meta-status preservation `M_meta`; restricted scenario-level entailment to semantic conclusions; made unresolved outputs eligible only as request-permitted meta-status results; aligned C10 and F2 with per-output and per-obligation typing; added request-relative composition statuses and failure conditions; and moved the versioned C23 contract to a separate repository interface file. |
| 3.3.0-beta1 | 2026-07-12 | Separated the total audit evaluator `Evaluate_5` from the successful composition operator `Compose_5`; removed C14 self-reference; prohibited heuristic artifacts from serving as theorem-certified premises or conclusions; changed representation, certificate, result-status, and completeness fields to output- or obligation-indexed maps; required a shared scenario space with injective identity-preserving alignment; defined semantic entailment on `U_5`; restricted composition to explicit meaning-preserving operations; corrected mandatory-interface absence, unresolved-output, failure, validation, summary, and supersession terminology. |
| 3.2.0-beta1 | 2026-07-12 | Updated the general interface tuple to separate certificate type, conformance, result status, and completeness; removed unresolved status from the certificate-type taxonomy; separated set, scalar, and heuristic representation classes; added explicit successful-certificate eligibility rules; removed circularity from the principal theorem by proving that eligible inputs yield `Record_5` with successful `Cert_5`; strengthened candidate-equivalence requirements to preserve compatible-state and report semantics; corrected remaining analysis-domain, T4, implementation-profile, summary, and supersession terminology. |
| 3.1.0-beta1 | 2026-07-12 | Added the versioned AWC-IF-C23 bridge; distinguished `S_h^(2)` from the refined `S_h^(23)` and required `S_h^(23) ⊆ S_h^(2)`; replaced the linear exactness hierarchy with typed certificate classes; separated interface conformance from result status; introduced well-typed domain embeddings into a common scenario space; generalized the analysis domain through a coverage certificate; defined `Compose_5`, `Record_5`, and successful `Cert_5`; and strengthened the principal result to a soundness and non-strengthening theorem. |
| 3.0.0-beta1 | 2026-07-12 | Rewrote T5 as the capstone composition and contract-preservation theorem; made T1–T3 mandatory and T4 optional; introduced the explicit C23 compatibility bridge; removed T5’s former pre-T3 candidate-state construction role; distinguished certified-measurement-to-report from raw-observation-to-report composition; aligned notation with T1–T4; added exactness, completeness, optional-interface, and provenance conditions; and separated implementation conformance from the mathematical theorem. |
| 2.0.0-beta1 | 2026-07-12 | Prior mathematical draft combining candidate-state construction, recovery objects, composition, reporting, and conformance requirements. Superseded by version 3.0.0-beta1. |

---

## 17. Summary

T5 certifies request-relative composition; it does not perform the upstream inference.

The mandatory chain is:

```text
T1 → T2 → C23 → T3 → T5
```

with:

```text
T4 optional
E0 optional
```

C23 is a separately versioned required interface:

```text
Interfaces/
AWC-IF-C23_Candidate-State_Compatibility_Evaluation.md
```

The interface tuple is represented by slots so absent interfaces are auditable without being modeled as nonexistent interface objects:

```text
J
=
(
  Slot_1,
  Slot_2,
  Slot_23,
  Slot_3,
  Slot_4,
  Slot_0
)
```

For every evaluated pair:

```text
Evaluate_5(J,R_5) → Record_5
```

For an eligible pair:

```text
Compose_5
:
Eligible_5
→
Cert_5
```

where:

```text
Cert_5
=
(
  Q_sem,
  M_meta
)
```

The request support set is dependency-closed:

```text
Used(J,R_5)
=
DependencyClosure_J
(
  selected_outputs
  ∪
  required_obligations
)
```

so every transitive output, assumption, mapping, completeness obligation, and provenance dependency is preserved.

Every semantic conclusion `Q ∈ Q_sem` requires a valid derivation:

```text
D_5(Q)
```

satisfying:

```text
Supports_5
(
  Γ_upstream,
  U_5,
  Q,
  D_5(Q)
)
```

and therefore:

```text
Γ_upstream ⊨_{U_5} Q
```

`M_meta` faithfully preserves:

- interface-slot presence;
- interface conformance;
- interface applicability;
- result statuses;
- obligation completeness;
- unresolved outputs;
- optional-interface status;
- request parameters;
- dependency closure;
- audit preservation;
- and provenance.

A successful certificate preserves the identity of each target semantic object or records its certified derivation from the source object. Certificate types and result statuses are preserved or validly weakened only through explicit recorded transitions.

Heuristic artifacts may be preserved in `Record_5`, but they do not become theorem-certified semantic conclusions.

Unresolved outputs may be preserved only as request-permitted meta-status results and may not support substantive semantic conclusions.

`Evaluate_5` distinguishes:

```text
COMPOSABLE
COMPOSABLE_WITH_UNRESOLVED_OUTPUTS
UNRESOLVED_EVALUATION
NONCOMPOSABLE
NOT_APPLICABLE
```

Only the first two statuses permit a successful `Cert_5`.

T5 establishes nothing stronger than the interfaces it composes. All other evaluated requests produce only `Record_5`, not a successful `Cert_5`.

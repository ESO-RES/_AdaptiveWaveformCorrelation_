# AWC-IF-C23 — Candidate-State Compatibility Evaluation Interface

```text
Interface ID: AWC-IF-C23
Version: 0.1
Date: 2026-07-12
Status: Internally frozen bridge-interface baseline

Consumes:
    • AWC-THM-2 candidate-domain and compatible-state outputs

Produces for:
    • AWC-THM-3 report-closure inputs
    • AWC-THM-5 composition and contract-preservation verification

Consumed by:
    • AWC-THM-5 version 3.6.0-beta1

Normative status:
    Non-normative research specification

Validation status:
    Not independently validated

Change policy:
    Semantic changes require a new interface version.
    Schema, serialization, implementation, and performance details
    belong in supporting specifications.
```

---

## 1. Purpose

AWC-IF-C23 defines the required bridge between:

```text
T2 finite candidate construction
```

and:

```text
T3 claim/report closure
```

The interface declares how T2 candidates are associated with exact or certified-enclosure compatible-state objects suitable for T3.

It is a mathematical interface contract. It is not an algorithm.

C23 does not:

- form T1 measurements;
- enumerate the T2 candidate domain;
- alter T2 branch or integer-vector identity;
- replace the T2-compatible state definition;
- select a preferred candidate;
- optimize an objective;
- perform T3 report closure;
- prove T4 perturbation stability;
- establish physical truth or authenticity;
- or specify software architecture.

Its function is to preserve and expose:

- candidate identity;
- state-set refinement;
- candidate-domain coverage;
- certified feasibility or emptiness;
- pruning and equivalence bases;
- enclosure direction;
- completeness;
- assumptions;
- limitations;
- and provenance.

---

## 2. Position in the AWC dependency structure

The required mathematical sequence is:

```text
T1 → T2 → C23 → T3 → T5
```

with optional T4 after T3 and before or into T5 composition.

C23 is not a theorem that replaces T2 or T3.

It consumes the candidate and state-set objects established by T2 and produces a versioned compatibility interface that T3 may use to establish report-level conclusions.

---

## 3. Interface object

A supplied C23 interface is represented abstractly by:

```text
I_23
=
(
  id_23,
  version_23,
  inputs_23,
  outputs_23,
  obligations_23,
  assumptions_23,
  domain_23,
  model_23,
  coordinates_23,
  units_23,
  gauges_23,
  representation_type_23,
  certificate_type_23,
  conformance_23,
  applicability_23,
  result_status_23,
  completeness_23,
  provenance_23
)
```

The interface must satisfy:

```text
id_23 = AWC-IF-C23
```

and:

```text
version_23 = 0.1
```

when consumed by AWC-THM-5 version 3.6.0-beta1.

Presence is represented by the consuming document’s interface slot and is not stored inside an absent C23 interface object.

---

## 4. Required T2 inputs

C23 consumes the exact T2 objects declared by the referenced T2 version.

At minimum, the input contract identifies:

```text
B
```

the finite branch set;

```text
A_b
```

the observation-index set for branch `b`;

```text
H_raw
```

the exact raw candidate domain;

```text
Ĥ_raw
```

the conservative raw candidate domain, when finite-precision endpoint handling requires it;

```text
H_cons
```

the exact compatible candidate domain defined by T2;

```text
Ĥ_cons
```

the conservative-domain compatible candidate set defined by T2; and:

```text
S_h^(2)
```

the T2-compatible state set for candidate:

```text
h = (b,n_b)
```

C23 must also consume or reference:

- T2 document ID and version;
- candidate and branch identifiers;
- observation identifiers;
- exact and conservative endpoint conventions;
- T2 assumptions;
- state coordinates;
- units;
- gauge conventions;
- model and constraint definitions;
- dependency metadata;
- representation and certificate types;
- result statuses;
- completeness statuses;
- and provenance.

Under T2’s declared assumptions:

```text
Ĥ_cons = H_cons
```

C23 preserves this theorem-defined equality.

C23 must not reinterpret `Ĥ_cons` as an unresolved implementation queue or a heuristic work list.

---

## 5. Candidate and state identity

Every candidate retains its T2 identity:

```text
h = (b,n_b)
```

where:

- `b` is the T2 branch identity;
- and `n_b` is the corresponding integer-vector identity.

Relabeling is permitted only through an explicit bijection or certified identity-preserving map.

For every analyzed candidate, C23 must identify the same T2 state variable:

```text
θ
```

or provide a certified coordinate transformation preserving the same physical or quotient-state meaning.

C23 may not:

- merge distinct candidates without a certified equivalence;
- split one candidate without recording the resulting identity relation;
- change branch semantics;
- reinterpret an observation;
- or silently replace the T2 state model.

---

## 6. Declared analysis domain

C23 declares an analysis domain:

```text
D_analysis ⊆ Ĥ_raw
```

`D_analysis` contains the candidates for which C23 supplies direct refined-state objects or certified bounds.

The declaration of a finite `D_analysis` does not by itself establish complete candidate coverage.

C23 must separately provide a coverage account for every candidate in:

```text
Ĥ_raw \ D_analysis
```

---

## 7. Candidate-state refinement

For every:

```text
h ∈ D_analysis
```

C23 declares an additional compatibility predicate:

```text
F_h^(23)(θ)
```

and defines the refined compatible-state set:

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

This containment is mandatory.

C23 may add declared compatibility constraints, but it may not enlarge or silently redefine the T2-compatible state set.

Every added constraint must be identified and linked to its assumptions and provenance. Examples include:

- additional timing constraints;
- propagation constraints;
- geometry constraints;
- calibration constraints;
- branch constraints;
- dependency constraints;
- evidence-validity conditions;
- alternate-model restrictions;
- claim-map compatibility conditions;
- or reporting-related compatibility conditions.

A changed propagation, clock, geometry, calibration, path, or branch model requires an explicit certified mapping or conservative-refinement relation.

---

## 8. Certified state bounds

For each analyzed candidate, C23 may provide:

```text
W_h ⊆ S_h^(23) ⊆ O_h
```

where:

- `W_h` is a certified inner feasible witness set;
- `O_h` is a certified outer state enclosure;
- and both refer to the same target state set `S_h^(23)`.

The following implications are permitted:

```text
O_h = ∅
⇒
S_h^(23) = ∅
```

and:

```text
W_h ≠ ∅
⇒
S_h^(23) ≠ ∅
```

The converse implications do not follow without a separate proof.

In particular:

- `W_h = ∅` does not certify `S_h^(23) = ∅`;
- failure to find a witness does not certify emptiness;
- an optimizer failure does not certify emptiness;
- a timeout does not certify emptiness;
- absence of samples does not certify emptiness;
- and a finite point cloud does not replace the complete state set without an exhaustiveness proof.

---

## 9. Candidate coverage contract

C23 must provide a candidate-coverage object:

```text
Coverage_23
```

defined over:

```text
Ĥ_raw
```

For every candidate `h ∈ Ĥ_raw`, the coverage object must record at least one disposition:

```text
CandidateDisposition
=
{
  DIRECTLY_ANALYZED,
  CERTIFIED_EXCLUDED_FROM_H_RAW,
  CERTIFIED_COMPATIBILITY_EMPTY,
  CERTIFIED_EQUIVALENT,
  REPORT_PRESERVING_COVERED,
  UNRESOLVED
}
```

The dispositions have the following meanings.

### 9.1 Directly analyzed

```text
h ∈ D_analysis
```

and C23 supplies `S_h^(23)` or a certified bound on it.

### 9.2 Certified exclusion

A valid certificate establishes:

```text
h ∉ H_raw
```

under the declared T2 endpoint and branch conventions.

### 9.3 Certified compatibility emptiness

A valid certificate establishes:

```text
S_h^(23) = ∅
```

Examples include an exact contradiction proof or:

```text
O_h = ∅
```

for a certified outer enclosure.

### 9.4 Certified equivalence

A valid certificate maps `h` to an analyzed candidate:

```text
e(h) ∈ D_analysis
```

and preserves every semantic object required downstream, including as applicable:

- compatible-state meaning;
- physical-equivalence or gauge meaning;
- claim-map image;
- resolution-map image;
- report-image meaning;
- certificate direction;
- assumptions;
- and provenance.

Candidate identity is not erased; the equivalence relation is recorded.

### 9.5 Report-preserving coverage

A valid T3-compatible certificate establishes that omitting direct state analysis for `h` cannot change the applicable report-level result.

This path must identify:

- the report object preserved;
- the claim and resolution maps used;
- the direction of any enclosure;
- the assumptions and domain;
- and the proof or certificate basis.

### 9.6 Unresolved coverage

No permitted certified path has yet been established.

An unresolved candidate must remain explicitly represented in the interface status and completeness records.

It may not be silently removed.

---

## 10. Coverage certificate

The interface must provide:

```text
coverage_certificate_23
```

that records:

- the declared `D_analysis`;
- the disposition of every candidate in `Ĥ_raw`;
- the certificate or proof basis for every certified non-direct disposition;
- the recorded reason and unresolved-status basis for every `UNRESOLVED` disposition;
- unresolved candidates;
- candidate-domain version and identity;
- completeness status;
- assumptions;
- domain;
- and provenance.

The coverage certificate may be:

```text
COMPLETE
```

only when every candidate in `Ĥ_raw` has a permitted certified disposition other than `UNRESOLVED`.

It may be:

```text
CERTIFIED_PARTIAL
```

when a certified subset of the domain is completely covered and the uncovered portion is explicitly identified.

Finiteness of `Ĥ_raw` does not itself establish complete coverage.

---

## 11. Pruning rules

A candidate may be removed from direct downstream consideration only through one of the following:

1. certified exclusion from `H_raw`;
2. exact proof that `S_h^(23) = ∅`;
3. an empty certified outer enclosure `O_h = ∅`;
4. certified equivalence preserving the required downstream semantics;
5. or a T3-valid report-preserving coverage certificate.

The following are not pruning certificates:

- optimizer failure;
- solver nonconvergence;
- timeout;
- absence of samples;
- an empty inner approximation;
- failure to find a feasible point;
- a high objective value without a theorem linking it to emptiness;
- an undocumented numerical tolerance;
- or manual omission.

Every pruning decision must preserve candidate identity, certificate direction, assumptions, domain, and provenance.

---

## 12. Per-output typing

For every C23 output `y`, the interface records:

```text
representation_type_23(y)
```

and:

```text
result_status_23(y)
```

When the output is mathematically certified, it also records:

```text
certificate_type_23(y)
```

The certificate-type map is partial.

A heuristic artifact has:

```text
representation_type_23(y)
=
HEURISTIC_ARTIFACT
```

```text
result_status_23(y)
=
HEURISTIC
```

and no certificate type.

A heuristic artifact may be preserved for audit but may not support:

- certified feasibility;
- certified emptiness;
- certified exclusion;
- certified equivalence;
- complete candidate coverage;
- or theorem-certified report closure.

---

## 13. Permitted representation and certificate classes

C23 uses the representation and certificate meanings consumed by T5.

### 13.1 Representation types

```text
CANDIDATE_DOMAIN
STATE_SET
REPORT_IMAGE
SCALAR_QUANTITY
LOGICAL_STATUS
HEURISTIC_ARTIFACT
```

### 13.2 Set certificate types

```text
ExactSet
CertifiedInnerSet
CertifiedOuterSet
CertifiedTwoSidedEnclosure
```

### 13.3 Scalar certificate types

```text
ExactScalar
CertifiedLowerBound
CertifiedUpperBound
CertifiedIntervalBound
```

### 13.4 Logical and status certificate types

```text
ExactLogicalCertificate
StatusPreservationCertificate
```

### 13.5 Result statuses

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

Certificate type, representation type, result status, and obligation completeness are distinct fields.

---

## 14. Completeness obligations

C23 must track at least the following obligations separately:

```text
candidate_identity_preservation
candidate_enumeration_reference
candidate_coverage
exact_domain_membership
compatibility_constraint_declaration
compatibility_evaluation
state_refinement_containment
state_enclosure
feasibility_certification
emptiness_certification
pruning_justification
equivalence_justification
report_preservation_justification
assumption_preservation
model_and_constraint_preservation
gauge_preservation
provenance
```

Each obligation receives one status:

```text
COMPLETE
CERTIFIED_PARTIAL
INCOMPLETE
UNRESOLVED
NOT_APPLICABLE
```

Completion of one obligation does not imply completion of another.

For example:

```text
candidate_coverage = COMPLETE
```

does not imply:

```text
state_enclosure = COMPLETE
```

and:

```text
feasibility_certification = COMPLETE
```

does not imply report-level closure.

---

## 15. Required output package

The C23 interface must provide or explicitly record:

```text
interface_id
interface_version
T2_document_id
T2_version
T3_target_document_id
candidate_domain_identity
H_raw_reference
Ĥ_raw_reference
H_cons_reference
Ĥ_cons_reference
D_analysis
Coverage_23
coverage_certificate_23
S_h^(2)_references
F_h^(23)_definitions
S_h^(23)_definitions_or_references
W_h_by_candidate_when_available
O_h_by_candidate_when_available
candidate_dispositions
retained_candidates
pruned_candidates
equivalent_candidates
report_preserving_covered_candidates
unresolved_candidates
pruning_certificates
equivalence_certificates
report_preservation_certificates
representation_type_by_output
certificate_type_by_output_when_applicable
result_status_by_output
completeness_status_by_obligation
assumption_ledger
model_and_constraint_ledger
identity_mappings
coordinate_and_unit_mappings
gauge_conventions
domain
limitations
provenance
```

The package may be human-readable or machine-readable, provided these meanings remain explicit.

---

## 16. Assumption and domain preservation

C23 must preserve every T2 assumption required by a consumed T2 object.

Every new C23 constraint must identify its own assumptions.

The C23 assumption ledger is:

```text
A_23
```

and must distinguish:

- inherited T2 assumptions;
- new C23 assumptions;
- discharged assumptions, if separately proved;
- unresolved assumptions;
- and non-applicable assumptions.

C23 conclusions apply only on the declared interface domain:

```text
U_23
```

No C23 conclusion may be extended outside `U_23` by relabeling or composition.

---

## 17. Gauge, coordinate, and unit preservation

C23 must identify:

- state coordinates;
- time and frequency coordinates;
- spatial coordinates;
- angular conventions;
- sign conventions;
- units;
- clock scales;
- gauge choices;
- and physical-equivalence relations.

A coordinate or unit transformation must be explicit and uncertainty-preserving.

A gauge-fixed state must not be interpreted as a unique physical state unless the applicable quotient or gauge conditions establish uniqueness.

---

## 18. Conformance and applicability

A supplied C23 interface receives one conformance state:

```text
CONFORMANT
NONCONFORMANT
NOT_EVALUATED
```

It is `CONFORMANT` only when:

1. the interface ID and version are declared;
2. the consumed T2 version is declared;
3. candidate identity is preserved;
4. `D_analysis ⊆ Ĥ_raw`;
5. every declared `S_h^(23)` satisfies:

```text
S_h^(23) ⊆ S_h^(2)
```

6. every non-direct certified disposition in:

```text
CERTIFIED_EXCLUDED_FROM_H_RAW
CERTIFIED_COMPATIBILITY_EMPTY
CERTIFIED_EQUIVALENT
REPORT_PRESERVING_COVERED
```

has a permitted certificate basis;
7. every candidate with disposition `UNRESOLVED` is explicitly recorded with unresolved result and completeness status, retained in the coverage account, and not silently pruned;
8. output typing and obligation completeness are recorded;
9. assumptions, domains, limitations, and provenance are preserved;
10. no heuristic artifact is represented as certified;
11. and no unresolved candidate is silently omitted.

A conformant interface receives one request-relative applicability state:

```text
APPLICABLE
NOT_APPLICABLE
UNRESOLVED
```

Applicability is evaluated by the consuming T3 or T5 request against the declared C23 domain, candidate identities, maps, versions, and required obligations.

---

## 19. Relationship to T3

T3 may consume:

- `D_analysis`;
- `Coverage_23`;
- `coverage_certificate_23`;
- exact `S_h^(23)` objects;
- certified `W_h` and `O_h`;
- pruning certificates;
- equivalence certificates;
- report-preserving coverage certificates;
- gauge and physical-equivalence treatment;
- claim-map and resolution-map compatibility;
- per-output representation, certificate, and result statuses;
- obligation-level completeness;
- assumptions;
- domain;
- limitations;
- and provenance.

C23 does not establish report-level closure.

T3 remains responsible for establishing any report-image sandwich, report-class closure, classification, unresolved status, or retained-domain certificate.

---

## 20. Relationship to T5

T5 may verify that C23:

- is present in the required interface slot;
- has interface ID `AWC-IF-C23`;
- has version `0.1`;
- is conformant and applicable to the declared request;
- preserves T2 candidate and state identity;
- satisfies `S_h^(23) ⊆ S_h^(2)`;
- provides the coverage and completeness information required by the request;
- preserves representation, certificate, result-status, assumption, domain, limitation, and provenance information;
- and composes with T3 without strengthening any upstream conclusion.

T5 does not execute C23, construct `S_h^(23)`, prove emptiness, or generate coverage certificates.

---

## 21. Failure and unresolved conditions

Conditions C23-F1 through C23-F11 are nonconformance or failure conditions when established.

C23-F12 is an unresolved-status condition. It does not by itself make a faithfully recorded interface nonconformant, but it limits downstream conclusions and may prevent a requested successful T5 certificate.

### C23-F1 — Candidate identity mismatch

A branch, integer vector, observation, or state object changes identity without a certified map.

### C23-F2 — State-set enlargement

A declared refined state set does not satisfy:

```text
S_h^(23) ⊆ S_h^(2)
```

### C23-F3 — Undeclared constraint substitution

A model or constraint is changed without an explicit mapping or conservative-refinement certificate.

### C23-F4 — Candidate omission

A candidate in `Ĥ_raw` has no direct analysis entry and no declared coverage disposition.

### C23-F5 — Invalid pruning

A candidate is pruned using optimizer failure, timeout, absent samples, empty inner approximation, or an undocumented tolerance.

### C23-F6 — Invalid emptiness claim

Emptiness is inferred without an exact contradiction proof or an empty certified outer enclosure.

### C23-F7 — Invalid equivalence

Candidates are treated as equivalent without preserving the downstream state, gauge, claim-map, resolution-map, and report-image semantics required by the request.

### C23-F8 — Certificate-direction error

An inner, outer, exact, or two-sided object is reinterpreted in an invalid direction.

### C23-F9 — Completeness suppression

An unresolved, partial, or incomplete obligation is reported as complete.

### C23-F10 — Heuristic upgrade

A heuristic artifact is used as a certified feasibility, emptiness, exclusion, equivalence, coverage, or closure result.

### C23-F11 — Assumption or provenance suppression

A required assumption, domain limitation, transformation, or provenance link is omitted.

### C23-F12 — Unresolved coverage

One or more candidates remain `UNRESOLVED`.

This condition does not automatically make the interface nonconformant when the unresolved status is faithfully recorded, but it limits downstream conclusions and may prevent a requested successful T5 certificate.

---

## 22. Claims not established

AWC-IF-C23 does not establish:

- that any candidate is physically true;
- source authenticity;
- recording integrity;
- evidence admissibility;
- unique candidate identity;
- unique physical state;
- exact report closure;
- candidate-level closure;
- perturbation stability;
- calibrated probability;
- empirical model validity;
- implementation correctness;
- computational complexity;
- or operational readiness.

---

## 23. Validation requirements

Before AWC-IF-C23 version 0.1 is treated as independently validated, the project should provide:

1. independent mathematical review;
2. candidate-identity preservation tests;
3. T2 version and endpoint-convention tests;
4. `D_analysis ⊆ Ĥ_raw` tests;
5. state-refinement containment tests;
6. exact, inner, outer, and two-sided certificate-direction tests;
7. certified feasibility tests;
8. certified emptiness tests;
9. negative tests for optimizer-failure and timeout pruning;
10. complete and partial candidate-coverage tests;
11. omitted-candidate detection tests;
12. equivalence-preservation tests;
13. report-preserving coverage tests;
14. gauge and coordinate consistency tests;
15. unit and dimensional-consistency tests;
16. assumption-ledger tests;
17. output-typing tests;
18. obligation-completeness tests;
19. heuristic-isolation tests;
20. unresolved-candidate preservation tests;
21. provenance tests;
22. T2-to-C23 integration tests;
23. C23-to-T3 integration tests;
24. and C23-to-T5 conformance tests.

Passing implementation tests validates an implementation profile, not this mathematical interface by itself.

---

## 24. Revision history

| Version | Date | Summary |
|---|---:|---|
| 0.1 | 2026-07-12 | Established the versioned T2-to-T3 candidate-state compatibility interface consumed by frozen AWC-THM-5 version 3.6.0-beta1; defined candidate identity, `D_analysis`, `S_h^(23) ⊆ S_h^(2)`, certified state bounds, candidate dispositions, coverage certificates, pruning and equivalence rules, per-output typing, obligation completeness, conformance, applicability, downstream handoff, nonclaims, and validation requirements; and corrected conformance handling so faithfully recorded `UNRESOLVED` dispositions do not require a nonexistent certificate basis or automatically make the interface nonconformant. |

---

## 25. Summary

AWC-IF-C23 is the required versioned bridge:

```text
T2 → C23 → T3
```

It preserves the T2 candidate identity:

```text
h = (b,n_b)
```

and defines only a refinement:

```text
S_h^(23)
=
{
  θ ∈ S_h^(2) :
  F_h^(23)(θ)
}
```

with:

```text
S_h^(23) ⊆ S_h^(2)
```

It requires a declared analysis domain:

```text
D_analysis ⊆ Ĥ_raw
```

and a certified or explicitly unresolved disposition for every candidate in `Ĥ_raw`.

It may provide:

```text
W_h ⊆ S_h^(23) ⊆ O_h
```

but an empty inner set or failed search never certifies emptiness.

C23 does not perform report closure or end-to-end composition. It supplies the candidate-state, coverage, certificate, completeness, assumption, limitation, and provenance objects consumed by T3 and verified by T5.

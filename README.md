# Adaptive Waveform Correlation (AWC)

> **A theorem-aligned research framework for conditional acoustic inference, finite ambiguity analysis, report closure, perturbation stability, end-to-end composition, and witness-cloud scaling.**

**README revision:** 1.9  
**Architecture alignment date:** 2026-07-12  
**Document status:** Research specification; non-operational

Adaptive Waveform Correlation (AWC) is a mathematical research framework for analyzing acoustic observations collected by asynchronous and distributed devices. AWC does not treat a numerical solution as self-validating. It keeps measurements, assumptions, discrete hypotheses, compatible state sets, report classes, uncertainty domains, composition contracts, and scaling claims separate so that each conclusion can be traced to declared conditions.

AWC is developed alongside the **Draft Acoustic Incident Reconstruction Specification (AIRS)**, a proposed auditable workflow for physics-constrained analysis of separately acquired recordings.

> [!IMPORTANT]
> This repository is a research specification. It is **not** a validated forensic standard, certified localization product, completed software implementation, or empirical performance study. It does not yet include a reference implementation, automated test suite, benchmark dataset, or reproducible validation pipeline.

![AWC theorem-aligned framework overview](_AWC_Framework.PNG)

## Core principles

- Every certification claim is conditional on explicit assumptions.
- Model compatibility is not equivalent to physical truth, source authenticity, causality, or evidence integrity.
- Wrapped-phase ambiguity must be represented rather than silently discarded.
- Exact domains and conservative finite-precision supersets must remain distinguishable.
- Report-level closure is weaker than candidate-level or exact state-set closure.
- Theorem interfaces must preserve units, coordinates, domains, exactness classes, and semantic meaning.
- Perturbation stability does not convert a preferred candidate into ground truth.
- Witness scaling requires a declared probability model, dependence model, event-acceptance model, and aggregation rule.
- Non-resolution, incompatibility, and incomplete search are valid reportable outcomes.
- Numerical convergence alone does not establish a valid inference.

## Repository status

The current theorem architecture and AIRS workflow are documented, but the repository is not yet an independently validated end-to-end system.

| Area | Current state |
|---|---|
| AIRS specification | Research Draft 0.1 — internally stabilized; not independently validated |
| Theorems 1–2 | Mathematical drafts |
| Theorems 3–4 | Internally frozen 1.0 research documents; not independently validated |
| Theorem 5 | Mathematical draft, version 2.0.0-beta1 |
| Theorem 6 | Mathematical draft, version 2.0.0-beta1; revision required |
| Reference implementation | Not included |
| Automated tests | Not included |
| Benchmark data | Not included |
| Reproducible empirical validation | Not included |
| Architecture figures | Proposed conceptual assets; not evidence of implementation or performance |

“Draft,” “Frozen,” and version numbers describe internal document revision states. They do not imply independent peer review, mechanized proof verification, empirical validation, certification, or operational readiness.

## Suggested reading order

1. Read **Core principles** and **Scope and non-claims**.
2. Review the **AWC Framework** figure.
3. Read T1–T3 for the primary inference path.
4. Read T4 for optional perturbation-stability analysis.
5. Read T5 for interface composition and contract preservation.
6. Read T6 together with its current revision limitations.
7. Use AIRS for procedural and audit context.

## Theorem series

| Theorem | Document | Declared maturity | Validation status |
|---|---|---|---|
| T1 | [Conditional Relative Same-Event Measurement Formation](Theorems/Theorem_1_Conditional_Relative_Same_Event_Measurement_Formation.md) | Theorem Draft 0.5 | Not independently validated |
| T2 | [Finite Integer Ambiguity Under Bounded Admissible Differences](Theorems/Theorem_2_Finite_Integer_Ambiguity_Under_Bounded_Admissible_Differences.md) | Theorem Draft 0.7 | Not independently validated |
| T3 | [Conditional Resolution-Level Report Closure and Classification](Theorems/Theorem_3_Conditional_Resolution_Level_Report_Closure_and_Classification.md) | Internally frozen 1.0 | Not independently validated |
| T4 | [Conditional Perturbation-Stable Candidate and Report-Class Recovery](Theorems/Theorem_4_Conditional_Perturbation_Stable_Candidate_and_Report_Class_Recovery.md) | Internally frozen 1.0 | Not independently validated |
| T5 | [Conditional End-to-End Inference Composition](Theorems/Theorem_5_Conditional_End-to-End_Inference_Composition.md) | Mathematical Draft 2.0.0-beta1 | Not independently validated |
| T6 | [Conditional Witness-Cloud Scaling](Theorems/Theorem_6_Certified_Witness-Cloud_Scaling.md) | Mathematical Draft 2.0.0-beta1 | Not independently validated; mathematical and metadata revision pending |

> [!NOTE]
> The T6 link retains the current repository filename. The displayed title is intentionally qualified as “Conditional” because the present draft does not establish complete inference reliability.

### What each theorem addresses

**T1 — Conditional measurement formation.** Defines conditions under which two observers may produce a bounded-error, relative, same-event wrapped-phase observation. It does not infer absolute source range from raw microphone phase.

**T2 — Finite integer ambiguity.** Gives sufficient conditions under which integer-cycle ambiguity reduces to a finite exact domain or a conservative outward-rounded domain. It does not guarantee existence, uniqueness, exhaustive search, or physical correctness of a surviving candidate.

**T3 — Report closure and classification.** Defines conditions for establishing the complete report-class image of compatible states at a declared resolution, relative to the declared model, candidate domain, and certified search-completeness status. It distinguishes report-level closure from stronger candidate-level and exact state-set closure.

**T4 — Perturbation-stable recovery.** Gives sufficient conditions for candidate identity, report-class identity, or local gauge-fixed state behavior to remain stable over a declared perturbation set. Objective separation does not establish truth, authenticity, or integrity.

**T5 — End-to-end composition.** Requires valid T1–T3 interfaces and may additionally consume a valid T4 stability interface when T4 is invoked. It must preserve units, domains, exactness status, uncertainty meaning, and semantic contracts without strengthening, reinterpreting, or silently replacing upstream conclusions. T5 is a composition and contract-preservation theorem, not an optimization stage.

**T6 — Conditional witness-cloud scaling.** Develops model-dependent bounds for wrong-hypothesis survival as additional witnesses are incorporated. The current draft does not by itself establish complete inference reliability; correct-hypothesis retention, false rejection, family-wise error, dependence, and aggregation rules require explicit treatment.

## Dependency and processing views

The repository separates formal theorem dependency from conceptual processing order and optional analysis stages.

### Current architectural intent

```text
T1 → T2 → T3 ───────────────→ T5 → T6
              └→ [T4] ──────→┘
```

- T1 forms conditional pairwise observations.
- T2 constructs finite exact or conservative candidate domains.
- T3 establishes report-level closure and classification over certified candidate accounting.
- T4 is an optional perturbation-stability analysis.
- T5 requires valid T1–T3 interfaces and may additionally consume a declared T4 interface when T4 is invoked.
- T5 must not strengthen, reinterpret, or silently replace upstream conclusions.
- T6 applies a declared witness-dependence model to derive conditional scaling bounds.

> [!NOTE]
> The architecture figures treat T4 as optional. The current T5 document metadata still lists T4 under `Depends on`; that document-level dependency statement must be reconciled in a later theorem revision.

### Conceptual inference flow

```text
Raw recordings, metadata, calibration, event association,
and environmental/propagation information
                         │
                         ▼
T1: pairwise, same-event, bounded relative measurements
                         │
                         ▼
T2: finite branch-aware candidate construction

    Exact raw domain:
    H_raw

    Conservative outward-rounded domain:
    H_raw ⊆ Ĥ_raw

    Theorem-defined consistency sets:
    H_cons  = {h ∈ H_raw  : S_h ≠ ∅}
    Ĥ_cons = {h ∈ Ĥ_raw : S_h ≠ ∅}

    T2 proves:
    Ĥ_cons = H_cons
                         │
                         ▼
Certified candidate-state classification

    Non-normative operational bookkeeping sets introduced in this README:

    H_cert:
    candidates for which h ∈ H_raw and S_h ≠ ∅
    are both certified

    H_work:
    candidates not yet eliminated by certified exact-domain
    exclusion or certified compatibility emptiness

    For every h ∈ Ĥ_raw:
    - certify exact T2 membership when possible;
    - prune when h ∉ H_raw is certified;
    - construct or conservatively enclose S_h;
    - add h to H_cert only when h ∈ H_raw and S_h ≠ ∅
      are both certified;
    - retain h in H_work while exact membership or
      compatibility remains unresolved;
    - prune only when exact analysis establishes S_h = ∅
      or a valid certified outer enclosure of S_h is empty;
    - preserve unresolved decisions and record
      search-completeness status.

    Certified-set relationships:
    H_cert ⊆ H_cons = Ĥ_cons ⊆ H_work ⊆ Ĥ_raw

    With complete certified membership and compatibility
    classification:
    H_cert = H_work = Ĥ_cons = H_cons
                         │
                         ▼
T3: claim/report images, closure, and classification
                         │
              ┌──────────┴──────────┐
              │                     │
              │          Optional T4: perturbation-
              │          stability certification
              │                     │
              └──────────┬──────────┘
                         ▼
T5: end-to-end composition and contract preservation
                         │
                         ▼
T6: conditional witness-scaling bounds under a declared
    probability, dependence, event-acceptance, and
    aggregation model
```

`Ĥ_cons` retains its theorem-defined meaning; it is not an unresolved working set. Under T2’s declared definitions and assumptions, the theorem establishes `Ĥ_cons = H_cons`. This equality concerns the theorem-defined compatible-state sets; it does not imply that a finite-precision implementation has completed exact membership, compatibility, or search classification.

`H_cert` and `H_work` are operational bookkeeping sets used to describe incomplete certified computation:

- `H_cert` contains candidates already certified to satisfy exact raw-domain membership and nonempty compatibility.
- `H_work` contains all candidates not yet eliminated by certified exact-domain exclusion or certified compatibility emptiness.
- A failed numerical search, an empty inner approximation, or the absence of a computed point is not sufficient to prune a candidate.

These symbols are not currently theorem-defined interfaces and must not be attributed to T2 or T3 unless they are formally incorporated into those documents.

When `H_cert ≠ H_work`, T3 may report conservative claim-image enclosures or an unresolved closure status. Exact report-level closure may nevertheless be certified when the report-class image induced by `H_cert` is proven equal to the conservative report-class image induced by `H_work` at the declared resolution. Candidate-level classification may therefore remain incomplete even when report-level closure is complete.

## AIRS documentation

- [Draft Acoustic Incident Reconstruction Specification (AIRS) 0.1](docs/AIRS_Standard.md)
- [AIRS Troubleshooting Guide](docs/AIRS_Troubleshooting_Guide.md)

AIRS provides procedural and audit context for testing whether recordings remain compatible with declared timing, propagation, clock, source, path, and geometry models. AIRS is not an independently validated forensic standard and is not automatically a mathematical premise of a theorem unless explicitly imported.

## Examples

The examples are explanatory research guides, not validated case studies:

- [Bat Crack → Glove Thud](examples/Bat_to_Glove.md)
- [Concert Audio Analysis](examples/Concert_Reverberation.md)
- [Sports Stadium Audio Analysis](examples/Stadium_Analysis.md)

## Architecture assets

The repository contains three current architecture figures:

- [AWC Framework](_AWC_Framework.PNG) — theorem-aligned conceptual and epistemic overview.
- [AWC Computational Architecture](Layers/_AWC_Architecture_Layer.PNG) — proposed flow of mathematical objects, candidate sets, numerical operations, and certificates.
- [AWC Implementation Architecture](Layers/_AWC_Implementation_Layer.PNG) — proposed software-module, service, security, provenance, and orchestration design.

The figures are proposed architecture assets. They do not establish that depicted software modules, datasets, tests, performance results, reliability gains, or field validation currently exist.

> [!WARNING]
> The framework figure is the current semantic reference. The computational and implementation figures should be synchronized with the current exact/conservative T2 accounting and optional-T4 interface. Any use of `H_cert` or `H_work` should be identified as non-normative computational bookkeeping unless those symbols are formally added to the theorem interfaces.

### Distinguishing the three figures

| Figure | Primary purpose |
|---|---|
| Framework | Explain theorem dependencies, assumptions, claim strength, exact/conservative status, and valid unresolved outcomes |
| Computational architecture | Explain mathematical data flow and the numerical and set-based operations required to realize the theorem interfaces |
| Implementation architecture | Explain how a future software system could organize services, APIs, storage, audit, trust, and workflow execution |

Legacy conceptual assets are retained for historical reference under:

- [`Layers/diagrams/legacy-conceptual/`](Layers/diagrams/legacy-conceptual/)
- [`Theorems/diagrams/legacy-conceptual/`](Theorems/diagrams/legacy-conceptual/)
- [`diagrams/legacy-conceptual/`](diagrams/legacy-conceptual/)

These assets are historical and non-normative. They may reflect superseded theorem meanings, dependencies, or claims.

## Speculative research notes

- [Cosmic Witness Cloud](research-notes/speculative/cosmic-witness-cloud.md)

Material under `research-notes/speculative/` is exploratory and non-normative. It is outside the theorem series unless separately formalized, reviewed, and incorporated.

## Repository layout

```text
AdaptiveWaveformCorrelation/
├── README.md
├── LICENSE
├── _AWC_Framework.PNG
├── Theorems/
│   ├── Theorem_1_Conditional_Relative_Same_Event_Measurement_Formation.md
│   ├── Theorem_2_Finite_Integer_Ambiguity_Under_Bounded_Admissible_Differences.md
│   ├── Theorem_3_Conditional_Resolution_Level_Report_Closure_and_Classification.md
│   ├── Theorem_4_Conditional_Perturbation_Stable_Candidate_and_Report_Class_Recovery.md
│   ├── Theorem_5_Conditional_End-to-End_Inference_Composition.md
│   ├── Theorem_6_Certified_Witness-Cloud_Scaling.md
│   └── diagrams/legacy-conceptual/
├── docs/
│   ├── AIRS_Standard.md
│   └── AIRS_Troubleshooting_Guide.md
├── examples/
│   ├── Bat_to_Glove.md
│   ├── Concert_Reverberation.md
│   └── Stadium_Analysis.md
├── Layers/
│   ├── _AWC_Architecture_Layer.PNG
│   ├── _AWC_Implementation_Layer.PNG
│   └── diagrams/legacy-conceptual/
├── diagrams/legacy-conceptual/
│   └── _aWc_method_.jpg
└── research-notes/speculative/
    └── cosmic-witness-cloud.md
```

## Scope and non-claims

The repository does **not** by itself certify or establish:

- hardware accuracy, synchronization, or sensor calibration;
- source authenticity, causality, absence of editing, or evidence integrity;
- a unique physical source location in every admissible case;
- implementation correctness, production readiness, or operational availability;
- forensic or legal admissibility;
- empirical superiority over alternative methods;
- calibrated confidence or probability from an objective score alone;
- guaranteed reliability from adding witnesses;
- independent mathematical review or mechanized proof verification.

A conclusion is supported only to the extent that the applicable assumptions, interface contracts, numerical requirements, search-completeness conditions, and uncertainty domains are satisfied.

## Known open issues

1. Reconcile T4 optionality with the current T5 dependency metadata and theorem text.
2. Correct the T6 document identifier and standardize its metadata block.
3. Reconcile the formal T6 document title with the qualified public-facing title used in this README.
4. Define T6 family-wise wrong-hypothesis survival, correct-hypothesis retention, false rejection, empty-set risk, and overall reliability quantities explicitly.
5. Restrict any effective-witness-count result to a declared dependence model or externally certified interface.
6. Standardize theorem metadata, notation, versioning, and cross-theorem interface definitions.
7. Synchronize the computational and implementation figures with the framework’s current T2 candidate accounting, `H_cert`/`H_work` bookkeeping, and optional-T4 semantics.
8. Normalize architecture-asset filenames and add editable figure sources, generation provenance, and an automated relative-link check.
9. Add primary-literature positioning, a bibliography, and `CITATION.cff`.
10. Implement a reference computational realization with automated tests and reproducible validation artifacts.

## Planned validation path

Before empirical or operational claims are made, the project should provide:

1. machine-checkable interface and notation registries;
2. unit and property tests for measurement formation and interval/candidate enumeration;
3. exhaustive small-case tests for exact versus conservative candidate accounting;
4. certified membership, set-image, pruning, and search-completeness tests for T2–T3;
5. perturbation-domain tests for T4;
6. composition-contract tests for T5;
7. simulation studies separating false acceptance, false rejection, correct-hypothesis retention, and empty-set risk for T6;
8. versioned datasets, experiment manifests, scripts, logs, and generated figures;
9. independent mathematical and domain-expert review.

## Citation

A formal citation record has not yet been added. When referencing this repository, identify the specific theorem or AIRS document, its declared version, and the repository revision used. Do not cite a conceptual figure as empirical evidence without corresponding reproducible artifacts.

## License

Except where otherwise noted, the original documentation, diagrams, and images in this repository are licensed under the Creative Commons Attribution-ShareAlike 4.0 International License. See [LICENSE](LICENSE) for the repository notice. Third-party materials are excluded unless explicitly stated, and future software may use a separate software license.

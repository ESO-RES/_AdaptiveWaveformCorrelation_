# Draft Acoustic Incident Reconstruction Specification (AIRS)
## Physics-Constrained Analysis of Separately Acquired Recordings

```text
Version: AIRS Draft 0.1
Status: Stable research draft
Effective date: 2026-07-11
Supersedes: Earlier AIRS draft specifications
Validation status: Not independently validated
```

AIRS defines a proposed, repeatable, and auditable workflow for testing whether measurements from multiple recordings are compatible with a declared acoustic timing, propagation, clock, source, and geometry model.

Recordings may include audio and optional video captured by phones, cameras, dashcams, dedicated recorders, or other consumer and professional devices.

> **Status:** Draft research specification.  
> AIRS is not yet an independently validated forensic standard, a certified localization system, or proof that arbitrary recordings are authentic.

AIRS is designed to:

- preserve source evidence and analysis provenance,
- separate measurements from assumptions,
- test multiple event, clock, source, path, and geometry hypotheses,
- quantify uncertainty and covariance,
- reject incompatible hypotheses,
- retain competing admissible hypotheses,
- and report non-resolvable cases without forcing a preferred narrative.

AIRS does **not** guarantee:

- identity,
- intent,
- causality,
- authenticity,
- absence of editing,
- exact source or recorder location,
- unique phase-cycle assignment,
- or a unique global reconstruction.

---

## 1. Normative Language

The terms **must**, **must not**, **required**, **shall**, and **shall not** identify mandatory AIRS requirements.

The terms **should**, **recommended**, and **may** identify preferred or optional practices.

A result is AIRS-conformant only when the analyst states:

- the measurement model,
- the assumptions,
- the parameter constraints,
- the uncertainty model,
- the search procedure,
- the rejected and retained hypotheses,
- and the limitations of the conclusion.

---

## 2. Definitions

### Observer

A recording device or recording channel that provides audio and optional video.

### Incident

A bounded time interval containing one or more events of interest.

### Event

A physically or operationally defined occurrence that may produce an acoustic observation.

Examples include:

- impact,
- crack,
- thud,
- whistle,
- shout,
- collision,
- pyrotechnic report,
- public-address cue,
- or a defined acoustic pattern.

### Event Association

A hypothesis that observations on different devices correspond to the same physical event.

### Effective Acoustic Source

The position or distributed source model that best represents the acoustic radiation used in the analysis.

The effective acoustic source may differ from the visible mechanical contact point.

### Direct Arrival Candidate

A candidate onset believed to represent the earliest modeled propagation component rather than a later reflection.

### Propagation Path

A direct, reflected, diffracted, refracted, electronically delayed, or otherwise modeled route from source generation to a recorder.

### Clock Offset

A constant additive difference between a device time coordinate and the selected working time coordinate.

### Clock Scale

The ratio between device-recorded time units and physical or working time units.

### Clock Drift

Time variation in clock scale beyond a single constant factor.

### Event-Dependent Latency

A processing, buffering, filtering, codec, operating-system, or detection delay that differs between events or changes with time.

### Wrapped Phase

A phase observation reported modulo `2π`.

### Integer-Cycle Ambiguity

The unknown integer number of full phase cycles associated with a wrapped phase observation.

### Admissible Hypothesis

A hypothesis that satisfies the declared physical, timing, measurement, uncertainty, and integrity constraints.

### Retained Hypothesis Set

The hypotheses found and retained by the performed search.

When the search is incomplete, heuristically pruned, or manually restricted, the retained hypothesis set must not be represented as the complete admissible solution set.

### Admissible Solution Set

The complete set of hypotheses satisfying the declared constraints within the declared bounds. Completeness requires that the applicable hypothesis space has been exhaustively searched or that excluded regions have been independently demonstrated to be inadmissible.

### Constraint Closure

The condition in which all included observations have been jointly evaluated under the declared model and the admissible solution set has been characterized.

Constraint closure may be claimed only when the applicable hypothesis space has been exhaustively evaluated within declared bounds, or when excluded regions have been independently shown to be inadmissible.

Constraint closure does **not** require that only one solution survive.

Closure may produce:

- one admissible solution,
- multiple admissible solutions,
- or no admissible solution.

For incomplete searches, the report shall instead state:

> The retained hypothesis set has been characterized within the searched hypothesis space.

### Non-Resolvable

A result in which the available evidence and declared model do not distinguish the retained hypotheses to the required resolution.

### Integrity Exception

Evidence of discontinuity, alteration, corruption, or unsupported processing that violates the assumed measurement model.

An integrity exception is not automatically proof of malicious editing.

---

## 3. Scope and Preconditions

### 3.1 Minimum Evidence

An AIRS analysis requires:

- at least two separately acquired observations,
- access to original or highest-quality available files,
- documented provenance for each file,
- identifiable event candidates,
- and a declared physical and timing model.

Three or more observers are generally preferred, but observer count alone does not establish observability or uniqueness.

Separately acquired does not necessarily mean statistically independent. Shared devices, clocks, software pipelines, platform transcoding, reposting lineage, or common calibration sources must be documented and represented in the dependency or covariance model.

### 3.2 Optional Supporting Evidence

Supporting evidence may include:

- calibrated or surveyed recorder positions,
- known field or venue geometry,
- video reconstruction,
- weather records,
- public-address system configuration,
- event logs,
- device metadata,
- pilot tones,
- or external timing references.

### 3.3 Exclusions and Exceptions

A recording must not be treated as an ordinary measurement under the baseline model when it contains unmodeled:

- inserted or removed samples,
- discontinuous resampling,
- variable time warping,
- duplicated intervals,
- severe corruption,
- or synthesized, generated, or transformed content not represented by the declared measurement and source model.

Such material may still be analyzed under an explicit alternate model, but the transformation must be identified, parameterized, and validated.

---

## 4. Evidence Handling and Chain of Custody

### 4.1 Acquisition Record

For each source file, record:

- stable evidence identifier,
- original filename,
- source device and model when known,
- acquisition path,
- cryptographic hash, preferably SHA-256,
- file size,
- container and codec,
- nominal sample rate,
- channel layout,
- nominal and variable video frame rate,
- creation and modification timestamps,
- and known transfers, exports, or platform processing.

Timestamps must not be assumed correct merely because they are present.

### 4.2 Preservation

The analyst shall:

- preserve original files as read-only,
- perform analysis on derived copies,
- retain pre- and post-conversion hashes,
- document every transcoding and resampling operation,
- and maintain a mapping from every derived artifact to its source evidence.

### 4.3 Reproducibility Record

The analysis record must identify:

- software and version,
- detector and configuration,
- filters,
- resampling method,
- event windows,
- model parameters,
- solver settings,
- random seeds when applicable,
- and all manually selected inputs.

---

## 5. Data Preparation

### 5.1 Decoding

Files should be decoded to a documented analysis format, preferably lossless PCM.

Resampling should be avoided when feasible. When required, the method and parameters must be logged.

Resampling several files to the same nominal sample rate does not remove their original clock-scale differences.

### 5.2 Quality Assessment

For each observer, document:

- clipping,
- automatic gain control,
- denoising,
- compression artifacts,
- codec priming,
- dropouts,
- duplicated or missing samples,
- discontinuities,
- channel mismatch,
- audio/video offset,
- and evidence of time-varying resampling.

### 5.3 Integrity Classification

Each file shall be classified as one of:

- no identified integrity exception,
- integrity exception requiring an alternate model,
- unusable under the declared model,
- or indeterminate.

Absence of an identified exception is not proof of authenticity.

---

## 6. Event Selection and Association

### 6.1 Event Candidate Generation

Candidate events may be identified using:

- broadband transient detection,
- matched filtering,
- waveform cross-correlation,
- GCC-PHAT,
- spectral-flux detection,
- multiband energy change,
- manual review,
- video cues,
- or a validated event detector.

### 6.2 Multiple Candidate Retention

When neighboring events may be confused, the analyst must retain and test multiple plausible event associations rather than immediately selecting the nearest or loudest candidate.

### 6.3 Event Association Evidence

Event association should consider:

- event order,
- waveform similarity,
- spectral structure,
- surrounding acoustic context,
- video evidence,
- metadata time,
- source-position feasibility,
- propagation bounds,
- and clock continuity.

### 6.4 Direct Arrival Candidates

A candidate may be treated as a direct arrival only when:

- its onset is physically plausible,
- its timing is stable under reasonable detector and band changes,
- it is compatible with propagation bounds,
- and alternate reflected or loudspeaker paths have been considered.

When a direct arrival cannot be distinguished:

- retain alternate path hypotheses,
- increase uncertainty,
- or report the event as non-resolvable.

---

## 7. Source and Propagation Classes

AIRS analyses must identify the source class used for each event.

### 7.1 Direct Point or Compact Source

For source position `xₑ` and recorder position `sᵢ`:

```text
rᵢ,e = ‖sᵢ − xₑ‖
pᵢ,e = rᵢ,e/c
```

under a homogeneous, stationary, straight-path model.

### 7.2 Distributed or Extended Source

Crowd reactions, large structural impacts, and distributed pyrotechnics may require a spatial or temporal source model rather than one point source.

### 7.3 Public-Address or Electronically Delayed Source

For loudspeaker path `k`:

```text
pᵢₖ,e = δₖ,e + ‖sᵢ − lₖ‖/c
```

where:

- `lₖ` is the loudspeaker position,
- `δₖ,e` is the electronic and processing delay in physical seconds,
- and the reference time for `τₑ` must be declared.

If `τₑ` is defined at loudspeaker emission, the corresponding electronic delay must not be added again.

### 7.4 General Propagation Model

For complex environments, `pᵢ,e` may include:

- wind advection,
- spatially varying sound speed,
- atmospheric refraction,
- diffraction,
- reflection,
- terrain or structural effects,
- or electronic delay.

The analyst must state whether `pᵢ,e` represents:

- direct geometric travel time,
- effective travel time,
- selected path travel time,
- or a fitted propagation parameter.

---

## 8. Observer Clock and Measurement Model

For event `e` on observer `i`, use:

```text
yᵢ,e = βᵢ + αᵢ(τₑ + pᵢ,e) + ℓᵢ,e + εᵢ,e
```

where:

- `yᵢ,e` is the recorded event time,
- `βᵢ` is the constant clock offset,
- `αᵢ` is the clock-scale factor,
- `τₑ` is the physical or working event time,
- `pᵢ,e` is modeled propagation time,
- `ℓᵢ,e` is event-dependent latency in recorded-time units,
- and `εᵢ,e` is measurement noise and unmodeled error.

Clock convention:

```text
αᵢ = recorded-time units per unit of physical or working time
```

For an ideal clock:

```text
αᵢ = 1
```

A constant processing delay that affects all included events equally may be absorbed into `βᵢ`.

Event-dependent or time-varying delay must not be assumed to cancel.

---

## 9. Clock Drift, Gauge, and Observability

### 9.1 Centered Drift Model

Define physical arrival time:

```text
uᵢ,e = τₑ + pᵢ,e
```

Choose a reference time `u_ref` near the analyzed interval:

```text
qᵢ,e = uᵢ,e − u_ref
```

A higher-order local clock model is:

```text
yᵢ,e
= βᵢ
+ αᵢqᵢ,e
+ ½γᵢqᵢ,e²
+ ℓᵢ,e
+ εᵢ,e
```

where `γᵢ` represents clock-rate drift.

In the centered model, `βᵢ` is the device-time intercept at `u_ref`.

### 9.2 Additive Gauge

Set:

```text
β_ref = 0
```

for one designated reference device, or impose an equivalent external timing constraint.

Without an additive reference, a common timing shift may be exchanged between the event times and device offsets.

### 9.3 Time-Scale Reference

Set:

```text
α_ref = 1
```

only when:

- the reference device is externally calibrated, or
- the reference device is explicitly chosen to define the working time unit.

Otherwise, uncertainty in `α_ref` must be retained or an independent scale constraint must be imposed.

### 9.4 Observability

The analyst must evaluate whether the requested parameters are observable under the available:

- observer geometry,
- event diversity,
- source constraints,
- clock references,
- propagation model,
- and measurement precision.

A numerical optimizer returning one parameter vector does not establish observability, uniqueness, or physical correctness.

### 9.5 Spatial Gauge

When source and recorder positions are jointly estimated, the coordinate system must be fixed using surveyed anchors, declared coordinate constraints, or an equivalent spatial gauge.

Without such constraints, the recovered configuration may be identifiable only up to:

- global translation,
- global rotation,
- reflection,
- and, when sound speed or the working time scale is also unconstrained, possible scale ambiguity.

A solver returning one coordinate representation does not establish that the absolute orientation, handedness, origin, or scale has been determined.

---

## 10. Two-Event Interval Model

For events `a` and `b` on observer `i`:

```text
Δyᵢ(a,b) = yᵢ,b − yᵢ,a
```

Then:

```text
Δyᵢ(a,b)
= αᵢ[(τ_b − τ_a) + (pᵢ,b − pᵢ,a)]
  + Δℓᵢ(a,b)
  + Δεᵢ(a,b)
```

The constant offset `βᵢ` cancels.

The corrected physical interval is:

```text
T̂ᵢ(a,b)
= [Δyᵢ(a,b) − Δℓᵢ(a,b)]/αᵢ
  − [pᵢ,b − pᵢ,a]
```

Raw two-event intervals are not generally expected to match across observers when the effective source positions or propagation paths differ.

Separate impulses must not be treated as one continuous carrier-phase observation.

---

## 11. Cross-Observer Timing Consistency

Define the clock-corrected arrival:

```text
zᵢ,e = (yᵢ,e − βᵢ − ℓᵢ,e)/αᵢ
```

For observers `i` and `j`, define:

```text
eᵢⱼ,e
= zᵢ,e
− zⱼ,e
− (pᵢ,e − pⱼ,e)
```

A compatible model predicts:

```text
eᵢⱼ,e ≈ 0
```

within the declared uncertainty.

For two events `a` and `b`:

```text
Eᵢⱼ(a,b)
= Δyᵢ(a,b)/αᵢ
  − Δyⱼ(a,b)/αⱼ
  − [(pᵢ,b − pᵢ,a) − (pⱼ,b − pⱼ,a)]
  − Δℓᵢ(a,b)/αᵢ
  + Δℓⱼ(a,b)/αⱼ
```

A compatible model predicts:

```text
Eᵢⱼ(a,b) ≈ 0
```

These are model-consistency tests, not proof of authenticity.

---

## 12. Pairwise Closure

Define the pairwise-lag sign convention:

```text
Δt_AB,e = t_A,e − t_B,e
```

For lags derived from one internally assigned set of event times:

```text
Δt_AB,e + Δt_BC,e = Δt_AC,e
```

For independently measured noisy lags:

```text
Δt̂_AB,e + Δt̂_BC,e ≈ Δt̂_AC,e
```

Closure may therefore be algebraically automatic when pairwise lags come from one shared fitted timeline.

Closure can identify incompatible measurements, but it does not independently establish:

- correct event association,
- direct-path selection,
- source identity,
- authenticity,
- absence of editing,
- or unique geometry.

---

## 13. Phase and Integer-Cycle Measurements

Phase-based inference is optional and conditional.

### 13.1 Minimum Phase Requirements

Phase may be used only when:

- the same physical event is correctly associated,
- the analysis frequency and bandwidth are declared,
- the selected propagation component is consistent across observers,
- clock offset, scale, drift, and event-window alignment are corrected or bounded,
- source phase is canceled, calibrated, pilot-referenced, or otherwise eliminated,
- differential PA-chain, loudspeaker, microphone, filter, and device phase is calibrated or bounded,
- cross-observer coherence is adequate,
- and integer-cycle ambiguity is explicitly modeled.

Computing phase consistently across observers is necessary but not sufficient.

### 13.2 Fourier and Cross-Spectrum Convention

Adopt:

```text
X(f) = ∫x(t)e⁻ʲ²πft dt
```

Define:

```text
Xᵢ,e(f) = Fourier transform of the declared same-event analysis
           window from observer i after documented preprocessing

*         = complex conjugation

wrap(θ)   ∈ (−π, π]
```

and:

```text
φᵢⱼ,e(f) = arg{Xⱼ,e(f)X*ᵢ,e(f)}
```

With this convention, a positive propagation-time difference `pᵢ,e − pⱼ,e` contributes a positive phase term.

### 13.3 Relative-Phase Model

A general same-event model is:

```text
φᵢⱼ,e(f)
≈ wrap{
    2πf[pᵢ,e − pⱼ,e + κᵢⱼ,e]
    + ψᵢⱼ(f)
    + ηᵢⱼ,e(f)
  }
```

where:

- `κᵢⱼ,e` is residual timing error after clock and event alignment,
- `ψᵢⱼ(f)` is differential system phase not represented in `p`,
- and `ηᵢⱼ,e(f)` is phase noise and model error.

### 13.4 Corrected Phase Observable

Using estimated corrections:

```text
φ̃ᵢⱼ,e(f)
= wrap{
    φᵢⱼ,e(f)
    − 2πfκ̂ᵢⱼ,e
    − ψ̂ᵢⱼ(f)
  }
```

Uncertainty in `κ̂ᵢⱼ,e` and `ψ̂ᵢⱼ(f)` must be propagated.

If uncertainty in:

```text
2πfκ̂ᵢⱼ,e + ψ̂ᵢⱼ(f)
```

is comparable to `π` radians or spans one or more full cycles, the correction must not be reduced to one deterministic wrapped-phase value. The analysis must retain a wrapped probability distribution, interval set, or multiple integer-cycle hypotheses.

The general wrapped timing-ambiguity model is:

```text
Δpᵢⱼ,e
≈ [nᵢⱼ,e + φ̃ᵢⱼ,e(f)/(2π)]/f

nᵢⱼ,e ∈ ℤ
```

where:

```text
Δpᵢⱼ,e = pᵢ,e − pⱼ,e
```

When one declared reference sound speed `c` is appropriate, the distance-equivalent form is:

```text
cΔpᵢⱼ,e
≈ λ[nᵢⱼ,e + φ̃ᵢⱼ,e(f)/(2π)]

λ = c/f
```

Under spatially varying sound speed, wind, refraction, or electronically delayed paths, `Δpᵢⱼ,e` is the primary inferred quantity. Conversion to geometric distance requires the declared propagation model.

The quantity `cΔpᵢⱼ,e` is an effective path-length equivalent. It must not automatically be interpreted as purely geometric distance when `p` includes electronic delay or other non-geometric effects.

### 13.5 Prohibited Phase Interpretation

AIRS must not infer continuous carrier phase across separate, independently generated events unless a physically justified coherent reference exists.

Equivalent periods are a conversion from time, not evidence of observed continuous phase.

---

## 14. Environmental and Propagation Constraints

The propagation model must state its assumptions.

For a homogeneous-air approximation:

```text
pᵢ,e = rᵢ,e/c
```

The analysis should record or bound:

- temperature,
- humidity,
- pressure,
- wind speed and direction,
- spatial gradients,
- indoor or outdoor conditions,
- roof status,
- and path-specific obstructions.

For significant gradients, wind, diffraction, or refraction, use a general travel-time model rather than one constant `c`.

Environmental uncertainty shared across observations must be represented as covariance rather than duplicated as independent error.

---

## 15. Hypothesis Generation and Search

### 15.1 Candidate Dimensions

The search may include hypotheses over:

- event association,
- event order,
- direct versus reflected path,
- source class,
- source location,
- recorder location,
- clock offset,
- clock scale,
- clock drift,
- event-dependent latency,
- PA delay,
- propagation model,
- phase correction,
- and integer-cycle assignment.

### 15.2 Search Completeness

The analyst must state whether the search was:

- exhaustive within declared bounds,
- bounded but incomplete,
- heuristically pruned,
- or manually restricted.

A unique retained solution has no uniqueness significance when plausible alternatives were never generated or tested.

### 15.3 Rejection Log

Rejected hypotheses must be logged with explicit reasons, such as:

- propagation-bound violation,
- implausible clock parameters,
- incompatible event ordering,
- unsupported path selection,
- poor residuals,
- phase incoherence,
- geometry-bound violation,
- integrity exception,
- or numerical failure.

---

## 16. Estimation, Residuals, and Robustness

The estimation procedure shall report:

- objective function,
- residual definitions,
- parameter bounds,
- weighting model,
- covariance model,
- solver status,
- numerical conditioning,
- and sensitivity to initialization.

When outliers or model violations are plausible, use:

- robust estimation,
- mixture or alternate-hypothesis models,
- leave-one-observer-out analysis,
- leave-one-event-out analysis,
- and explicit outlier reporting.

A low residual does not prove that the model is correct.

---

## 17. Uncertainty and Covariance

Continuous parameter uncertainty must include all material sources, including:

- event detection,
- clock offset,
- clock scale,
- clock drift,
- event-dependent latency,
- source position,
- recorder position,
- PA electronic delay,
- sound speed,
- atmosphere,
- multipath parameters when represented continuously,
- and phase correction.

Discrete uncertainties—including event association, source class, path selection, integrity model, and integer-cycle assignment—must be represented as separate hypothesis branches, mixture components, or model alternatives. They must not be collapsed into a single Gaussian covariance term unless a justified probabilistic model has been established.

Shared parameters create correlated errors.

Examples include:

- common source-position error,
- common atmospheric model error,
- shared PA-delay error,
- shared event-time calibration error,
- shared clock-reference error,
- and common phase-calibration bias.

When combining estimates, use a covariance-aware method rather than independent inverse-variance weighting when correlations are material.

Integrity exceptions must not be converted automatically into Gaussian uncertainty.

---

## 18. Result Classification

Every analyzed hypothesis set shall receive one primary inference classification. Each case shall also receive a separate integrity status.

### 18.1 Resolved Within the Declared Model

One admissible region or solution remains, and competing hypotheses are separated by the declared uncertainty and decision criteria.

The surviving admissible region must also satisfy a predeclared resolution requirement. One connected but excessively broad, weakly identified, or gauge-dependent region shall be classified as non-resolvable rather than resolved.

The classification **Resolved Within the Declared Model** may be used only when the search was exhaustive within the declared bounds or when excluded hypothesis regions were independently shown to be inadmissible.

This does not prove authenticity or physical uniqueness outside the tested model.

### 18.2 Provisionally Resolved Within the Searched Hypothesis Space

One admissible region or solution remains within the tested hypothesis space, but heuristic pruning, manual restriction, or incomplete search may have omitted plausible alternatives.

The report must identify the omitted or unsearched hypothesis regions and must not describe the result as globally unique.

### 18.3 Multiple Admissible Solutions

Two or more materially distinct and sufficiently characterized hypothesis branches remain compatible with the declared model.

Each surviving branch and its uncertainty region must be reported.

This classification applies when the surviving branches can be individually bounded and meaningfully distinguished as alternative solutions, even though the evidence cannot select one branch.

### 18.4 Non-Resolvable

The surviving hypothesis set cannot be characterized at the predeclared resolution.

This includes:

- one excessively broad admissible region;
- overlapping branches that cannot be meaningfully separated;
- weakly identified or gauge-dependent parameters;
- or measurements insufficient to bound the requested timing, location, geometry, or model distinction.

When several distinct, bounded branches survive, use **Multiple Admissible Solutions**. When the surviving set itself cannot be usefully bounded or separated, use **Non-Resolvable**.

### 18.5 No Admissible Solution Found in the Searched Hypothesis Space

No tested hypothesis satisfies the declared measurement, propagation, uncertainty, and integrity constraints within the searched hypothesis space.

The report must state whether unsearched, manually excluded, or heuristically pruned hypotheses could remain.

This result does not automatically prove editing, fabrication, or incompatibility across the complete declared model.

### 18.6 Model-Incompatible Within Declared Bounds

No admissible solution remains after an exhaustive search within the declared bounds, or all excluded hypothesis regions have been independently shown to be inadmissible.

This does not automatically prove editing or fabrication.

### 18.7 Integrity Status

Each case shall separately be classified as:

- no identified integrity exception;
- integrity exception modeled explicitly;
- integrity exception not adequately modeled;
- or indeterminate.

An integrity exception does not automatically determine the primary inference classification and does not establish malicious editing.

---

## 19. Acceptance Criteria

A hypothesis may be retained only when:

- event associations are physically and contextually plausible,
- clock parameters satisfy declared bounds,
- propagation paths satisfy declared bounds,
- residuals are compatible with the uncertainty model,
- phase prerequisites are satisfied when phase is used,
- integrity assumptions are not violated or are explicitly modeled,
- and the hypothesis survives all applicable declared adversarial tests.

AIRS does not require rejection merely because multiple solutions survive.

AIRS requires that multiplicity be reported.

Resolution requirements, acceptance thresholds, parameter bounds, and decision rules used for confirmatory classification must be declared before the final result used for classification is inspected. Post-hoc thresholds may be reported only as exploratory sensitivity analyses and must not be used to support a classification of **Resolved Within the Declared Model**.

---

## 20. Adversarial and Sensitivity Tests

The analysis should test, when relevant:

1. neighboring-event substitution;
2. alternate direct, reflected, and PA paths;
3. clock-scale and drift sensitivity;
4. source-position sensitivity;
5. recorder-position sensitivity;
6. atmospheric-model sensitivity;
7. event-window and detector sensitivity;
8. leave-one-observer-out analysis;
9. leave-one-event-out analysis;
10. multiband timing and coherence;
11. video-audio consistency;
12. phase-calibration sensitivity;
13. alternate integer-cycle assignments;
14. discontinuity and resampling tests;
15. alternate source-class models;
16. and search-completeness limitations.

Consistency means that a hypothesis survives the tested constraints. It is not, by itself, proof of authenticity.

---

## 21. Required Reporting

### 21.1 Evidence Manifest

Report:

- observer identifiers,
- source hashes,
- provenance,
- media metadata,
- acquisition path,
- the per-file integrity classification from Section 5.3,
- and the overall case integrity status from Section 18.7.

### 21.2 Event Table

For every observer and event, report as applicable:

| Field | Meaning |
|---|---|
| Observer ID | Stable recording identifier |
| Event ID | Cross-observer event-group identifier |
| Event class | Direct, PA, distributed, reflected, or other |
| Recorded event time | `yᵢ,e` |
| Clock offset | `βᵢ` |
| Clock scale | `αᵢ` |
| Clock drift | `γᵢ` when modeled |
| Selected source/path | Declared source and propagation hypothesis |
| Propagation time | `pᵢ,e` |
| Event latency | `ℓᵢ,e` |
| Detection uncertainty | Timing uncertainty |
| Phase observable | Only when prerequisites are met |
| Corrected residual | Model residual |
| Status | Retained, rejected, ambiguous, or non-resolvable |

### 21.3 Solution-Set Report

Report:

- number of generated hypotheses,
- number of optimized hypotheses,
- pruning rules,
- retained hypotheses,
- rejected hypotheses,
- solution regions,
- covariance,
- residuals,
- and search-completeness limitations.

### 21.4 Integrity Report

Report:

- identified discontinuities,
- timing anomalies,
- unmodeled transformations,
- and their effect on admissibility.

---

## 22. Prohibited Output Styles

An AIRS report must not present:

- exact point claims without justified uncertainty,
- exact distance from raw wrapped phase,
- authenticity conclusions from consistency alone,
- editing conclusions from one residual anomaly,
- unique geometry claims without observability analysis,
- continuous phase claims across independent events,
- or calibrated-probability language from an uncalibrated score.

Use “uncertainty interval,” “admissible region,” or another technically justified term unless a formal confidence or credible interval has actually been constructed.

---

## 23. Validation Protocol

### 23.1 Reproducibility

An independent analyst must be able to reproduce:

- decoded analysis files,
- event windows,
- detector outputs,
- model inputs,
- parameter bounds,
- candidate hypotheses,
- solver outputs,
- residuals,
- and classifications

using the logged configuration and evidence hashes.

### 23.2 Synthetic Validation

Synthetic tests should include:

- known geometry,
- known clock offset and scale,
- clock drift,
- event-dependent latency,
- wrong event association,
- phase-cycle ambiguity,
- hardware phase bias,
- strong reflection,
- missing direct path,
- distributed source,
- PA electronic delay,
- correlated model error,
- atmospheric gradients,
- timing edits,
- and non-resolvable cases.

### 23.3 Controlled Recording Validation

Controlled trials should include:

- surveyed source and recorder positions,
- calibrated or independently measured clocks,
- documented atmosphere,
- known PA delays when used,
- multiple devices and codecs,
- reflective and non-reflective environments,
- and blinded event association when feasible.

### 23.4 Independent Review

Claims of forensic reliability require independent replication, error-rate characterization, and validation outside the development team.

---

## 24. AIRS Conformance Checklist

Minimum conformance requires:

1. source hashes and provenance recorded;
2. originals preserved;
3. all conversions logged;
4. event candidates and alternate associations documented;
5. source and propagation classes declared;
6. clock offset and scale modeled or bounded;
7. clock gauge and time-scale reference declared;
8. spatial gauge declared when geometry is jointly estimated;
9. drift modeled or bounded when material;
10. propagation assumptions and environmental bounds stated;
11. phase prerequisites satisfied when phase is used;
12. integer-cycle ambiguity modeled when applicable;
13. continuous uncertainty and covariance reported;
14. discrete hypothesis dimensions retained separately;
15. rejected hypotheses logged;
16. search completeness or pruning disclosed;
17. retained hypothesis set distinguished from the admissible solution set;
18. constraint closure claimed only when justified;
19. searched-space and exhaustive no-solution classifications distinguished;
20. one primary inference classification assigned;
21. integrity status assigned separately;
22. multiple admissible solutions retained;
23. non-resolvable outcomes permitted;
24. outputs reproducible from the case configuration.

---

## 25. Standard Deliverables

An AIRS-conformant case package should include:

- case summary,
- evidence manifest,
- source-media hashes,
- event and observer table,
- model specification,
- clock and propagation assumptions,
- uncertainty and covariance report,
- residual report,
- solution-set report,
- rejection log,
- integrity report,
- adversarial-test report,
- reproducibility package,
- and limitations statement.

---

## 26. Appropriate Result Language

Appropriate:

> The selected hypothesis is compatible with the declared timing, source, propagation, clock, and uncertainty model.

Appropriate:

> The result is provisionally resolved within the searched hypothesis space; plausible alternatives may remain outside the tested search bounds.

Appropriate:

> Multiple hypotheses remain admissible under the declared model.

Appropriate:

> The available evidence is non-resolvable at the requested precision.

Appropriate:

> No admissible solution was found in the searched hypothesis space; unsearched or pruned alternatives may remain.

Appropriate:

> No admissible solution remains within the exhaustively searched declared bounds; this result does not by itself establish editing or fabrication.

Not appropriate:

> The reconstruction proves the recording is authentic.

Not appropriate:

> Phase proves the exact distance.

Not appropriate:

> A successful optimizer proves the solution is unique.

Not appropriate:

> Constraint closure proves there was no editing.

---

## 27. Standard Language for Reports or Testimony

> AIRS constrains interpretations of separately acquired recordings to those compatible with the declared physical, timing, propagation, calibration, integrity, and uncertainty model. The analysis reports the admissible solution set when constraint closure has been established, or the retained hypothesis set and search limitations when it has not. Competing solutions and non-resolvable outcomes are reported explicitly. Compatibility does not by itself establish authenticity, identity, intent, causality, or uniqueness outside the tested model.

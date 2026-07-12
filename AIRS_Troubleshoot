# AIRS Troubleshooting Guide
## Failure Modes, Diagnostic Tests, and Non-Convergence Examples

```text
Document ID: AIRS-TRB-0.1
Version: AIRS Troubleshooting Draft 0.1
Status: Stable informative research draft
Effective date: 2026-07-11
Applies to: AIRS Draft 0.1
Normative status: Informative and non-normative
Validation status: Not independently validated
```

This guide explains how to diagnose failed, ambiguous, unstable, or misleading acoustic reconstructions performed under the **Draft Acoustic Incident Reconstruction Specification (AIRS) 0.1**.

It does not add requirements to AIRS Draft 0.1. When this guide conflicts with the AIRS specification, the specification controls.

Requirement-like language in this guide summarizes or applies requirements from AIRS Draft 0.1. It does not create independent normative requirements. Where the guide uses **must**, **must not**, **shall**, or equivalent language, authority derives from the referenced AIRS provision.

AIRS treats failure, ambiguity, and non-resolution as valid analytical outcomes. A solver result is not accepted merely because it converges numerically, and a failed solver does not by itself establish that the physical model is incompatible.

---

## 1. Troubleshooting Principles

Troubleshooting under AIRS should preserve the distinction among:

- measurement failure,
- event-association failure,
- propagation-model failure,
- clock-model failure,
- geometric non-observability,
- phase ambiguity,
- integrity exceptions,
- numerical optimization failure,
- incomplete hypothesis search,
- and genuinely model-incompatible evidence.

The analyst should not collapse these conditions into a generic label such as “non-convergence.”

Every investigation should answer four separate questions:

1. **Did the software converge numerically?**
2. **Does the fitted solution satisfy the declared physical and uncertainty constraints?**
3. **Was the relevant hypothesis space searched adequately?**
4. **What primary inference classification and integrity status follow from the evidence?**

---

## 2. AIRS Result Outcomes Used in This Guide

Once sufficient diagnostic work has been completed, the case should receive one primary AIRS inference classification:

- **Resolved Within the Declared Model**
- **Provisionally Resolved Within the Searched Hypothesis Space**
- **Multiple Admissible Solutions**
- **Non-Resolvable**
- **No Admissible Solution Found in the Searched Hypothesis Space**
- **Model-Incompatible Within Declared Bounds**

Until the evidence, implementation, and search provide an adequate basis, the operational status may be recorded as **classification pending**. This is an informative workflow status defined by this guide, not an AIRS inference classification.

Each case receives a separate integrity status, including while its inference classification is pending:

- no identified integrity exception;
- integrity exception modeled explicitly;
- integrity exception not adequately modeled;
- or indeterminate.

A numerical failure is not itself an AIRS inference classification. The analyst must determine whether the failure is caused by implementation, conditioning, initialization, model mismatch, or lack of observability.

---

## 3. Diagnostic Sequence

When an analysis fails or produces an implausible result, proceed in this order.

### Step 1 — Confirm evidence identity and provenance

Verify:

- source hashes,
- filenames,
- channel selection,
- extraction settings,
- sample rates,
- media duration,
- and source-to-derived-file mappings.

### Step 2 — Inspect continuity and processing

Check for:

- inserted or removed samples,
- discontinuous resampling,
- codec priming,
- audio dropouts,
- variable time warping,
- duplicated intervals,
- platform transcoding,
- denoising,
- automatic gain control,
- and audio/video clock separation.

### Step 3 — Recheck event candidates

Confirm:

- event order,
- waveform and spectral similarity,
- neighboring candidate events,
- visible event cues,
- and plausible source locations.

Retain alternate associations when more than one candidate remains plausible.

### Step 4 — Test clock models

Fit or bound:

- clock offset,
- clock scale,
- centered clock drift,
- segment-dependent discontinuities,
- and event-dependent latency.

Do not interpret a changing lag as clock drift until moving sources, PA routing, reflections, and path switching have been tested.

### Step 5 — Test source and path classes

Compare:

- direct point-source paths,
- reflected or diffracted paths,
- distributed sources,
- public-address paths,
- and general travel-time models.

### Step 6 — Evaluate observability and gauges

Confirm that:

- the additive timing gauge is fixed,
- the working time scale is defined,
- the spatial coordinate gauge is fixed when geometry is estimated,
- and the requested parameters are observable.

### Step 7 — Inspect uncertainty and covariance

Verify that:

- shared errors are represented as covariance,
- discrete alternatives remain separate hypothesis branches,
- integrity exceptions are not converted into ordinary Gaussian noise,
- and phase-calibration uncertainty is propagated.

### Step 8 — Inspect the search

State whether the search was:

- exhaustive within declared bounds,
- bounded but incomplete,
- heuristically pruned,
- or manually restricted.

### Step 9 — Inspect numerical behavior

Check:

- initialization sensitivity,
- local minima,
- scaling,
- parameter correlations,
- rank deficiency,
- Jacobian conditioning,
- solver tolerances,
- and reproducibility across runs.

### Step 10 — Assign the result

Assign a separate integrity status in all cases. When the diagnostic basis is adequate, assign one primary inference classification; otherwise, record the workflow status as **classification pending**. Do not use **Resolved Within the Declared Model** unless the surviving region satisfies the predeclared resolution requirement.

---

## 4. Quick Diagnostic Matrix

| Symptom | Likely cause | Immediate test | Typical disposition or reporting consequence |
|---|---|---|---|
| Different devices select neighboring transients | Wrong event association | Test alternate event groupings | **Multiple Admissible Solutions**, **Non-Resolvable**, or **No Admissible Solution Found in the Searched Hypothesis Space** |
| Lag changes steadily over time | Clock-scale error, drift, moving source, or path change | Compare clock and propagation alternatives | **Resolved Within the Declared Model**, **Provisionally Resolved Within the Searched Hypothesis Space**, or **Non-Resolvable** |
| Lag jumps abruptly | Timing edit, dropped samples, segment change, or path switch | Segment-wise continuity test | Test alternate path branches and assign integrity status separately |
| Strongest peak gives impossible geometry | Reflection or PA path selected | Compare earliest and later arrivals | **Multiple Admissible Solutions** or **Non-Resolvable** |
| Phase gives many ranges | Integer-cycle ambiguity | Use broadband timing and geometry bounds | **Multiple Admissible Solutions** or **Non-Resolvable** |
| Phase residuals remain inconsistent across device pairs or show unexplained nonlinear frequency dependence after modeled delay and calibration corrections | Hardware phase, multipath, clock residual, calibration error, or low coherence | Calibrate, inspect coherence, and compare against the expected linear phase slope | Exclude phase from inference or expand uncertainty and retain alternate branches |
| Optimizer returns many equivalent coordinates | Spatial gauge or insufficient geometry | Fix anchors and inspect rank | **Non-Resolvable** |
| Optimizer returns one unstable solution | Poor conditioning or local minimum | Refit from multiple starts | Workflow status remains **classification pending** until numerical stability is evaluated; the later outcome is often **Provisionally Resolved Within the Searched Hypothesis Space** or **Non-Resolvable** |
| No tested hypothesis fits | Wrong search bounds, omitted model, or incompatible evidence | Expand alternatives and audit pruning | **No Admissible Solution Found in the Searched Hypothesis Space** or **Model-Incompatible Within Declared Bounds** |
| Pairwise closure is perfect | Lags derived from one fitted timeline | Recompute independent pairwise measurements | Record the source of closure and draw no authenticity conclusion |
| Tiny residuals but implausible parameters | Overfitting or weak bounds | Inspect parameters and held-out events | Reject the fitted hypothesis |
| Per-device errors appear independent but move together | Shared calibration or model bias | Add covariance/shared parameter | Wider uncertainty or different classification |

---

## 5. Scenario 1 — Wrong Event Association

### Description

Several similar sounds occur close together, such as multiple whistles, impacts, claps, or shouted syllables. One device is paired to a neighboring event rather than the intended event.

### Indicators

- event order differs across devices;
- waveform similarity is weak outside a narrow window;
- propagation residuals require implausible clock changes;
- one observer becomes an apparent outlier;
- or a nearby candidate produces much smaller residuals.

### Diagnostic Actions

- generate multiple event candidates;
- compare event order and surrounding context;
- test waveform and spectral similarity;
- use video and scoreboard evidence;
- and refit all plausible associations.

### Correct Interpretation

A wrong association is a discrete hypothesis failure, not ordinary timing noise.

### Possible Outcomes

- correct association retained and wrong branch rejected;
- **Multiple Admissible Solutions** if distinct associations remain bounded;
- **Non-Resolvable** if candidates cannot be separated;
- or **No Admissible Solution Found in the Searched Hypothesis Space** if no tested association fits.

---

## 6. Scenario 2 — Clock Offset Mistaken for Geometry

### Description

One recording is consistently delayed relative to another, and the delay is interpreted as source or recorder distance.

### Indicators

- approximately constant cross-device lag across events;
- implausibly large inferred distance;
- geometry changes when a different reference event is used;
- or the same lag appears for unrelated source positions.

### Diagnostic Actions

Fit:

```text
yᵢ,e = βᵢ + αᵢ(τₑ + pᵢ,e) + ℓᵢ,e + εᵢ,e
```

and test whether a constant `βᵢ` explains the lag.

### Correct Interpretation

A constant cross-device delay combines clock offset, constant device latency, propagation, and source-path delay. It does not identify geometry by itself.

Under the AIRS measurement model, a constant device or processing latency may be absorbed into `βᵢ`. Without an external calibration, known timing reference, or additional structural constraint, constant clock offset and constant latency are generally not separately identifiable. The fitted `βᵢ` should therefore be interpreted as an effective additive timing offset unless its components have been independently calibrated.

---

## 7. Scenario 3 — Clock Scale or Drift Beyond the Declared Model

### Description

Recordings align near one time but progressively diverge across the incident.

### Indicators

- residuals vary approximately linearly or quadratically with time;
- an affine clock model improves the fit;
- a centered drift term further improves residuals;
- or required scale and drift exceed declared device bounds.

### Diagnostic Actions

Define the physical arrival time and centered arrival-time coordinate:

```text
uᵢ,e = τₑ + pᵢ,e
qᵢ,e = uᵢ,e − u_ref
```

Then compare:

```text
yᵢ,e = βᵢ + αᵢqᵢ,e + ℓᵢ,e + εᵢ,e
```

with:

```text
yᵢ,e
= βᵢ
+ αᵢqᵢ,e
+ ½γᵢqᵢ,e²
+ ℓᵢ,e
+ εᵢ,e
```

Also test source movement, PA routing changes, reflections, and path switching.

### Correct Interpretation

`αᵢ` is clock scale. `γᵢ` represents drift in the centered higher-order model. A value of `αᵢ` different from one is not, by itself, a drift measurement.

### Possible Outcomes

- clock model retained;
- drift-bounded branch rejected;
- **Non-Resolvable** if clock and propagation effects remain coupled;
- or an integrity exception if the lag changes discontinuously.

---

## 8. Scenario 4 — Timing Discontinuity or Time Warping

### Description

A recording contains inserted or removed samples, discontinuous resampling, variable playback speed, or another unmodeled timing transformation.

### Indicators

- abrupt residual jumps;
- inconsistent clock parameters across adjacent segments;
- duplicated waveform sections;
- missing intervals;
- or segment-specific sample-rate behavior.

### Diagnostic Actions

- inspect sample continuity;
- compare segment-wise clock fits;
- search for repeated or missing waveform blocks;
- inspect container timestamps and edit lists;
- and test an explicit piecewise or transformed-time model.

### Correct Interpretation

This is an integrity condition. It is not ordinary Gaussian timing uncertainty.

### Possible Integrity Status

- integrity exception modeled explicitly;
- integrity exception not adequately modeled;
- or indeterminate.

The primary inference classification is assigned separately.

---

## 9. Scenario 5 — Insufficient Observer Geometry

### Description

Recorders are clustered, nearly collinear, or positioned so that many source locations yield similar travel-time differences.

### Indicators

- elongated or unbounded location regions;
- large covariance eigenvalues;
- strong dependence on small timing perturbations;
- equivalent mirrored configurations;
- or high Jacobian condition number.

### Diagnostic Actions

- inspect the information or sensitivity matrix;
- add surveyed spatial anchors;
- include events from geometrically diverse source positions;
- test leave-one-observer-out stability;
- and verify the spatial gauge.

### Correct Interpretation

A solver may return one coordinate vector even when the geometry is not unique.

### Possible Outcomes

- **Multiple Admissible Solutions** for distinct, bounded branches;
- **Non-Resolvable** for broad, overlapping, or weakly identified regions.

---

## 10. Scenario 6 — Unfixed Timing or Spatial Gauge

### Description

The model estimates event times, clock offsets, source positions, and recorder positions without fixing a reference.

### Indicators

- singular or nearly singular normal equations;
- parameters translate or rotate together with unchanged residuals;
- different initializations yield shifted or mirrored configurations;
- or absolute event time changes while relative timing remains fixed.

### Diagnostic Actions

Declare:

```text
β_ref = 0
```

to fix the additive timing gauge.

Set:

```text
α_ref = 1
```

only when the reference clock is calibrated or intentionally defines the working time unit.

Fix the spatial frame using surveyed anchors or equivalent coordinate constraints.

### Correct Interpretation

Gauge-equivalent parameterizations are not distinct physical reconstructions. They should be normalized to a declared timing and spatial convention before uniqueness is assessed. Uncertainty in surveyed anchors, calibrated references, and other constraints used to fix the gauges must remain in the uncertainty model.

---

## 11. Scenario 7 — Reverberation or Reflection Selected as the Direct Path

### Description

A later reflection is stronger than the direct arrival and is selected as the event time.

### Indicators

- largest peak is later than a weaker onset;
- timing changes with bandpass filter;
- inferred geometry violates propagation bounds;
- or different devices select different reflection orders.

### Diagnostic Actions

- compare earliest, strongest, and most coherent arrivals;
- inspect time-frequency structure;
- retain multiple path candidates;
- compare direct and reflected path models;
- and use room or venue geometry when available.

### Correct Interpretation

GCC-PHAT and cross-correlation do not guarantee direct-path recovery.

### Possible Outcomes

- selected direct path retained;
- bounded alternative paths reported as **Multiple Admissible Solutions**;
- or **Non-Resolvable** if the propagation components cannot be separated.

---

## 12. Scenario 8 — Public-Address Path Mistaken for a Field Source

### Description

A recorder receives an amplified event from a nearby loudspeaker, but the analysis treats it as direct propagation from the visible field event.

### Indicators

- apparent distance is inconsistent with the venue;
- nearby recorders show unexpectedly different delays;
- strong frequency-dependent path behavior appears;
- or a configured PA delay explains the discrepancy.

### Diagnostic Actions

Test:

```text
pᵢₖ,e = δₖ,e + ‖sᵢ − lₖ‖/c
```

for plausible loudspeakers and delay zones.

Declare whether `τₑ` is defined at trigger generation or loudspeaker emission.

### Correct Interpretation

Electronic delay is measured in physical seconds but is not geometric distance.

### Possible Outcomes

- PA-path model retained;
- direct-field model rejected;
- multiple loudspeaker paths retained;
- or **Non-Resolvable** when routing and delay configuration are unknown.

---

## 13. Scenario 9 — Distributed Source Forced Into a Point-Source Model

### Description

Crowd reactions, applause, structural vibration, or distributed pyrotechnics are modeled as one instantaneous source point.

### Indicators

- broad or observer-dependent onset;
- different sections appear to react at different times;
- point-source residuals remain structured;
- or location estimates move with the chosen analysis window.

### Diagnostic Actions

- model a distributed source;
- use section-level or temporal activation components;
- reduce claimed timing precision;
- and test whether the point-source model is rejected.

### Correct Interpretation

The peak of a distributed reaction is not a universal physical event time.

### Possible Outcomes

- distributed-source model retained;
- point-source branch rejected;
- or **Non-Resolvable** at fine timing or location resolution.

---

## 14. Scenario 10 — Integer-Cycle Phase Ambiguity

### Description

A narrowband same-event phase observation admits many integer-cycle assignments.

### Indicators

- several values of `nᵢⱼ,e` satisfy wrapped phase;
- coarse timing uncertainty exceeds a significant fraction of one period;
- or multiple geometry branches differ by approximately `1/f` in propagation time.

### Diagnostic Actions

Use broadband timing, geometry bounds, calibrated pilots, repeated compatible events, and propagation constraints.

The general phase ambiguity is:

```text
Δpᵢⱼ,e
≈ [nᵢⱼ,e + φ̃ᵢⱼ,e(f)/(2π)]/f
```

### Correct Interpretation

Wrapped phase supplies a fractional cycle, not the absolute cycle count.

### Possible Outcomes

- one integer branch retained after independent constraints;
- **Multiple Admissible Solutions** if several bounded branches remain;
- or **Non-Resolvable** when the branches cannot be bounded or separated.

Constraint closure must not be claimed unless the applicable integer and model space was exhaustively evaluated or excluded regions were independently shown inadmissible.

---

## 15. Scenario 11 — Uncalibrated Hardware or Processing Phase

### Description

Relative phase is interpreted as propagation delay without accounting for microphones, filters, devices, loudspeakers, PA chains, or residual clock alignment.

### Indicators

- corrected phase residuals remain inconsistent across device pairs;
- inferred delay is unstable across frequency after accounting for the expected linear phase slope;
- phase disagrees with the selected broadband-delay branch;
- or correction uncertainty is comparable to `π` radians or larger.

### Diagnostic Actions

Estimate or bound:

```text
κ̂ᵢⱼ,e
```

and:

```text
ψ̂ᵢⱼ(f)
```

Then compute:

```text
φ̃ᵢⱼ,e(f)
= wrap{
    φᵢⱼ,e(f)
    − 2πfκ̂ᵢⱼ,e
    − ψ̂ᵢⱼ(f)
  }
```

### Correct Interpretation

When correction uncertainty is comparable to `π` radians or spans one or more full cycles, retain a wrapped distribution, interval set, or multiple integer hypotheses. Do not report one deterministic corrected phase.

---

## 16. Scenario 12 — Separate Events Treated as One Coherent Carrier

### Description

Two independently generated impulses are assigned a continuous phase count between them.

### Indicators

- phase from one event is extrapolated to another event;
- source waveform differs materially;
- no shared oscillator or coherent pilot exists;
- or cycle count is inferred only from elapsed time.

### Diagnostic Actions

Use the two-event interval model:

```text
Δyᵢ(a,b)
= αᵢ[(τ_b − τ_a) + (pᵢ,b − pᵢ,a)]
  + Δℓᵢ(a,b)
  + Δεᵢ(a,b)
```

### Correct Interpretation

Equivalent periods are a conversion from time. They are not evidence of observed continuous phase across separate events.

The cross-event phase branch must be rejected unless a physically justified coherent reference exists.

---

## 17. Scenario 13 — Pairwise Closure Misinterpreted as Independent Proof

### Description

Pairwise lags close exactly because they were derived from one shared fitted timeline.

### Indicators

```text
Δt_AB,e + Δt_BC,e = Δt_AC,e
```

holds exactly despite noisy data.

### Diagnostic Actions

Determine whether pairwise values were:

- independently measured, or
- algebraically derived from one set of fitted event times.

### Correct Interpretation

Closure is automatic for lags derived from one shared timeline. It does not prove event identity, path correctness, authenticity, or absence of editing.

---

## 18. Scenario 14 — Atmospheric or Wind Model Failure

### Description

A constant sound speed is used despite significant wind, temperature gradient, or path-dependent conditions.

### Indicators

- residuals correlate with path direction;
- upwind and downwind paths show opposite biases;
- outdoor fits change materially with weather assumptions;
- or one effective `c` cannot fit all paths.

### Diagnostic Actions

- obtain or bound weather conditions;
- use a path-specific travel-time model;
- test sound-speed and wind sensitivity;
- and represent shared environmental parameters as covariance.

### Correct Interpretation

For complex propagation, `pᵢ,e` is the primary modeled quantity. Distance conversion requires the declared environmental model.

---

## 19. Scenario 15 — Shared Error Treated as Independent Noise

### Description

Several observations depend on the same uncertain source position, PA delay, atmosphere, clock reference, or calibration, but the analysis treats their errors as independent.

### Indicators

- combined uncertainty becomes implausibly small;
- residuals move together;
- leave-one-observer-out estimates change less than expected while all remain biased;
- or repeated measurements share the same systematic offset.

### Diagnostic Actions

Construct a covariance model containing shared parameters or latent error terms.

### Correct Interpretation

Independent inverse-variance weighting is invalid when material correlation exists.

### Possible Outcome

The best estimate may remain similar while its uncertainty region expands enough to change the case from **Resolved Within the Declared Model** to **Non-Resolvable**.

---

## 20. Scenario 16 — Discrete Alternatives Collapsed Into Gaussian Error

### Description

Event identity, source class, path selection, integrity model, or integer-cycle assignment is represented as one enlarged standard deviation.

### Indicators

- one broad unimodal result hides distinct physical branches;
- the mean falls between physically meaningful solutions;
- or confidence language is applied to a non-Gaussian multimodal set.

### Diagnostic Actions

Represent discrete alternatives as:

- separate hypothesis branches;
- mixture components;
- or explicit model alternatives.

### Correct Interpretation

Discrete model uncertainty is not ordinary continuous covariance unless a justified probabilistic model is established.

---

## 21. Scenario 17 — Numerical Non-Convergence

### Description

The optimizer stops, diverges, reaches iteration limits, or produces unstable results.

### Indicators

- strong initialization dependence;
- parameter values at bounds;
- nearly singular Jacobian;
- poor scaling;
- oscillating objective;
- or inconsistent results across software or runs.

### Diagnostic Actions

- nondimensionalize or rescale parameters;
- fix gauges;
- tighten physically justified bounds;
- use multiple initializations;
- inspect gradients and rank;
- simplify the model;
- separate discrete branches before continuous fitting;
- and verify implementation with synthetic cases.

### Correct Interpretation

Numerical non-convergence may reflect:

- a software defect;
- poor conditioning;
- gauge freedom;
- weak observability;
- local minima;
- or model incompatibility.

Under AIRS Draft 0.1, numerical non-convergence must not be reported directly as proof that the evidence is inconsistent.

---

## 22. Scenario 18 — Low Residual but Physically Invalid Solution

### Description

The optimizer returns a small objective value by using implausible clocks, paths, delays, or geometry.

### Indicators

- clock scale outside declared bounds;
- source outside feasible region;
- negative or impossible path delay;
- excessive drift;
- or strong dependence on one outlier.

### Diagnostic Actions

- enforce declared physical bounds;
- inspect every fitted parameter;
- evaluate held-out events;
- perform leave-one-event-out and leave-one-observer-out tests;
- and test alternate models.

### Correct Interpretation

Residuals must be compatible with the declared uncertainty and weighting model. A small residual or objective value alone is not sufficient to establish physical compatibility.

---

## 23. Scenario 19 — Incomplete Search Reported as Unique

### Description

A heuristic or manually limited search finds one surviving solution, and the result is described as unique.

### Indicators

- candidate pruning was undocumented;
- integer branches were truncated;
- alternate paths were not generated;
- or source regions were excluded without proof.

### Diagnostic Actions

State whether the search was exhaustive, bounded but incomplete, heuristically pruned, or manually restricted.

### Correct Interpretation

Use:

> The result is provisionally resolved within the searched hypothesis space.

Do not claim constraint closure or a complete admissible solution set.

---

## 24. Scenario 20 — No Solution Found

### Description

No tested hypothesis satisfies the declared constraints.

### Diagnostic Actions

First determine whether:

- the search was incomplete;
- plausible paths or event associations were omitted;
- parameter bounds were too narrow;
- the clock model was inadequate;
- the source class was wrong;
- an integrity exception was unmodeled;
- or a software defect occurred.

### Correct Classification

Use **No Admissible Solution Found in the Searched Hypothesis Space** when unsearched or pruned alternatives may remain.

Use **Model-Incompatible Within Declared Bounds** only after exhaustive search within declared bounds or independent demonstration that excluded regions are inadmissible.

Neither classification independently proves editing or fabrication.

---

## 25. Scenario 21 — Post-Hoc Threshold Selection

### Description

Acceptance or resolution thresholds are changed after inspecting the result so that one preferred hypothesis becomes resolved.

### Indicators

- tolerance changed after fitting;
- parameter bounds narrowed after alternatives appeared;
- resolution requirement was not declared;
- or exploratory sensitivity choices are presented as confirmatory.

### Diagnostic Actions

Separate:

- predeclared confirmatory criteria; and
- post-hoc exploratory sensitivity analyses.

### Correct Interpretation

AIRS Draft 0.1 does not permit post-hoc thresholds to support a classification of **Resolved Within the Declared Model**.

---

## 26. Scenario 22 — Audio and Video Clocks Assumed Identical

### Description

Visible frames are used as exact audio-time anchors without validating the relationship between the audio and video clocks.

### Indicators

- audio/video offset changes over time;
- variable-frame-rate media is present;
- decoded frame timestamps are irregular;
- or audio events drift relative to visible actions.

### Diagnostic Actions

- inspect stream timestamps separately;
- estimate audio/video offset and drift;
- test codec and container timing;
- and retain uncertainty in visual event timing.

### Correct Interpretation

A stable nominal video frame rate does not prove an exact audio sample clock.

---

## 27. Scenario 23 — One Broad Region Misclassified as Resolved

### Description

Only one connected solution region remains, but it is too large to answer the stated question.

### Indicators

- location region spans several venue sections;
- timing interval exceeds the declared requirement;
- parameters remain gauge dependent;
- or model classes overlap throughout the region.

### Correct Interpretation

One connected region is not automatically a resolved result.

Use **Non-Resolvable** when the surviving set exceeds the predeclared timing, location, geometry, or model-discrimination resolution.

---

## 28. Scenario 24 — Distinct Bounded Alternatives Misclassified as Non-Resolvable

### Description

Several discrete, well-bounded branches remain, but the report combines them into one vague ambiguous result.

### Correct Interpretation

Use **Multiple Admissible Solutions** when the branches:

- are materially distinct;
- are individually bounded;
- and can be meaningfully described as alternative solutions.

Use **Non-Resolvable** when the surviving set cannot itself be usefully bounded or separated.

---

## 29. Scenario 25 — Shared Recording Lineage Mistaken for Independent Evidence

### Description

Two apparent observers are copies, edits, reposts, or transcodes derived from one original recording.

### Indicators

- identical background noise and reverberation;
- matching codec defects or dropouts;
- identical automatic-gain behavior;
- waveform agreement beyond what separate microphones should produce;
- or matching discontinuities and timing edits.

### Diagnostic Actions

- compare provenance and metadata;
- perform waveform and spectral fingerprinting;
- inspect codec and platform-processing signatures;
- test whether one recording can be generated from the other by delay, gain, filtering, resampling, or transcoding;
- and document reposting or derivative lineage.

### Correct Interpretation

Derivative recordings are not independent acoustic observers. They may still provide provenance or continuity information, but they must not be counted as independent geometry or timing constraints.

### Possible Consequences

- identify the common underlying acoustic observation;
- collapse derivative copies into one observer for timing and geometry inference, or model the derivation deterministically;
- use covariance only for partially shared or imperfectly dependent processing;
- reduce the effective observer count;
- reassess observability and all result classifications;
- and reconsider the primary inference classification, which may change to **Provisionally Resolved Within the Searched Hypothesis Space**, **Multiple Admissible Solutions**, **Non-Resolvable**, or another supported AIRS classification.

Exact or near-exact derivative dependence must not be handled solely by assigning a correlation coefficient and retaining each copy as a separate acoustic observer.

---

## 30. Scenario 26 — Event-Dependent Latency Mistaken for Clock Error

### Description

Detection, buffering, filtering, codec, automatic-gain, or operating-system delay changes between events, but the analysis assumes one constant clock offset.

### Indicators

- some events align while others retain observer-specific residuals;
- residuals correlate with amplitude, frequency content, clipping, or detector threshold;
- different onset detectors produce event-specific shifts;
- or one constant `βᵢ` cannot explain the timing while no smooth clock drift is present.

### Diagnostic Actions

- compare multiple onset detectors and frequency bands;
- inspect codec, filtering, and automatic-gain behavior;
- estimate or bound `ℓᵢ,e` separately from `βᵢ` in recorded-time units, or explicitly transform a physical-time latency through the declared clock-scale model;
- test whether the latency pattern is deterministic, stochastic, or a discrete processing state;
- and propagate latency uncertainty.

### Correct Interpretation

A constant latency may be absorbed into clock offset. Event-dependent latency cannot be assumed to cancel and must not automatically be interpreted as clock drift or propagation change.

Because `ℓᵢ,e` is expressed in recorded-time units in AIRS Draft 0.1, latency estimates expressed in physical seconds must be converted consistently using the applicable clock-scale convention.

### Possible Outcomes

- an event-dependent latency model is retained;
- the constant-offset-only branch is rejected;
- **Multiple Admissible Solutions** remain when latency states cannot be distinguished;
- or **Non-Resolvable** applies when latency cannot be bounded at the required timing resolution.

---

## 31. Scenario 27 — Clock Model Not Temporally Observable

### Description

The analysis estimates `βᵢ`, `αᵢ`, and `γᵢ` without enough independent events, temporal span, or external timing information.

### Indicators

- large clock-parameter covariance;
- offset, scale, and drift trade against event times or source motion;
- drift changes greatly with initialization;
- additional clock terms reduce residuals without improving held-out predictions;
- or the fitted time span is too short to separate scale from drift.

### Diagnostic Actions

- inspect rank and parameter correlations;
- compare nested clock models;
- increase temporal span or event diversity;
- add calibrated timing references;
- fix unsupported parameters to justified values or bounds;
- and test held-out events.

### Correct Interpretation

A more complex clock model may fit better while remaining unobservable. Unsupported clock terms should not be used to absorb propagation or event-association errors.

### Possible Outcomes

- reject the overparameterized clock branch;
- retain a simpler observable clock model;
- classify the result as **Non-Resolvable** when clock and event or propagation parameters remain coupled;
- or report **Provisionally Resolved Within the Searched Hypothesis Space** when only a limited clock family was tested.

---

## 32. Scenario 28 — Shared Clock or Multichannel Acquisition Mistaken for Independent Clocks or Acquisition Chains

### Description

Several channels from one device, synchronized recorder array, or shared acquisition system are treated as having independent clocks, processing chains, or statistically independent errors merely because they are stored as separate channels or files.

### Indicators

- identical sample counts and timestamps;
- simultaneous dropouts or discontinuities;
- one shared codec or container timebase;
- common automatic-gain, filtering, or resampling behavior;
- or channel metadata identifying one acquisition device.

### Diagnostic Actions

- inspect channel layout and acquisition metadata;
- determine which clocks, converters, buffers, and processing stages are shared;
- distinguish separate microphone measurements from separate timing references;
- model shared clock and processing parameters explicitly;
- and represent remaining common errors through shared parameters or covariance.

### Correct Interpretation

Separate channels may contribute useful spatial, phase, or amplitude information when their geometry and calibration are known. They do not provide independent clock constraints merely because they are stored as separate channels or files.

Shared-clock channels may be retained as separate acoustic measurement channels when they contain distinct microphone observations. They must share the applicable device-clock and processing model and must not be counted as independent clock observations or statistically independent evidence without an explicit dependency model.

### Possible Consequences

- reduce the effective number of independent clocks and acquisition chains, without necessarily discarding distinct microphone channels;
- retain distinct microphone channels under one shared device-clock model;
- revise covariance and observability;
- and reconsider the primary inference classification.

---

## 33. Troubleshooting Logs

Every troubleshooting action should be recorded with:

- issue identifier;
- affected observer, event, and hypothesis;
- observed symptom;
- suspected cause;
- diagnostic test;
- software version and configuration;
- parameter changes;
- result before and after the test;
- current workflow status, including **classification pending** when applicable;
- retained and rejected alternatives;
- effect on uncertainty;
- effect on primary inference classification;
- and effect on integrity status.

Manual intervention must be distinguishable from automated processing.

---

## 34. Minimum Troubleshooting Tests

An implementation should be tested against at least:

1. wrong neighboring-event association;
2. arbitrary clock offset;
3. clock-scale error;
4. centered clock drift;
5. abrupt timing discontinuity;
6. insufficient observer geometry;
7. unfixed timing gauge;
8. unfixed spatial gauge;
9. reflection stronger than the direct path;
10. missing direct path;
11. distributed PA system;
12. distributed crowd source;
13. integer-cycle ambiguity;
14. hardware phase bias;
15. phase-correction uncertainty comparable to `π` radians or spanning one or more full cycles;
16. nonuniform atmosphere;
17. shared covariance bias;
18. discrete multimodal hypotheses;
19. solver local minima;
20. low-residual physically invalid solution;
21. incomplete search;
22. no-solution searched-space case;
23. exhaustive model-incompatible case;
24. post-hoc threshold attempt;
25. audio/video clock mismatch;
26. shared recording lineage mistaken for independent evidence;
27. event-dependent latency mistaken for clock error;
28. temporally unobservable clock model;
29. shared clock or multichannel acquisition mistaken for independent clocks or acquisition chains;
30. multiple bounded solutions;
31. one broad non-resolvable region;
32. and explicitly modeled integrity exceptions.

---

## 35. Appropriate Troubleshooting Language

Appropriate:

> The selected event association was rejected because it required propagation and clock parameters outside the declared bounds.

Appropriate:

> Multiple bounded path hypotheses remain admissible and are reported separately.

Appropriate:

> The direct arrival could not be distinguished from later reflections at the predeclared timing resolution.

Appropriate:

> The optimizer did not converge; the workflow status remained **classification pending** while numerical conditioning, gauge constraints, implementation correctness, and model alternatives were investigated.

Appropriate:

> No admissible solution was found in the searched hypothesis space; unsearched alternatives may remain.

Not appropriate:

> The solver failed, so the recording is fake.

Not appropriate:

> The pairwise matrix closes, so there was no editing.

Not appropriate:

> The phase branch with the smallest residual is the true distance.

Not appropriate:

> One plotted coordinate solution proves the geometry is unique.

---

## 36. Relationship to AIRS Draft 0.1

This guide:

- is informative and non-normative;
- does not alter AIRS Draft 0.1;
- does not define forensic validity;
- and does not convert compatibility into authenticity.

Normative requirements remain in the AIRS specification.

A troubleshooting result should ultimately be reported using the inference classifications, integrity status, search-completeness language, uncertainty treatment, and claim limitations defined by AIRS Draft 0.1.

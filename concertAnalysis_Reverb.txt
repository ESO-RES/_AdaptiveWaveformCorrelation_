# Concert Audio Analysis
## A Physics-Constrained Multi-Device Timing, Propagation, and Reverberation Guide

This guide describes how cameras with audio tracks, phones, and dedicated recorders can be used to analyze a live concert containing repeated acoustic events such as kick hits, snare hits, vocal cues, claps, pyrotechnic reports, and cymbal crashes.

The method does **not** assume that:

- consumer devices share a clock,
- repeated musical events preserve a common carrier phase,
- a narrowband phase value directly reveals absolute distance,
- all listeners receive sound from one point source,
- or cross-device consistency proves authenticity.

The objective is to determine which event associations, clock models, propagation paths, source configurations, and venue geometries remain compatible with the recordings and their declared uncertainties.

This is a proposed research workflow, not a validated forensic standard or a claim that arbitrary audience recordings automatically provide absolute phase range.

---

## 1. Concert Events and Effective Acoustic Sources

Let:

- e = one selected concert event
- τₑ = physical occurrence time of event e
- sᵢ = position of recorder i
- xₑ = effective acoustic source position for event e
- pᵢ,e = modeled propagation time from event e to recorder i
- c = effective sound speed under a simplified homogeneous-air model

For a single point-source approximation:

```text
rᵢ,e = ‖sᵢ − xₑ‖
pᵢ,e = rᵢ,e/c
```

The effective acoustic source may not coincide with the visible performer or instrument.

Examples include:

- an acoustic snare plus its amplified version,
- a vocal signal radiated by multiple loudspeakers,
- a kick drum reproduced by subwoofer arrays,
- a delayed fill speaker closer to the audience than the main stage,
- a pyrotechnic report plus venue reflections,
- and crowd reactions originating throughout the venue.

The source model must identify which arrival component is being measured.

---

## 2. Distributed Public-Address Systems

Many concerts use multiple loudspeakers with electronic delay, including:

- main left and right arrays,
- subwoofer arrays,
- front fills,
- side fills,
- under-balcony fills,
- and delay towers.

Let:

- lₖ = position of loudspeaker k
- δₖ,e = electronic or processing delay applied to event e at loudspeaker k
- gᵢₖ,e = path gain from loudspeaker k to recorder i

A simplified loudspeaker-path arrival time is:

```text
pᵢₖ,e = δₖ,e + ‖sᵢ − lₖ‖/c
```

A recorder may receive several overlapping arrivals:

```text
hᵢ,e(t) = Σₖ gᵢₖ,e · hᵢₖ,e(t − pᵢₖ,e) + reverberation
```

The earliest detectable arrival, strongest arrival, and perceptually dominant arrival may be different.

Therefore, a concert should not automatically be modeled as one stage point source. The analysis must state whether it uses:

- the earliest direct arrival,
- a selected loudspeaker path,
- an effective source approximation,
- or a multi-source propagation model.

---

## 3. What Each Device Records

A useful timing model for event e on device i is:

```text
yᵢ,e = βᵢ + αᵢ(τₑ + pᵢ,e) + ℓᵢ,e + εᵢ,e
```

where:

- yᵢ,e = event time in device-recorded coordinates
- βᵢ = constant device clock offset
- αᵢ = device clock-scale factor
- pᵢ,e = selected or modeled propagation time
- ℓᵢ,e = event-dependent processing or detection delay
- εᵢ,e = measurement noise and unmodeled error

Under this convention, ℓᵢ,e and εᵢ,e are expressed in device-recorded time units.

A constant device delay that affects all events equally is absorbed into βᵢ. Event-dependent latency, adaptive processing, dropped samples, resampling changes, and onset-selection differences do not necessarily cancel.

Clock convention:

```text
αᵢ = recorded-time units per unit of physical time
```

For an ideal clock:

```text
αᵢ = 1
```

---

## 4. What Can and Cannot Be Inferred

Potentially supportable conclusions include:

- two clips contain compatible instances of the same event,
- a device clock exhibits measurable scale error or drift,
- selected arrivals are compatible with a declared venue and source model,
- one event association fits better than alternatives,
- or the available data are non-resolvable.

The recordings do not automatically establish:

- absolute recorder position,
- a unique venue geometry,
- continuous phase coherence across a set,
- authenticity,
- absence of editing,
- or a single physical source path.

---

## 5. Event Selection

Useful events have:

- a sharp and identifiable onset,
- adequate signal-to-noise ratio,
- distinguishable waveform or spectral structure,
- sufficient separation from neighboring events,
- and support across several devices.

Possible anchors include:

- isolated snare hits,
- kick transients with a clear high-frequency onset,
- hand claps,
- vocal consonants,
- stage pyrotechnics,
- cue tones,
- and abrupt lighting or video events with an audio counterpart.

Repeated beats are dangerous because adjacent hits may be nearly interchangeable. Event identity must be tested rather than assumed.

A kick hit on one device must not be paired with the next kick hit on another merely because their filtered waveforms look similar.

---

## 6. Source-Media Preservation

For every source file, record:

- original filename,
- cryptographic hash,
- container and codec metadata,
- nominal audio sample rate,
- video frame rate,
- channel layout,
- duration,
- and every transcoding or extraction operation.

Never overwrite the original media.

Evidence of inserted or removed samples, discontinuous resampling, duplicated frames, altered timing, or missing intervals should be treated as an integrity condition or alternate hypothesis rather than ordinary Gaussian uncertainty.

---

## 7. Event-Detection Workflow

### Step 1 — Extract audio reproducibly

Convert each source to a documented analysis format, preferably lossless PCM.

Do not assume that resampling several files to the same nominal sample rate removes their original clock-scale differences.

### Step 2 — Detect broadband onsets

Use broadband evidence as the primary timing measurement.

Candidate methods include:

- matched filtering,
- waveform cross-correlation,
- GCC-PHAT,
- spectral-flux onset detection,
- multiband energy change,
- or a validated transient detector.

### Step 3 — Generate multiple candidates

For repetitive music, retain several plausible event candidates per device rather than immediately choosing the nearest or loudest transient.

### Step 4 — Associate events across devices

Use:

- coarse metadata time,
- event order,
- waveform similarity,
- spectral shape,
- neighboring musical context,
- stage-video evidence,
- known set timing,
- propagation feasibility,
- and clock-drift continuity.

### Step 5 — Reject or retain alternate associations

A defensible analysis reports competing event groupings when more than one remains plausible.

---

## 8. Clock Alignment Across a Concert Set

A constant cross-device time offset does not reveal geometry by itself. It combines recording start time, clock offset, device latency, and propagation delay.

For a set of associated events, define the corrected device time:

```text
zᵢ,e = (yᵢ,e − βᵢ − ℓᵢ,e)/αᵢ
```

The model predicts:

```text
zᵢ,e ≈ τₑ + pᵢ,e
```

For two events a and b recorded by device i:

```text
Δyᵢ(a,b) = yᵢ,b − yᵢ,a
```

and:

```text
Δyᵢ(a,b)
= αᵢ[(τ_b − τ_a) + (pᵢ,b − pᵢ,a)]
  + Δℓᵢ(a,b)
  + Δεᵢ(a,b)
```

The constant offset βᵢ cancels within one recording. Clock scale, event-dependent propagation, and event-dependent latency do not.

Repeated events can support estimation of αᵢ and clock drift, but only after event identity and source-path changes are modeled.

---

## 9. Centered Clock-Drift Model

A single αᵢ assumes locally linear clock behavior.

Define physical arrival time:

```text
uᵢ,e = τₑ + pᵢ,e
```

Choose a reference time u_ref near the analyzed interval:

```text
qᵢ,e = uᵢ,e − u_ref
```

A higher-order model is:

```text
yᵢ,e = βᵢ + αᵢqᵢ,e + ½γᵢqᵢ,e² + ℓᵢ,e + εᵢ,e
```

where γᵢ represents clock-rate drift.

In the centered model, βᵢ is the device-time intercept at u_ref. Centering reduces parameter correlation and improves numerical conditioning.

Do not interpret a changing cross-device lag as clock drift until source changes, PA delay changes, and path-selection changes have been tested.

---

## 10. Reverberation and Multipath

Concert venues produce:

- wall and ceiling reflections,
- floor reflections,
- balcony paths,
- crowd scattering,
- stage reflections,
- and multiple delayed loudspeaker arrivals.

A filtered transient may contain a direct component followed by stronger reflections. The largest peak is not necessarily the direct path.

Recommended practice:

- analyze broadband and multiband arrivals,
- inspect time-frequency structure,
- compare early and late correlation peaks,
- report coherence,
- retain alternate path hypotheses,
- and mark events non-resolvable when the direct arrival cannot be distinguished.

GCC-PHAT can reduce some spectral-coloration effects, but it does not guarantee direct-path recovery in a reverberant or multi-source field.

---

## 11. Role of Narrowband Phase

Narrowband phase is not the primary cross-device timing observable for arbitrary concert recordings.

Filtering a transient into a narrow band creates a ringing waveform. Its measured phase may depend on:

- the original source waveform,
- the selected filter and its group delay,
- microphone response,
- device processing,
- clock offset,
- resampling,
- loudspeaker phase response,
- multipath,
- and the chosen analysis window.

For the **same event**, source phase may cancel in a justified inter-device cross-spectrum model. A more complete relative-phase observation is:

```text
φᵢⱼ,e(f)
≈ wrap{2πf[pᵢ,e − pⱼ,e + κᵢⱼ,e]
       + ψᵢⱼ(f)
       + ηᵢⱼ,e(f)}
```

where:

- κᵢⱼ,e = residual inter-device timing error after clock and event alignment
- ψᵢⱼ(f) = differential device, filter, and hardware phase
- ηᵢⱼ,e(f) = noise and model error

Only after clock offset, scale, drift, and event-window alignment have been adequately corrected may one assume:

```text
κᵢⱼ,e ≈ 0
```

The clock-corrected form is then:

```text
φᵢⱼ,e(f)
≈ wrap{2πf[pᵢ,e − pⱼ,e] + ψᵢⱼ(f) + ηᵢⱼ,e(f)}
```

This relationship is useful only when:

- the same physical event is correctly associated,
- the same propagation component is selected,
- clock effects are corrected or bounded,
- differential hardware phase is calibrated or eliminated,
- and cross-device coherence is adequate.

Separate kick, snare, vocal, and cymbal events do not generally preserve a common source phase. Phase must not be counted continuously from one independent event to another.

---

## 12. Coarse Timing Before Phase Refinement

At frequency f:

```text
λ = c/f
```

At 1 kHz with c ≈ 344 m/s:

```text
λ ≈ 0.344 m
1 period ≈ 1 ms
```

This does **not** mean that one measured wrapped phase uniquely reveals distance.

Wrapped phase supplies only a fractional-cycle observation:

```text
fractional cycle = φ/2π
```

The unknown integer cycle count remains:

```text
range difference ≈ λ(n + φ/2π)
```

Use broadband delay, geometry bounds, calibrated pilots, repeated observations, or other constraints to resolve or limit n.

Phase may then refine a coarse arrival estimate when the phase model is valid.

---

## 13. Numerical Venue Example

Assume that the selected propagation paths to two recorders differ in effective length by:

```text
Δr = rᵢ,e − rⱼ,e ≈ 61 m
c ≈ 344 m/s
```

The propagation-time difference is:

```text
Δp = pᵢ,e − pⱼ,e
   ≈ Δr/c
   ≈ 61/344
   ≈ 0.1773 s
   ≈ 177.3 ms
```

At 1 kHz, this duration contains:

```text
0.1773 s × 1000 Hz ≈ 177.3 equivalent periods
```

This is a time conversion, not an automatically observed absolute cycle count.

A wrapped phase measurement reveals only the fractional portion unless the 177-cycle ambiguity is resolved by independent constraints.

If a delay speaker adds 25 ms of electronic delay, the selected path changes by another:

```text
25 ms × 1000 Hz = 25 equivalent periods
```

A seating interpretation that ignores the PA delay could therefore be wrong by many metres.

---

## 14. Cross-Device Consistency

For the same event e on devices i and j, define:

```text
zᵢ,e = (yᵢ,e − βᵢ − ℓᵢ,e)/αᵢ
zⱼ,e = (yⱼ,e − βⱼ − ℓⱼ,e)/αⱼ
```

A timing-and-propagation residual is:

```text
eᵢⱼ,e = zᵢ,e − zⱼ,e − (pᵢ,e − pⱼ,e)
```

A compatible model predicts:

```text
eᵢⱼ,e ≈ 0
```

within uncertainty.

For two events a and b, a difference-of-intervals residual can eliminate constant clock offsets:

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

This is a model-consistency test, not proof of authenticity.

---

## 15. Pairwise Matrices and Closure

A pairwise lag matrix can be useful for detecting gross inconsistency.

Define the pairwise-lag sign convention:

```text
Δt_AB,e = t_A,e − t_B,e
```

For lags computed from one internally assigned set of event times, algebraic closure is exact:

```text
Δt_AB,e + Δt_BC,e = Δt_AC,e
```

For independently measured noisy lags:

```text
Δt̂_AB,e + Δt̂_BC,e ≈ Δt̂_AC,e
```

Closure may therefore occur automatically when all pairwise lags were derived from one internally assigned set of event times.

Closure can detect incompatible measurements, but it does not independently prove:

- correct event identity,
- correct source selection,
- correct direct-path selection,
- authenticity,
- or unique venue geometry.

Report the source of every pairwise lag and whether the matrix was constructed from independent measurements or from one shared fitted timeline.

---

## 16. Multi-Band Analysis

Broadband agreement is generally more informative than one narrow frequency.

Recommended bands depend on the event and recording quality, but the analysis should examine:

- onset timing,
- cross-correlation peak stability,
- coherence,
- phase slope or group delay,
- and direct-versus-reflected path behavior.

Multi-band disagreement may indicate:

- frequency-dependent loudspeaker paths,
- crossover behavior,
- microphone processing,
- multipath,
- wrong event association,
- or editing.

It is not automatically evidence of fabrication.

Likewise, multi-band agreement is supportive but not proof of authenticity.

---

## 17. Estimating Recorder or Seating Geometry

Recorder position may be constrained when enough information is known, including:

- source or loudspeaker positions,
- electronic PA delays,
- clock scale and offset,
- selected propagation paths,
- sound speed,
- and adequate sensor geometry.

A single cross-device offset is insufficient because it combines:

```text
clock offset
+ device latency
+ propagation delay
+ source-path delay
```

Approximate seating or recorder geometry should be reported as a region with uncertainty, not as an exact seat, unless independent surveyed constraints support that precision.

Distributed PA systems can make the strongest arrival correspond to a nearby fill speaker rather than the stage. In that case, “distance to stage” is the wrong geometric interpretation.

---

## 18. Combining Repeated Events

Repeated events should be combined only after testing whether they share the same source and propagation model.

Possible event classes include:

- main-array vocal events,
- acoustic drum transients,
- amplified drum transients,
- subwoofer-dominated kick events,
- pyrotechnic reports,
- and crowd-originated events.

Do not average incompatible classes.

For a compatible class, estimate:

- clock parameters,
- source or loudspeaker path,
- event times,
- residuals,
- outliers,
- and covariance.

A stable result means that clock-corrected timing and propagation residuals remain compatible across the selected events. It does not mean that absolute carrier phase remains stable across the concert.

---

## 19. Uncertainty and Covariance

For the device-specific estimate of physical event time:

```text
τ̂ᵢ,e = (yᵢ,e − βᵢ − ℓᵢ,e)/αᵢ − pᵢ,e
```

a first-order uncertainty model should include contributions from:

- event detection,
- clock offset,
- clock scale,
- clock drift,
- event-dependent latency,
- recorder position,
- source or loudspeaker position,
- electronic PA delay,
- sound speed,
- path selection,
- and multipath.

Shared source locations, PA delays, atmosphere, event associations, and venue geometry create correlated errors across devices.

A result should be marked **non-resolvable** when uncertainty or covariance prevents meaningful discrimination among competing hypotheses.

---

## 20. Multi-Device Evidence Matrix

For each device and event, report at minimum:

| Field | Meaning |
|---|---|
| Device ID | Stable recording-source identifier |
| Event ID | Cross-device event-group identifier |
| Event class | Snare, kick, vocal, pyrotechnic, crowd, or other |
| Recorded event time yᵢ,e | Event time in device coordinates |
| Clock offset βᵢ | Estimated or nuisance time offset |
| Clock scale αᵢ | Estimated timebase scale |
| Clock drift γᵢ | Higher-order drift when modeled |
| Selected source/path | Stage, main array, fill, delay tower, or alternate |
| Propagation pᵢ,e | Modeled travel and electronic delay |
| Event latency ℓᵢ,e | Event-dependent processing or detection delay |
| Coherence | Cross-device coherence metric |
| Corrected residual | Timing-and-propagation model residual |
| Uncertainty | Declared standard uncertainty or interval |
| Status | Accepted, rejected, ambiguous, or non-resolvable |

The audit record should also preserve detector configuration, software version, source hashes, filters, resampling operations, and all rejected event associations.

---

## 21. Adversarial and Integrity Checks

Recommended checks include:

1. **Adjacent-beat substitution**  
   Pair neighboring kick or snare hits and compare model residuals.

2. **Alternate loudspeaker path**  
   Test main-array, fill, and delay-tower hypotheses.

3. **Clock-drift sensitivity**  
   Refit with affine and higher-order clock models.

4. **Leave-one-device-out analysis**  
   Refit after removing each device.

5. **Leave-one-event-out analysis**  
   Refit after removing each event.

6. **Direct-versus-reflection analysis**  
   Compare early and late correlation peaks.

7. **Multiband consistency**  
   Compare timing and coherence across bands.

8. **Video-audio consistency**  
   Compare visible stage actions, lighting cues, and pyrotechnics with audio timing.

9. **Editing and continuity analysis**  
   Test for duplicated samples, removed intervals, discontinuous resampling, and altered timing.

10. **Search-completeness reporting**  
    State whether event combinations, clock models, and propagation paths were exhaustively tested or heuristically pruned.

11. **Alternate venue or source hypothesis**  
    Test whether another geometry explains the recordings comparably well.

Consistency means that a declared hypothesis survives the tested constraints. It does not prove that the recordings are authentic or unedited.

---

## 22. Minimum Validation Tests

A software implementation should include at least the following tests.

### Test 1 — Shared point source

Simulate one source, known recorder positions, synchronized clocks, and no reverberation. Recover the expected TDOA values.

### Test 2 — Clock offset

Add arbitrary βᵢ values. Verify that multi-event clock estimation or within-device intervals handle the offsets correctly.

### Test 3 — Clock scale

Apply known αᵢ values and verify their recovery from repeated associated events.

### Test 4 — Clock drift

Apply known γᵢ values over a long set and verify that the centered model improves the residuals.

### Test 5 — Wrong beat association

Pair one device to an adjacent beat. The correct association should produce materially better residuals.

### Test 6 — Delay speaker

Add a secondary loudspeaker with known electronic delay. Verify that a stage-only point-source model fails and the multi-source model succeeds.

### Test 7 — Strong reflection

Create a reflection stronger than the direct path. Verify that the system retains alternate path hypotheses or returns non-resolvable.

### Test 8 — Missing direct path

Remove the direct component for one device. The result should not silently interpret a reflection as exact geometry.

### Test 9 — Narrowband ambiguity

Create a 1 kHz observation with many possible integer cycles. Verify that wrapped phase alone does not produce a unique range.

### Test 10 — Hardware phase offset

Add differential microphone or filter phase. Verify that uncalibrated phase is rejected or assigned larger uncertainty.

### Test 11 — Source-class change

Mix acoustic drum events with PA-dominated events. Verify that incompatible source classes are not averaged as one geometry.

### Test 12 — Non-resolvable case

Create competing event and path hypotheses within the uncertainty limit. The system must report ambiguity or non-resolvable.

### Test 13 — Timing edit

Insert or remove samples between events. Verify that the system flags a continuity or clock-model violation.

### Test 14 — Correlated PA-delay error

Bias one shared PA delay parameter. Verify that the error appears as shared covariance rather than independent device noise.

---

## 23. Appropriate Result Language

Appropriate:

> The selected event associations are compatible with the declared clock, source, propagation, and uncertainty model.

Appropriate:

> The recordings support a bounded recorder-location region under the selected loudspeaker-path hypothesis.

Appropriate:

> The available recordings are non-resolvable because direct and reflected paths cannot be distinguished.

Not appropriate:

> Phase proves the exact seats.

Not appropriate:

> Stable phase across the set proves the clips are genuine.

Not appropriate:

> A closed pairwise matrix proves there was no editing.

Not appropriate:

> One fitted venue geometry proves authenticity.

---

## 24. Practical Uses

With adequate calibration and uncertainty reporting, the workflow may support:

- coarse synchronization of separately acquired concert recordings,
- clock-scale and drift correction,
- event association across devices,
- comparison of alternate loudspeaker paths,
- approximate recorder-location constraints,
- detection of gross timing discontinuities,
- and creation of a crowd-sourced mix.

Sample-level summation of consumer recordings may still fail because of spatial decorrelation, reverberation, automatic processing, and residual clock error. A practical crowd mix may require time-varying alignment, source separation, or selection rather than direct coherent summation.

---

## 25. Mental Model Summary

- Concert audio is usually a multi-source, multi-path problem.
- The visible stage action may not be the effective acoustic source.
- Distributed PA delays can dominate apparent geometry.
- Broadband event timing is the primary observable.
- Repeated events can estimate clock scale only after event and path association.
- Narrowband phase is a conditional refinement, not automatic absolute range.
- Separate musical events do not preserve continuous carrier phase.
- Pairwise closure is a consistency check, not authenticity proof.
- Geometry must be reported with uncertainty and alternate path hypotheses.
- Editing is an integrity hypothesis, not ordinary random noise.
- Non-resolvable is a valid result.

---

## 26. Final Corrected Claim

> Concert analysis is a multi-event, multi-source, multi-path timing problem. Separately acquired recordings may constrain event identity, device clocks, selected propagation paths, and recorder geometry when source configuration, PA delays, reverberation, and uncertainty are explicitly modeled. Narrowband phase may refine a calibrated same-event measurement, but it does not establish absolute distance, continuous phase coherence across a set, or authenticity by itself.

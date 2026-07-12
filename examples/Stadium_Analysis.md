# Sports Stadium Audio Analysis
## A Physics-Constrained Multi-Device Timing, Propagation, and Geometry Guide

This guide describes how cameras with audio tracks, phones, and dedicated recorders can be used to analyze acoustic events in sports stadiums and arenas.

Possible events include:

- bat cracks,
- ball or puck impacts,
- basketball rim or backboard strikes,
- referee whistles,
- starting pistols,
- field-goal kicks,
- goal horns,
- public-address announcements,
- pyrotechnic reports,
- and crowd reactions.

The method does **not** assume that:

- consumer devices share a clock,
- all stadium sounds originate from one point,
- repeated events preserve a common carrier phase,
- raw event intervals are identical across devices,
- a narrowband phase value directly reveals absolute distance,
- pairwise closure proves authenticity,
- or one fitted geometry proves that recordings are genuine.

The objective is to determine which event associations, clock models, propagation paths, source configurations, and recorder geometries remain compatible with the recordings and their declared uncertainties.

This is a proposed research workflow, not a validated forensic standard or a claim that arbitrary stadium recordings automatically provide absolute phase range.

---

## 1. Event Classes

Stadium sounds should be divided into physically distinct event classes.

### 1.1 Direct field events

Examples:

- bat crack,
- ball striking a glove,
- ball or puck striking a surface,
- rim or backboard impact,
- referee whistle,
- starting pistol,
- and player contact.

A simplified point-source model may be reasonable when the source position and direct path are identifiable.

### 1.2 Amplified or electronically triggered events

Examples:

- public-address speech,
- goal horns,
- scoreboard tones,
- music cues,
- replay audio,
- and loudspeaker-amplified whistles or announcements.

These events may radiate from many loudspeakers with different electronic delays.

### 1.3 Distributed crowd events

Examples:

- cheering,
- booing,
- chants,
- applause,
- and wave-like reactions.

Crowd reactions are distributed in space and develop over time. They should not normally be treated as one instantaneous point source.

### 1.4 Mixed events

A direct field event may be followed by:

- amplified replay audio,
- a scoreboard tone,
- announcer speech,
- and a crowd response.

These are separate source processes and must not be combined as though they were one coherent acoustic event.

---

## 2. Physical Events and Coordinates

Let:

- e = one selected event
- τₑ = physical occurrence time of event e
- sᵢ = position of recorder i
- xₑ = effective acoustic source position for event e
- pᵢ,e = modeled propagation time from event e to recorder i
- c = effective sound speed under a simplified homogeneous-air model

For a direct point-source approximation:

```text
rᵢ,e = ‖sᵢ − xₑ‖
pᵢ,e = rᵢ,e/c
```

The effective acoustic source may differ from the visually identified mechanical contact point.

Examples include:

- vibration radiating along a bat,
- a glove impact radiating from the glove, hand, and body,
- a whistle radiating directionally from the official,
- a ball impact exciting a wall or backboard,
- and a pyrotechnic event containing several spatially separated charges.

Any difference between the visual event position and effective acoustic source position must be estimated, bounded, or included in the source-position uncertainty.

---

## 3. Stadium Public-Address Systems

Many stadiums use distributed loudspeaker systems, including:

- main bowl arrays,
- field-level fills,
- concourse loudspeakers,
- under-balcony fills,
- scoreboard loudspeakers,
- and delay zones.

Let:

- lₖ = position of loudspeaker k
- δₖ,e = electronic or processing delay for event e on loudspeaker path k
- gᵢₖ,e = gain from loudspeaker k to recorder i

For an amplified event, τₑ is the declared reference generation or trigger time before path-specific PA routing. The term δₖ,e contains the electronic and processing delay from that reference to loudspeaker-path emission. If τₑ is instead defined at loudspeaker emission, the corresponding δₖ,e term must not be added again.

The delay δₖ,e is expressed in physical seconds before device clock scaling. It may include source-to-loudspeaker routing, configured delay, digital processing, and transmission latency.

A simplified loudspeaker-path travel time is:

```text
pᵢₖ,e = δₖ,e + ‖sᵢ − lₖ‖/c
```

A recorder may receive several overlapping loudspeaker paths. Using absolute physical time, a more explicit model is:

```text
xᵢ,e(t)
= Σₖ gᵢₖ,e · [aₖ,e * h̃ᵢₖ,e](t − τₑ − pᵢₖ,e)
  + vᵢ,e(t)
```

where:

- t = absolute physical time
- τₑ = declared reference generation or trigger time for event e
- aₖ,e(t) = zero-referenced event waveform emitted by loudspeaker k before the path delay is applied
- h̃ᵢₖ,e(t) = zero-referenced acoustic path response from loudspeaker k to recorder i, with the bulk delay pᵢₖ,e removed
- * = convolution
- vᵢ,e(t) = noise and unmodeled reverberant contribution

If hᵢₖ,e(t) is instead a measured impulse response that already contains the complete electronic and acoustic delay, the separate shift by pᵢₖ,e must not be applied.

The earliest arrival, strongest arrival, and perceptually dominant arrival may be different.

The analysis must state whether it uses:

- the earliest direct field arrival,
- a selected loudspeaker path,
- an effective-source approximation,
- or a multi-source propagation model.

---

## 4. What Each Device Records

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

A camera may also contain separate audio and video clocks. A stable video frame rate does not prove that the audio sample clock is exact.

---

## 5. What Can and Cannot Be Inferred

Potentially supportable conclusions include:

- two clips contain compatible instances of the same event,
- one event association fits better than alternatives,
- a device clock exhibits measurable offset, scale error, or drift,
- selected arrivals are compatible with a declared stadium and source model,
- recorder position is constrained to a bounded region,
- or the available data are non-resolvable.

The recordings do not automatically establish:

- exact seating locations,
- a unique stadium geometry,
- continuous phase coherence across a game,
- authenticity,
- absence of editing,
- or one unique physical propagation path.

---

## 6. Source-Media Preservation

For every source file, record:

- original filename,
- cryptographic hash,
- container and codec metadata,
- nominal audio sample rate,
- nominal and variable video frame rate,
- channel layout,
- duration,
- timestamps when available,
- and every transcoding or extraction operation.

Never overwrite the original media.

Evidence of inserted or removed samples, discontinuous resampling, duplicated frames, altered timing, or missing intervals should be treated as an integrity condition or alternate hypothesis rather than ordinary Gaussian uncertainty.

---

## 7. Event Selection

Useful events have:

- a sharp and identifiable onset,
- adequate signal-to-noise ratio,
- distinguishable waveform or spectral structure,
- sufficient separation from neighboring events,
- and support across several devices.

Possible anchors include:

- isolated bat cracks,
- whistles with a clear onset,
- ball or puck impacts,
- starting pistols,
- rim or backboard strikes,
- pyrotechnic reports,
- and electronically triggered tones with known routing.

Poor precision anchors include:

- the peak of a crowd cheer,
- long announcer phrases,
- music already reverberant in the bowl,
- and events dominated by automatic gain control.

Crowd reactions may support coarse chronology, but their onset is spatially distributed and socially delayed.

---

## 8. Event-Detection Workflow

### Step 1 — Extract audio reproducibly

Convert each source to a documented analysis format, preferably lossless PCM.

Do not assume that resampling files to the same nominal rate removes the original clock-scale differences.

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

Retain several plausible event candidates when neighboring sports actions, whistles, claps, or impacts could be confused.

### Step 4 — Associate events across devices

Use:

- coarse metadata time,
- event order,
- waveform similarity,
- spectral shape,
- game context,
- scoreboard and video evidence,
- source-position feasibility,
- propagation bounds,
- and clock-drift continuity.

### Step 5 — Retain alternate associations

A defensible analysis reports competing event groupings when more than one remains plausible.

---

## 9. Clock Alignment Across a Game

A constant cross-device time offset does not reveal seating geometry by itself. It combines:

```text
recording start offset
+ device clock offset
+ constant device latency
+ propagation delay
+ source-path delay
```

For associated events, define the clock-corrected arrival:

```text
zᵢ,e = (yᵢ,e − βᵢ − ℓᵢ,e)/αᵢ
```

The model predicts:

```text
zᵢ,e ≈ τₑ + pᵢ,e
```

Repeated events may support estimation of αᵢ and clock drift, but only after event identity and source-path changes are modeled.

Do not interpret changing cross-device lag as clock drift until movement of the source, PA routing, replay audio, reflections, and path-selection changes have been tested.

---

## 10. Centered Clock-Drift Model

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

---

## 11. Clock Gauge and Observability

The timing model contains an additive gauge freedom unless a reference is fixed.

Set:

```text
β_ref = 0
```

for one designated reference device to fix the additive timing gauge.

Set:

```text
α_ref = 1
```

only when the reference device is externally calibrated or is explicitly chosen to define the working time unit. Otherwise, retain uncertainty in α_ref or impose an independent time-scale constraint.

Equivalent external clock constraints may be used instead.

Without a clock reference or equivalent constraint:

- only relative clock offsets are identifiable,
- absolute τₑ is not uniquely determined,
- a common timing shift can be exchanged between τₑ and the device offsets,
- and clock, source, and propagation parameters may remain coupled.

Joint recorder and source localization also requires sufficient geometric anchors, event diversity, and independent measurements. A numerical optimizer returning one parameter vector does not establish observability or uniqueness.

---

## 12. Two-Event Intervals

For two events a and b recorded by device i:

```text
Δyᵢ(a,b) = yᵢ,b − yᵢ,a
```

The interval model is:

```text
Δyᵢ(a,b)
= αᵢ[(τ_b − τ_a) + (pᵢ,b − pᵢ,a)]
  + Δℓᵢ(a,b)
  + Δεᵢ(a,b)
```

The constant clock offset βᵢ cancels.

The following do not automatically cancel:

- clock-scale error,
- source-position change,
- differential propagation,
- event-dependent latency,
- and detection error.

The corrected physical event interval is:

```text
T̂ᵢ(a,b)
= [Δyᵢ(a,b) − Δℓᵢ(a,b)]/αᵢ
  − [pᵢ,b − pᵢ,a]
```

Raw event-to-event intervals are not expected to be identical across devices when the two events occur at different source positions.

For the bat-crack and glove-thud case, use the complete model in:

```text
batToGlove_Dry.md
```

The bat and glove are separate impulses. Their narrowband phase must not be counted continuously from one event to the other.

---

## 13. Why Bat-to-Glove Raw Intervals Differ

Let:

- x_bat = effective bat acoustic source
- x_glove = effective glove acoustic source
- D = ‖x_glove − x_bat‖

For recorder i under a homogeneous direct-path model:

```text
Δrᵢ = ‖sᵢ − x_glove‖ − ‖sᵢ − x_bat‖
```

The reverse triangle inequality gives:

```text
|Δrᵢ| ≤ D
```

Therefore:

```text
|Δrᵢ/c| ≤ D/c
```

Define the single-device geometry term:

```text
Gᵢ = Δrᵢ/c
```

After clock normalization and in the absence of differential latency and measurement error, the magnitude of the geometry-induced interval difference between devices i and j is bounded above by:

```text
|Gᵢ − Gⱼ| ≤ 2D/c
```

For a 60 ft source separation:

```text
D ≈ 18.288 m
c ≈ 344 m/s
2D/c ≈ 106.4 ms
```

This is a theoretical upper bound. Whether it can be approached depends on the permitted recorder positions and stadium geometry.

For a 60 ft source separation, the geometry-induced difference can approach 106.4 ms and may exceed 100 ms only for recorder configurations near the permitted geometric extremes. Less extreme placements produce smaller differences.

---

## 14. Reverberation, Reflections, and Occlusion

Stadiums and arenas produce:

- roof and canopy reflections,
- seating-bowl reflections,
- scoreboard reflections,
- field and floor reflections,
- concourse leakage,
- crowd scattering,
- and multiple loudspeaker arrivals.

A filtered transient may contain a direct component followed by stronger reflections. The largest peak is not necessarily the direct path.

Recommended practice:

- analyze broadband and multiband arrivals,
- inspect time-frequency structure,
- compare early and late correlation peaks,
- report coherence,
- retain alternate path hypotheses,
- and mark events non-resolvable when the direct arrival cannot be distinguished.

GCC-PHAT may reduce some spectral-coloration effects, but it does not guarantee direct-path recovery in a reverberant or multi-source field.

---

## 15. Outdoor Atmosphere and Wind

Open stadiums may have significant:

- wind,
- temperature gradients,
- humidity variation,
- vertical sound-speed gradients,
- and changing atmospheric conditions during a game.

A simple model uses:

```text
pᵢ,e = rᵢ,e/c
```

For higher-accuracy analysis, pᵢ,e should be treated as a modeled travel time rather than automatically as range divided by one constant c.

Record or estimate:

- air temperature,
- humidity,
- pressure,
- wind speed and direction,
- roof status,
- and relevant spatial gradients.

The same effective c should not be assumed across materially different times or paths without justification.

---

## 16. Role of Narrowband Phase

Narrowband phase is not the primary cross-device timing observable for arbitrary stadium recordings.

Filtering a transient into a narrow band creates a ringing waveform. Its phase may depend on:

- the source waveform,
- filter phase and group delay,
- microphone response,
- device processing,
- clock error,
- resampling,
- loudspeaker phase response,
- multipath,
- and the selected analysis window.

For the **same event**, source phase may cancel in a justified inter-device cross-spectrum model.

Adopt the Fourier-transform convention:

```text
X(f) = ∫x(t)e⁻ʲ²πft dt
```

Define the relative phase using the cross-spectrum order:

```text
φᵢⱼ,e(f) = arg{Xⱼ,e(f)X*ᵢ,e(f)}
```

where:

```text
X*ᵢ,e(f) = complex conjugate of Xᵢ,e(f)
```

With this convention, a positive propagation-time difference pᵢ,e − pⱼ,e contributes a positive phase term. Reversing the cross-spectrum order reverses the phase sign.

A more complete relative-phase model is:

```text
φᵢⱼ,e(f)
≈ wrap{2πf[pᵢ,e − pⱼ,e + κᵢⱼ,e]
       + ψᵢⱼ(f)
       + ηᵢⱼ,e(f)}
```

where:

- κᵢⱼ,e = residual inter-device timing error after clock and event alignment
- ψᵢⱼ(f) = differential PA-chain, loudspeaker, microphone, device, filter, and hardware phase not represented in p
- ηᵢⱼ,e(f) = noise and model error

Only after clock offset, scale, drift, and event-window alignment have been adequately corrected may one assume:

```text
κᵢⱼ,e ≈ 0
```

The clock-corrected form is:

```text
φᵢⱼ,e(f)
≈ wrap{2πf[pᵢ,e − pⱼ,e] + ψᵢⱼ(f) + ηᵢⱼ,e(f)}
```

This relationship is useful only when:

- the same event is correctly associated,
- the same propagation component is selected,
- clock effects are corrected or bounded,
- differential hardware phase is calibrated or eliminated,
- and cross-device coherence is adequate.

Separate bat cracks, whistles, impacts, horns, and crowd events do not generally preserve a common source phase.

---

## 17. Coarse Timing Before Phase Refinement

At frequency f:

```text
λ = c/f
```

At 1 kHz with c ≈ 344 m/s:

```text
λ ≈ 0.344 m
1 period ≈ 1 ms
```

This does **not** mean that one wrapped phase uniquely reveals distance.

Wrapped phase supplies only a fractional-cycle observation.

Define the corrected phase observable using estimated clock and hardware-phase corrections:

```text
φ̃ᵢⱼ,e(f)
= wrap{φᵢⱼ,e(f)
       − 2πfκ̂ᵢⱼ,e
       − ψ̂ᵢⱼ(f)}
```

Uncertainty in κ̂ᵢⱼ,e and ψ̂ᵢⱼ(f) must be propagated into the uncertainty of φ̃ᵢⱼ,e, the retained integer-cycle hypotheses, and the inferred propagation-time difference.

Then:

```text
fractional cycle = φ̃ᵢⱼ,e/2π
```

The unknown integer remains:

```text
cΔpᵢⱼ,e
≈ λ(nᵢⱼ,e + φ̃ᵢⱼ,e/2π)

nᵢⱼ,e ∈ ℤ
```

where:

```text
Δpᵢⱼ,e = pᵢ,e − pⱼ,e
```

The residual term ηᵢⱼ,e(f) belongs in the uncertainty model and is not treated as a known correction.

The quantity cΔpᵢⱼ,e is an effective path-length difference. It must not automatically be interpreted as purely geometric distance when p includes electronic PA delay.

Use broadband delay, geometry bounds, calibrated pilots, repeated observations, or other constraints to resolve or limit nᵢⱼ,e.

Phase may then refine a coarse arrival estimate when the phase model is valid.

---

## 18. Numerical Stadium Example

Assume that selected direct propagation paths from one field event to two recorders differ in length by:

```text
Δr = rᵢ,e − rⱼ,e ≈ 73 m
c ≈ 344 m/s
```

The propagation-time difference is:

```text
Δp = pᵢ,e − pⱼ,e
   ≈ Δr/c
   ≈ 73/344
   ≈ 0.2122 s
   ≈ 212.2 ms
```

At 1 kHz:

```text
0.2122 s × 1000 Hz ≈ 212.2 equivalent periods
```

This is a time conversion, not an automatically observed absolute cycle count.

A wrapped phase measurement reveals only the fractional portion unless the 212-cycle ambiguity is resolved by independent constraints.

If a stadium loudspeaker path adds 30 ms of electronic delay:

```text
30 ms × 1000 Hz = 30 equivalent periods
```

At c ≈ 344 m/s, 30 ms is equivalent to approximately:

```text
344 m/s × 0.030 s ≈ 10.3 m
```

of acoustic travel time.

It does **not** mean that the loudspeaker is physically 10.3 m farther away.

---

## 19. Cross-Device Consistency

For the same event e on devices i and j:

```text
zᵢ,e = (yᵢ,e − βᵢ − ℓᵢ,e)/αᵢ
zⱼ,e = (yⱼ,e − βⱼ − ℓⱼ,e)/αⱼ
```

Define the timing-and-propagation residual:

```text
eᵢⱼ,e = zᵢ,e − zⱼ,e − (pᵢ,e − pⱼ,e)
```

A compatible model predicts:

```text
eᵢⱼ,e ≈ 0
```

within uncertainty.

For two events a and b, define:

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

## 20. Pairwise Matrices and Closure

A pairwise lag matrix can help identify gross inconsistency.

Define the sign convention:

```text
Δt_AB,e = t_A,e − t_B,e
```

For lags computed from one internally assigned set of event times:

```text
Δt_AB,e + Δt_BC,e = Δt_AC,e
```

For independently measured noisy lags:

```text
Δt̂_AB,e + Δt̂_BC,e ≈ Δt̂_AC,e
```

Closure may therefore occur automatically when all pairwise lags were derived from one shared fitted timeline.

Closure can detect incompatible measurements, but it does not independently prove:

- correct event identity,
- correct source selection,
- correct direct-path selection,
- authenticity,
- absence of editing,
- or unique stadium geometry.

Report the source of every pairwise lag and whether the matrix was constructed from independent measurements or from one shared timeline.

---

## 21. Multi-Band Analysis

Broadband agreement is generally more informative than one narrow frequency.

The analysis should examine:

- onset timing,
- cross-correlation peak stability,
- coherence,
- phase slope or group delay,
- and direct-versus-reflected path behavior.

Multi-band disagreement may indicate:

- frequency-dependent loudspeaker paths,
- microphone processing,
- multipath,
- wind or atmospheric effects,
- wrong event association,
- or editing.

It is not automatically evidence of fabrication.

Multi-band agreement is supportive but not proof of authenticity.

---

## 22. Estimating Recorder or Seating Geometry

Recorder position may be constrained when enough information is known, including:

- event source positions,
- loudspeaker positions,
- electronic PA delays,
- clock parameters,
- selected propagation paths,
- atmospheric travel-time model,
- and adequate geometry.

A single cross-device lag is insufficient because it combines:

```text
clock offset
+ device latency
+ propagation delay
+ source-path delay
```

Approximate seating or recorder geometry should be reported as a region with uncertainty, not as an exact section, row, or seat unless independent surveyed constraints support that precision.

A strong arrival from a nearby fill speaker can make “distance to the field” the wrong interpretation.

---

## 23. Combining Events Across a Game

Events should be combined only after testing whether they share compatible source and propagation models.

Possible classes include:

- direct bat cracks,
- direct whistles,
- amplified announcements,
- scoreboard tones,
- goal horns,
- field pyrotechnics,
- and distributed crowd reactions.

Do not average incompatible classes.

For a compatible event class, estimate:

- clock parameters,
- source or loudspeaker path,
- event times,
- residuals,
- outliers,
- and covariance.

A stable result means that clock-corrected timing and propagation residuals remain compatible across selected events. It does not mean that absolute carrier phase remains stable across the game.

---

## 24. Crowd Reactions

Crowd reactions should be modeled as distributed and delayed processes.

A crowd response may include:

- local spectators reacting first,
- visual and acoustic reaction delays,
- propagation of cheering through seating sections,
- PA reinforcement,
- and automatic gain control on devices.

The “peak cheer time” is not a universal physical event time.

Crowd audio may support:

- coarse event ordering,
- section-level clustering,
- and contextual event association.

It should not normally be used as a millisecond-precision point-source anchor.

---

## 25. Uncertainty and Covariance

For the device-specific estimate of physical event time under the selected clock reference or gauge:

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
- PA electronic delay,
- sound speed,
- wind and atmospheric gradients,
- path selection,
- and multipath.

Shared source positions, PA delays, atmosphere, event associations, and stadium geometry create correlated errors across devices.

A result should be marked **non-resolvable** when uncertainty or covariance prevents meaningful discrimination among competing hypotheses.

---

## 26. Multi-Device Evidence Matrix

For each device and event, report at minimum:

| Field | Meaning |
|---|---|
| Device ID | Stable recording-source identifier |
| Event ID | Cross-device event-group identifier |
| Event class | Direct field, PA, crowd, pyrotechnic, or other |
| Recorded event time yᵢ,e | Event time in device coordinates |
| Clock offset βᵢ | Estimated or nuisance time offset |
| Clock scale αᵢ | Estimated timebase scale |
| Clock drift γᵢ | Higher-order drift when modeled |
| Selected source/path | Field source, loudspeaker, reflection, or alternate |
| Propagation pᵢ,e | Modeled travel and electronic delay |
| Event latency ℓᵢ,e | Event-dependent processing or detection delay |
| Coherence | Cross-device coherence metric |
| Corrected residual | Timing-and-propagation model residual |
| Uncertainty | Declared standard uncertainty or interval |
| Status | Accepted, rejected, ambiguous, or non-resolvable |

The audit record should preserve detector configuration, software version, source hashes, filters, resampling operations, weather assumptions, and rejected event associations.

---

## 27. Adversarial and Integrity Checks

Recommended checks include:

1. **Adjacent-event substitution**  
   Pair a recording with a neighboring whistle, impact, bat crack, or crowd peak.

2. **Alternate source path**  
   Test direct field, PA, fill-speaker, and reflected-path hypotheses.

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
   Compare visible field actions, scoreboard changes, and officiating signals with audio timing.

9. **Weather-model sensitivity**  
   Recompute across plausible sound-speed and wind conditions.

10. **Editing and continuity analysis**  
    Test for duplicated samples, removed intervals, discontinuous resampling, and altered timing.

11. **Search-completeness reporting**  
    State whether event combinations, clock models, and propagation paths were exhaustively tested or heuristically pruned.

12. **Alternate stadium or geometry hypothesis**  
    Test whether another source and recorder geometry explains the data comparably well.

Consistency means that a declared hypothesis survives the tested constraints. It does not prove that recordings are authentic or unedited.

---

## 28. Minimum Validation Tests

A software implementation should include at least the following tests.

### Test 1 — Direct point source

Simulate one field source, known recorder positions, synchronized clocks, and no reflections. Recover expected TDOA values.

### Test 2 — Clock offset

Add arbitrary βᵢ values. Verify that clock estimation or within-device intervals handle them correctly.

### Test 3 — Clock scale

Apply known αᵢ values and verify recovery from repeated associated events.

### Test 4 — Clock drift

Apply known γᵢ values across a game and verify that the centered clock model improves residuals.

### Test 5 — Wrong event association

Pair one device to a neighboring whistle, impact, or bat crack. The correct association should produce materially better residuals.

### Test 6 — Distributed PA

Add loudspeakers with known electronic delays. Verify that a single field-point model fails and the PA model succeeds.

### Test 7 — Strong reflection

Create a reflection stronger than the direct path. Verify that alternate paths are retained or the result becomes non-resolvable.

### Test 8 — Missing direct path

Remove the direct component for one device. The result must not silently interpret a reflection as exact geometry.

### Test 9 — Narrowband ambiguity

Create a 1 kHz observation with many possible integer cycles. Verify that wrapped phase alone does not produce a unique range.

### Test 10 — Hardware phase offset

Add differential microphone or filter phase. Verify that uncalibrated phase is rejected or assigned larger uncertainty.

### Test 11 — Bat-to-glove geometry

Simulate near-bat and near-glove recorders. Verify that raw intervals differ by the predicted differential propagation terms and recover one corrected physical interval.

### Test 12 — Crowd-source distribution

Simulate a spatially distributed reaction. Verify that a point-source model produces poor residuals or an expanded uncertainty region.

### Test 13 — Nonuniform atmosphere

Simulate wind or a sound-speed gradient. Verify that a general pᵢ,e model outperforms rᵢ,e/c.

### Test 14 — Non-resolvable case

Create competing event and path hypotheses within the uncertainty limit. The system must report ambiguity or non-resolvable.

### Test 15 — Timing edit

Insert or remove samples between events. Verify that the system flags a continuity or clock-model violation.

### Test 16 — Correlated PA-delay error

Bias one shared PA-delay parameter. Verify that the error appears as shared covariance rather than independent device noise.

---

## 29. Appropriate Result Language

Appropriate:

> The selected event associations are compatible with the declared clock, source, propagation, atmosphere, and uncertainty model.

Appropriate:

> The recordings support a bounded recorder-location region under the selected direct-field or loudspeaker-path hypothesis.

Appropriate:

> The available recordings are non-resolvable because direct and reflected arrivals cannot be distinguished.

Not appropriate:

> Phase proves the exact seats.

Not appropriate:

> Stable phase across the game proves the clips are genuine.

Not appropriate:

> A closed pairwise matrix proves there was no editing.

Not appropriate:

> Matching raw bat-to-glove intervals prove a common play.

Not appropriate:

> One fitted stadium geometry proves authenticity.

---

## 30. Practical Uses

With adequate calibration and uncertainty reporting, the workflow may support:

- coarse synchronization of separately acquired stadium recordings,
- clock-scale and drift correction,
- event association across devices,
- comparison of alternate direct and PA paths,
- approximate recorder-location constraints,
- timing comparison between field and scoreboard events,
- detection of gross timing discontinuities,
- and creation of a crowd-sourced event reconstruction.

Sample-level summation of consumer recordings may still fail because of spatial decorrelation, reverberation, distributed sources, automatic processing, and residual clock error.

A practical crowd mix may require time-varying alignment, source separation, event-class selection, or noncoherent mixing rather than direct sample summation.

---

## 31. Mental Model Summary

- Stadium audio is a multi-event, multi-source, multi-path problem.
- Direct field sounds, PA sounds, and crowd reactions are different event classes.
- The visible event position may not be the effective acoustic source.
- Distributed PA delays can dominate apparent seating geometry.
- Broadband event timing is the primary observable.
- Raw two-event intervals may differ across devices because source positions change.
- Narrowband phase is a conditional same-event refinement, not automatic absolute range.
- Separate events do not preserve continuous carrier phase.
- Pairwise closure is a consistency check, not authenticity proof.
- Crowd reactions are distributed and should not be treated as exact point events.
- Geometry must be reported with uncertainty and alternate path hypotheses.
- Editing is an integrity hypothesis, not ordinary random noise.
- Non-resolvable is a valid result.

---

## 32. Final Corrected Claim

> Stadium analysis is a multi-event, multi-source, multi-path timing and geometry problem. Separately acquired recordings may constrain event identity, device clocks, selected field or loudspeaker paths, and recorder geometry when source configuration, PA delays, atmosphere, reverberation, and uncertainty are explicitly modeled. Raw event intervals and wrapped phase values are not expected to be universally identical across devices. Narrowband phase may refine a calibrated same-event measurement, but it does not establish absolute distance, continuous phase coherence across a game, exact seating, or authenticity by itself.

# Bat Crack → Glove Thud
## A Physics-Constrained Multi-Device Timing and Geometry Guide

This guide describes how multiple cameras with audio tracks, phones, and dedicated audio recorders can be used to analyze one baseball play containing two separate acoustic events:

1. the bat striking the ball, and
2. the ball entering the glove.

The method does **not** assume that the raw crack-to-thud interval is identical across devices. Each recorder observes the same physical ball-flight interval plus a device-specific differential sound-propagation delay.

The objective is to estimate a common physical interval only after correcting for:

- bat, glove, and recorder geometry,
- atmospheric propagation,
- sample-clock scale or drift,
- event-detection uncertainty,
- device processing latency,
- multipath and reverberation,
- and source-position uncertainty.

This is a proposed research workflow, not a claim that arbitrary consumer recordings automatically provide absolute phase range or forensic proof.

---

## 1. Physical Events and Coordinates

Let:

- x_bat = effective acoustic source position for the selected bat onset
- x_glove = effective acoustic source position for the selected glove onset
- sᵢ = position of recorder i
- τ_bat = physical time of bat impact
- τ_glove = physical time of glove impact
- T_ball = τ_glove − τ_bat
- c = effective speed of sound under the simplified homogeneous-air model

The effective acoustic source positions may differ slightly from the visually identified mechanical contact points. The bat may radiate from multiple portions of the bat, while the glove event may include radiation from the glove, ball, hand, body, or nearby structures. Any difference between the effective acoustic source and mechanical contact point must be estimated, bounded, or included in the source-position uncertainty.

The geometric propagation ranges are:

```text
rᵢ,bat   = ‖sᵢ − x_bat‖
rᵢ,glove = ‖sᵢ − x_glove‖
```

For a general propagation environment, define:

```text
pᵢ,e = modeled propagation time from event e to recorder i
```

Under a homogeneous, stationary, straight-path model:

```text
pᵢ,e = rᵢ,e/c
```

The physical quantity of interest is:

```text
T_ball = τ_glove − τ_bat
```

This is the ball-flight interval between the two source events. It is not, in general, equal to the raw interval measured by every recorder.

---

## 2. What Each Device Records

Each device may have:

- an unknown recording start time,
- an unknown constant clock offset,
- sample-clock scale error or drift,
- codec and operating-system latency,
- automatic gain control or denoising,
- different microphone and filter responses,
- and different propagation paths.

A useful timing model for event e on device i is:

```text
yᵢ,e = βᵢ + αᵢ(τₑ + pᵢ,e) + ℓᵢ,e + εᵢ,e
```

where:

- yᵢ,e = recorded event time
- βᵢ = constant device clock offset
- αᵢ = device clock-scale factor
- pᵢ,e = modeled acoustic propagation time
- ℓᵢ,e = event-dependent processing or detection delay
- εᵢ,e = measurement noise and unmodeled error

In this convention, ℓᵢ,e and εᵢ,e are expressed in device-recorded time units and are added after the physical arrival time is mapped through the device clock. If latency is instead modeled in physical-time units, it must be placed inside the αᵢ scaling term.

A constant codec, buffering, or operating-system delay that affects both events equally is absorbed into βᵢ and cancels in the within-device interval. The term ℓᵢ,e represents only event-dependent or time-varying delay.

Clock convention:

```text
αᵢ = recorded-time units per unit of physical time
```

For an ideal clock:

```text
αᵢ = 1
```

Under this convention:

```text
αᵢ > 1
```

means the device-reported interval is longer than the corresponding physical interval.

---

## 3. Correct Crack-to-Thud Interval Model

For device i, the recorded interval is:

```text
Δyᵢ = yᵢ,glove − yᵢ,bat
```

Substituting the device model gives:

```text
Δyᵢ = αᵢ[T_ball + (pᵢ,glove − pᵢ,bat)] + Δℓᵢ + Δεᵢ
```

where:

```text
Δℓᵢ = ℓᵢ,glove − ℓᵢ,bat
Δεᵢ = εᵢ,glove − εᵢ,bat
```

The constant offset βᵢ cancels because both events are measured within the same recording. The following terms do **not** automatically cancel:

- differential propagation geometry,
- clock-scale error,
- event-dependent processing delay,
- and onset-picking error.

Define the differential propagation time:

```text
Δpᵢ = pᵢ,glove − pᵢ,bat
```

The corrected estimate from device i is:

```text
T̂ᵢ = (Δyᵢ − Δℓᵢ)/αᵢ − Δpᵢ
```

Under the homogeneous-air model:

```text
Δrᵢ = rᵢ,glove − rᵢ,bat
Δpᵢ = Δrᵢ/c
```

so:

```text
T̂ᵢ = (Δyᵢ − Δℓᵢ)/αᵢ − Δrᵢ/c
```

When Δℓᵢ cannot be calibrated, it must remain in the uncertainty budget rather than being assumed to be zero.

---

## 4. Why Raw Intervals Differ Across Devices

A recorder near the bat generally receives the crack early and the glove thud later. Its raw interval tends to be **longer** than T_ball.

A recorder near the glove generally receives the crack later and the glove thud early. Its raw interval tends to be **shorter** than T_ball.

Let:

```text
D = ‖x_glove − x_bat‖
```

Under the straight-path homogeneous-air model, the reverse triangle inequality gives:

```text
|Δrᵢ| ≤ D
```

Therefore:

```text
|Δrᵢ/c| ≤ D/c
```

After clock normalization and in the absence of differential processing delays and measurement errors, the largest geometry-induced interval difference between two devices is approximately:

```text
2D/c
```

This geometry-induced difference can exceed 100 ms for a 60 ft bat-to-glove source separation.

Actual uncorrected device intervals can differ by more than this because of clock-scale differences, processing delays, incorrect event associations, or altered timing.

---

## 5. Numerical Baseball Example

Distinguish:

```text
L_ball = actual ball-path length
D      = ‖x_glove − x_bat‖
```

The flight-time estimate depends on the actual ball path:

```text
T_ball ≈ L_ball/v̄_ball
```

The acoustic propagation bound depends on the straight-line source separation:

```text
|Δrᵢ/c| ≤ D/c
```

For a simplified approximately straight trajectory, assume:

```text
L_ball ≈ D ≈ 60 ft ≈ 18.288 m
v̄_ball ≈ 90 mph ≈ 40.23 m/s
c ≈ 344 m/s
```

The approximate physical ball-flight time is:

```text
T_ball ≈ L_ball/v̄_ball
       ≈ 18.288/40.23
       ≈ 0.4545 s
       ≈ 454.5 ms
```

The maximum single-device geometry correction is:

```text
D/c ≈ 18.288/344
    ≈ 0.0532 s
    ≈ 53.2 ms
```

Under idealized extreme recorder placements, assume:

```text
α ≈ 1
Δℓ ≈ 0
Δε ≈ 0
```

Then:

```text
Recorder near bat:
(Δy − Δℓ)/α ≈ 454.5 ms + 53.2 ms = 507.7 ms

Recorder near glove:
(Δy − Δℓ)/α ≈ 454.5 ms − 53.2 ms = 401.3 ms
```

The idealized clock-normalized, geometry-induced disagreement between those devices is approximately:

```text
507.7 ms − 401.3 ms ≈ 106.4 ms
```

Both recordings can be physically correct.

The common physical interval is recovered only after correcting each recorder for differential propagation, clock scale, and event-dependent latency while accounting for measurement error.

---

## 6. Event Detection Workflow

### Step 1 — Preserve source media

For every file, record:

- original filename,
- cryptographic hash,
- container and codec metadata,
- nominal sample rate,
- channel layout,
- and any transcoding operations.

Never overwrite the source recording.

### Step 2 — Extract audio reproducibly

Convert each source to a documented analysis format, preferably lossless PCM. Preserve the original sample count and nominal sample rate in the audit record.

### Step 3 — Detect the bat event

Use the broadband transient to estimate the bat-crack onset on every device. Candidate methods include:

- matched filtering,
- generalized cross-correlation,
- GCC-PHAT,
- onset-energy change,
- or a validated transient detector.

### Step 4 — Detect the glove event

Detect the glove thud independently. Do not assume that the loudest later impulse is necessarily the correct glove event.

### Step 5 — Align event identities across devices

Build one cross-device group for the bat event and a separate group for the glove event. Use:

- temporal compatibility,
- waveform or spectral similarity,
- event order,
- known field geometry,
- video evidence,
- and propagation-time feasibility.

### Step 6 — Estimate or constrain source positions

Obtain x_bat and x_glove from one or more of:

- known field coordinates,
- calibrated video reconstruction,
- independent acoustic localization,
- surveyed landmarks,
- or a joint timing-and-geometry solver.

### Step 7 — Model propagation

For each event and device, estimate:

```text
pᵢ,e
```

For a baseline homogeneous-air analysis:

```text
pᵢ,e = ‖sᵢ − xₑ‖/c
```

For a higher-fidelity model, pᵢ,e may include:

- wind-advection effects,
- spatially varying sound speed,
- atmospheric refraction,
- terrain or structural diffraction,
- and a modeled direct-path travel time.

### Step 8 — Apply timing correction

For each device:

```text
Δpᵢ = pᵢ,glove − pᵢ,bat
T̂ᵢ = (Δyᵢ − Δℓᵢ)/αᵢ − Δpᵢ
```

Under the homogeneous-air model:

```text
Δrᵢ = ‖sᵢ − x_glove‖ − ‖sᵢ − x_bat‖
T̂ᵢ = (Δyᵢ − Δℓᵢ)/αᵢ − Δrᵢ/c
```

### Step 9 — Estimate the common interval

Combine valid device estimates with uncertainty weighting rather than a simple unweighted average.

---

## 7. Cross-Device Consistency Test

For devices i and j, define the general pairwise residual:

```text
eᵢⱼ = (Δyᵢ − Δℓᵢ)/αᵢ
      − (Δyⱼ − Δℓⱼ)/αⱼ
      − (Δpᵢ − Δpⱼ)
```

Under the homogeneous-air model:

```text
eᵢⱼ = (Δyᵢ − Δℓᵢ)/αᵢ
      − (Δyⱼ − Δℓⱼ)/αⱼ
      − (Δrᵢ − Δrⱼ)/c
```

Equivalently:

```text
eᵢⱼ = Δyᵢ/αᵢ − Δyⱼ/αⱼ
      − (Δrᵢ − Δrⱼ)/c
      − Δℓᵢ/αᵢ + Δℓⱼ/αⱼ
```

A compatible recording set should satisfy:

```text
eᵢⱼ ≈ 0
```

within the declared uncertainty.

The correct claim is therefore:

> Geometry- and propagation-corrected crack-to-thud intervals should agree across independent devices within clock, detection, propagation, latency, and position uncertainty.

The incorrect claim is:

> Raw crack-to-thud intervals are identical or inherently stable across devices.

---

## 8. Estimating the Common Ball-Flight Interval

Let σᵢ be the standard uncertainty of T̂ᵢ. Use inverse-variance weights:

```text
wᵢ = 1/σᵢ²
```

The weighted estimate is:

```text
T̂_ball = (Σᵢ wᵢT̂ᵢ)/(Σᵢ wᵢ)
```

Its idealized standard uncertainty is:

```text
σ_T = √[1/(Σᵢ wᵢ)]
```

This expression assumes independent device estimates.

Shared model errors create correlation, including:

- a common error in x_bat,
- a common error in x_glove,
- a shared sound-speed model,
- a shared event-association mistake,
- or a shared calibration bias.

For correlated estimates, define:

```text
t̂ = [T̂₁, T̂₂, …, T̂ₙ]ᵀ
𝟙  = [1, 1, …, 1]ᵀ
```

Then use the generalized least-squares estimate:

```text
T̂_ball = (𝟙ᵀC⁻¹t̂)/(𝟙ᵀC⁻¹𝟙)
```

with variance:

```text
Var(T̂_ball) = (𝟙ᵀC⁻¹𝟙)⁻¹
```

where C is the covariance matrix of the corrected device estimates.

C must include both device-specific uncertainty and shared covariance caused by common geometry, atmospheric, calibration, or event-association parameters.

If C is singular or poorly conditioned because of strong shared correlations, use a justified generalized inverse, regularization method, or explicit latent-parameter model rather than directly computing C⁻¹.

Use a robust estimator or explicit outlier model when one or more devices may contain bad detections, clipping, severe reverberation, or model violations.

---

## 9. Uncertainty Budget

Starting from:

```text
T̂ᵢ = (Δyᵢ − Δℓᵢ)/αᵢ − Δrᵢ/c
```

a first-order uncertainty approximation is:

```text
σ²_Tᵢ ≈ (σ²_Δyᵢ + σ²_Δℓᵢ)/αᵢ²
       + [(Δyᵢ − Δℓᵢ)²/αᵢ⁴]σ²_αᵢ
       + σ²_Δrᵢ/c²
       + (Δrᵢ²/c⁴)σ²_c
       + covariance terms
```

The terms represent uncertainty from:

- event-time estimation,
- event-dependent processing delay,
- sample-clock scale,
- bat, glove, and recorder positions,
- and sound speed.

This simplified expression assumes independent inputs except for the explicitly noted covariance terms. When source positions, recorder positions, sound speed, clock scale, or event times are jointly estimated, their covariance terms must be retained.

For the general propagation model:

```text
T̂ᵢ = (Δyᵢ − Δℓᵢ)/αᵢ − Δpᵢ
```

the uncertainty can be written as:

```text
σ²_Tᵢ ≈ (σ²_Δyᵢ + σ²_Δℓᵢ)/αᵢ²
       + [(Δyᵢ − Δℓᵢ)²/αᵢ⁴]σ²_αᵢ
       + σ²_Δpᵢ
       + covariance terms
```

Additional uncertainty may come from:

- wind and temperature gradients,
- atmospheric refraction,
- multipath,
- microphone group delay,
- automatic gain control,
- codec priming,
- and rolling resampling.

Evidence of editing, discontinuous resampling, duplicated samples, removed intervals, or altered event timing should be treated as an integrity failure or alternate hypothesis, not merely as additional Gaussian uncertainty.

A result should be marked **non-resolvable** when these uncertainties are too large to distinguish competing hypotheses.

---

## 10. Clock Offset, Clock Scale, and Drift

### 10.1 Constant clock offset

Let zᵢ,e denote the recorded event time excluding the constant device offset. Then:

```text
[βᵢ + zᵢ,glove] − [βᵢ + zᵢ,bat]
= zᵢ,glove − zᵢ,bat
```

A constant clock offset βᵢ cancels in the within-device interval.

Shared absolute recording start times are not required for the interval calculation once the bat and glove events have been correctly associated across devices.

### 10.2 Clock-scale error

Clock-scale error does not cancel. Under the adopted model:

```text
Δyᵢ = αᵢΔt_true + Δℓᵢ + Δεᵢ
```

where:

```text
Δt_true = T_ball + Δpᵢ
```

After correcting additive delay:

```text
(Δyᵢ − Δℓᵢ)/αᵢ ≈ Δt_true
```

For short baseball intervals, ordinary device drift may be small, but it must still be measured or bounded when making high-precision claims.

### 10.3 Clock drift beyond a single scale factor

A single αᵢ assumes locally linear clock behavior. Define the physical arrival time:

```text
uᵢ,e = τₑ + pᵢ,e
```

Choose a reference time u_ref near the analyzed events and define the centered time coordinate:

```text
qᵢ,e = uᵢ,e − u_ref
```

For longer recordings or unstable clocks, use a time-dependent clock model such as:

```text
yᵢ,e = βᵢ + αᵢqᵢ,e + ½γᵢqᵢ,e² + ℓᵢ,e + εᵢ,e
```

where γᵢ represents clock-rate drift. Centering the model near the analyzed events reduces parameter correlation and improves numerical conditioning.

### 10.4 Estimating αᵢ

Possible methods include:

- multiple known event intervals,
- sample-count comparison over long recordings,
- pilot tones,
- calibrated timestamps,
- cross-device drift fitting,
- or joint estimation from repeated shared events.

---

## 11. Role of Narrowband Phase

The bat crack and glove thud are separate impulses generated at different source positions. Their source phases are not generally coherent.

Therefore:

- measure the bat event independently,
- measure the glove event independently,
- do not count narrowband phase continuously from crack to thud,
- and do not interpret the elapsed interval as an unbroken carrier-phase observation.

At 1 kHz:

```text
0.4545 s × 1000 Hz ≈ 454.5 equivalent periods
```

This is a conversion from elapsed time to the number of 1 kHz periods that would fit inside that duration. It is **not** evidence that a coherent 1 kHz phase persisted from the bat crack to the glove thud.

Narrowband phase may refine each event’s arrival estimate only when the phase observable is physically meaningful, calibrated, and source-phase-corrected or reference-eliminated.

---

## 12. Sound Speed and Atmospheric Propagation

Sound speed depends on atmospheric conditions. A simplified dry-air approximation near ordinary temperatures is:

```text
c ≈ 331.3 + 0.606θ  m/s
```

where θ is air temperature in °C.

For high-accuracy analysis, record or estimate:

- temperature,
- humidity,
- pressure,
- wind speed and direction,
- and spatial gradients across the field.

The same c value must not be assumed automatically for recordings made under materially different conditions.

For significant wind or atmospheric gradients, replace the simple range-over-speed model:

```text
pᵢ,e = rᵢ,e/c
```

with a propagation solver or validated effective travel-time model.

---

## 13. Geometry Requirements

The correction requires sufficiently accurate estimates of:

- recorder positions,
- effective bat acoustic source position,
- effective glove acoustic source position,
- and the effective acoustic path.

For recorder i under the homogeneous-air model:

```text
Δrᵢ = ‖sᵢ − x_glove‖ − ‖sᵢ − x_bat‖
```

A position error of several metres can create a timing error of several milliseconds.

Geometry should be reported with:

- coordinate reference,
- measurement method,
- estimated uncertainty,
- source-position interpretation,
- and whether the positions represent mechanical contacts or effective acoustic origins.

A visually estimated location without calibration should not be treated as exact ground truth.

---

## 14. Multi-Device Evidence Matrix

For every device, report at minimum:

| Field | Meaning |
|---|---|
| Device ID | Stable identifier for the recording source |
| Bat arrival time | Detected bat-crack time in device coordinates |
| Glove arrival time | Detected glove-thud time in device coordinates |
| Raw interval Δyᵢ | Glove arrival minus bat arrival |
| Clock scale αᵢ | Estimated or assumed timebase scale |
| Bat propagation pᵢ,bat | Modeled bat-to-device travel time |
| Glove propagation pᵢ,glove | Modeled glove-to-device travel time |
| Differential propagation Δpᵢ | pᵢ,glove − pᵢ,bat |
| Processing correction Δℓᵢ | Event-dependent latency difference |
| Corrected interval T̂ᵢ | Estimated physical ball-flight interval |
| Standard uncertainty σᵢ | Declared uncertainty for T̂ᵢ |
| Residual | Difference from the common fitted interval |
| Status | Accepted, rejected, or non-resolvable |

Under the homogeneous-air model, also report:

| Field | Meaning |
|---|---|
| Bat range rᵢ,bat | Distance from device to bat source |
| Glove range rᵢ,glove | Distance from device to glove source |
| Differential range Δrᵢ | rᵢ,glove − rᵢ,bat |
| Geometry correction Δrᵢ/c | Differential propagation delay |

The audit record should also preserve the exact detector, configuration, software version, source hashes, and propagation model.

---

## 15. Adversarial and Integrity Checks

A strong analysis should test alternate explanations rather than treating consistency as automatic proof of authenticity.

Recommended checks include:

1. **Wrong-event pairing**  
   Pair the bat event with alternative later impulses and compare residuals.

2. **Leave-one-device-out analysis**  
   Refit after removing each device in turn.

3. **Clock-scale sensitivity**  
   Recompute results across plausible αᵢ ranges.

4. **Source-position sensitivity**  
   Perturb x_bat and x_glove within their uncertainty regions.

5. **Propagation-model sensitivity**  
   Recompute across plausible sound-speed, wind, and atmospheric models.

6. **Multipath rejection**  
   Compare direct-onset candidates with later reflections.

7. **Waveform and spectral comparison**  
   Verify that aligned events share compatible transient structure.

8. **Video-audio consistency**  
   Compare acoustic event ordering with independently reconstructed video timing.

9. **Outlier and cluster analysis**  
   Identify devices that form a separate timing or processing population.

10. **Editing and discontinuity analysis**  
    Test for duplicated samples, removed intervals, discontinuous resampling, altered event timing, or other violations of the measurement model.

11. **Search-completeness reporting**  
    State whether event associations and geometry hypotheses were exhaustively tested or heuristically pruned.

Consistency means that a hypothesis survives the declared model and uncertainty tests. It does not, by itself, prove that the media are authentic.

---

## 16. Minimum Validation Tests

A software implementation should include at least the following tests.

### Test 1 — Perpendicular-bisector geometry

Place a device so that:

```text
rᵢ,glove = rᵢ,bat
```

Expected result:

```text
Δrᵢ/c = 0
T̂ᵢ = (Δyᵢ − Δℓᵢ)/αᵢ
```

### Test 2 — Near-bat and near-glove devices

Verify approximately:

```text
Δy_near-bat/α   ≈ T_ball + D/c
Δy_near-glove/α ≈ T_ball − D/c
```

when Δℓ ≈ 0.

### Test 3 — Constant clock offset

Add an arbitrary βᵢ to both event times. The measured interval must remain unchanged.

### Test 4 — Clock-scale error

Apply a known αᵢ and verify that correction recovers the original interval.

### Test 5 — Noiseless recovery

With exact propagation, exact clock scale, exact latency correction, and exact detections, all corrected device estimates must recover T_ball to numerical precision.

### Test 6 — Geometry uncertainty

Increase source-position uncertainty and verify that the reported timing uncertainty increases.

### Test 7 — Wrong glove event

Pair the bat crack with an incorrect later event. Cross-device residuals should increase substantially.

### Test 8 — Outlier device

Corrupt one device’s event time. A robust estimator should isolate the outlier without materially shifting the consensus.

### Test 9 — Correlated model error

Shift the assumed glove position for all devices. The implementation should show a shared bias rather than falsely treating all device errors as independent.

### Test 10 — Non-resolvable case

Create a case where timing, propagation, and geometry uncertainty exceed the separation between competing hypotheses. The system must return non-resolvable rather than a high-confidence answer.

### Test 11 — Curved ball path

Set:

```text
L_ball > D
```

and verify that the flight-time model uses L_ball while the propagation bound continues to use D.

### Test 12 — Effective source offset

Offset the effective acoustic source from the visual contact point and verify that the resulting timing bias is captured by the source-position uncertainty or corrected geometry.

### Test 13 — Nonuniform propagation

Simulate wind or a spatial sound-speed gradient and verify that a general pᵢ,e model outperforms the simple rᵢ,e/c approximation.

### Test 14 — Timing edit integrity failure

Insert or remove samples between the two events and verify that the system flags the recording as violating the clock or continuity model rather than treating the change as ordinary random uncertainty.

---

## 17. Correct Interpretation of Results

A valid result supports the following statement:

> Each device records the same physical ball-flight interval plus a device-specific differential acoustic propagation delay. After correcting for propagation, clock scale, event-dependent latency, and measurement uncertainty, the recovered physical interval should agree across independent recordings.

A valid result does **not** automatically establish that:

- raw intervals must match,
- phase remains coherent between the bat and glove events,
- every residual inconsistency proves editing,
- one fitted geometry proves authenticity,
- or a successful numerical optimization proves physical correctness.

---

## 18. Mental Model Summary

- The bat crack and glove thud are separate acoustic events.
- Their effective acoustic source positions may differ from the visible mechanical contact points.
- Every recorder observes a different pair of propagation times.
- Constant device start-time offsets cancel within a recording.
- Clock scale, event detection, processing latency, and propagation errors do not automatically cancel.
- The geometry-induced cross-device difference can exceed 100 ms across a 60 ft source separation.
- Arbitrary raw recording differences are not universally bounded by 2D/c.
- The actual ball-path length controls flight time; straight-line source separation controls the differential-propagation bound.
- Propagation-corrected intervals, not raw intervals, are the shared physical quantity.
- Equivalent periods are a time conversion, not continuous phase tracking.
- Phase may refine a calibrated single-event measurement; it does not replace the two-event timing model.
- A trustworthy system reports uncertainty, covariance, alternate hypotheses, integrity failures, outliers, and non-resolvable cases.

---

## 19. Final Corrected Claim

> The bat-to-glove example is a two-event timing, propagation, and geometry problem. Each recorder measures the physical ball-flight interval plus a recorder-specific differential sound-propagation delay. Raw intervals are not expected to be identical. After correcting for effective source and recorder geometry, propagation, clock scale, and event-dependent processing delay—and accounting for uncertainty and covariance—the recovered physical interval should be mutually consistent across separately acquired recordings.

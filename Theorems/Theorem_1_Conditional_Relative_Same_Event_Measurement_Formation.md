# Theorem 1 — Conditional Relative Same-Event Measurement Formation

```text
Document ID: AWC-THM-1-0.5
Version: Theorem Draft 0.5
Status: Conditional mathematical result
Applies to: AIRS Draft 0.1
Normative status: Informative and non-normative
Validation status: Not independently validated
Supersedes: Image-only aWc Theorem 1 — Measurement Formation Theorem
```

## 1. Purpose

This theorem states the conditions under which two acoustic observers may produce a bounded-error, relative, same-event wrapped-phase observation suitable for use within an AIRS-compatible hypothesis analysis.

The theorem does **not** convert raw microphone phase into absolute source range. It produces an optional pairwise observation of propagation-time difference modulo one period, subject to explicit timing, calibration, coherence, path-selection, and phase-error assumptions.

The primary AIRS timing observation remains:

```text
yᵢ,e = βᵢ + αᵢ(τₑ + pᵢ,e) + ℓᵢ,e + εᵢ,e
```

The phase observable developed here is a conditional refinement of that timing model, not a replacement for it.

---

## 2. Notation

For observers `i` and `j`, event `e`, and declared analysis frequency `f > 0`:

- `τₑ` is the physical or working event time;
- `pᵢ,e` and `pⱼ,e` are the modeled propagation times to observers `i` and `j`;
- `Δpᵢⱼ,e = pᵢ,e − pⱼ,e`;
- `Xᵢ,e(f)` and `Xⱼ,e(f)` are Fourier coefficients from declared same-event analysis windows after documented preprocessing and transformation onto a common physical or declared working-frequency coordinate. When spectra remain in device-recorded frequency coordinates, the applicable clock-scale transformation must be applied before coefficients are compared at a common `f`;
- `κᵢⱼ,e` is the true pairwise non-propagation timing offset entering the extracted spectral phase before the explicit residual correction in Section 4. It may include remaining clock-alignment and event-window offset after earlier preprocessing and is expressed in units of the physical or declared working-time coordinate used by `Δpᵢⱼ,e`. Corrections originating in recorded-time units must be transformed through the applicable clock model before use here;
- `ψᵢⱼ(f)` is differential system phase not represented in the propagation model;
- `ηᵢⱼ,e(f) ∈ (−π, π]` is aggregate phase-estimation noise and declared residual model error on the principal circular branch;
- `κ̂ᵢⱼ,e` and `ψ̂ᵢⱼ(f)` are the applied timing and system-phase corrections;
- `wrap(θ) ∈ (−π, π]`;
- `dₛ¹(a,b) = |wrap(a − b)|` is circular distance on the unit circle;
- `nᵢⱼ,e(f) ∈ ℤ` is an integer-cycle hypothesis at frequency `f`;
- and `λ = c/f` only when one declared constant sound speed `c` is appropriate.

`f` is expressed in cycles per unit of the same physical or declared working-time coordinate used for `Δpᵢⱼ,e` and `κᵢⱼ,e`. When the distance-equivalent form is used, `c` is expressed in distance per that same time unit.

The Fourier convention is:

```text
X(f) = ∫x(t)e⁻ʲ²πft dt
```

The pairwise cross-spectrum convention is:

```text
φᵢⱼ,e(f) = arg{Xⱼ,e(f)X*ᵢ,e(f)}
```

With this convention, a positive propagation-time difference `pᵢ,e − pⱼ,e` contributes a positive phase term.

---

## 3. Assumptions

The theorem applies only when all applicable assumptions below are satisfied or bounded explicitly.

### A1 — Common physical event

Observers `i` and `j` contain the same physical event `e`. Event identity is established independently of the phase result.

### A2 — Consistent propagation component

The selected analysis windows represent compatible propagation components. A direct arrival on one observer must not be paired silently with a reflection, diffraction, public-address path, or different source component on the other.

### A3 — Declared frequency and bandwidth

The analysis frequency `f`, bandwidth, window, taper, filtering, and preprocessing are declared. The usable signal component is nonzero and sufficiently stable within the selected band.

### A4 — Common source phase is eliminated

Source phase is canceled by the same-event cross-spectrum, calibrated, pilot-referenced, or otherwise eliminated by a physically justified model.

Separate independently generated events do not satisfy this assumption merely because they have similar spectra.

### A5 — Adequate coherence

Cross-observer coherence and signal quality are adequate for the declared phase-estimation method. A threshold or other admissibility rule is predeclared.

### A6 — Clock and event-window correction

Clock offset, scale, drift, discontinuities, and event-window alignment are modeled or corrected sufficiently that the remaining pairwise timing contribution over the analysis window can be represented by one scalar `κᵢⱼ,e`. The value `κ̂ᵢⱼ,e` is the estimate explicitly removed in the corrected phase observable.

Residual within-window time warping or clock-scale variation must be negligible, bounded within `ηᵢⱼ,e(f)`, or represented by a richer model; it must not be treated automatically as a constant phase offset.

### A7 — Differential system phase correction

Differential phase from microphones, filters, codecs, devices, loudspeakers, public-address chains, and other processing is calibrated, bounded, or retained as an explicit model term `ψᵢⱼ(f)`.

### A8 — Bounded residual phase error

After applying the declared corrections:

```text
|κᵢⱼ,e − κ̂ᵢⱼ,e| ≤ ε_κ
```

```text
dₛ¹(ψᵢⱼ(f), ψ̂ᵢⱼ(f)) ≤ ε_ψ
```

```text
|ηᵢⱼ,e(f)| ≤ ε_η
```

for justified nonnegative bounds `ε_κ`, `ε_ψ`, and `ε_η`.

### D1 — Downstream dependency condition

For downstream AIRS inference, shared clocks, shared acquisition chains, derivative recordings, common calibration, common propagation parameters, and other dependencies are represented explicitly. Nominal observer count is not treated as independent information by default.

This dependency condition is not required for the algebraic circular-error identity below, but it is required when combining Theorem 1 outputs with other evidence.

---

## 4. Conditional Spectral Measurement Model

Under the assumptions above, define `ηᵢⱼ,e(f)` to include all remaining phase-estimation error and declared model residual. The pairwise same-event phase is then represented modulo `2π` as:

```text
φᵢⱼ,e(f)
=
wrap{
    2πf[Δpᵢⱼ,e + κᵢⱼ,e]
    + ψᵢⱼ(f)
    + ηᵢⱼ,e(f)
  }
```

Define the corrected relative-phase observable:

```text
φ̃ᵢⱼ,e(f)
= wrap{
    φᵢⱼ,e(f)
    − 2πfκ̂ᵢⱼ,e
    − ψ̂ᵢⱼ(f)
  }
```

Define the total phase-error bound:

```text
ε_φ = 2πfε_κ + ε_ψ + ε_η
```

---

## 5. Theorem Statement

### Theorem 1 — Bounded Relative Same-Event Phase Formation

Under Assumptions A1–A8, the corrected phase observable satisfies the circular bound:

```text
dₛ¹(
  φ̃ᵢⱼ,e(f),
  2πfΔpᵢⱼ,e
)
≤ ε_φ
```

When:

```text
ε_φ < π
```

there exists an integer-cycle hypothesis `nᵢⱼ,e(f) ∈ ℤ` and a timing error `eᵢⱼ,e(f)` such that:

```text
Δpᵢⱼ,e
=
[nᵢⱼ,e(f) + φ̃ᵢⱼ,e(f)/(2π)]/f
+ eᵢⱼ,e(f)
```

with:

```text
|eᵢⱼ,e(f)| ≤ ε_φ/(2πf)
```

Therefore, the measurement front end produces a **bounded-error family of pairwise propagation-time-difference hypotheses**, indexed by `nᵢⱼ,e(f)`.

For a multi-frequency analysis, integer-cycle hypotheses across frequencies must satisfy a declared joint consistency model; they may not be selected independently frequency by frequency.

When a single declared constant sound speed `c` is justified, the signed path-length-difference equivalent is:

```text
cΔpᵢⱼ,e
=
λ[nᵢⱼ,e(f) + φ̃ᵢⱼ,e(f)/(2π)]
+ eᵈᵢⱼ,e(f)
```

where:

```text
λ = c/f
```

and:

```text
|eᵈᵢⱼ,e(f)| ≤ λ ε_φ/(2π)
```

This quantity is a signed path-length-difference equivalent, not an absolute source range. The form is not valid when propagation requires a path-specific travel-time model rather than one constant `c`.

---

## 6. Proof

From the exact modulo-`2π` pairwise model:

```text
φᵢⱼ,e(f)
=
wrap{
    2πf[Δpᵢⱼ,e + κᵢⱼ,e]
    + ψᵢⱼ(f)
    + ηᵢⱼ,e(f)
  }
```

and the definition of the corrected phase:

```text
φ̃ᵢⱼ,e(f)
=
wrap{
    φᵢⱼ,e(f)
    − 2πfκ̂ᵢⱼ,e
    − ψ̂ᵢⱼ(f)
  }
```

translation invariance of circular distance gives:

```text
dₛ¹(
  φ̃ᵢⱼ,e(f),
  2πfΔpᵢⱼ,e
)
=
dₛ¹(
  2πf(κᵢⱼ,e − κ̂ᵢⱼ,e)
  + ψᵢⱼ(f)
  − ψ̂ᵢⱼ(f)
  + ηᵢⱼ,e(f),
  0
)
```

Applying the circular triangle inequality:

```text
dₛ¹(
  φ̃ᵢⱼ,e(f),
  2πfΔpᵢⱼ,e
)
≤
2πf|κᵢⱼ,e − κ̂ᵢⱼ,e|
+ dₛ¹(ψᵢⱼ(f), ψ̂ᵢⱼ(f))
+ |ηᵢⱼ,e(f)|
```

Using Assumption A8:

```text
dₛ¹(
  φ̃ᵢⱼ,e(f),
  2πfΔpᵢⱼ,e
)
≤
2πfε_κ + ε_ψ + ε_η
=
ε_φ
```

which establishes the circular phase bound.

Now define the principal circular residual:

```text
ρᵢⱼ,e(f)
=
wrap{
  φ̃ᵢⱼ,e(f) − 2πfΔpᵢⱼ,e
}
```

Then:

```text
|ρᵢⱼ,e(f)| ≤ ε_φ
```

and, by the definition of wrapping, there exists an integer `mᵢⱼ,e(f) ∈ ℤ` such that:

```text
φ̃ᵢⱼ,e(f) − 2πfΔpᵢⱼ,e
=
ρᵢⱼ,e(f) + 2πmᵢⱼ,e(f)
```

Let:

```text
nᵢⱼ,e(f) = −mᵢⱼ,e(f)
```

Rearranging gives:

```text
Δpᵢⱼ,e
=
[nᵢⱼ,e(f) + φ̃ᵢⱼ,e(f)/(2π)]/f
− ρᵢⱼ,e(f)/(2πf)
```

Set:

```text
eᵢⱼ,e(f) = −ρᵢⱼ,e(f)/(2πf)
```

so that:

```text
|eᵢⱼ,e(f)| ≤ ε_φ/(2πf)
```

The condition `ε_φ < π` ensures that the declared residual bound does not cover the entire phase circle and therefore yields a nontrivial bounded branch around each integer-cycle hypothesis.

The constant-`c` signed path-length-difference equivalent follows by multiplication by `c`. ∎

---

## 7. Output of Theorem 1

For each admissible observer pair, event, frequency, and selected path branch, the output is:

```text
{
  observer_pair,
  event_id,
  frequency,
  bandwidth,
  phase_convention,
  corrected_wrapped_phase,
  phase_error_bound_or_distribution,
  timing_correction,
  system_phase_correction,
  coherence_measure,
  path_hypothesis,
  frequency_indexed_integer_cycle_hypotheses,
  dependency_metadata
}
```

The primary mathematical output is:

```text
Δpᵢⱼ,e
∈
⋃ n∈ℤ
[
  (n + φ̃ᵢⱼ,e(f)/(2π))/f − ε_φ/(2πf),
  (n + φ̃ᵢⱼ,e(f)/(2π))/f + ε_φ/(2πf)
]
```

subject to the declared model and bounds.

When `ε_φ ≥ π`, adjacent integer-cycle intervals touch or overlap, and their union covers the complete real propagation-time-difference axis. The bounded phase result then supplies no timing exclusion by itself. Information may still remain in a nonuniform wrapped distribution or through independent timing, geometry, propagation, or calibration constraints.

Theorem 1 does not by itself make this set finite. Finite ambiguity requires additional independent timing, geometric, propagation, and search bounds.

---

## 8. Observability and Gauge Conditions

This theorem forms a pairwise relative observable. It does not fix:

- the additive event-time gauge;
- the working time-scale gauge;
- the spatial translation, rotation, or reflection gauge;
- source position;
- observer position;
- absolute propagation time;
- or absolute range.

A later reconstruction must apply the AIRS clock, propagation, geometry, observability, and search-completeness requirements.

Gauge-equivalent parameterizations are not distinct physical solutions.

---

## 9. Conditions Requiring Set-Valued Phase Treatment

Define the residual correction error on the circle as:

```text
r_corr,ᵢⱼ,e(f)
=
wrap{
  2πf(κᵢⱼ,e − κ̂ᵢⱼ,e)
  + ψᵢⱼ(f)
  − ψ̂ᵢⱼ(f)
}
```

A single deterministic corrected phase must not be reported when the circular uncertainty support of `r_corr,ᵢⱼ,e(f)` approaches or covers the full phase circle, when the corresponding unwrapped correction-error hypotheses span one or more full cycles, or when correction and phase-estimation uncertainty combine so that:

```text
ε_φ ≥ π
```

In that case, retain one or more of:

- a wrapped probability distribution;
- a circular interval set;
- multiple calibration branches;
- multiple event-window branches;
- multiple path branches;
- or multiple integer-cycle hypotheses.

The theorem then applies to each retained admissible branch or to the declared set-valued representation, not to one arbitrarily selected phase value.

---

## 10. Failure Conditions

The theorem is not applicable, or its output must be rejected or broadened, when any material condition below is unresolved:

- wrong event association;
- separate events treated as one coherent carrier;
- incompatible direct, reflected, diffracted, or public-address paths;
- inadequate coherence;
- clipping or nonlinear processing that invalidates the phase model;
- unbounded clock or event-window error;
- unbounded differential hardware or processing phase;
- event-dependent latency treated as a constant clock offset;
- shared acquisition dependencies treated as independent evidence;
- derivative recordings counted as independent observers;
- analysis-frequency instability;
- unmodeled source motion within the window;
- nonstationary or distributed source behavior incompatible with the model;
- or correction uncertainty covering the phase circle.

Failure of these conditions is a model or evidence issue. It must not be hidden by inflating an ordinary independent Gaussian error term without justification.

---

## 11. Claims Not Established

Theorem 1 does **not** establish:

- absolute source-to-observer range;
- source location;
- unique geometry;
- the correct integer-cycle assignment;
- correct event association;
- direct-path selection;
- authenticity;
- absence of editing;
- statistical independence of observers;
- exhaustive hypothesis search;
- finite ambiguity;
- globally consistent reconstruction;
- robust recovery;
- forensic validity;
- or certified performance.

A small phase residual does not establish that the selected physical model is correct.

---

## 12. Relationship to AIRS Draft 0.1

This theorem is an informative mathematical specialization of the AIRS same-event relative-phase model.

It depends particularly on the AIRS provisions concerning:

- observer clock and measurement modeling;
- centered clock drift and observability;
- event association;
- propagation-path declaration;
- pairwise timing;
- phase prerequisites;
- cross-spectrum sign convention;
- corrected relative phase;
- integer-cycle ambiguity;
- covariance and dependency;
- search completeness;
- prohibited output styles;
- and validation.

If this theorem conflicts with AIRS Draft 0.1, AIRS Draft 0.1 controls.

---

## 13. Validation Requirements

Before implementation claims are made, the theorem should be exercised with synthetic and measured cases covering at least:

1. ideal coherent same-event observations;
2. known integer-cycle alternatives;
3. timing-correction error below and above the declared bound;
4. hardware-phase error below and above the declared bound;
5. phase uncertainty near `π`;
6. direct-path versus reflection mismatch;
7. wrong event association;
8. low coherence;
9. shared-clock multichannel acquisition;
10. derivative recording lineage;
11. event-dependent latency;
12. nonconstant propagation speed;
13. multiple frequencies and bandwidths;
14. sign-convention verification;
15. and held-out reconstruction tests.

Validation results must distinguish:

- independent mathematical review of the theorem statement, assumptions, and proof;
- software implementation correctness;
- numerical performance;
- and empirical applicability to a declared use case.

---

## 14. Revision History

| Version | Date | Change |
|---|---|---|
| 0.5 | 2026-07-11 | Corrected the interpretation of `κᵢⱼ,e` as the true non-propagation timing term estimated by `κ̂ᵢⱼ,e`; required comparison on a common physical or working-frequency coordinate; added within-window clock-scale and time-warping limits; and rewrote the key circular-distance equality in a directly auditable zero-referenced form. |
| 0.4 | 2026-07-11 | Removed the remaining working-time-unit ambiguity; distinguished circular uncertainty support from unwrapped multi-cycle correction hypotheses; and replaced experimental wording about theorem correctness with independent mathematical review. |
| 0.3 | 2026-07-11 | Added explicit dimensional-consistency requirements for frequency, timing, and sound speed; defined circular residual correction error for set-valued phase treatment; and stated the loss of timing exclusion when `ε_φ ≥ π`. |
| 0.2 | 2026-07-11 | Replaced approximate phase notation with an exact modulo-`2π` bounded-error model; defined timing units and circular distance; made the proof circularly rigorous; clarified set-valued correction uncertainty, signed path-length difference, explicit interval output, multi-frequency integer consistency, and downstream dependency handling. |
| 0.1 | 2026-07-11 | Replaced the image-only absolute wrapped-range formulation with a conditional AIRS-compatible relative same-event phase theorem. Added explicit clock, calibration, coherence, path, dependency, uncertainty, integer-cycle, limitation, and validation requirements. |

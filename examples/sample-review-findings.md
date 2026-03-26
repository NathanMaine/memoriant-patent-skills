# Sample Patent Review Findings

**Application reviewed:** "Adaptive Resonant Wireless Power Transfer System with Tissue-Impedance Compensation for Implantable Medical Devices" (fictional provisional)
**Review date:** 2026-03-25
**Claims reviewed:** 3
**Sections reviewed:** Abstract, Background, Summary, Detailed Description

---

## Executive Summary

| Issue type | Count | Highest severity |
|------------|-------|-----------------|
| 35 USC 101 (Subject matter) | 0 | — |
| 35 USC 102 (Novelty) | 1 | Medium |
| 35 USC 103 (Obviousness) | 2 | High |
| 35 USC 112(a) (Enablement) | 1 | Low |
| 35 USC 112(b) (Definiteness) | 2 | Medium |
| MPEP 608 (Formalities) | 2 | Low |

**Overall filing readiness:** Conditional — address the two High/Medium 103 rejections and the 112(b) definiteness issues before filing non-provisional.

---

## 35 USC 101 — Subject Matter Eligibility

**Finding:** No rejection anticipated.

The claims are directed to a physical method of operating electromagnetic hardware (coil, amplifier, measurement bridge) and a resulting physical system. There is no abstract idea, mathematical concept standing alone, or mental process at issue. Alice/Mayo step 2B is not implicated. The claims recite meaningful limitations including specific hardware components and physical measurements.

**Severity:** None

---

## 35 USC 102 — Novelty

### Finding 102-1

**Severity:** Medium

**Claim(s) affected:** Claim 1

**Issue:** US10,998,762 (Johansson et al., CardioSync Technologies) discloses a system that "dynamically adjusts the resonant frequency in response to tissue impedance changes" for cardiac implants, which may anticipate the method steps of Claim 1 if the examiner reads "minimizes reflected impedance magnitude" as equivalent to Johansson's impedance-response adjustment.

**Suggestion:** Amend Claim 1 to more specifically recite the swept-frequency measurement approach and the explicit identification of an impedance minimum, distinguishing from systems that adjust frequency based on a feedback signal without performing a full sweep. Add language such as "wherein identifying comprises computing a minimum of |Z_ref(f)| across at least 100 discrete frequency steps within the swept range." Also add the periodic re-sweep limitation as a claim element rather than leaving it in the description only.

---

## 35 USC 103 — Obviousness

### Finding 103-1

**Severity:** High

**Claim(s) affected:** Claims 1 and 3

**Issue:** An examiner is likely to combine US10,998,762 (adaptive frequency adjustment for cardiac WPT) with US10,673,281 (Vasquez et al., miniaturized coil at 13.56 MHz) to argue that the 80–500 kHz frequency range of Claim 3 is an obvious design choice. Both references operate in the kHz–MHz range and are directed to IMD charging. The combination would suggest to a person of ordinary skill that selecting an operating frequency within this range is routine optimization.

**Suggestion:** Add a specific technical rationale in the specification for why the 80–500 kHz range is non-obvious — e.g., data showing that this range uniquely balances tissue absorption, regulatory SAR limits, and coil miniaturization constraints in a way not taught or suggested by the prior art. Consider adding experimental efficiency data to the specification as factual support for unexpected results.

### Finding 103-2

**Severity:** High

**Claim(s) affected:** Claim 2

**Issue:** The thermal safety interlock of Claim 2 (curtailing power when temperature exceeds a threshold) is likely to be found obvious in view of US10,862,337 (Lindqvist et al., thermal management for WPT receivers) combined with the general knowledge that thermal safety is required under ISO 14708-1. Thermal monitoring and power curtailment in response to temperature exceedance is a well-known safety pattern in implantable device charging.

**Suggestion:** Consider whether the thermal interlock can be claimed with greater specificity that would distinguish from Lindqvist — for example, the use of predictive temperature modeling (not just reactive threshold detection), or integration of the thermal signal with the resonance-tracking algorithm to proactively reduce power before the threshold is reached. If the innovation is purely in the thermal response mechanism, that mechanism needs more specific claim language.

---

## 35 USC 112(a) — Enablement

### Finding 112(a)-1

**Severity:** Low

**Affected section:** Detailed Description — Claim 1 step "identifying an optimal operating frequency"

**Issue:** The specification describes the resonance-tracking algorithm at a high level but does not provide sufficient detail for the microcontroller firmware implementation. An examiner may question whether a person of ordinary skill could implement the impedance-minimization algorithm without undue experimentation, particularly the handling of multi-modal impedance curves (where |Z_ref(f)| has multiple local minima).

**Suggestion:** Add a paragraph to the Detailed Description describing how the algorithm handles multi-modal impedance responses — for example, by selecting the global minimum, or by initializing from the previously known optimal frequency to prefer local continuity. Pseudocode or a flow diagram (even informal) would strengthen enablement.

---

## 35 USC 112(b) — Definiteness

### Finding 112(b)-1

**Severity:** Medium

**Claim(s) affected:** Claim 2

**Issue:** "a predetermined safety threshold" in Claim 2 is a relative term that may be found indefinite. The specification mentions 40.5°C but Claim 2 does not recite a specific value or a standard by which the threshold is determined, making the claim boundary unclear.

**Suggestion:** Either (a) recite the specific threshold value in the claim ("a surface temperature exceeding 40.5 degrees Celsius"), or (b) anchor the threshold to a defined standard ("a surface temperature exceeding the maximum allowable implant surface temperature as defined by ISO 14708-1"). Option (a) is simpler; option (b) provides flexibility if the standard value changes.

### Finding 112(b)-2

**Severity:** Medium

**Claim(s) affected:** Claim 1

**Issue:** "periodic intervals" in Claim 1 is indefinite as claimed. Without a bound, this term could encompass intervals of hours or milliseconds, making the claim scope unclear.

**Suggestion:** Claim 3 already recites "between 20 seconds and 60 seconds" — either incorporate this limitation into Claim 1 or add language such as "periodic intervals of less than 120 seconds" to provide a definite boundary.

---

## MPEP 608 — Formalities

### Finding 608-1

**Severity:** Low

**Issue:** The abstract exceeds the USPTO recommended length of 150 words. The sample abstract is approximately 155 words. For a non-provisional filing, the abstract should be revised to 150 words or fewer per 37 CFR 1.72(b).

**Suggestion:** Remove one sentence from the abstract. The sentence describing the thermal monitor can be condensed: "A thermal safety interlock curtails power if receiver surface temperature approaches 40.5°C."

### Finding 608-2

**Severity:** Low

**Issue:** The specification references figures (FIG. 1, FIG. 2) in the filing checklist but no drawings are included in this draft. For the non-provisional, formal drawings must be submitted that conform to 37 CFR 1.84 (black ink, specific margins, reference numerals consistent with the description).

**Suggestion:** Use `/patent-diagrams` to generate reference-numbered patent drawings before filing the non-provisional. Ensure each element recited in the claims (primary coil, secondary coil, microcontroller, impedance measurement bridge) appears in at least one figure with a consistent reference numeral.

---

## Recommended Actions (Priority Order)

1. **[High]** Strengthen Claim 1 with specific swept-frequency language to distinguish US10,998,762.
2. **[High]** Add technical rationale and experimental data to the specification addressing 103-1 and 103-2.
3. **[Medium]** Fix Claim 2 threshold definiteness (112(b)-1) — specify 40.5°C or ISO 14708-1.
4. **[Medium]** Fix Claim 1 "periodic intervals" indefiniteness (112(b)-2).
5. **[Low]** Trim abstract to 150 words.
6. **[Low]** Generate and attach patent diagrams before non-provisional filing.

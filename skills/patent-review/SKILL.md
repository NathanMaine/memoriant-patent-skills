---
name: patent-review
description: "v1.0.0 — AI-assisted review of patent applications against all major USPTO rejection types including 101, 102, 103, 112(a), 112(b), and MPEP 608 formalities."
---

# Patent Review Skill

> DISCLAIMER: This skill assists with application review and does not constitute legal advice. All findings should be reviewed by a registered patent attorney or agent before responding to Office Actions or making filing decisions.

## Rejection Types Reference Table

| Rejection | Statute | What It Checks | Common Issues |
|-----------|---------|---------------|---------------|
| § 101 | 35 U.S.C. § 101 | Patent-eligible subject matter | Abstract ideas (Alice), laws of nature (Mayo), natural phenomena |
| § 102 | 35 U.S.C. § 102 | Novelty — each claim element anticipated | Single prior art reference discloses every element of a claim |
| § 103 | 35 U.S.C. § 103 | Non-obviousness — combination of references | PHOSITA would combine references to arrive at claimed invention |
| § 112(a) | 35 U.S.C. § 112(a) | Written description + enablement | Claim scope exceeds what is described; undue experimentation to enable |
| § 112(b) | 35 U.S.C. § 112(b) | Definiteness of claims | Antecedent basis failures; terms of degree without standard; unclear scope |
| MPEP 608 | 37 C.F.R. § 1.71–1.84 | Formalities | Drawing requirements, abstract length, claim format, ADS completeness |

---

## Review Workflow

### Step 1 — Read Claims First
Before reviewing the specification, read all claims carefully:
- Identify each independent claim and its dependent claim tree
- List every structural element and functional limitation in each independent claim
- Note any means-plus-function (MPF) language under § 112(f)
- Flag any unusual terminology or claim scope questions

### Step 2 — § 101 Patent-Eligibility Review
Apply the Alice/Mayo two-step framework (USPTO Step 2A / Step 2B):

**Step 2A, Prong 1 — Is the claim directed to a judicial exception?**
- Abstract ideas: mathematical concepts, mental processes, certain methods of organizing human activity
- Laws of nature: natural phenomena, natural products
- If NO judicial exception → claim is patent-eligible (done)

**Step 2A, Prong 2 — Does the claim integrate the exception into a practical application?**
- Does the claim improve the functioning of a computer or technical field?
- Does it apply the exception with particular machines or transformations?
- Is it applied to a specific technological environment?
- If YES → claim is patent-eligible (done)

**Step 2B — Does the claim add significantly more?**
- Are there additional elements beyond the exception?
- Do they amount to significantly more than the exception itself?
- "Well-understood, routine, conventional" elements do NOT add significantly more

**Check for:**
- Software claims that merely apply abstract math to generic hardware
- Claims that recite "using a computer" without improving the computer itself
- Claims where the inventive concept is only in the abstract idea portion

**MPEP reference:** MPEP § 2106

### Step 3 — § 102 Novelty Review
For each independent claim:
1. Parse every claim element (structural + functional)
2. For each prior art reference, map its disclosures to claim elements
3. A rejection requires ONE reference to disclose EVERY element of the claim
4. Check both express and inherent disclosures

**Check for:**
- Claims that exactly match a prior art disclosure
- Prior art that inherently performs a claimed function (even if not explicitly stated)
- Prior art published before the effective filing date

**Prior art categories under § 102(a)(1):** patents, printed publications, public use, on sale, otherwise available to the public before effective filing date

**MPEP reference:** MPEP § 2131–2138

### Step 4 — § 103 Obviousness Review
For each independent claim:
1. Identify the primary reference (closest prior art)
2. Identify secondary references that teach missing elements
3. Assess whether a PHOSITA would be motivated to combine them
4. Consider secondary considerations (commercial success, long-felt need, failure of others, unexpected results)

**KSR factors for combination (KSR Int'l v. Teleflex, 550 U.S. 398 (2007)):**
- Combining known elements per known methods yields predictable results
- Simple substitution of one known element for another
- Use of known technique to improve similar devices
- Applying known technique to a known problem

**Check for:**
- Claims that combine features from two or more references
- Claims that use known techniques in a new context
- Claims where the combination yields predictable results

**MPEP reference:** MPEP § 2141–2145

### Step 5 — § 112(a) Written Description and Enablement Review
**Written description check:**
- Does the specification describe each claimed feature in sufficient detail?
- Are all claim elements supported by the original disclosure?
- For each independent claim element, find where it is described in the specification

**Enablement check:**
- Can a PHOSITA make and use the invention based on the disclosure alone?
- Is undue experimentation required? (Wands factors)
- Are working examples provided, or is the disclosure purely theoretical?

**Wands factors for undue experimentation:**
1. Quantity of experimentation needed
2. Amount of direction/guidance presented
3. Presence of working examples
4. Nature of the invention
5. State of the prior art
6. Skill level of those in the art
7. Predictability of the art
8. Breadth of the claims

**MPEP reference:** MPEP § 2161–2165

### Step 6 — § 112(b) Definiteness Review
**Antecedent basis check (most common issue):**
- Every element introduced with "a" or "an" must later be referred to as "the" or "said"
- Every "the [element]" or "said [element]" must have a prior antecedent in the same claim or a parent claim
- Check each dependent claim references correct parent claim elements

**Terms requiring definite standard:**
- "About," "substantially," "approximately" — must have a standard in the art or specification
- "High," "low," "fast," "slow" — relative terms need context
- "Configured to" — acceptable; "adapted to" — generally acceptable

**Means-plus-function (MPF) under § 112(f):**
- Claims using "means for [function]" are interpreted as MPF claims
- Specification must disclose corresponding structure for each MPF element
- Review each "means for" element and find its structural counterpart

**MPEP reference:** MPEP § 2171–2174

### Step 7 — MPEP 608 Formalities Review
**Abstract (MPEP § 608.01(b)):**
- [ ] ≤150 words
- [ ] On a separate page
- [ ] Does not begin with "This invention..."
- [ ] Representative figure designated

**Claims (MPEP § 608.01(n)):**
- [ ] Numbered consecutively starting from 1
- [ ] Each claim is a single sentence
- [ ] Dependent claims properly reference parent claims
- [ ] No claim depends from itself or from a later-numbered claim

**Specification (MPEP § 608.01):**
- [ ] Sections present: background, summary, brief description of drawings, detailed description
- [ ] Best mode described (for non-provisionals)
- [ ] All drawings referenced in specification
- [ ] All reference numerals in drawings defined in specification

**Drawings (37 C.F.R. § 1.84 for non-provisional):**
- [ ] Black ink on white paper
- [ ] Margins: top/left/right ≥ 2.5cm, bottom ≥ 1.0cm
- [ ] Sheet size: 21.0 × 29.7cm (A4) or 21.6 × 27.9cm (letter)
- [ ] Reference numerals consistent between drawings and specification
- [ ] Figure numbers in order

---

## Suggested Fixes for Common Issues

### § 101 — Abstract Idea Rejection
**Fix:** Add claim language that ties the abstract idea to specific technical improvements.
- Instead of: "processing data to generate a result"
- Try: "processing meeting audio data using a transformer-based NLP model to generate structured action items, thereby reducing manual note-taking burden by [X]%"
- Add: specific machine, transformation, or technical effect language

### § 102 — Anticipation
**Fix:** Amend claims to add limitations NOT found in the reference.
- Identify the element(s) the reference does NOT disclose
- Add those elements as additional claim limitations
- Consider adding dependent claims to create fallback positions

### § 103 — Obviousness
**Fix:** Argue motivation to combine is absent, or amend to add non-obvious features.
- Attack the combination: was there teaching away? different purposes?
- Introduce secondary considerations evidence: commercial success, long-felt need
- Amend to add synergistic or unexpected results not suggested by the combination

### § 112(a) — Written Description
**Fix:** Amend the specification (before filing) or claims (after filing).
- Before filing: add more description of the claimed features with working examples
- After filing: narrow claims to match what is actually described
- Cannot add new matter to the specification after filing (35 U.S.C. § 132)

### § 112(b) — Antecedent Basis
**Fix:** Correct the claim language.
- Add proper antecedent: change "the processor" to "a processor" on first introduction
- Fix dependent claims: add the element to the independent claim or correct the dependency
- Replace vague relative terms with quantified ranges or defined standards from the specification

### Formalities
**Fix:** Correct per MPEP requirements.
- Abstract length: trim to ≤150 words while preserving key disclosures
- Claim numbering: renumber consecutively
- Drawing margins: redraw to meet 37 C.F.R. § 1.84 requirements

---

## Output Format

The review produces a structured findings report:

```markdown
## Patent Application Review Report

**Application:** [Title]
**Review date:** YYYY-MM-DD
**Reviewer:** Patent Review Skill (AI-assisted — not legal advice)

### Executive Summary
[Overall patentability assessment: strong / moderate / concerns noted]

### § 101 Findings
- **Status:** Pass / Concerns / Likely Rejection
- **Issues:** [description]
- **Affected claims:** [list]
- **Suggested fix:** [specific amendment]

### § 102 Findings
- **Status:** Pass / Concerns / Likely Rejection
- **Reference:** [if applicable]
- **Affected claims:** [list]
- **Suggested fix:** [specific amendment]

### § 103 Findings
[same structure]

### § 112(a) Findings
[same structure]

### § 112(b) Findings
- **Antecedent basis issues:** [specific claims and elements]
- **Indefinite terms:** [list]
- **Suggested fix:** [specific language]

### Formalities Findings
- **Abstract:** [Pass / word count issue]
- **Claims:** [Pass / numbering / dependency issues]
- **Drawings:** [Pass / margin/numeral issues]

### Priority Recommendations
1. [Most critical issue to address]
2. [Second priority]
3. [Additional items]
```

---

## Usage

To review a patent application, provide:
1. **Application text** — full specification and claims (or draft)
2. **Prior art references** — if available from a patent-search run
3. **Filing format** — provisional, non-provisional, or PCT
4. **Specific concerns** — any known § 101 / § 102 / § 103 risks

The skill will run all 7 review steps and produce a structured findings report with MPEP citations and suggested claim amendments.

---
## Version History
- **v1.0.0** (2026-03-25) — Initial release

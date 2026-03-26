---
name: patent-draft
description: "v1.0.0 — Generate patent applications in USPTO provisional, non-provisional, or PCT format from an invention description and prior art analysis."
---

# Patent Draft Skill

> DISCLAIMER: This skill generates draft patent applications as a starting point for review by a registered patent attorney or agent. No filing should occur without professional legal review.

## Filing Format Comparison

| Feature | Provisional | Non-Provisional | PCT |
|---------|-------------|-----------------|-----|
| Cost (USPTO) | $320 (micro) / $800 (small) / $1,600 (large) | $800–$1,800+ (micro–large) | $1,478+ |
| Formal claims required | No | Yes | Yes |
| Examined | No | Yes | Yes (national phase) |
| Patent term | None (placeholder) | 20 years from filing | 20 years from earliest priority |
| Validity | 12 months | Full application | 30 months to national phase |
| International coverage | No | US only | 150+ countries (PCT) |
| Best for | Early disclosure, 12-month runway | US protection | Worldwide protection strategy |

**Key rule:** A non-provisional or PCT application must be filed within **12 months** of the provisional filing date to claim priority benefit under 35 U.S.C. § 119(e).

---

## Requirements Per Format

### Provisional Application
**Required sections:**
- Title of Invention
- Description of the Invention (full written description — no formal claims required)
- Drawings (if any — informal drawings acceptable)
- Cover sheet (ADS not required but recommended)

**Formality requirements:**
- No formal claims required (but including them strengthens the disclosure)
- No oath or declaration required
- No information disclosure statement (IDS) required
- Drawings may be informal (no draftsperson required)
- Filed with USPTO via EFS-Web/Patent Center

**Best practices:**
- Include as much detail as possible — the provisional defines the scope of priority
- Include multiple embodiments even if informal
- Use the same terminology that will appear in the non-provisional claims
- Consider including draft claims to establish claim scope

### Non-Provisional Utility Application
**Required sections (37 C.F.R. § 1.77):**
1. Title of Invention
2. Cross-Reference to Related Applications (if applicable)
3. Statement Regarding Federally Sponsored Research (if applicable)
4. Background of the Invention
5. Brief Summary of the Invention
6. Brief Description of the Drawings
7. Detailed Description of the Preferred Embodiment(s)
8. Claims (at least one independent claim required)
9. Abstract (≤150 words)
10. Drawings (formal, per 37 C.F.R. § 1.84)

**Formality requirements:**
- Formal drawings required (black ink, specific margins, reference numerals)
- Claims must be numbered consecutively
- Oath or Declaration (ADS or separate form)
- Application Data Sheet (ADS) required
- Information Disclosure Statement (IDS) — not required at filing but must be filed within 3 months or before first Office Action
- Filing fee payment

### PCT Application
**Required sections:**
- Request (PCT/RO/101 form)
- Description (same as non-provisional specification)
- Claims (at least one)
- Abstract (≤150 words)
- Drawings (if referenced in description)

**Formality requirements:**
- Must designate Receiving Office (USPTO for US applicants)
- International Search Report (ISR) issued by ISA (usually USPTO, EPO, or JPO)
- Written Opinion issued with ISR
- 30-month deadline for national phase entry in each country
- Translation requirements vary by country

---

## Multi-Embodiment Drafting Guidance

Patent applications should describe all commercially relevant embodiments to maximize protection:

### Structure for Multiple Embodiments
1. **Primary embodiment** — the best mode, fully described with all components
2. **Alternative embodiments** — variations in key components or configurations
3. **Optional features** — elements that may or may not be present
4. **Combinatorial disclosure** — explicitly state which features can be combined

### Language Patterns
- "In one embodiment..." — introduces primary embodiment
- "In another embodiment..." — introduces alternative
- "In some embodiments..." — covers a class of variations
- "Optionally, the system further comprises..." — optional features
- "The [component] may be [X] or alternatively [Y]..." — explicit alternatives

### Embodiment Coverage Strategy
- Identify all commercially viable configurations
- Include software, hardware, and hybrid embodiments where applicable
- Describe both the apparatus and the method of using it
- Consider system, method, and computer-readable medium (CRM) claim formats

---

## Claim Writing Strategy

Claims define the legal scope of protection. Use a layered strategy:

### Claim Hierarchy
1. **Broad independent claims** — capture the core inventive concept with minimal limitations
2. **Narrow independent claims** — alternative approaches to the same inventive concept
3. **Dependent claims** — add specific features as fallback positions

### Independent Claim Structure (Apparatus)
```
A system for [function], comprising:
  a [component A] configured to [do X];
  a [component B] configured to [do Y]; and
  a [component C] configured to [do Z using output of A and B].
```

### Independent Claim Structure (Method)
```
A method for [function], comprising:
  [verb]-ing [object] to [achieve result];
  [verb]-ing [object] based on [prior step]; and
  [verb]-ing [object] to produce [output].
```

### Independent Claim Structure (CRM)
```
A non-transitory computer-readable medium storing instructions that, when executed by a processor, cause the processor to:
  [action 1];
  [action 2]; and
  [action 3].
```

### Dependent Claim Patterns
- Add structural specificity: "The system of claim 1, wherein the [component] comprises..."
- Add functional specificity: "The method of claim 1, further comprising..."
- Add configuration alternatives: "The system of claim 1, wherein the [component] is a [specific type]..."

### Claim Writing Rules
- Each claim must be a single sentence
- Antecedent basis: every element must be introduced with "a" or "an" before using "the"
- Avoid functional claiming at the point of novelty (MPF claims under § 112(f))
- Do not mix apparatus and method limitations in a single claim
- Draft at least 3 independent claims covering: system, method, and CRM

---

## Abstract Rules

Per MPEP § 608.01(b):
- Maximum **150 words**
- Must describe the nature and gist of the invention
- Should mention the problem solved and the key solution
- Do not begin with "This invention relates to..."
- Do not use "I" or "we"
- Must be on a separate page
- Representative drawing should be designated (figure number)

**Abstract template:**
```
A [system/method/apparatus] for [function] [solves problem] by [key mechanism].
The [system/method] comprises [key components/steps]. In operation, [brief description
of how it works]. The [system/method] provides [key advantage] over prior approaches
by [distinguishing feature].
```

---

## Application Data Sheet (ADS) Requirements

Required for non-provisional applications per 37 C.F.R. § 1.76:

| Section | Required Fields |
|---------|----------------|
| Applicant Information | Full legal name, address, citizenship |
| Inventor Information | Full name, address, citizenship for each inventor |
| Correspondence Address | Address for USPTO correspondence |
| Application Type | Utility, design, plant |
| Filing Date Info | Priority claims, continuation info |
| Representative Information | Attorney/agent name, registration number |
| Domestic Benefit Claims | Prior provisional or non-provisional applications |
| Foreign Priority Claims | Foreign applications claiming priority |

---

## 12-Month Provisional Deadline Warning

**CRITICAL:** Under 35 U.S.C. § 119(e), the non-provisional (or PCT) application claiming benefit of a provisional must be filed within **12 months** of the provisional filing date.

- No extensions available — this is a hard statutory deadline
- Missing the deadline forfeits the priority date benefit
- The provisional itself becomes abandoned (not published)
- Calendar the deadline immediately upon provisional filing
- Consider filing the non-provisional earlier if public disclosure is imminent

---

## Filing Checklists

### Provisional Application Checklist
- [ ] Title of invention
- [ ] Written description covering all embodiments
- [ ] Drawings (informal acceptable)
- [ ] Cover sheet with inventor names and addresses
- [ ] Correspondence address
- [ ] Filing fee payment
- [ ] Calendar 12-month deadline for non-provisional filing

### Non-Provisional Application Checklist
- [ ] Title of invention
- [ ] Cross-references (if continuation or CIP)
- [ ] Background section
- [ ] Summary of invention
- [ ] Brief description of drawings
- [ ] Detailed description of embodiments
- [ ] At least one independent claim
- [ ] Abstract (≤150 words, separate page)
- [ ] Formal drawings (if any)
- [ ] Application Data Sheet (ADS)
- [ ] Oath or Declaration
- [ ] Filing fee payment
- [ ] IDS (within 3 months of filing or before first Office Action)

### PCT Application Checklist
- [ ] Request form (PCT/RO/101)
- [ ] Description (full specification)
- [ ] Claims (at least one)
- [ ] Abstract (≤150 words)
- [ ] Drawings (if referenced)
- [ ] Priority document (if claiming earlier filing date)
- [ ] Filing fee (international filing fee + search fee)
- [ ] Designation of Receiving Office
- [ ] Power of Attorney (if filed by agent)
- [ ] Calendar 30-month national phase deadlines per country

---

## Usage

To draft a patent application, provide:
1. **Invention description** — technical details, components, how it works
2. **Prior art analysis** — results from patent-search skill (to differentiate claims)
3. **Filing format** — provisional, non-provisional, or PCT
4. **Inventor information** — names and addresses (for non-provisional/PCT)
5. **Preferred embodiment** — the best mode for the invention

The skill will generate a complete draft application with all required sections, layered claims, and a filing checklist.

---
## Version History
- **v1.0.0** (2026-03-25) — Initial release

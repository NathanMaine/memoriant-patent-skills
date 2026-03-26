---
name: patent-pipeline
description: "v1.0.0 — Run the full patent workflow from invention idea to filing-ready draft. Orchestrates search, analysis, drafting, review, and export in sequence."
---

# Patent Pipeline Skill

Run the complete Memoriant Patent Platform workflow from a raw invention description to a filing-ready patent application package.

## Full Pipeline Stages

| Stage | Name | Description | Output |
|-------|------|-------------|--------|
| 1 | Invention Capture | Structured intake of invention details, inventors, and filing goals | Invention disclosure document |
| 2 | Prior Art Search | USPTO 7-step prior art search across PatentsView and USPTO databases | Prior art report with relevance scores |
| 3 | Prior Art Gate | Human review of search results; pipeline pauses if conflicts found | Go/No-go decision |
| 4 | Patentability Analysis | § 101 / § 102 / § 103 / § 112 analysis against prior art findings | Patentability assessment report |
| 5 | Claim Strategy | Generate broad-to-narrow claim hierarchy with fallback positions | Draft claim set |
| 6 | Application Drafting | Generate full specification: background, summary, detailed description | Draft application (all sections) |
| 7 | Diagram Generation | Generate system architecture and flow chart diagrams | Figures with reference numerals |
| 8 | Application Review | Review draft against all rejection types; identify issues | Review report with suggested fixes |
| 9 | Revision | Apply review findings to amend claims and specification | Revised application |
| 10 | Export | Generate DOCX and PDF output in USPTO format | Filing package (DOCX + PDF) |

---

## Prior Art Gate

The pipeline **pauses after Stage 2** to present search findings for human review.

**Gate criteria:**

| Finding | Action |
|---------|--------|
| No highly relevant prior art | Auto-advance to Stage 4 (with user confirmation) |
| Medium-relevance prior art found | Present findings, request human go/no-go decision |
| High-relevance prior art found | **PAUSE** — flag specific overlapping references, require explicit user decision |
| Blocking prior art found | **STOP** — recommend consultation with patent attorney before proceeding |

**Why this gate exists:** Prior art that anticipates or renders obvious the core inventive concept can make a patent application inadvisable. The pipeline surfaces this risk before investing effort in drafting.

**At the gate, the user can:**
- **Continue** — proceed knowing the prior art landscape
- **Refocus** — update the invention description to emphasize a different aspect
- **Abandon** — stop the pipeline (prior art blocks protection)
- **Narrow** — proceed with narrowed claim scope to avoid prior art

---

## Resuming from Any Stage

The pipeline saves state after each stage. To resume from a specific stage:

```bash
# Resume from Stage 6 (drafting) with existing prior art results
curl -X POST http://localhost:8000/api/pipeline/resume \
  -H "Content-Type: application/json" \
  -d '{
    "session_id": "session_abc123",
    "resume_from_stage": 6,
    "user_decision": "continue"
  }'
```

**Session state includes:**
- Invention disclosure
- Prior art search results and relevance scores
- Patentability analysis
- Draft claims (current version)
- Application text (current version)
- Review findings
- Stage completion status

**Stage identifiers for resume:**
- `invention_capture` — Stage 1
- `prior_art_search` — Stage 2
- `prior_art_gate` — Stage 3
- `patentability_analysis` — Stage 4
- `claim_strategy` — Stage 5
- `application_drafting` — Stage 6
- `diagram_generation` — Stage 7
- `application_review` — Stage 8
- `revision` — Stage 9
- `export` — Stage 10

---

## Progress Tracking

The pipeline provides real-time progress updates:

```json
{
  "session_id": "session_abc123",
  "invention_title": "AI-Powered Meeting Intelligence System",
  "current_stage": "application_drafting",
  "stages_complete": ["invention_capture", "prior_art_search", "prior_art_gate", "patentability_analysis", "claim_strategy"],
  "stages_pending": ["diagram_generation", "application_review", "revision", "export"],
  "gate_status": "cleared",
  "prior_art_findings": {
    "high_relevance": 0,
    "medium_relevance": 3,
    "low_relevance": 12
  },
  "estimated_completion": "2 stages remaining (~15 minutes)",
  "filing_deadline": {
    "provisional_filed": "2025-01-15",
    "nonprovisional_due": "2026-01-15",
    "days_remaining": 297
  }
}
```

Check pipeline status:
```bash
curl http://localhost:8000/api/pipeline/status/session_abc123
```

---

## Export Formats

The pipeline exports a complete filing package:

### DOCX Export
- USPTO-formatted Word document
- Standard section headers and formatting
- Editable for attorney review and amendment
- Suitable for patent prosecution correspondence

### PDF Export
- Print-ready PDF formatted for USPTO submission
- Embedded fonts and margins per 37 C.F.R. § 1.52
- Non-editable (for filing or archival)

### Export Package Contents
```
filing_package_[session_id]/
├── application.docx          # Full application (editable)
├── application.pdf           # Full application (print-ready)
├── claims_only.docx          # Claims section only (for review)
├── figures/
│   ├── fig1_system.svg       # System architecture diagram
│   ├── fig2_method.svg       # Flow chart
│   └── fig3_detail.svg       # Detail view (if generated)
├── prior_art_report.pdf      # Prior art search findings
├── patentability_analysis.pdf # § 101/102/103 analysis
├── review_report.pdf         # Application review findings
└── filing_checklist.pdf      # Filing checklist (format-specific)
```

Request export:
```bash
curl -X POST http://localhost:8000/api/pipeline/export \
  -H "Content-Type: application/json" \
  -d '{
    "session_id": "session_abc123",
    "formats": ["docx", "pdf"],
    "include_supporting_docs": true
  }'
```

---

## API-Connected Mode vs Standalone Mode

### API-Connected Mode
- Requires the Memoriant Patent Platform backend running (`http://localhost:8000` by default)
- Accesses live PatentsView and USPTO databases via search provider integrations
- Persists session state in the backend database
- Supports full pipeline orchestration with real-time status
- Export via backend DOCX/PDF generation pipeline

**Start the backend:**
```bash
docker compose up -d
# or
uvicorn api.main:app --host 0.0.0.0 --port 8000
```

**Run full pipeline:**
```bash
curl -X POST http://localhost:8000/api/pipeline/start \
  -H "Content-Type: application/json" \
  -d '{
    "invention_title": "AI-Powered Meeting Intelligence System",
    "invention_description": "...",
    "inventors": [{"name": "Jane Doe", "address": "..."}],
    "filing_format": "provisional",
    "search_depth": "standard"
  }'
```

### Standalone Mode
- No backend required
- Uses Claude Code directly with built-in skills
- Prior art search via WebFetch to PatentsView API
- Application generated as local markdown files
- Export via local Pandoc installation (if available)
- Session state saved as local JSON files in `~/.memoriant-patent/sessions/`

**Run in standalone mode:**
Invoke the `patent-pipeline` skill directly in Claude Code:
1. Provide invention description
2. Skill executes each stage using other patent skills (`patent-search`, `patent-draft`, `patent-review`, `patent-diagrams`)
3. Output saved to `./output/[session_id]/`

---

## Starting a Pipeline Session

To start the full pipeline, provide:

1. **Invention title** — short descriptive title
2. **Invention description** — technical details, components, how it works, key advantages
3. **Filing format** — provisional, non-provisional, or PCT
4. **Inventor information** — names and addresses (required for non-provisional/PCT)
5. **Search depth** — quick (top 25 results), standard (top 100), deep (full citation chain)
6. **Technology area** — for CPC code identification in prior art search

The pipeline will execute all stages sequentially, pausing at the prior art gate and revision stage for human input, and deliver a complete filing-ready package.

---
## Version History
- **v1.0.0** (2026-03-25) — Initial release

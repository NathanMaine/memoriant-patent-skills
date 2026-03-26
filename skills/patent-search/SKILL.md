---
name: patent-search
description: "v1.0.0 — Search US patents for prior art using the USPTO 7-step methodology. Supports keyword, CPC classification, inventor, assignee, citation chain, and date range searches across PatentsView and USPTO databases."
---

# Patent Search Skill

> DISCLAIMER: This skill is a research aid only and does not constitute legal advice. Prior art search results should be reviewed by a registered patent attorney or agent before making any filing decisions.

## USPTO 7-Step Prior Art Search Strategy

The USPTO recommends the following systematic approach for prior art searching:

### Step 1 — Brainstorm Keywords and Synonyms
- Identify all terms describing the invention: functional terms, structural terms, trade names
- List synonyms, related terms, and broader/narrower concepts
- Consider how different disciplines describe the same concept
- Document keywords in a search log for reproducibility

### Step 2 — Classify the Invention Using CPC
- Use the USPTO CPC classification search at https://www.uspto.gov/patents/search/classification
- Identify the most relevant CPC subgroups (e.g., G06F 40/30 for NLP)
- Check parent and sibling classes for related subject matter
- Record all CPC codes to use as search filters

### Step 3 — Search US Patents (PatentsView + USPTO Full Text)
- Search PatentsView API for structured data queries
- Use USPTO Patent Full-Text Database for keyword searches in claims and specifications
- Start broad, then narrow using Boolean operators and field filters

### Step 4 — Search US Patent Applications (Pre-Grant Publications)
- Search USPTO Patent Application Full-Text Database (AppFT)
- Pre-grant publications are prior art from their filing date (post-March 2001)
- Use same keywords and CPC codes as granted patent search

### Step 5 — Search Foreign Patents and NPL
- EPO Espacenet (worldwide): https://worldwide.espacenet.com
- WIPO PatentScope (PCT applications): https://patentscope.wipo.int
- Google Scholar for non-patent literature (NPL)
- IEEE Xplore, ACM Digital Library for technical papers

### Step 6 — Trace Forward and Backward Citations
- For each highly relevant reference, examine all patents it cites (backward citations)
- Examine all patents that cite the reference (forward citations)
- Citation chains often reveal the most relevant prior art
- PatentsView supports citation chain queries

### Step 7 — Review Results and Compile Report
- Score each reference for relevance (high / medium / low)
- Note specific claims or disclosures that overlap with the invention
- Identify claim elements NOT found in prior art (patentability gaps)
- Produce a structured prior art report

---

## PatentsView API Reference

**Base endpoint:** `https://search.patentsview.org/api/v1/`

**Authentication:** Free tier — no API key required for basic queries. Rate limit: 45 requests/minute.

**Key endpoints:**

| Endpoint | Description |
|----------|-------------|
| `GET /patent/` | Search granted US patents |
| `GET /patent/{patent_id}` | Retrieve a specific patent by ID |
| `GET /application/` | Search patent applications (pre-grant) |
| `GET /inventor/` | Search by inventor |
| `GET /assignee/` | Search by assignee/company |
| `GET /cpc_subgroup/` | Browse CPC classification codes |

**Query operators:**

| Operator | Syntax | Description |
|----------|--------|-------------|
| equals | `{"field": "value"}` | Exact match |
| contains | `{"_contains": {"field": "value"}}` | Substring match |
| begins_with | `{"_begins": {"field": "value"}}` | Prefix match |
| AND | `{"_and": [...]}` | All conditions must match |
| OR | `{"_or": [...]}` | Any condition must match |
| date range | `{"_gte": {"date": "2020-01-01"}}` | Greater than or equal |

**Key field names:**

| Field | Description |
|-------|-------------|
| `patent_id` | USPTO patent number (e.g., "10123456") |
| `patent_title` | Title of the patent |
| `patent_abstract` | Abstract text |
| `patent_date` | Grant date (YYYY-MM-DD) |
| `patent_type` | "utility", "design", "plant", "reissue" |
| `inventor_last_name` | Inventor last name |
| `assignee_organization` | Assignee company name |
| `cpc_subgroup_id` | CPC classification code |
| `cited_patent_id` | Patents cited by this patent (backward) |
| `citing_patent_id` | Patents that cite this patent (forward) |

**Example queries:**

Keyword search in title and abstract:
```bash
curl -X GET "https://search.patentsview.org/api/v1/patent/" \
  -H "Content-Type: application/json" \
  -d '{
    "q": {"_or": [
      {"_contains": {"patent_title": "natural language processing"}},
      {"_contains": {"patent_abstract": "meeting intelligence"}}
    ]},
    "f": ["patent_id", "patent_title", "patent_date", "assignee_organization"],
    "o": {"per_page": 25, "page": 1}
  }'
```

CPC classification search:
```bash
curl -X GET "https://search.patentsview.org/api/v1/patent/" \
  -H "Content-Type: application/json" \
  -d '{
    "q": {"_and": [
      {"cpc_subgroup_id": "G06F40/30"},
      {"_gte": {"patent_date": "2018-01-01"}}
    ]},
    "f": ["patent_id", "patent_title", "patent_date", "cpc_subgroup_id"],
    "o": {"per_page": 50}
  }'
```

Assignee search:
```bash
curl -X GET "https://search.patentsview.org/api/v1/patent/" \
  -H "Content-Type: application/json" \
  -d '{
    "q": {"_contains": {"assignee_organization": "Acme Corp"}},
    "f": ["patent_id", "patent_title", "patent_date"],
    "o": {"per_page": 100}
  }'
```

---

## Search Strategy Guidance

### When to use Keyword Search
- Best for: novel terminology, specific technical phrases, brand names
- Use when: CPC codes are uncertain or too broad
- Tip: search title, abstract, and claims separately — relevant art often appears in claims only

### When to use CPC Classification Search
- Best for: systematic coverage of a technology area
- Use when: technology is well-established with clear classification
- Tip: check both the most specific subgroup AND its parent group

### When to use Citation Chain Search
- Best for: finding the most relevant prior art once a few key references are identified
- Use when: a patent or application appears highly relevant
- Tip: forward citations reveal art that built on the same foundation — often directly relevant

### When to use Inventor/Assignee Search
- Best for: competitive intelligence, tracking a company's patent portfolio
- Use when: the inventor or company is known to work in the relevant field
- Tip: combine with date range to see recent filings

### Search Priority Order
1. CPC classification (broadest systematic coverage)
2. Keyword search in claims (closest to invention elements)
3. Assignee/inventor search (competitive landscape)
4. Citation chain from most relevant references

---

## Result Formatting

Present search results as a structured markdown comparison table:

```markdown
## Prior Art Search Results — [Invention Title]

**Search date:** YYYY-MM-DD
**Databases searched:** PatentsView, USPTO Full Text, [others]
**Keywords used:** [list]
**CPC codes searched:** [list]

### Results Summary

| Patent No. | Title | Assignee | Date | Relevance | Key Overlap |
|------------|-------|----------|------|-----------|-------------|
| US10,xxx,xxx | ... | ... | 2021-03-15 | HIGH | Claims 1-3 disclose... |
| US9,xxx,xxx | ... | ... | 2019-07-22 | MEDIUM | Abstract describes... |
| US20210xxxxx | ... | ... | 2021-08-05 | LOW | Related field only |

### High Relevance References — Detailed Analysis

#### US10,xxx,xxx — [Title]
- **Filed:** YYYY-MM-DD | **Granted:** YYYY-MM-DD
- **Assignee:** [Company]
- **Key disclosure:** [What it teaches that overlaps]
- **Overlap with invention:** [Specific elements]
- **Distinctions:** [What is NOT disclosed — patentability gap]

### Patentability Gap Analysis
The following inventive elements were NOT found in the prior art:
1. [Element 1]
2. [Element 2]

### Recommended Next Steps
- Manually review: [list of references]
- Investigate CPC codes: [additional codes to check]
- Consider NPL search in: [specific journals/conferences]
```

---

## Usage

To run a patent search, provide:
1. **Invention description** — what the invention does, key technical components
2. **Keywords** — key terms (will be supplemented with synonyms)
3. **Technology area** — for CPC code identification
4. **Date range** (optional) — default: all dates

The skill will execute the 7-step methodology and return a formatted prior art report.

---
## Version History
- **v1.0.0** (2026-03-25) — Initial release

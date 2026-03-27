<p align="center">
  <img src="https://img.shields.io/badge/claude--code-plugin-8A2BE2" alt="Claude Code Plugin" />
  <img src="https://img.shields.io/badge/skills-6-blue" alt="6 Skills" />
  <img src="https://img.shields.io/badge/agents-4-green" alt="4 Agents" />
  <img src="https://img.shields.io/badge/license-MIT-green" alt="MIT License" />
</p>

# Memoriant Patent Skills

A Claude Code plugin that gives you a complete patent workflow — from invention idea to filing-ready application. Search prior art across multiple databases, analyze patentability against all major USPTO rejection types, draft applications in any filing format, and generate patent diagrams.

**No servers. No Docker. Just install and use.**

## Install

```bash
/install NathanMaine/memoriant-patent-skills
```

## Cross-Platform Support

This plugin works with multiple AI coding assistants:

### Claude Code (Primary)
```bash
/install NathanMaine/memoriant-patent-skills
```

### OpenAI Codex CLI
```bash
git clone https://github.com/NathanMaine/memoriant-patent-skills.git ~/.codex/skills/patent
codex --enable skills
```

### Gemini CLI
```bash
gemini extensions install https://github.com/NathanMaine/memoriant-patent-skills.git --consent
```

## Skills

| Skill | Command | What It Does |
|-------|---------|-------------|
| **Patent Search** | `/patent-search` | Multi-strategy prior art search using USPTO 7-step methodology |
| **Patent Draft** | `/patent-draft` | Generate provisional, non-provisional, or PCT applications |
| **Patent Review** | `/patent-review` | Review against 101, 102, 103, 112(a), 112(b), formalities |
| **Patent Diagrams** | `/patent-diagrams` | System architecture, flowcharts, reference numbering |
| **Patent Pipeline** | `/patent-pipeline` | Full end-to-end: idea to filing-ready draft |
| **Patent Config** | `/patent-config` | Configure LLM and search providers |

## Agents

| Agent | Best Model | Specialty |
|-------|-----------|-----------|
| **Prior Art Searcher** | Opus 4.6 (1M context) | Autonomous multi-strategy search |
| **Patent Drafter** | Opus 4.6 + extended thinking | Multi-embodiment drafting, layered claims |
| **Patent Reviewer** | Opus 4.6 + extended thinking | Full rejection screening (101-112) |
| **Patent Illustrator** | Sonnet 4.6 | Diagram generation, reference numerals |

## Quick Start

```bash
# Search for prior art
/patent-search "wireless power transfer for implantable medical devices"

# Draft a provisional application
/patent-draft

# Review a draft against USPTO standards
/patent-review

# Run the full pipeline
/patent-pipeline
```

## Search Providers

| Provider | Cost | Default | API Key |
|----------|------|---------|---------|
| PatentsView / PatentSearch | Free (API key required) | On | [Get key](https://patentsview.org/apis/keyrequest) |
| USPTO Open Data Portal | Free (no key needed) | On | None |
| SerpAPI (Google Patents) | Paid ($50/mo) | Off (opt-in) | [serpapi.com](https://serpapi.com) |

### Setting Up PatentsView API Key (Free)

PatentsView provides free access to 76M+ US patents. As of March 2026, PatentsView has migrated to the **USPTO Open Data Portal** and uses the new **PatentSearch API**.

**Step 1: Request an API key**

Go to: https://patentsview.org/apis/keyrequest

Or directly: https://patentsview-support.atlassian.net/servicedesk/customer/portal/1/group/1/create/18

**Step 2: Fill out the form**

You'll need:
- Your name
- Your email address
- A description of what you'll use the API for (e.g., "Prior art search for patent applications using Memoriant Patent Platform")

**Step 3: Use the key**

Once you receive your API key by email, set it as an environment variable:

```bash
export PATENTSVIEW_API_KEY=your-key-here
```

Or add it to your `.env` file:

```
PATENTSVIEW_API_KEY=your-key-here
```

**Usage limits:**
- 45 requests per minute (our platform limits to 30/min to stay well under)
- API keys do not expire
- One key per user

**Note:** If new API key grants are temporarily suspended during the USPTO migration, the platform still works with the USPTO Open Data Portal (no key required) and SerpAPI (paid).

## What It Covers

**Prior Art Search** — keyword, CPC classification, inventor/assignee, citation chains, date range, boolean combinations

**Patentability Analysis:**
- Subject matter eligibility (35 USC 101)
- Novelty (35 USC 102)
- Obviousness (35 USC 103)
- Claims definiteness (35 USC 112(b))
- Specification enablement (35 USC 112(a))
- Formalities (MPEP 608)

**Filing Formats:**
- USPTO provisional application
- USPTO non-provisional (utility) application
- PCT international format

## Examples

Sample outputs showing what each skill produces:

| Example | What it shows |
|---------|--------------|
| [sample-search-results.md](examples/sample-search-results.md) | Prior art search for "wireless power transfer for medical implants" — 5 patents with relevance analysis |
| [sample-draft-provisional.md](examples/sample-draft-provisional.md) | Provisional patent application with abstract, background, description, 3 claims, and filing checklist |
| [sample-review-findings.md](examples/sample-review-findings.md) | Review findings covering 101, 102, 103, 112(a), 112(b), and MPEP 608 with severity levels and suggestions |

## Full Platform

For the complete self-hosted platform with web UI, database, Docker deployment, and team features, see:

**[Memoriant Patent Platform](https://github.com/NathanMaine/memoriant-patent-platform)**

## Disclaimer

This plugin is a research and drafting aid, not a substitute for professional legal counsel. Always have a qualified patent attorney review applications before filing.

## License

[MIT](LICENSE)

Built by [Nathan Maine](https://github.com/NathanMaine)

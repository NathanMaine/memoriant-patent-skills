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

| Provider | Cost | Default |
|----------|------|---------|
| PatentsView | Free (API key required) | On |
| USPTO Open Data Portal | Free | On |
| SerpAPI (Google Patents) | Paid | Off (opt-in) |

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

## Full Platform

For the complete self-hosted platform with web UI, database, Docker deployment, and team features, see:

**[Memoriant Patent Platform](https://github.com/NathanMaine/memoriant-patent-platform)**

## Disclaimer

This plugin is a research and drafting aid, not a substitute for professional legal counsel. Always have a qualified patent attorney review applications before filing.

## License

[MIT](LICENSE)

Built by [Nathan Maine](https://github.com/NathanMaine)

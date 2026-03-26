# Memoriant Patent Skills

AI-powered patent workflow skills for coding agents.

## Available Skills

### patent-search
Search US patents for prior art using the USPTO 7-step methodology. Supports keyword, CPC classification, inventor, assignee, citation chain, and date range searches across PatentsView and USPTO databases.

Skill file: `skills/patent-search/SKILL.md`

### patent-draft
Generate patent applications in provisional, non-provisional (utility), or PCT international format from an invention description and prior art analysis.

Skill file: `skills/patent-draft/SKILL.md`

### patent-review
AI-assisted review of patent applications against all major USPTO rejection types: 35 USC 101, 102, 103, 112(a), 112(b), and MPEP 608 formalities.

Skill file: `skills/patent-review/SKILL.md`

### patent-diagrams
Generate patent diagrams with reference numbering for patent applications. System architecture, flowcharts, and component views in informal or formal modes.

Skill file: `skills/patent-diagrams/SKILL.md`

### patent-pipeline
End-to-end patent workflow from invention idea to filing-ready application. Runs search, analysis, drafting, review, and export in sequence.

Skill file: `skills/patent-pipeline/SKILL.md`

### patent-config
Configure patent platform settings: LLM provider, search providers, API keys, and operating mode.

Skill file: `skills/patent-config/SKILL.md`

## Available Agents

### prior-art-searcher
Autonomous multi-strategy prior art search agent following the USPTO 7-step methodology.

Agent file: `agents/prior-art-searcher.md`

### patent-drafter
Multi-embodiment patent application drafting agent with iterative refinement and layered claim strategy.

Agent file: `agents/patent-drafter.md`

### patent-reviewer
Full rejection pre-screening agent covering 35 USC 101, 102, 103, 112(a), 112(b), and MPEP 608 formalities.

Agent file: `agents/patent-reviewer.md`

### patent-illustrator
Patent diagram generation agent using visual-explainer for rendering with USPTO reference numeral conventions.

Agent file: `agents/patent-illustrator.md`

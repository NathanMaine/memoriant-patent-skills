# Security Policy

## What This Plugin Does

This plugin consists entirely of markdown instruction files (SKILL.md and agent .md files). It contains:
- No executable code
- No shell scripts
- No network calls
- No file system modifications beyond what Claude Code normally does

All API calls (PatentsView, USPTO, SerpAPI) are made by Claude Code itself using its standard tools, not by any code in this plugin.

## API Key Handling

API keys are configured via Claude Code's `userConfig` system:
- Keys are prompted at plugin enable time
- Keys are stored by Claude Code's built-in credential management
- Keys are never logged, displayed, or transmitted by the plugin
- Keys marked as `sensitive: true` in plugin.json

## Reporting a Vulnerability

If you discover a security issue, please email nathan@memoriant.com (do not open a public issue).

We will respond within 48 hours and provide a fix timeline.

## Auditing This Plugin

This plugin is easy to audit:
1. All files are markdown — readable in any text editor
2. No `node_modules`, no Python packages, no compiled binaries
3. Total codebase is ~6,000 lines of markdown
4. Review any SKILL.md file to see exactly what instructions are given to the AI

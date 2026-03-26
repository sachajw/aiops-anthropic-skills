# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Fork of `anthropics/skills` — the official Anthropic Agent Skills repository. Skills are self-contained folders of instructions, scripts, and resources that Claude loads dynamically to improve performance on specialized tasks.

Full specification: https://agentskills.io/specification

## Repository Structure

- `skills/` — All skill implementations (17 skills)
- `template/` — Minimal `SKILL.md` skeleton for new skills
- `spec/` — Pointer to the Agent Skills specification
- `.claude-plugin/marketplace.json` — Defines three plugin bundles: `document-skills`, `example-skills`, `claude-api`

## Skill Format

Each skill is a directory with at minimum a `SKILL.md` file:

```markdown
---
name: skill-name          # Required: unique identifier (lowercase, hyphens)
description: When/what     # Required: trigger description
---

# Skill Title
[Instructions for Claude]
```

Skills may also bundle: `scripts/` (executable Python/JS/shell), `references/` (docs loaded on demand), `agents/` (sub-agent instructions), `assets/` (templates, fonts, icons).

## Skill Categories

**Document skills** (proprietary, source-available): `docx`, `pdf`, `pptx`, `xlsx` — rely on Python scripts in `scripts/office/`, require `pandoc`, `soffice` (LibreOffice), and Python libs like `pypdf`, `pdfplumber`.

**Example skills** (Apache 2.0): `algorithmic-art`, `brand-guidelines`, `canvas-design`, `doc-coauthoring`, `frontend-design`, `internal-comms`, `mcp-builder`, `skill-creator`, `slack-gif-creator`, `theme-factory`, `web-artifacts-builder`, `webapp-testing`.

**API skill**: `claude-api` — multi-language SDK docs organized by language (`python/`, `typescript/`, `java/`, `go/`, `ruby/`, `csharp/`, `php/`, `curl/`).

## Development Notes

- This is a content-only repository — no build system, package manager, or test runner at the repo level.
- The `skill-creator` skill has its own Python-based eval tooling in `skills/skill-creator/scripts/`.
- Document skills share infrastructure in their respective `scripts/office/` directories.
- Validation for document skills: `python scripts/office/validate.py` (within each skill directory).

## Claude Code Plugin Installation

```
/plugin marketplace add anthropics/skills
/plugin install document-skills@anthropic-agent-skills
/plugin install example-skills@anthropic-agent-skills
```

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A Claude Code plugin (`mysuperpowers`) that installs workflow skills into the agent's context. Skills are markdown files the agent loads on demand via the `Skill` tool. A SessionStart hook injects the `using-mysuperpowers` orientation skill automatically at every session start.

## Plugin Structure

```
skills/           # Each subdirectory is one skill (name = directory name)
  skill-name/
    SKILL.md      # Required. YAML frontmatter + markdown content
hooks/
  session-start   # Bash script that injects using-mysuperpowers at startup
  hooks.json      # Hook registration (SessionStart → session-start)
.claude-plugin/
  plugin.json     # Plugin metadata
  marketplace.json # Local dev marketplace config
```

## Skill File Format

Every `SKILL.md` requires YAML frontmatter with exactly two fields:

```yaml
---
name: skill-name-with-hyphens
description: Use when [specific triggering conditions — NOT a workflow summary]
---
```

- `name`: letters, numbers, hyphens only
- `description`: starts with "Use when…", third person, max ~500 chars, describes **triggering conditions only** — never summarizes the skill's workflow (agents may follow the description instead of reading the full skill if it contains workflow steps)
- Total frontmatter: max 1024 characters

## Installing for Development

```bash
/plugin install /path/to/mysuperpowers
```

Restart Claude Code after installation. The agent should acknowledge mysuperpowers in its first response.

## The Two-Phase Workflow (Hard Rule)

**Planning** and **execution** always run in separate sessions. This is enforced by the skills, not optional:

- **Planning session**: `brainstorming` → `creating-prd` (optional) → `milestone-planning` (optional). After `milestone-planning` produces `docs/features/<name>/plan.md`, the session **stops**. Never begin implementation in the planning session.
- **Execution session**: User pastes a milestone's execution prompt from `plan.md`. `executing-from-plan` activates, suppresses planning skills, and hands off to TDD/debugging/review skills. One milestone per session.

## Skill Authoring (writing-skills)

The `writing-skills` skill defines TDD for documentation: write baseline test (run a pressure scenario without the skill), write minimal skill to fix the failure, refactor to close loopholes. The `render-graphs.js` script in `skills/writing-skills/` renders `.dot` flowcharts to SVG:

```bash
./skills/writing-skills/render-graphs.js skills/some-skill           # separate SVGs
./skills/writing-skills/render-graphs.js skills/some-skill --combine # one combined SVG
```

Personal/user-specific skills go in `~/.claude/skills/` (not in this repo).

## Hook Mechanics

`hooks/session-start` reads `skills/using-mysuperpowers/SKILL.md`, escapes it for JSON, and outputs a platform-appropriate JSON response (different keys for Claude Code vs Cursor vs Copilot CLI). The hook detects the platform via environment variables (`CLAUDE_PLUGIN_ROOT`, `CURSOR_PLUGIN_ROOT`, `COPILOT_CLI`).

## Skill Invocation Rules (enforced by using-mysuperpowers)

- Skills are **mandatory** when they match — not optional. Even a 1% chance of applicability triggers invocation.
- Process skills (brainstorming, debugging) take priority over implementation skills.
- Conversational queries, typos, and one-line fixes skip the planning flow entirely.
- Never use the `Read` tool on skill files — always use the `Skill` tool.

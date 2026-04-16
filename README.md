# mysuperpowers

A structured development workflow plugin for Claude Code.

## Introduction

mysuperpowers is a personal development workflow plugin for Claude Code, built on the skills framework pattern from [obra/superpowers](https://github.com/obra/superpowers). It installs a set of skills — structured process guides — that the agent follows automatically when the task matches, covering everything from initial brainstorming through final branch integration.

The main thing it does differently from stock Superpowers: planning and execution run in separate sessions by design. Brainstorming, PRD creation, and milestone planning happen in a single planning session. Each milestone then executes in its own fresh session, started by pasting a self-contained execution prompt from the plan file. This keeps the context window clean and the starting state deterministic. The plugin also adds full update and revision flows across all three planning skills, so when a feature changes mid-development, the design, PRD, and plan can all be updated without starting over.

The execution skills (TDD, debugging, code review, verification, branch completion) are adapted from [obra/superpowers](https://github.com/obra/superpowers), which provided the skills framework pattern and the execution-phase discipline. The PRD creation skill draws on the [closedloop-ai prd-creator](https://github.com/closedloop-ai/claude-plugins) for its discovery questions, ID conventions (US-###, AC-###, Q-###), and "keep it light" philosophy. Both are MIT licensed; see Credits below.

## How it works

Skills are markdown files. Each one describes when to activate and how to proceed. The agent uses the `Skill` tool to load a skill's full content on demand and then follows it — checklists, decision flows, hard gates and all.

At session start, a SessionStart hook injects the `using-mysuperpowers` skill directly into the agent's context. This bootstraps the entire framework: the agent immediately knows what skills are available, when to invoke them, and that invocation is mandatory — not optional. When a skill applies to the current task, the agent must invoke it before doing anything else, including asking clarifying questions.

Skills can be rigid or flexible. Rigid skills (TDD, debugging) are followed exactly — no adapting away the discipline. Flexible skills (planning, patterns) apply principles to context. The skill itself tells you which it is.

## Installation (development mode)

mysuperpowers is not on the Claude Code plugin marketplace. Install it as a local plugin in dev mode.

1. Clone or download this repository to a local directory.

2. Install it as a local plugin in Claude Code:

   ```
   /plugin install /path/to/mysuperpowers
   ```

   > **Note:** The Claude Code plugin system is still evolving. Verify the exact command against the current Claude Code documentation if the above doesn't work.

3. Restart Claude Code.

4. Start a fresh session. The agent should acknowledge it has mysuperpowers in its first response — that's the SessionStart hook firing.

## The Workflow

Development follows two distinct phases. They never run in the same session.

### Planning phase

Run in a single session. The output is `plan.md` — the agent stops there.

1. Describe an idea or task. `brainstorming` activates in Create Mode.
2. The skill runs a Socratic design conversation: explores project context, asks clarifying questions one at a time, proposes 2–3 approaches with trade-offs, and presents a design for approval.
3. The approved design is saved to `docs/features/<feature-name>/<feature-name>-design.md`.
4. Brainstorming asks: "Would you like a PRD?" This step is optional.
5. If yes, `creating-prd` activates. It asks seven discovery questions conversationally, then drafts a 15-section document in two parts — business context (overview, goals, user stories, sequencing) and implementation detail (requirements, acceptance criteria, open questions, risks). Saved to `docs/features/<feature-name>/prd.md`.
6. creating-prd asks: "Would you like an implementation plan?" Also optional.
7. If yes, `milestone-planning` activates. It decomposes the work into milestones — each one scoped to be reviewable by a human in a single PR sitting. For each milestone it generates a self-contained execution prompt. The full plan is saved to `docs/features/<feature-name>/plan.md`.
8. **The skill stops.** It does not offer to begin execution. The user opens a new session for each milestone.

Each milestone runs in its own session because planning-phase context contaminates execution decisions. A session that starts mid-planning carries assumptions that muddle implementation choices. Starting clean means the agent reasons from the plan and PRD, not from the conversation that produced them.

### Execution phase

One fresh session per milestone.

1. Open a new Claude Code session. Copy the milestone's execution prompt from `plan.md` and paste it in.
2. `executing-from-plan` activates. It reads the plan, verifies the milestone exists and its declared dependencies are complete, suppresses planning skills for the session, confirms with one line, and hands off.
3. `test-driven-development` drives the implementation: write a failing test, watch it fail, write minimal code to pass, refactor. No production code without a failing test first.
4. `systematic-debugging` activates for any failure: root cause investigation before any fix attempt.
5. `requesting-code-review` dispatches a review subagent on completed work. `receiving-code-review` handles the response — verify before implementing, push back with technical reasoning when the suggestion is wrong.
6. `verification-before-completion` gates any completion claim. Evidence before assertions, always. No "should pass" without running the command.
7. When the milestone is complete, `finishing-a-development-branch` presents four options: merge locally, push and create a PR, keep as-is, or discard. The user chooses. The skill executes the choice and stops.
8. Open a new session for the next milestone.

## Updating and Revising Features

When a feature's design changes mid-development, all three planning skills support update and revision modes. Changes cascade from design → PRD → plan, but each step is user-driven, not automatic.

**brainstorming Revision Mode** is a focused, delta-only conversation. Instead of the full discovery flow, it asks four questions: what's changing, what's motivating the change, what stays the same, and what are the implications. It presents a change summary for explicit confirmation, updates the design file, and then asks whether the PRD needs updating. If yes, it hands off to creating-prd skill.

**creating-prd Update Mode** walks through affected PRD sections one at a time: quote the current content, propose the specific change, get approval, apply in-place. Untouched sections are left exactly as they are. A change log entry is added automatically on every save, newest-first.

**milestone-planning Update Mode** has three flows, selected by execution state. If no milestones have been executed yet, Flow A runs an in-place edit of the affected milestones. If some milestones are executed and the change affects completed work, Flow B appends a revision milestone — labeled `### Milestone N (Revision): Short name` — with a Change summary field explaining what prior work is being reworked. If the change is purely additive (new scope, no existing work affected), Flow C appends an additive milestone — `### Milestone N (Additive): Short name`. Existing milestone numbers are never renumbered. Revision and additive milestones are permanent records: once appended, they are not modified.

## Skills Library

### Planning

- **brainstorming** — Design refinement through Socratic dialogue; Create Mode for new features, Revision Mode for focused delta updates to existing designs
- **creating-prd** — Lightweight PRD from spec or rough idea; 15-section two-part structure; Create Mode and Update Mode with automatic change log
- **milestone-planning** — Decompose a feature into human-PR-reviewable milestones with self-contained execution prompts; Create Mode and Update Mode with three flows (in-place, revision, additive)

### Routing

- **executing-from-plan** — Session routing layer; intercepts milestone execution prompts, verifies plan and dependencies, suppresses planning skills, hands off to the execution toolkit

### Execution

- **test-driven-development** — Strict red-green-refactor; failing test required before any production code; no exceptions
- **systematic-debugging** — Four-phase root cause investigation before any fix; gather evidence, form a single hypothesis, test minimally
- **verification-before-completion** — Evidence before completion claims; run the command, read the output, then claim the result
- **requesting-code-review** — Dispatches a code-reviewer subagent with precisely crafted context; mandatory after major features and before merge
- **receiving-code-review** — Technical verification before implementing feedback; push back with reasoning when the suggestion is wrong; no performative agreement
- **finishing-a-development-branch** — End-of-milestone integration; four structured options (merge / PR / keep / discard); user always chooses

### Meta

- **using-mysuperpowers** — Orientation and workflow rules; bootstrapped at session start; defines skill priority and the two-phase workflow
- **writing-skills** — TDD applied to process documentation; how to write, test, and iterate skills that actually change agent behavior

## Philosophy

- **Test-driven development.** Write the test first, watch it fail, write minimal code to pass. If you didn't see the test fail, you don't know if it tests the right thing.
- **Plan then execute, in separate sessions.** Planning produces a plan file. Execution reads that file. They don't share a context window — that's intentional, not overhead.
- **Human in the loop at key checkpoints.** Design approval, PRD approval, plan approval, merge decision. The agent stops and waits at each one.
- **Update over rewrite.** Revision and additive milestones are append-only. Existing milestone numbers are never renumbered. The plan file is a record, not a scratchpad.
- **Systematic over ad-hoc.** Process skills activate before anything else. When a skill applies, it's mandatory. "This is simple" is not an exemption.

## Credits

**[obra/superpowers](https://github.com/obra/superpowers)** (MIT) — source of the skills framework pattern and the execution-phase skills (TDD, debugging, verification, code review, branch completion). This plugin would not exist without it.

**[closedloop-ai/claude-plugins](https://github.com/closedloop-ai/claude-plugins)** (MIT) — source of the PRD discovery questions, ID conventions (US-###, AC-###.#, Q-###), and "keep it light" philosophy borrowed by the creating-prd skill.

## License

MIT License — see [LICENSE](LICENSE).

## Status

This plugin is under active personal development. It is not on an official marketplace and is maintained for my own workflow. Feel free to fork or adapt it for your own use.

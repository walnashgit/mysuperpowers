# Graph Report - .  (2026-07-05)

## Corpus Check
- Corpus is ~43,976 words - fits in a single context window. You may not need a graph.

## Summary
- 165 nodes · 209 edges · 16 communities detected
- Extraction: 86% EXTRACTED · 12% INFERRED · 1% AMBIGUOUS · INFERRED: 26 edges (avg confidence: 0.76)
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- [[_COMMUNITY_Systematic Debugging|Systematic Debugging]]
- [[_COMMUNITY_Plan-Execute Workflow|Plan-Execute Workflow]]
- [[_COMMUNITY_CLAUDE.md Testing & Persuasion|CLAUDE.md Testing & Persuasion]]
- [[_COMMUNITY_Brainstorming & Code Review Requests|Brainstorming & Code Review Requests]]
- [[_COMMUNITY_Skill Authoring Best Practices|Skill Authoring Best Practices]]
- [[_COMMUNITY_TDD Anti-Patterns|TDD Anti-Patterns]]
- [[_COMMUNITY_Cross-Platform Tool Mapping|Cross-Platform Tool Mapping]]
- [[_COMMUNITY_Visual Companion Infra|Visual Companion Infra]]
- [[_COMMUNITY_Verification & Review Reception|Verification & Review Reception]]
- [[_COMMUNITY_PRD Creation & Credits|PRD Creation & Credits]]
- [[_COMMUNITY_Graph Rendering Script|Graph Rendering Script]]
- [[_COMMUNITY_UpdateRevision Flows|Update/Revision Flows]]
- [[_COMMUNITY_Condition-Based Waiting Example|Condition-Based Waiting Example]]
- [[_COMMUNITY_Helper.js Client|Helper.js Client]]
- [[_COMMUNITY_Plugin Structure & Hooks|Plugin Structure & Hooks]]
- [[_COMMUNITY_Incomplete Mocks Anti-Pattern|Incomplete Mocks Anti-Pattern]]

## God Nodes (most connected - your core abstractions)
1. `Systematic Debugging Overview / Core Principle` - 14 edges
2. `Persuasion Principles for Skill Design` - 12 edges
3. `executing-from-plan: routing layer overview` - 10 edges
4. `Writing Skills skill` - 9 edges
5. `TDD Overview / Core Principle` - 8 edges
6. `milestone-planning overview` - 8 edges
7. `Testing Skills With Subagents` - 8 edges
8. `Anthropic Skill Authoring Best Practices` - 8 edges
9. `Defense-in-Depth Validation pattern` - 7 edges
10. `Visual Companion Guide` - 7 edges

## Surprising Connections (you probably didn't know these)
- `Rationale: session boundaries intentional not ceremony` --semantically_similar_to--> `Rationale: fresh session per milestone`  [INFERRED] [semantically similar]
  skills/milestone-planning/SKILL.md → README.md
- `Skill File Format (YAML frontmatter rules)` --conceptually_related_to--> `TDD Overview / Core Principle`  [INFERRED]
  CLAUDE.md → skills/test-driven-development/SKILL.md
- `The Two-Phase Workflow (Hard Rule)` --conceptually_related_to--> `The Workflow (Planning + Execution phases)`  [INFERRED]
  CLAUDE.md → README.md
- `Execution phase steps` --references--> `Systematic Debugging Overview / Core Principle`  [EXTRACTED]
  README.md → skills/systematic-debugging/SKILL.md
- `executing-from-plan: routing layer overview` --conceptually_related_to--> `Rationale: fresh session per milestone`  [INFERRED]
  skills/executing-from-plan/SKILL.md → README.md

## Hyperedges (group relationships)
- **Debugging skill pressure-test validation suite** — pressure1_emergency_production_fix, pressure2_sunk_cost_exhaustion, pressure3_authority_social_pressure, test_academic_systematic_debugging, debugging_overview [EXTRACTED 0.90]
- **Four validation layers forming defense-in-depth** — defense_layer1_entry, defense_layer2_business, defense_layer3_environment, defense_layer4_debug, defense_in_depth [EXTRACTED 0.90]
- **Planning-to-execution handoff chain across skills** — creatingprd_overview, milestoneplanning_overview, executingfromplan_overview, readme_two_phase_workflow [INFERRED 0.85]
- **Code review request/response cycle** — requesting_code_review_skill, receiving_code_review_skill, code_reviewer_agent_template [INFERRED 0.85]
- **TDD-based skill testing and bulletproofing methodology** — writing_skills_skill, testing_skills_subagents, persuasion_principles, claude_md_testing_example [INFERRED 0.80]
- **Cross-platform tool mapping references used by mysuperpowers orientation skill** — using_mysuperpowers_skill, copilot_tools_mapping, codex_tools_mapping, gemini_tools_mapping [EXTRACTED 0.90]

## Communities

### Community 0 - "Systematic Debugging"
Cohesion: 0.09
Nodes (29): Skill File Format (YAML frontmatter rules), Skill Invocation Rules, Condition-Based Waiting technique, waitFor() generic polling implementation, Bulletproofing Elements (language & structural defenses), Source Material: Jesse's CLAUDE.md 4-phase framework, Creation Log: Systematic Debugging Skill, Testing Approach: 4 validation pressure tests (+21 more)

### Community 1 - "Plan-Execute Workflow"
Cohesion: 0.19
Nodes (20): The Two-Phase Workflow (Hard Rule), creating-prd overview, Checklist: parse, verify plan, check deps, confirm, HARD-GATE: planning skills suppressed, executing-from-plan: routing layer overview, 4 structured options: merge / PR / keep / discard, finishing-a-development-branch overview, Steps: verify tests, check uncommitted changes, determine base branch (+12 more)

### Community 2 - "CLAUDE.md Testing & Persuasion"
Cohesion: 0.12
Nodes (19): Testing CLAUDE.md Skills Documentation example, Testing Protocol (baseline/variant/pressure/meta-test), Documentation Variants (NULL/A/B/C/D), Authority principle, Cialdini, R.B. (2021) Influence: The Psychology of Persuasion, Commitment principle, Liking principle, Meincke et al. (2025) Call Me A Jerk study (+11 more)

### Community 3 - "Brainstorming & Code Review Requests"
Cohesion: 0.16
Nodes (15): Create Mode (brainstorming), creating-prd skill (external), Design doc (docs/features/<name>/<name>-design.md), milestone-planning skill (external), Revision Mode (brainstorming), Brainstorming Ideas Into Designs skill, Spec Self-Review step, Code Review Agent template (+7 more)

### Community 4 - "Skill Authoring Best Practices"
Cohesion: 0.15
Nodes (14): Anthropic Skill Authoring Best Practices, Concise is key principle, Degrees of freedom (high/medium/low), Writing effective descriptions (third person), Evaluation-driven development, Naming conventions (gerund form), Progressive disclosure patterns, Runtime environment (filesystem-based skill loading) (+6 more)

### Community 5 - "TDD Anti-Patterns"
Cohesion: 0.2
Nodes (10): Anti-Pattern 5: Integration Tests as Afterthought, Anti-Pattern 3: Mocking Without Understanding, Anti-Pattern 2: Test-Only Methods in Production, Anti-Pattern 1: Testing Mock Behavior, Compaction Policy, Compact Checkpoint after TDD cycle, TDD Iron Law: no production code without failing test, Red-Green-Refactor cycle (+2 more)

### Community 6 - "Cross-Platform Tool Mapping"
Cohesion: 0.24
Nodes (10): Environment Detection (git worktree/branch), Named agent dispatch workaround (Codex), Codex Tool Mapping, Copilot CLI Tool Mapping, No subagent support (Gemini CLI), Gemini CLI Tool Mapping, Platform Adaptation section, The Rule (invoke skills before any response) (+2 more)

### Community 7 - "Visual Companion Infra"
Cohesion: 0.22
Nodes (9): Frame template CSS classes (options, cards, mockup, pros-cons), Brainstorm Companion Frame Template (CSS/theme), Browser Events Format (JSONL), scripts/helper.js (client-side), screen_dir (content directory), scripts/start-server.sh, state_dir (events directory), scripts/stop-server.sh (+1 more)

### Community 8 - "Verification & Review Reception"
Cohesion: 0.22
Nodes (9): Compact Checkpoint, Response Pattern (READ/UNDERSTAND/VERIFY/EVALUATE/RESPOND/IMPLEMENT), Code Review Reception skill, YAGNI Check for 'Professional' Features, Verification Before Completion skill, The Gate Function (IDENTIFY/RUN/READ/VERIFY/CLAIM), Iron Law: NO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE, Verification Red Flags (+1 more)

### Community 9 - "PRD Creation & Credits"
Cohesion: 0.32
Nodes (8): Create Mode checklist and process, Discovery Questions (7 questions), ID Conventions (US-###, AC-###.#, Q-###), PRD Structure (15 sections, two parts), closedloop-ai prd-creator (external project), obra/superpowers (external project), Credits (obra/superpowers, closedloop-ai), mysuperpowers plugin overview

### Community 10 - "Graph Rendering Script"
Cohesion: 0.53
Nodes (4): combineGraphs(), extractDotBlocks(), main(), renderToSvg()

### Community 11 - "Update/Revision Flows"
Cohesion: 0.33
Nodes (6): Update Mode overview, Flow A: In-place update, Flow B: Revision milestone, Flow C: Additive milestone, Update Mode overview, Updating and Revising Features

### Community 12 - "Condition-Based Waiting Example"
Cohesion: 0.5
Nodes (0): 

### Community 13 - "Helper.js Client"
Cohesion: 0.67
Nodes (0): 

### Community 14 - "Plugin Structure & Hooks"
Cohesion: 1.0
Nodes (2): Hook Mechanics (session-start hook), Plugin Structure (directory layout)

### Community 15 - "Incomplete Mocks Anti-Pattern"
Cohesion: 1.0
Nodes (1): Anti-Pattern 4: Incomplete Mocks

## Ambiguous Edges - Review These
- `Pressure Test 1: Emergency Production Fix` → `Testing Approach: 4 validation pressure tests`  [AMBIGUOUS]
  skills/systematic-debugging/CREATION-LOG.md · relation: references
- `Testing Approach: 4 validation pressure tests` → `Academic Test: Systematic Debugging Skill`  [AMBIGUOUS]
  skills/systematic-debugging/CREATION-LOG.md · relation: references
- `Testing Approach: 4 validation pressure tests` → `Pressure Test 3: Authority + Social Pressure`  [AMBIGUOUS]
  skills/systematic-debugging/CREATION-LOG.md · relation: references

## Knowledge Gaps
- **66 isolated node(s):** `Philosophy principles`, `Plugin Structure (directory layout)`, `Hook Mechanics (session-start hook)`, `Skill Invocation Rules`, `Debugging Integration (write failing test for bugs)` (+61 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **Thin community `Plugin Structure & Hooks`** (2 nodes): `Hook Mechanics (session-start hook)`, `Plugin Structure (directory layout)`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Incomplete Mocks Anti-Pattern`** (1 nodes): `Anti-Pattern 4: Incomplete Mocks`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **What is the exact relationship between `Pressure Test 1: Emergency Production Fix` and `Testing Approach: 4 validation pressure tests`?**
  _Edge tagged AMBIGUOUS (relation: references) - confidence is low._
- **What is the exact relationship between `Testing Approach: 4 validation pressure tests` and `Academic Test: Systematic Debugging Skill`?**
  _Edge tagged AMBIGUOUS (relation: references) - confidence is low._
- **What is the exact relationship between `Testing Approach: 4 validation pressure tests` and `Pressure Test 3: Authority + Social Pressure`?**
  _Edge tagged AMBIGUOUS (relation: references) - confidence is low._
- **Why does `Requesting Code Review skill` connect `Brainstorming & Code Review Requests` to `Verification & Review Reception`, `Cross-Platform Tool Mapping`?**
  _High betweenness centrality (0.118) - this node is a cross-community bridge._
- **Why does `Code Review Reception skill` connect `Verification & Review Reception` to `Brainstorming & Code Review Requests`?**
  _High betweenness centrality (0.113) - this node is a cross-community bridge._
- **What connects `Philosophy principles`, `Plugin Structure (directory layout)`, `Hook Mechanics (session-start hook)` to the rest of the system?**
  _66 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `Systematic Debugging` be split into smaller, more focused modules?**
  _Cohesion score 0.09 - nodes in this community are weakly interconnected._
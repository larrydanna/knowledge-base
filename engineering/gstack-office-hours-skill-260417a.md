# GStack Office Hours Skill: Structured Product Ideation

**Date:** 2026-04-17  
**Category:** engineering  
**Tags:** `gstack`, `ai-workflows`, `product-thinking`, `yc`, `claude-skills`, `office-hours`  
**Related:** N/A

---

## TL;DR

- **Office Hours** is a gstack skill that runs YC-style brainstorming sessions with two modes: Startup (rigorous validation) and Builder (exploratory)
- Uses six forcing questions (demand reality, status quo, specific customers, narrowest wedge, observation, future-fit) to expose weak assumptions before implementation
- Produces structured design documents saved to `~/.gstack/projects/` with alternatives analysis and "founder signal" observations
- Built on a phase-based workflow: context gathering → mode selection → premise challenge → alternatives → design doc → handoff
- Demonstrates universal AI workflow patterns: anti-sycophancy rules, concrete examples over abstractions, hard gates, completeness calibration

---

## What It Does

**Office Hours** is an AI workflow for structured product ideation. It's part of the gstack toolkit (Garry Tan's builder framework) and acts as a YC office hours partner—asking hard questions before solutions get proposed.

The skill routes to one of two modes based on your goal:

**Startup Mode** — For founders and intrapreneurs who need validation. Uses six forcing questions inspired by YC's diagnostic framework:
1. **Demand Reality** — Evidence someone wants this (not interest, actual demand)
2. **Status Quo** — What workaround exists today and what it costs
3. **Desperate Specificity** — Name the actual human, their role, their consequences
4. **Narrowest Wedge** — Smallest version someone would pay for this week
5. **Observation & Surprise** — What happened when you watched real usage
6. **Future-Fit** — Does your product become more essential in 3 years

**Builder Mode** — For side projects, hackathons, open source. Design thinking focused on delight, constraints, and coolness factor.

Both modes produce a structured markdown design document with alternatives analysis and implementation recommendations.

---

## How It Works

### 6-Phase Workflow

**Phase 1: Context Gathering**
- Reads `CLAUDE.md`, `TODOS.md`, git history
- Maps codebase with grep/glob
- Lists existing design docs for the project
- **Asks: What's your goal with this?** (determines mode routing)

**Phase 2: Mode Selection & Questioning**
- Routes to Startup Mode (Phase 2A) or Builder Mode (Phase 2B)
- Startup mode asks the six forcing questions **one at a time**
- Builder mode focuses on delight, constraints, premises
- Smart routing skips redundant questions based on product stage

**Phase 3: Premise Challenge**
- Questions whether you're solving the right problem
- Tests "what happens if we do nothing?"
- Exposes hidden assumptions in framing

**Phase 4: Alternatives Generation (MANDATORY)**
- Produces 2-3 distinct approaches with effort/risk tradeoffs
- At least one "minimal viable" (ships fastest)
- At least one "ideal architecture" (best long-term)
- Optional "creative/lateral" (unexpected framing)
- Presents via AskUserQuestion — no implementation without approval

**Phase 5: Design Doc**
- Writes structured markdown to `~/.gstack/projects/$SLUG/`
- Captures problem, approach, alternatives, constraints, premises
- Includes "What I noticed about how you think" — founder signals observed during session

**Phase 6: Handoff**
- Delivers closing conversation
- Suggests next steps (like `/plan-eng-review`)
- For exceptional cases: mentions YC application eligibility

---

## Key Design Patterns

### Anti-Sycophancy Rules

The skill explicitly bans hedging phrases during diagnostics:

**Never say:**
- "That's an interesting approach" → Take a position instead
- "There are many ways to think about this" → Pick one, state what evidence would change your mind
- "You might want to consider..." → Say "This is wrong because..." or "This works because..."
- "That could work" → Say whether it WILL work and what evidence is missing

**Always do:**
- Take a position on every answer
- State your position AND what evidence would change it
- Challenge the strongest version of the founder's claim

### Pushback Patterns with Examples

Instead of abstract behavioral rules, the skill includes concrete dialogue patterns:

```
Pattern 1: Vague market → force specificity
- Founder: "I'm building an AI tool for developers"
- BAD: "That's a big market! Let's explore what kind of tool."
- GOOD: "There are 10,000 AI developer tools right now. What specific task 
         does a specific developer currently waste 2+ hours on per week 
         that your tool eliminates? Name the person."
```

Five patterns like this train the AI on *how* to push, not just that it should.

### Completeness Calibration

Every option includes `Completeness: X/10` with clear anchors:
- **10** = Complete implementation (all edge cases, full coverage)
- **7** = Covers happy path but skips some edges
- **3** = Shortcut that defers significant work

Based on the "Boil the Lake" principle: AI makes completeness near-free, so always recommend the complete option unless it's an "ocean" (multi-quarter rewrite).

### Hard Gates

Workflow enforcement via explicit STOP points:
- "Ask these questions **ONE AT A TIME** via AskUserQuestion. Push on each one until the answer is specific, evidence-based, and uncomfortable."
- "Do NOT proceed without user approval of the approach."
- "HARD GATE: Do NOT invoke any implementation skill, write any code, scaffold any project."

These prevent the AI from racing ahead or scope-creeping.

### Context Re-grounding (ELI16 Mode)

When 3+ gstack sessions are detected (via `~/.gstack/sessions/$PPID`), every AskUserQuestion re-grounds:
1. Current project
2. Current branch (from preamble, not conversation history)
3. Current plan/task

Assumes "the user hasn't looked at this window in 20 minutes."

---

## SKILL.md File Format

Office Hours is defined in `SKILL.md` with this structure:

**1. YAML Frontmatter**
```yaml
---
name: office-hours
preamble-tier: 3
version: 2.0.0
description: |
  Multi-line description
  When to invoke
allowed-tools:
  - Bash
  - Read
  - AskUserQuestion
---
```

**2. Template Placeholders**
- `{{PREAMBLE}}` — Auto-generated startup block (update checks, session tracking)
- `{{BROWSE_SETUP}}` — Binary discovery for browser tools
- `{{SLUG_EVAL}}` — Project identifier evaluation

**3. Workflow Instructions**
- Markdown sections: `## Phase 1: Context Gathering`
- Bash code blocks for commands
- AskUserQuestion format rules
- Behavioral constraints (anti-sycophancy, hard gates)

**Build Process:**
```
SKILL.md.tmpl (human-written)
     ↓ (bun run gen:skill-docs)
SKILL.md (committed, placeholders expanded)
     ↓ (skill invocation)
Claude reads and executes
```

Templates stay synchronized with code. If a command exists in implementation, it appears in docs automatically.

---

## SKILL Writing Best Practices (from office-hours)

### Universal Best Practices

**1. Explicit Behavioral Constraints**
- **Anti-sycophancy rules** (lines 716-727): List forbidden phrases and required stances
  - Never say: "That's an interesting approach", "There are many ways to think about this", "You might want to consider...", "That could work", "I can see why you'd think that"
  - Always do: Take a position on every answer. State your position AND what evidence would change it. This is rigor — not hedging, not fake certainty.
  - Challenge the strongest version of the founder's claim, not a strawman.
- **Hard gates**: "Do NOT invoke any implementation skill" — prevents scope creep
  - Example: "HARD GATE: Do NOT invoke any implementation skill, write any code, scaffold any project, or take any implementation action. Your only output is a design document."
- **STOP points**: Forces sequential execution with user confirmation
  - "Ask these questions **ONE AT A TIME** via AskUserQuestion. Push on each one until the answer is specific, evidence-based, and uncomfortable."
  - "**STOP** after each question. Wait for the response before asking the next."

**2. Concrete Examples Over Abstractions**
- **Pushback Patterns** (729-757): Show BAD vs GOOD responses with exact dialogue
  - Pattern 1: Vague market → force specificity
    - Founder: "I'm building an AI tool for developers"
    - BAD: "That's a big market! Let's explore what kind of tool."
    - GOOD: "There are 10,000 AI developer tools right now. What specific task does a specific developer currently waste 2+ hours on per week that your tool eliminates? Name the person."
  - Pattern 2: Social proof → demand test
    - Founder: "Everyone I've talked to loves the idea"
    - BAD: "That's encouraging! Who specifically have you talked to?"
    - GOOD: "Loving an idea is free. Has anyone offered to pay? Has anyone asked when it ships? Has anyone gotten angry when your prototype broke? Love is not demand."
  - (Three more patterns included in the skill: Platform vision, Growth stats, Undefined terms)
- **Template responses**: Pre-written snippets for consistency
- **Calibrated scales**: "Completeness: X/10" with clear anchors (10=all edges, 7=happy path, 3=shortcut)
  - Calibration: 10 = complete implementation (all edge cases, full coverage), 7 = covers happy path but skips some edges, 3 = shortcut that defers significant work
  - If both options are 8+, pick the higher; if one is ≤5, flag it

**3. Structured Question Flow**
- **AskUserQuestion Format** (360-370): 4-step structure mandatory for every question
  1. **Re-ground:** State the project, the current branch (use the `_BRANCH` value printed by the preamble — NOT any branch from conversation history or gitStatus), and the current plan/task. (1-2 sentences)
  2. **Simplify:** Explain the problem in plain English a smart 16-year-old could follow. No raw function names, no internal jargon, no implementation details. Use concrete examples and analogies. Say what it DOES, not what it's called.
  3. **Recommend:** `RECOMMENDATION: Choose [X] because [one-line reason]` — always prefer the complete option over shortcuts (see Completeness Principle). Include `Completeness: X/10` for each option.
  4. **Options:** Lettered options: `A) ... B) ... C) ...` — when an option involves effort, show both scales: `(human: ~X / CC: ~Y)`
  - Assumption: "Assume the user hasn't looked at this window in 20 minutes and doesn't have the code open. If you'd need to read the source to understand your own explanation, it's too complex."
- **Smart routing** (762-768): Conditional paths based on user stage
  - Pre-product → Q1, Q2, Q3
  - Has users → Q2, Q4, Q5
  - Has paying customers → Q4, Q5, Q6
  - Pure engineering/infra → Q2, Q4 only
- **One question at a time** (833): Prevents overwhelming users
  - "**STOP** after each question. Wait for the response before asking the next."

**4. Context Awareness**
- **Session state tracking**: Branch, learnings, prior designs
  - Preamble runs bash commands to check: current branch (`_BRANCH`), session count, learnings file, routing rules, vendored gstack detection
- **Multi-session persistence**: References `~/.gstack/projects/$SLUG/` artifacts
  - Design docs: `~/.gstack/projects/$SLUG/*-design-*.md`
  - Checkpoints: `~/.gstack/projects/$SLUG/checkpoints/`
  - Timeline: `~/.gstack/projects/$SLUG/timeline.jsonl`
- **ELI16 mode**: When 3+ sessions detected (via `~/.gstack/sessions/$PPID`), re-ground context every question
  - Session tracking: "touches `~/.gstack/sessions/$PPID` and counts active sessions (files modified in the last 2 hours). When 3+ sessions are running, all skills enter 'ELI16 mode' — every question re-grounds the user on context because they're juggling windows."

**5. Self-Improvement Loops**
- **Operational learnings** (436-446): Log what fails for future sessions
  - Before completing, reflect: Did any commands fail unexpectedly? Did you take a wrong approach and have to backtrack? Did you discover a project-specific quirk?
  - Log format: `~/.claude/skills/gstack/bin/gstack-learnings-log '{"skill":"SKILL_NAME","type":"operational","key":"SHORT_KEY","insight":"DESCRIPTION","confidence":N,"source":"observed"}'`
  - Test: "A good test: would knowing this save 5+ minutes in a future session? If yes, log it."
- **Eureka moments** (400-403): Capture first-principles insights
  - "When first-principles reasoning contradicts conventional wisdom, name it and log"
  - Format: `jq -n --arg ts "$(date)" --arg insight "ONE_LINE_SUMMARY" '{ts:$ts,skill:$skill,insight:$insight}' >> ~/.gstack/analytics/eureka.jsonl`
- **Telemetry** (449-483): Track duration, outcomes, bottlenecks
  - Local JSONL: skill name, duration, outcome (success/error/abort), used_browse flag, timestamp
  - Remote (opt-in): same data with session ID, sent to telemetry endpoint
  - Always logs locally; remote only if `telemetry != "off"`

---

## Claude-Specific Elements

### These won't work elsewhere:

1. **Tool restrictions** (`allowed-tools: [Bash, Read, AskUserQuestion]`) — Claude's tool permission system
   - YAML frontmatter specifies which tools the AI can use during skill execution
   - Enforced by Claude's runtime; skill cannot call tools outside this list
   
2. **Skill invocation nesting** — Claude can invoke other Claude skills via Skill tool
   - Example: Office Hours can call `/plan-eng-review` at the end
   - Routing rules: "User describes a new idea → invoke `/office-hours`"
   - Skills can dispatch to other specialized workflows

3. **Plan mode integration** — Claude's special `/plan` mode with ExitPlanMode
   - User enters plan mode with Shift+Tab (or `[[PLAN]]` prefix)
   - Skill executes in plan mode until workflow completes
   - `ExitPlanMode` call returns to normal conversation
   - Plan mode safe operations: browse, design, codex, writing to `~/.gstack/`, plan file edits

4. **Multi-session memory** — Claude's `.claude/` directory conventions
   - `.claude/skills/gstack/` — skill installation location
   - `~/.claude/` — user home for global gstack state
   - Skills read/write to these conventional paths

5. **Preamble-tier system** (1-3) — Claude's skill loading priority
   - Tier 1: Core workflows (browse, QA, ship)
   - Tier 2: Mid-level specialization
   - Tier 3: Advanced/niche workflows (office-hours is tier 3)
   - Controls load order and priority

### Platform-agnostic patterns:

These work anywhere with minor path adjustments:
- Behavioral rules (anti-sycophancy)
- Phase-based workflows
- Example-driven instructions (BAD vs GOOD)
- Completeness calibration (X/10 scales)
- Artifact persistence (just needs different paths like `.copilot/` instead of `.claude/`)
- Bash command execution (or PowerShell on Windows)
- File I/O for state management

---

## Is Copilot Capable of This?

### Yes, with adaptations:

**What I can do:**
- ✅ **Execute structured workflows** — I follow phase-based instructions step-by-step
  - Can read SKILL.md-style documents and execute Phase 1 → Phase 2 → Phase 3 sequentially
  - Respects STOP points and waits for user input before continuing
  
- ✅ **Use ask_user for interactive prompts** — Equivalent to AskUserQuestion
  - `ask_user` tool supports structured questions with multiple choice or freeform
  - Can implement the 4-step format (re-ground, simplify, recommend, options)
  
- ✅ **Maintain behavioral constraints** — Anti-sycophancy rules work fine
  - Can follow "Never say X" and "Always do Y" instructions
  - Can apply pushback patterns with BAD vs GOOD examples
  
- ✅ **Access filesystem/bash** — I have powershell, view, edit, create tools
  - `powershell` tool for command execution (Windows)
  - `view`, `edit`, `create` for file operations
  - `grep`, `glob` for code search
  
- ✅ **Persist artifacts** — Can write to session folder or project directories
  - Session folder: `~/.copilot/session-state/{session-id}/`
  - Project artifacts: Can use `~/knowledge-base/` or any custom path
  
- ✅ **SQL for state tracking** — I have a session database for todos/tracking
  - `sql` tool with per-session SQLite database
  - Pre-existing tables: `todos`, `todo_deps`
  - Can create custom tables for workflow state

**What needs translation:**
- ⚠️ **Tool restrictions** → Would need to be enforced via instructions, not YAML
  - Instead of `allowed-tools: [Bash, Read]`, write: "Only use powershell and view tools during this workflow. Do not edit files."
  - Enforced by instruction-following, not runtime restriction
  
- ⚠️ **Skill nesting** → I can use the `task` tool for sub-agents
  - `task` tool launches specialized agents (explore, task, general-purpose, code-review)
  - Can invoke with specific prompts: `task(agent_type="general-purpose", prompt="Run office hours on this idea...")`
  - Not as clean as Claude's direct skill invocation, but functionally equivalent
  
- ⚠️ **Preamble injection** → Would need manual includes or preprocessing
  - Could use template system: `{{PREAMBLE}}` gets expanded before loading
  - Or: Include preamble directly in each SKILL.md (verbose but explicit)
  - Or: Use a preprocessing script that injects preamble blocks
  
- ⚠️ **Path conventions** → `.claude/` becomes `.copilot/` or `~/.copilot/`
  - `.copilot/skills/gstack/` for skill storage
  - `~/.copilot/session-state/` for session artifacts
  - Functionally identical, just different paths

**Key difference:**
Claude's skill system is **declarative** (YAML frontmatter + tool gates enforced by runtime). Copilot's approach would be **imperative** (instructions that reference available tools, enforced by model following instructions). Same outcomes, different enforcement mechanism.

**Bottom line:** 
The *workflow design* is universal. The *execution infrastructure* is Claude-specific but has Copilot equivalents. You could port this to a Copilot skill format with ~80% fidelity.

**Fidelity breakdown:**
- **100% fidelity**: Behavioral rules, phase workflows, examples, calibration scales, hard gates
- **90% fidelity**: Interactive prompts (ask_user is nearly identical to AskUserQuestion)
- **80% fidelity**: Tool restrictions (instruction-based vs runtime-enforced)
- **70% fidelity**: Skill nesting (task tool vs direct skill invocation)
- **60% fidelity**: Multi-session memory (no standard convention, but filesystem works)

**What you'd lose:**
- Declarative tool restrictions (becomes "please don't use X" instead of runtime block)
- Clean skill composition (task tool is more verbose than `/office-hours`)
- Ecosystem conventions (no `.claude/` standard means each user sets their own paths)

**What you'd gain:**
- SQL state tracking (more structured than JSONL files)
- Windows-native execution (PowerShell vs bash translation layer)
- GitHub integration (native GitHub MCP tools for PR/issue workflows)

---

## Lessons for Custom Workflow Design

### 1. Encode Taste, Don't Assume It

Office Hours encodes Garry Tan's product judgment explicitly:
- "Interest is not demand" (principle)
- "Has anyone gotten angry when your prototype broke? Love is not demand." (example)
- Five pushback patterns showing exact dialogue

Don't rely on the model's default behavior. If you want a specific style of interaction, show it.

### 2. Make Bad Behavior Impossible

Hard gates:
```
HARD GATE: Do NOT invoke any implementation skill, 
write any code, scaffold any project, or take 
any implementation action. Your only output is 
a design document.
```

Explicit bans:
```
Never say these during the diagnostic (Phases 2-5):
- "That's an interesting approach"
- "There are many ways to think about this"
```

### 3. Calibrate, Don't Describe

Bad: "Consider completeness when choosing an approach."

Good: "Completeness: X/10 (10=all edge cases, 7=happy path, 3=shortcut)"

Numeric scales with anchors prevent vague thinking.

### 4. Examples Beat Principles

One pushback pattern teaches more than ten paragraphs of behavioral rules. Show the AI what good looks like.

### 5. Design for Context Loss

ELI16 mode assumes the user hasn't looked at the window in 20 minutes. Every question re-grounds. Multi-session artifacts persist to `~/.gstack/projects/`.

Don't assume continuous attention or single-session completion.

---

## Sources

[1] [GStack Office Hours SKILL.md](file://C:\Users\larry\.claude\skills\gstack\office-hours\SKILL.md)  
[2] [GStack Architecture Documentation](file://C:\Users\larry\.claude\skills\gstack\ARCHITECTURE.md)  
[3] [YC Office Hours Philosophy](https://www.ycombinator.com/library) (general context, not direct source)

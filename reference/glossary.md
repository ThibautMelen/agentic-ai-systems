<div align="center">

[🏠 Home](../README.md) › [📖 Reference](./) › **Glossary A-Z**

[← Reference](./) ━━●━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ [Visual Standards →](visual-standards.md)

</div>

---

# Glossary A-Z

> Complete cross-reference of all agentic terminology

---

## A

**ACI (Agent-Computer Interface)**
: The design layer between AI agents and computer tools. Coined by Anthropic, emphasizing that tool interfaces should be optimized for agent ergonomics (clear documentation, error handling, output structure) not just human usability (HCI).
: *Also known as:* Tool Interface, Agent Tooling Layer

**AGENTS.md**
: Repo-level instruction file read natively by most 2026 harnesses (Codex, Copilot, Cursor, Gemini CLI, goose, Zed, Warp, opencode…) — the "instructions" layer of the de-facto config stack. Claude Code reads CLAUDE.md instead. See [What Changed 2026](../foundations/what-changed-2026.md).
: *Spec:* [agents.md](https://agents.md/)

**Agent**
: ⚠️ **Ambiguous term** — can mean:
: 1. **Generic:** Any autonomous AI system (Main Agent, Subagent)
: 2. **Anthropic Pattern #6:** System where LLMs **dynamically direct their own processes** (🐔 Autonomous Agent)
: In Claude Code, the 🐔 Main Agent orchestrates all operations. Contrast Agents (pattern) with Workflows.
: *See also:* Main Agent, Subagent, 🐔 Autonomous Agent

**Agentic Systems**
: Umbrella term for any system using LLMs with tool-calling and control flow. Encompasses both Workflows (predefined orchestration) and Agents (dynamic direction).
: *Also known as:* Agentic Architecture, Autonomous Systems

**AskUserQuestion**
: Tool for human-in-the-loop interactions. Presents structured questions with options to the user. Key component of Wizard Workflows.

```python
AskUserQuestion(questions=[{
    "header": "Confirm",
    "question": "Proceed with migration?",
    "options": [
        {"label": "Yes", "description": "Continue"},
        {"label": "No", "description": "Cancel"}
    ]
}])
```

**🐔 Autonomous Agent**
: An agent that independently plans, executes, and adapts without constant human guidance. The only true "Agent" pattern in Anthropic's taxonomy (vs Workflows).
: *Also known as:* Self-Directed Agent, True Agent

**Augmented LLM**
: The 🦄 Building Block — foundation for all agentic systems. An LLM enhanced with retrieval (RAG/docs), tools (actions), and memory (context persistence).
: *Also known as:* 🦄 Building Block, Enhanced LLM, Tooled LLM
: *See also:* Building Block

**agentId**
: Unique identifier assigned to each subagent execution. Used with `resume` parameter to continue a previous subagent conversation. Agent transcripts are stored as `agent-{agentId}.jsonl`.
: *See also:* resume, Resumable Subagents

---

## B

**🦄 Building Block**
: Anthropic's term for the **Augmented LLM** — the foundational unit of all agentic systems. An LLM enhanced with retrieval, tools, and memory.
: ⚠️ **Not to be confused with:** Claude Code Components (Subagent, Slash Command, Skill, Hook) which are abstractions built ON TOP of the building block.
: *See also:* Augmented LLM
: *See also:* [Building Block Pattern](../foundations/augmented-llm.md)

**Built-in Subagents**
: Pre-configured subagents available out of the box in Claude Code.
: *See:* [Built-in Subagents Reference](built-in-subagents.md)

---

## C

**Checkpointing**
: Saving workflow state to enable resume after interruption. Key mechanism of Multi-Window Context pattern.

**CLAUDE.md**
: Project instruction file loaded automatically by Claude Code. Part of the State Layer.

**Component**
: Claude Code abstractions for organizing agent capabilities: 🐦 Subagent, 🦴 Slash Command, 📚 Skill, 🪝 Hook.
: ⚠️ **Not to be confused with:** 🦄 Building Block (Anthropic's Augmented LLM concept).

**Context Management**
: Automatic compaction and context management to ensure agents don't run out of context. Core capability of Claude Agent SDK.

---

## D

**Context Engineering**
: The 2026 umbrella discipline that absorbed prompt engineering: treat the context window as a budget — compaction, just-in-time retrieval, memory files, sub-agents as context isolation. Coined canonical by Anthropic (Sept 2025).
: *See:* [What Changed 2026](../foundations/what-changed-2026.md)

**Delegation Layer**
: Layer 3 in the architecture. Contains Slash Commands and Skills that define workflows and capabilities.
: *See:* [Delegation Layer](../implementation/architecture/03-delegation-layer.md)

**🏎️ Direct Execution (Baseline)**
: The foundation - single augmented LLM call with no orchestration. Pattern #0 in our taxonomy. Fastest execution path.

---

## E

**🩻 Evaluator-Optimizer**
: Anthropic pattern for iterative improvement through generate-evaluate-feedback loops.
: *See:* [Evaluator-Optimizer Pattern](../workflows/05-evaluator-optimizer.md)

**Execution Layer**
: Layer 4 in the architecture. Where Subagents and Tools perform actual work.
: *See:* [Execution Layer](../implementation/architecture/04-execution-layer.md)

---

## H

**Harness**
: The loop *around* the model: tool plumbing, permissioning, budgets, retries, verification. "Harness engineering" became the 2026 job title for making long-running agents reliable.
: *See:* [What Changed 2026](../foundations/what-changed-2026.md)

**Hook**
: Shell command or prompt triggered by Claude Code events. Types: `command` (shell) or `prompt` (LLM-based).

```json
{
  "hooks": {
    "PostToolUse": [{
      "matcher": "Write",
      "hooks": [{ "type": "command", "command": "npm run lint" }]
    }]
  }
}
```

: *See:* [Hook Component](../implementation/components/hook.md)

**Human-in-the-Loop**
: Design pattern where human approval/input is required at key points. Implemented via AskUserQuestion in Wizard Workflows.

**Hook Events**
: Lifecycle events that trigger hooks. Official events: `PreToolUse`, `PostToolUse`, `PermissionRequest`, `UserPromptSubmit`, `Stop`, `SubagentStop`, `PreCompact`, `SessionStart`, `SessionEnd`, `Notification`.

---

## L

**Layer**
: One of 5 architectural levels: User, Main Agent, Delegation, Execution, State.

---

## M

**Main Agent**
: The central Claude Code agent that orchestrates all operations. Only entity that can spawn Subagents.

**Main Agent Layer**
: Layer 2 in the architecture. The orchestration center.

**🧬 Master-Clone**
: Claude Code pattern for spawning multiple isolated subagents handling independent domains. Variant of 🛤️ Parallelization.
: *See:* [Master-Clone in Parallelization](../workflows/03-parallelization.md#variant--master-clone)

**MCP (Model Context Protocol)**
: The de-facto protocol for giving agents tools/resources. Registry live since Sept 2025; `.mcpb` bundles; the 2026-07-28 spec makes the core stateless and deprecates sampling/roots/logging. Governed by the Agentic AI Foundation (Linux Foundation) since Dec 2025.
: *See:* [What Changed 2026](../foundations/what-changed-2026.md)

**Model-invoked**
: Capability (like Skills) that Claude autonomously decides when to use based on context. Contrast with User-invoked (Slash Commands).

**🖥️ Multi-Window Context**
: Claude Code pattern for checkpointing and resuming long workflows. Implementation of 🐔 Autonomous Agent.
: *See:* [Multi-Window Context](../agents/multi-window.md)

---

## O

**Orchestrator**
: The coordinating entity in Orchestrator-Workers pattern. In Claude Code, this is the Main Agent.

**Orchestrator-Workers**
: Anthropic pattern where a central orchestrator delegates to specialized workers.

---

## P

**🚂 Parallel Tool Calling**
: Claude Code pattern for executing multiple independent tool calls in a single message. Variant of 🛤️ Parallelization.

```python
# Single message, parallel execution
[
    Read(file_path="file1.ts"),
    Read(file_path="file2.ts"),
    Grep(pattern="TODO")
]
```

**🛤️ Parallelization**
: Anthropic pattern for executing independent tasks simultaneously.

**Pattern**
: A reusable solution to a common agentic system design problem.

**Permission Modes**
: Subagent tool permission control. Values: `default`, `acceptEdits`, `bypassPermissions`, `plan`, `ignore`.

| Mode | Behavior |
|------|----------|
| `default` | Asks permission for each tool |
| `acceptEdits` | Auto-approves Write/Edit |
| `bypassPermissions` | All tools auto-approved |
| `plan` | Read-only planning mode |
| `ignore` | Skip permission prompts |

**📚 Progressive Skills**
: Claude Code mechanism for loading capabilities on-demand based on task context. Implementation of 🚦 Routing.

**🎛️ Programmatic Orchestration**
: Claude Code mechanism where external code (Agent SDK) controls agent invocation and workflow.

**⛓️ Prompt Chaining**
: Anthropic pattern for sequential execution where each step feeds the next.

**Prompt-based Hook**
: Hook using `type: "prompt"` for LLM evaluation (via Haiku) instead of bash command. Supports context-aware decisions.

---

## R

**resume**
: Parameter for the Task tool that allows continuing a previous subagent conversation. Pass the `agentId` from a previous execution to maintain context.
: *See also:* agentId, Resumable Subagents

**🚦 Routing**
: Anthropic pattern for directing inputs to specialized handlers based on classification.
: *See:* [Routing Pattern](../workflows/02-routing.md)

**Resumable Subagents**
: Subagents that can be resumed via `resume` parameter to continue previous conversations using their `agentId`. Agent transcripts are stored in project directory as `agent-{agentId}.jsonl`.

```python
# Resume with previous context
Task(
    subagent_type="code-analyzer",
    prompt="Now analyze authorization logic",
    resume="abc123"  # agentId from previous execution
)
```

---

## S

**SKILL.md (Agent Skills)**
: Progressive-disclosure procedure folders for agents — open spec since Dec 2025 ([agentskills.io](https://agentskills.io/specification)), adopted by 30+ platforms. The "procedures" layer of the config stack; this repo's [Skill](../implementation/components/skill.md) page covers the Claude Code implementation.

**Sectioning**
: Sub-variant of 🛤️ Parallelization where tasks are split into independent subtasks processed concurrently. Focus on task decomposition.
: *Also known as:* Task Splitting, Parallel Decomposition
: *Claude Code:* Parallel Tool Calling, Master-Clone

**Session Management**
: Resume and fork capabilities for maintaining conversation context across sessions. Core feature of Claude Agent SDK.

**📚 Skill**
: Reusable methodology/capability that enhances agent behavior. Model-invoked (Claude decides when to use). Located in `.claude/skills/*/SKILL.md`.

```bash
.claude/skills/test-driven-development/
└── SKILL.md   # Contains description + instructions
```

> Skill name from directory name. Frontmatter: `name` (optional, max 64 chars), `description` (required, max 1024 chars), `allowed-tools` (optional, restricts tool access).

: *See:* [Skill Component](../implementation/components/skill.md)

**Slash Command**
: User-invokable workflow starting with `/`. Located in `.claude/commands/*.md`.

```markdown
# .claude/commands/generate.md
---
description: Generate localization files
argument-hint: [locale]
---
```

> Command name from filename. Supported: `description`, `argument-hint`, `allowed-tools`, `model`, `disable-model-invocation`.

**State Layer**
: Layer 5 in the architecture. Handles persistence, memory, and context.

**Subagent**
: Specialized agent 🪺 spawned via Task tool. Cannot spawn other subagents. Located in `.claude/agents/*.md`.

```markdown
# .claude/agents/reviewer.md
---
name: code-reviewer
description: Expert code review specialist
tools: Read, Grep, Glob
---
```

> `tools` is a comma-separated string. `description` is required.

: *See:* [Subagent Component](../implementation/components/subagent.md)

**🦑 Orchestrator-Workers (Claude Code)**
: Anthropic pattern where a central orchestrator delegates to specialized workers. In Claude Code, the 🐔 Main Agent spawns 🐦 Subagents via the Task tool.

---

## T

**Task tool (🪺 spawn)**
: The mechanism for 🪺 spawning Subagents.

```python
Task(
    subagent_type="code-reviewer",
    prompt="Review auth module"
)
```

**TodoWrite**
: Tool for task tracking and progress visibility.

**Tool**
: Executable capability (Read, Write, Bash, Grep, etc.) available to agents.

---

## U

**User Layer**
: Layer 1 in the architecture. Entry point for all human interactions.

**User-invoked**
: Capability explicitly triggered by user (like Slash Commands with `/`). Contrast with Model-invoked (Skills).

---

## V

**Voting**
: Sub-variant of 🛤️ Parallelization where multiple instances run the same task and a consensus mechanism selects the best result. Focus on quality/reliability.
: *Also known as:* Consensus Mechanism, Redundant Execution
: *Use case:* Critical decisions, validation, diverse perspectives

---

## W

**🧙 Wizard Workflows**
: Claude Code pattern for multi-step processes with explicit user confirmation at each phase. Implementation of Human-in-the-Loop.
: *See:* [Wizard Workflow in Prompt Chaining](../workflows/01-prompt-chaining.md#variant--wizard-workflows)

**Worker**
: Specialized executor in Orchestrator-Workers pattern. In Claude Code, these are Subagents.

**Workflow**
: Anthropic official term for agentic systems where LLMs are orchestrated through **predefined code paths**. Includes 5 patterns: Prompt Chaining, Routing, Parallelization, Orchestrator-Workers, Evaluator-Optimizer.
: *Contrast with:* Agent (dynamic self-direction)
: *Also known as:* Orchestration Pattern, Predefined Pipeline

---

<div align="center">

[← Reference](./) ━━●━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ [Visual Standards →](visual-standards.md)

</div>

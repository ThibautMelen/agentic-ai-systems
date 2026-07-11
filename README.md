<div align="center">

# Agentic AI Systems 🐔

**Agentic systems explained with chickens — because AI orchestration doesn't have to be scary**

*Main Agent spawns Subagents like a hen with her chicks 🐔🪺🐦*

[![patterns proven](https://github.com/ThibautMelen/agentic-ai-systems/actions/workflows/check.yml/badge.svg)](https://github.com/ThibautMelen/agentic-ai-systems/actions/workflows/check.yml)
[![Claude Code](https://img.shields.io/badge/Claude_Code-CLI-8b5cf6?style=flat-square&logo=anthropic&logoColor=white)](https://docs.anthropic.com/en/docs/claude-code)
[![Anthropic Research](https://img.shields.io/badge/Anthropic-Research-ec4899?style=flat-square&logo=anthropic&logoColor=white)](https://www.anthropic.com/research/building-effective-agents)
[![SuperNovae](https://img.shields.io/badge/SuperNovae-Studio-ff6b35?style=flat-square&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0xMiAyTDkgOUwyIDEyTDkgMTVMMTIgMjJMMTUgMTVMMjIgMTJMMTUgOVoiLz48L3N2Zz4=)](https://github.com/SuperNovae-studio)
[![Awesome](https://awesome.re/mentioned-badge-flat.svg)](https://github.com/hesreallyhim/awesome-claude-code)
[![License](https://img.shields.io/badge/License-MIT-10b981?style=flat-square)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-06b6d4?style=flat-square)](CONTRIBUTING.md)
[![Mermaid](https://img.shields.io/badge/Mermaid-Diagrams-f59e0b?style=flat-square&logo=mermaid&logoColor=white)](https://mermaid.js.org/)

[🦄 Foundations](foundations/) • [⚙️ Workflows](workflows/) • [🐔 Autonomous](agents/) • [📜 As Code](patterns-as-code/) • [🛠️ Implementation](implementation/) • [🗺️ Guides](guides/)

</div>

---

## Overview

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#8b5cf6', 'primaryTextColor': '#fff', 'primaryBorderColor': '#7c3aed', 'lineColor': '#a78bfa', 'secondaryColor': '#ec4899', 'tertiaryColor': '#6366f1', 'noteTextColor': '#fff', 'noteBkgColor': '#8b5cf6', 'textColor': '#fff' }}}%%
mindmap
  root((🐔 Agentic Systems))
    🦄 Foundations
      Augmented LLM
      What Changed 2026
    ⚙️ Workflows
      🏎️ Baseline
      ⛓️ Chaining
      🚦 Routing
      🛤️ Parallel
      🦑 Orchestrator
      🩻 Evaluator
    🐔 Autonomous Agent
      The Alternative
      Multi-Window
    🛠️ Implementation
      🐦 Subagent
      🦴 Command
      📚 Skill
      🪝 Hook
    📜 Patterns as Code
      Check before
      Trace after
```

---

> [!TIP]
> **New in the 2026 edition** — [🗞️ What Changed 2025-2026](foundations/what-changed-2026.md) (the dated map: context engineering, the multi-agent debate, the AGENTS.md · SKILL.md · MCP stack, harness engineering) and [📜 Patterns as Code](patterns-as-code/) (every pattern as a runnable file — checked in CI on every push, no API key needed).

<p align="center">
  <a href="patterns-as-code/"><img src="https://raw.githubusercontent.com/supernovae-st/nika/main/media/gifs/chat-to-workflow.optimized.gif" alt="A repeated chat prompt becomes a workflow file; checked before a token is spent, then a real local run — the patterns in this repo, as runnable files" width="850"></a>
</p>
<p align="center"><sub>⬆️ real capture: a repeated prompt graduates into a checked, runnable file — <a href="patterns-as-code/">every pattern in this repo works this way</a> · and <a href="patterns-as-code/real-world/">three of them run a real campaign daily</a> 🛰️</sub></p>

## 🗺️ Navigation

<table>
<tr>
<td width="50%" valign="top">

### 🦄 [Foundations](foundations/)
*The building block for everything*

| | |
|---|---|
| [🦄 Augmented LLM](foundations/augmented-llm.md) | LLM + Retrieval + Tools + Memory |
| [🗞️ What Changed 2025-2026](foundations/what-changed-2026.md) | Context engineering · skills/MCP stack · harness era |

---

### ⚙️ [Workflows](workflows/)
*Predefined orchestration — code controls the flow*

| # | Workflow | Use When |
|:-:|----------|----------|
| 0 | [🏎️ Baseline](workflows/00-baseline.md) | Simple, 1-step task |
| 1 | [⛓️ Prompt Chaining](workflows/01-prompt-chaining.md) | Sequential steps |
| 2 | [🚦 Routing](workflows/02-routing.md) | Classify & dispatch |
| 3 | [🛤️ Parallelization](workflows/03-parallelization.md) | Independent tasks |
| 4 | [🦑 Orchestrator](workflows/04-orchestrator-workers.md) | Expert delegation |
| 5 | [🩻 Evaluator](workflows/05-evaluator-optimizer.md) | Quality iteration |

</td>
<td width="50%" valign="top">

### 🐔 [Autonomous Agent](agents/)
*Dynamic autonomy — LLM controls the flow*

| Pattern | Use When |
|---------|----------|
| [🐔 Autonomous Agent](agents/autonomous.md) | Open-ended problems |
| [🖥️ Multi-Window](agents/multi-window.md) | Cross-session state (variant) |

---

### 🛠️ [Implementation](implementation/)
*Claude Code components & architecture*

| Component | Location |
|-----------|----------|
| [🐦 Subagent](implementation/components/subagent.md) | `.claude/agents/*.md` |
| [🦴 Command](implementation/components/slash-command.md) | `.claude/commands/*.md` |
| [📚 Skill](implementation/components/skill.md) | `.claude/skills/*/SKILL.md` |
| [🪝 Hook](implementation/components/hook.md) | `.claude/settings.json` |

---

### 🗺️ [Guides](guides/) & [📖 Reference](reference/)

| Resource | Description |
|----------|-------------|
| [Selection Guide](guides/README.md) | Choose the right pattern |
| [📜 Patterns as Code](patterns-as-code/) | Every pattern as a runnable, checkable file |
| [Use Cases](guides/use-cases/) | 6 validated examples |
| [Glossary](reference/glossary.md) | A-Z definitions |
| [Visual Standards](reference/visual-standards.md) | Colors & emojis |

</td>
</tr>
</table>

---

## Quick Decision

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    START((🎯 Task)) --> DEST{Destructive?}
    DEST -->|Yes| WIZ[🧙 Wizard]
    DEST -->|No| COMP{Complex?}
    COMP -->|No| BASE[🏎️ Baseline]
    COMP -->|Yes| PRED{Predictable<br/>steps?}
    PRED -->|Yes| WORK{Need<br/>specialists?}
    PRED -->|No| AGENT[🐔 Autonomous]
    WORK -->|No| CHAIN[⛓️ Chain]
    WORK -->|Yes| ORCH[🦑 Orchestrator]

    classDef default fill:#f8fafc,stroke:#64748b,stroke-width:1px,color:#1e293b
    classDef decision fill:#fef3c7,stroke:#f59e0b,stroke-width:2px,color:#92400e
    classDef baseline fill:#64748b,stroke:#475569,stroke-width:2px,color:#ffffff
    classDef wizard fill:#14b8a6,stroke:#0d9488,stroke-width:2px,color:#ffffff
    classDef workflow fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef agent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff

    START:::decision
    DEST:::decision
    COMP:::decision
    PRED:::decision
    WORK:::decision
    BASE:::baseline
    WIZ:::wizard
    CHAIN:::workflow
    ORCH:::workflow
    AGENT:::agent
```

| Situation | → Use |
|-----------|-------|
| Simple task (1 step) | [🏎️ Baseline](workflows/00-baseline.md) |
| Sequential (2-4 steps) | [⛓️ Prompt Chaining](workflows/01-prompt-chaining.md) |
| Categorize inputs | [🚦 Routing](workflows/02-routing.md) |
| Independent subtasks | [🛤️ Parallelization](workflows/03-parallelization.md) |
| Multiple specialists | [🦑 Orchestrator-Workers](workflows/04-orchestrator-workers.md) |
| Quality iteration | [🩻 Evaluator-Optimizer](workflows/05-evaluator-optimizer.md) |
| Open-ended / unknown steps | [🐔 Autonomous Agent](agents/autonomous.md) |
| Destructive operations | [🧙 Wizard](workflows/01-prompt-chaining.md#advanced-wizard-pattern) |
| Long-running (>10 min) | [🖥️ Multi-Window Context](agents/multi-window.md) |

---

## Anthropic Taxonomy

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    subgraph WORKFLOWS["⚙️ WORKFLOWS"]
        direction TB
        W1[🏎️ Baseline]
        W2[⛓️ Prompt Chaining]
        W3[🚦 Routing]
        W4[🛤️ Parallelization]
        W5[🦑 Orchestrator]
        W6[🩻 Evaluator]
    end

    subgraph AGENTS["🐔 AUTONOMOUS AGENT"]
        direction TB
        A1[🐔 The Alternative]
        A2[🖥️ Multi-Window variant]
    end

    CODE[📝 Code controls] --> WORKFLOWS
    WORKFLOWS --> LLM[🧠 LLM controls]
    LLM --> AGENTS

    classDef workflowBox fill:#ede9fe,stroke:#8b5cf6,stroke-width:2px,color:#5b21b6
    classDef agentBox fill:#fce7f3,stroke:#ec4899,stroke-width:2px,color:#9d174d
    classDef control fill:#f1f5f9,stroke:#64748b,stroke-width:1px,color:#475569

    WORKFLOWS:::workflowBox
    AGENTS:::agentBox
    CODE:::control
    LLM:::control
```

> **Key distinction:** Workflows have predefined paths (code controls). Agents decide their own path (LLM controls).

---

## Critical Rule

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    U1[🙋‍♀️ User] -->|request| MA[🐔 Main Agent]
    MA -->|🪺 spawn| SA1[🐦 Subagent]
    MA -->|🪺 spawn| SA2[🐦 Subagent]
    SA1 -->|result| MA
    SA2 -->|result| MA
    MA -->|response| U2[💁‍♀️ User]

    SA1 x--x|"❌ CANNOT spawn"| SA3[🐦]

    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff
    classDef sub fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff
    classDef blocked fill:#ef4444,stroke:#dc2626,stroke-width:2px,color:#ffffff,stroke-dasharray: 5 5

    U1:::user
    U2:::user
    MA:::main
    SA1:::sub
    SA2:::sub
    SA3:::blocked
```

> **🐦 Subagents cannot spawn other 🐦 subagents.** All delegation flows through 🐔 Main Agent.

---

## Repository Structure

```
.
├── README.md                      # 🏠 You are here
│
├── foundations/                   # 🦄 Core concepts
│   └── augmented-llm.md
│
├── workflows/                     # ⚙️ Predefined orchestration
│   ├── 00-baseline.md
│   ├── 01-prompt-chaining.md
│   ├── 02-routing.md
│   ├── 03-parallelization.md
│   ├── 04-orchestrator-workers.md
│   └── 05-evaluator-optimizer.md
│
├── agents/                        # 🐔 Autonomous Agent (the alternative)
│   ├── autonomous.md              # The pattern
│   └── multi-window.md            # Variant
│
├── implementation/                # 🛠️ Claude Code specifics
│   ├── components/                # 🐦🦴📚🪝
│   └── architecture/              # 5-layer system
│
├── guides/                        # 🗺️ Selection & use cases
│   └── use-cases/                 # 6 validated examples
│
└── reference/                     # 📖 Glossary, standards
```

---

## References

| Resource | Link |
|----------|------|
| Building Effective Agents | [anthropic.com/engineering](https://www.anthropic.com/engineering/building-effective-agents) |
| Claude Code Docs | [docs.anthropic.com](https://docs.anthropic.com/en/docs/claude-code) |
| Agent SDK | [docs.anthropic.com/agent-sdk](https://docs.anthropic.com/docs/en/agent-sdk) |
| Anthropic Cookbook | [github.com/anthropics](https://github.com/anthropics/anthropic-cookbook) |
| Agent Skills spec | [agentskills.io](https://agentskills.io/specification) |
| Agentic AI Foundation (MCP · AGENTS.md · goose) | [aaif.io](https://aaif.io/) |
| Patterns as runnable files (this repo) | [patterns-as-code/](patterns-as-code/) |

---

## Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md).

**Requirements:** Official sources • Code examples • Mermaid diagrams • Established format

---

<div align="center">

<sub>Built with Claude Code | Based on Anthropic documentation | 2025-2026</sub><br/>
<sub>Independent community resource — not affiliated with Anthropic</sub>

<br/>

<a href="https://github.com/ThibautMelen">
  <img src="https://avatars.githubusercontent.com/u/20891897?s=200&v=4" alt="ThibautMelen" width="32"/>
</a>
&nbsp;❤️&nbsp;
<a href="https://github.com/SuperNovae-studio">
  <img src="https://avatars.githubusercontent.com/u/33066282?s=200&v=4" alt="SuperNovae Studio" width="32"/>
</a>
&nbsp;🏴‍☠️

</div>

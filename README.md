<div align="center">

# Agentic AI Systems 🐔

**Design patterns for building agentic AI systems | Explained simply**

<sub>Mermaid diagrams 📊 • Clear examples 💡 • Chicken metaphors 🐔🐦<br/>
Because complex patterns deserve simple explanations.</sub>

<br/>

<!-- Credibility -->
<a href="https://docs.anthropic.com/en/docs/claude-code">
  <img src="https://img.shields.io/badge/Claude_Code-CLI-8b5cf6?style=flat-square&logo=anthropic" alt="Claude Code CLI"/>
</a>
<a href="https://www.anthropic.com/research/building-effective-agents">
  <img src="https://img.shields.io/badge/Based_on-Anthropic_Research-ec4899?style=flat-square" alt="Anthropic Research"/>
</a>
<a href="https://github.com/hesreallyhim/awesome-claude-code">
  <img src="https://awesome.re/mentioned-badge-flat.svg" alt="Awesome Claude Code"/>
</a>

<br/>

<!-- Stats -->
<img src="https://img.shields.io/badge/Patterns-9-8b5cf6?style=flat-square" alt="9 Patterns"/>
<img src="https://img.shields.io/badge/Components-4-ec4899?style=flat-square" alt="4 Components"/>
<img src="https://img.shields.io/badge/Architecture-5_Layers-10b981?style=flat-square" alt="5 Layers"/>
<img src="https://img.shields.io/badge/🏴‍☠️🪐-SuperNovae-1e293b?style=flat-square" alt="SuperNovae Studio"/>

</div>

---

## Why This Repo? 🪺

Building effective AI agents requires proven patterns, not guesswork.

This repository distills **official Anthropic documentation** into actionable designs:

| What you get | Why it matters |
|--------------|----------------|
| 📊 **Mermaid diagrams** | See the architecture, don't just read about it |
| 💡 **Clear examples** | Copy-paste ready, not abstract theory |
| 🗺️ **Decision guides** | Know which pattern fits your use case |
| 🐔 **Chicken metaphors** | Remember patterns, not jargon |

*Why chickens? Because 🐔 Main Agent spawning 🐦 Subagents is way easier to remember than "hierarchical agent orchestration".*

---

## 🗺️ Navigation Hub

<table>
<tr>
<td width="50%" valign="top">

### 📚 Agentic Systems
**Theory & Patterns** — [Browse →](agentic-systems/)

| # | Pattern | Link |
|:-:|---------|:----:|
| 0 | 🧱 Building Block | [→](agentic-systems/00-building-block.md) |
| 1 | 🏎️ Baseline | [→](agentic-systems/01-baseline.md) |
| 2 | ⛓️ Prompt Chaining | [→](agentic-systems/02-prompt-chaining.md) |
| 3 | 🚦 Routing | [→](agentic-systems/03-routing.md) |
| 4 | 🛤️ Parallelization | [→](agentic-systems/04-parallelization.md) |
| 5 | 🦑 Orchestrator-Workers | [→](agentic-systems/05-orchestrator-workers.md) |
| 6 | 🩻 Evaluator-Optimizer | [→](agentic-systems/06-evaluator-optimizer.md) |
| 7 | 🐉 Autonomous Agents | [→](agentic-systems/07-autonomous-agents.md) |
| 8 | 🖥️ Multi-Window Context | [→](agentic-systems/08-multi-window-context.md) |

</td>
<td width="50%" valign="top">

### 🧩 Components
**Claude Code building blocks** — [Browse →](implementation/components/)

| Component | Location |
|-----------|----------|
| 🐦 [Subagent](implementation/components/subagent.md) | `.claude/agents/*.md` |
| 🦴 [Slash Command](implementation/components/slash-command.md) | `.claude/commands/*.md` |
| 📚 [Skill](implementation/components/skill.md) | `.claude/skills/*/SKILL.md` |
| 🪝 [Hook](implementation/components/hook.md) | `.claude/settings.json` |

<br/>

### 🏗️ Architecture
**5-Layer system** — [Browse →](implementation/architecture/)

| Layer | Link |
|-------|:----:|
| 🙋‍♀️ User Layer | [→](implementation/architecture/01-user-layer.md) |
| 🐔 Main Agent Layer | [→](implementation/architecture/02-main-agent-layer.md) |
| 🔀 Delegation Layer | [→](implementation/architecture/03-delegation-layer.md) |
| ⚡ Execution Layer | [→](implementation/architecture/04-execution-layer.md) |
| 💾 State Layer | [→](implementation/architecture/05-state-layer.md) |

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 🗺️ Guides
**Pattern selection** — [Browse →](guides/)

- [Selection Guide](guides/README.md)
- [Use Cases](guides/use-cases/)

</td>
<td width="50%" valign="top">

### 📖 Reference
**Quick lookups** — [Browse →](reference/)

- [Glossary A-Z](reference/glossary.md)
- [Visual Standards](reference/visual-standards.md)
- [Built-in Subagents](reference/built-in-subagents.md)

</td>
</tr>
</table>

---

## Overview

```mermaid
mindmap
  root((Agentic Systems))
    🧱 Building Block
      Augmented LLM
    Baseline
      🏎️ Direct Execution
    Workflows
      ⛓️ Prompt Chaining
      🚦 Routing
      🛤️ Parallelization
      🦑 Orchestrator-Workers
      🩻 Evaluator-Optimizer
    Agents
      🐉 Autonomous Agents
      🖥️ Multi-Window Context
    Components
      🐦 Subagent
      🦴 Slash Command
      📚 Skill
      🪝 Hook
```

---

## Quick Decision Tree

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    START((Task)) --> D{Destructive?}
    D -->|Yes| WIZ[🧙 Wizard]
    D -->|No| C{Complex?}
    C -->|No| DIRECT[🏎️ Direct]
    C -->|Yes| I{Independent?}
    I -->|Yes| PAR[🛤️ Parallel]
    I -->|No| SUB[🦑 Orchestrator]

    classDef baseline fill:#64748b,stroke:#475569,stroke-width:2px,color:#ffffff
    classDef wizard fill:#14b8a6,stroke:#0d9488,stroke-width:2px,color:#ffffff
    classDef parallel fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#ffffff
    classDef subagent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff

    DIRECT:::baseline
    WIZ:::wizard
    PAR:::parallel
    SUB:::subagent
```

```
Simple Task (1 step)          → 🏎️ Direct execution
Medium Task (2-4 steps)       → ⛓️ Prompt Chaining
Complex Task (5+ steps)       → 🦑 Orchestrator-Workers
Destructive Operation         → 🧙 Wizard Workflows (mandatory)
Long-Running (>10 min)        → 🖥️ Multi-Window Context
```

---

## Key Concepts

### Critical Rule

> **🐦 Subagents cannot spawn other 🐦 subagents.**
> All delegation must go through the 🐔 Main Agent.

### Anthropic Taxonomy

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         AGENTIC SYSTEMS (umbrella)                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  BASELINE (1)                    WORKFLOWS (5)          AGENTS (1)          │
│  ────────────                    ─────────────          ──────────          │
│  0. 🏎️ Direct Execution          1. ⛓️ Prompt Chaining   6. 🐉 Autonomous    │
│     (single augmented LLM)       2. 🚦 Routing                              │
│                                  3. 🛤️ Parallelization                      │
│                                  4. 🦑 Orchestrator-Workers                 │
│                                  5. 🩻 Evaluator-Optimizer                  │
│                                                                             │
│  CODE controls the flow ─────────────────────► LLM controls the flow        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

> Based on [Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents) (Anthropic, Dec 2024)

---

## Cross-Platform Compatibility

| Pattern | Claude | GPT Agents | Gemini ADK | LangGraph |
|:--------|:------:|:----------:|:----------:|:---------:|
| 🦑 Orchestrator-Workers | ✅ | ✅ Handoffs | ✅ Multi-agent | ✅ Subgraphs |
| 📚 Progressive Skills | ✅ | ❌ | ❌ | ❌ |
| 🚂 Parallel Tool Calling | ✅ | ✅ | ✅ ParallelAgent | ✅ Fan-out |
| 🧬 Master-Clone | ✅ | ✅ Dynamic | ✅ Custom | ✅ Send API |
| 🖥️ Multi-Window Context | ✅ | ⚠️ Sessions | ⚠️ ctx.state | ✅ Checkpointing |
| 🧙 Wizard Workflows | ✅ | ⚠️ | ✅ Tool Confirm | ✅ interrupt() |

**Legend:** ✅ Native | ⚠️ Partial | ❌ Not supported

---

## Repository Structure

```
.
├── README.md                    # 🏠 This file (navigation hub)
├── agentic-systems/             # 📚 Theory & Patterns (9 files)
│   ├── README.md                # Overview + index
│   ├── 00-building-block.md     # Augmented LLM foundation
│   ├── 01-baseline.md           # Direct execution
│   ├── 02-prompt-chaining.md    # Sequential + Wizard
│   ├── 03-routing.md            # Classification routing
│   ├── 04-parallelization.md    # Parallel + Master-Clone
│   ├── 05-orchestrator-workers.md
│   ├── 06-evaluator-optimizer.md
│   ├── 07-autonomous-agents.md
│   └── 08-multi-window-context.md
├── implementation/              # 🛠️ How to build
│   ├── components/              # 🧩 4 Claude Code components
│   └── architecture/            # 🏗️ 5-layer system
├── guides/                      # 🗺️ Pattern selection
│   └── use-cases/               # 6 validated examples
└── reference/                   # 📖 Quick lookups
    ├── glossary.md              # A-Z definitions
    ├── visual-standards.md      # Colors, emojis
    └── built-in-subagents.md    # Pre-configured agents
```

---

## References

| Resource | URL |
|----------|-----|
| Claude Code Docs | https://docs.anthropic.com/en/docs/claude-code |
| Agent SDK | https://docs.anthropic.com/docs/en/agent-sdk |
| Building Effective Agents | Anthropic Research Paper (Dec 2024) |
| Anthropic Cookbook | https://github.com/anthropics/anthropic-cookbook |

---

## Contributing

We welcome contributions! This repository aims to be the definitive collection of Claude agentic patterns.

### Ways to Contribute

- **Add new patterns** — Document systems from Anthropic sources
- **Improve existing content** — Add examples, clarify explanations
- **Fix issues** — Correct errors, update outdated information
- **Add translations** — Help make patterns accessible globally

### Requirements

All contributions must:
1. **Reference official sources** — Link to Anthropic docs or blog posts
2. **Include code examples** — Provide working, tested snippets
3. **Follow the pattern format** — Use the established template
4. **Add Mermaid diagrams** — Visual explanations where helpful

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

---

## License

MIT License — See [LICENSE](LICENSE) for details.

---

<p align="center">
  <sub>Built with Claude Code | Based on official documentation | November 2025</sub><br/>
  <sub>Independent community resource — not affiliated with Anthropic</sub>
</p>

<p align="center">
  <a href="https://github.com/ThibautMelen">
    <img src="https://avatars.githubusercontent.com/u/20891897?s=200&v=4" alt="ThibautMelen" width="40"/>
  </a>
  &nbsp;&nbsp;❤️&nbsp;&nbsp;
  <a href="https://github.com/SuperNovae-studio">
    <img src="https://avatars.githubusercontent.com/u/33066282?s=200&v=4" alt="SuperNovae Studio" width="40"/>
  </a>
  &nbsp;&nbsp;🏴‍☠️
</p>

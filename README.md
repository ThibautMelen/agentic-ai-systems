<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/78/Anthropic_logo.svg/1200px-Anthropic_logo.svg.png" alt="Anthropic Logo" width="120"/>
</p>

<h1 align="center">Claude Agentic Patterns</h1>

<p align="center">
  <strong>Official design patterns for building agentic AI systems with Claude</strong>
</p>

<p align="center">
  <em>Curated collection of validated orchestration patterns from Anthropic's documentation and engineering practices</em>
</p>

<p align="center">
  <a href="#patterns">Patterns</a> •
  <a href="#quick-start">Quick Start</a> •
  <a href="#architecture">Architecture</a> •
  <a href="#references">References</a> •
  <a href="#contributing">Contributing</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Claude-4.5-blueviolet?style=flat-square" alt="Claude 4.5"/>
  <img src="https://img.shields.io/badge/Source-Anthropic_Docs-green?style=flat-square" alt="Source: Anthropic Docs"/>
  <img src="https://img.shields.io/badge/Patterns-7-blue?style=flat-square" alt="7 Patterns"/>
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=flat-square" alt="MIT License"/>
  <img src="https://img.shields.io/badge/PRs-Welcome-brightgreen?style=flat-square" alt="PRs Welcome"/>
</p>

---

## Why This Repository?

Building effective AI agents requires proven architectural patterns. This repository distills **official Anthropic documentation** and **engineering blog posts** into actionable design patterns with:

- **Mermaid diagrams** for visual understanding
- **Code examples** ready for implementation
- **Decision guides** for pattern selection
- **Best practices** from Anthropic engineers

> All patterns are sourced from official Anthropic resources and validated against Claude Code, Agent SDK, and API documentation.

---

## Overview

```mermaid
mindmap
  root((Claude Agentic Patterns))
    Orchestration
      Subagents
      Master-Clone
      Wizard Workflows
    Loading
      Progressive Skills
      Multi-Window Context
    Execution
      Parallel Tool Calling
      Programmatic Orchestration
```

---

## Patterns

| # | Pattern | Description | Complexity | Source |
|---|---------|-------------|------------|--------|
| 01 | [**Subagent Orchestration**](patterns/01-subagent-orchestration.md) | Delegate to specialized agents with isolated context | Medium | [Docs](https://code.claude.com/docs/en/sub-agents) |
| 02 | [**Progressive Skills**](patterns/02-progressive-skills.md) | On-demand loading of modular capabilities | Medium | [Blog](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills) |
| 03 | [**Parallel Tool Calling**](patterns/03-parallel-tool-calling.md) | Maximize performance with simultaneous execution | Low | [Docs](https://docs.anthropic.com/docs/en/build-with-claude/prompt-engineering/claude-4-best-practices) |
| 04 | [**Master-Clone Architecture**](patterns/04-master-clone-architecture.md) | Dynamic self-spawning for flexible delegation | High | [Blog](https://blog.sshh.io/p/how-i-use-every-claude-code-feature) |
| 05 | [**Multi-Window Context**](patterns/05-multi-window-context.md) | State persistence across context windows | High | [Docs](https://docs.anthropic.com/docs/en/build-with-claude/context-windows) |
| 06 | [**Programmatic Orchestration**](patterns/06-programmatic-orchestration.md) | Code-based tool orchestration | Medium | [Blog](https://www.anthropic.com/engineering/advanced-tool-use) |
| 07 | [**Wizard Workflows**](patterns/07-wizard-workflows.md) | Multi-step processes with user confirmation | Medium | [Docs](https://code.claude.com/docs/en/common-workflows) |

---

## Quick Start

### Pattern Selection Guide

```mermaid
flowchart TD
    Start[Task Type?] --> Q1{Need specialized<br/>expertise?}

    Q1 -->|Yes| Q2{Fixed or<br/>dynamic?}
    Q1 -->|No| Q3{Multiple<br/>operations?}

    Q2 -->|Fixed workflows| P1[01: Subagent Orchestration]
    Q2 -->|Dynamic needs| P4[04: Master-Clone]

    Q3 -->|Yes, independent| P3[03: Parallel Tool Calling]
    Q3 -->|Yes, dependent| Q4{Complex logic?}
    Q3 -->|No| Direct[Direct execution]

    Q4 -->|Yes| P6[06: Programmatic Orchestration]
    Q4 -->|No| Sequential[Sequential calls]

    Start --> Q5{Long-running<br/>task?}
    Q5 -->|Yes| P5[05: Multi-Window Context]

    Start --> Q6{User approval<br/>needed?}
    Q6 -->|Yes| P7[07: Wizard Workflows]

    Start --> Q7{Modular<br/>capabilities?}
    Q7 -->|Yes| P2[02: Progressive Skills]
```

### By Use Case

| Use Case | Recommended Pattern(s) | Why |
|----------|----------------------|-----|
| Code review automation | Subagents + Parallel Tools | Specialized reviewers + concurrent file analysis |
| Complex refactoring | Master-Clone + Multi-Window | Dynamic delegation + state persistence |
| Data processing pipelines | Programmatic Orchestration | Explicit control flow + error handling |
| Guided deployments | Wizard Workflows | Checkpoint confirmations + rollback capability |
| Domain-specific tasks | Progressive Skills | On-demand expertise loading |
| Research & exploration | Subagents (Explore) | Isolated context + focused search |
| CI/CD automation | Parallel Tools + Programmatic | Speed + deterministic execution |
| Interactive assistants | Wizard + Skills | User guidance + modular capabilities |

---

## Architecture

### High-Level Overview

```mermaid
flowchart TB
    subgraph User["User Layer"]
        U[User Request]
    end

    subgraph Agent["Main Agent Layer"]
        MA[Claude Main Agent]
        TD[Task Decomposition]
    end

    subgraph Delegation["Delegation Layer"]
        SA[Subagents]
        SK[Skills]
        CL[Clones]
    end

    subgraph Execution["Execution Layer"]
        PT[Parallel Tools]
        PO[Programmatic Scripts]
        WZ[Wizard Steps]
    end

    subgraph State["State Layer"]
        CTX[Context Management]
        MEM[Memory/Persistence]
    end

    U --> MA
    MA --> TD
    TD --> SA & SK & CL
    SA & SK & CL --> PT & PO & WZ
    PT & PO & WZ --> CTX
    CTX <--> MEM
```

### Pattern Interactions

```mermaid
graph LR
    subgraph Core["Core Patterns"]
        P1[Subagents]
        P2[Skills]
        P3[Parallel Tools]
    end

    subgraph Advanced["Advanced Patterns"]
        P4[Master-Clone]
        P5[Multi-Window]
        P6[Programmatic]
        P7[Wizard]
    end

    P1 --> P3
    P2 --> P1
    P4 --> P1
    P5 --> P4
    P6 --> P3
    P7 --> P1
    P7 --> P2
```

### Pattern Synergies

| Combination | Use Case | Benefit |
|-------------|----------|---------|
| Subagents + Parallel | Multi-file operations | Concurrent specialized processing |
| Master-Clone + Multi-Window | Large refactors | Flexible delegation + state continuity |
| Skills + Wizard | Guided workflows | Domain expertise + user checkpoints |
| Programmatic + Parallel | Data pipelines | Deterministic + performant |

---

## Key Concepts

### Context Isolation

Each subagent operates in its own context window, preventing pollution and enabling focused task execution.

```mermaid
flowchart LR
    Main[Main Agent<br/>200k tokens] --> S1[Subagent 1<br/>Fresh context]
    Main --> S2[Subagent 2<br/>Fresh context]
    Main --> S3[Subagent 3<br/>Fresh context]
```

### Progressive Disclosure

Skills load information in stages to optimize token usage:

| Level | Content | Token Budget | When Loaded |
|-------|---------|--------------|-------------|
| 1. Metadata | Name, description | ~100 tokens | Always |
| 2. Instructions | Full prompt | <5k tokens | On trigger |
| 3. Resources | Files, examples | Unlimited | On demand |

### Parallelization

Claude 4.x models aggressively parallelize independent operations for optimal performance.

```mermaid
gantt
    title Sequential vs Parallel Execution
    dateFormat X
    axisFormat %s

    section Sequential
    Tool 1    :0, 3
    Tool 2    :3, 6
    Tool 3    :6, 9

    section Parallel
    Tool 1    :0, 3
    Tool 2    :0, 3
    Tool 3    :0, 3
```

### State Persistence

Long-running tasks persist state via multiple mechanisms:

| Mechanism | Best For | Example |
|-----------|----------|---------|
| Structured (JSON/YAML) | Queryable data | `tests.json` with status |
| Freeform (Markdown) | Progress notes | `progress.txt` |
| Git checkpoints | Code state | `git commit -m "WIP"` |

---

## References

### Official Anthropic Documentation

| Resource | Description |
|----------|-------------|
| [Claude Code: Subagents](https://code.claude.com/docs/en/sub-agents) | Complete subagent documentation |
| [Agent Skills Overview](https://docs.anthropic.com/docs/en/agents-and-tools/agent-skills/overview) | Skills architecture and usage |
| [Claude 4.5 Best Practices](https://docs.anthropic.com/docs/en/build-with-claude/prompt-engineering/claude-4-best-practices) | Prompting and orchestration tips |
| [Agent SDK](https://docs.anthropic.com/docs/en/agent-sdk/overview) | SDK documentation |
| [Common Workflows](https://code.claude.com/docs/en/common-workflows) | Practical workflow examples |
| [Tool Use](https://docs.anthropic.com/docs/en/agents-and-tools/tool-use/overview) | Tool calling patterns |
| [Memory Tool](https://docs.anthropic.com/docs/en/agents-and-tools/tool-use/memory-tool) | State persistence |

### Engineering Blog Posts

| Article | Key Insights |
|---------|--------------|
| [Advanced Tool Use](https://www.anthropic.com/engineering/advanced-tool-use) | Programmatic tool orchestration |
| [Equipping Agents with Skills](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills) | Skills architecture deep-dive |
| [Code Execution with MCP](https://www.anthropic.com/engineering/code-execution-with-mcp) | MCP integration patterns |

### Community Resources

| Resource | Description |
|----------|-------------|
| [Skills Cookbook](https://github.com/anthropics/claude-cookbooks/tree/main/skills) | Official skill examples |
| [Claude Code](https://github.com/anthropics/claude-code) | Reference implementation |
| [Awesome Claude Code](https://github.com/hesreallyhim/awesome-claude-code) | Community resources |

---

## Repository Structure

```
claude-agentic-patterns/
├── README.md                              # This file
├── CONTRIBUTING.md                        # Contribution guidelines
├── LICENSE                                # MIT License
├── patterns/
│   ├── 01-subagent-orchestration.md      # Subagent pattern
│   ├── 02-progressive-skills.md          # Skills pattern
│   ├── 03-parallel-tool-calling.md       # Parallel execution
│   ├── 04-master-clone-architecture.md   # Dynamic delegation
│   ├── 05-multi-window-context.md        # State persistence
│   ├── 06-programmatic-orchestration.md  # Code-based orchestration
│   └── 07-wizard-workflows.md            # Guided workflows
└── .github/
    └── ISSUE_TEMPLATE/
        └── pattern-proposal.md           # New pattern template
```

---

## Contributing

We welcome contributions! This repository aims to be the definitive collection of Claude agentic patterns.

### Ways to Contribute

- **Add new patterns** - Document patterns from Anthropic sources
- **Improve existing patterns** - Add examples, clarify explanations
- **Fix issues** - Correct errors, update outdated information
- **Add translations** - Help make patterns accessible globally

### Contribution Requirements

All contributions must:

1. **Reference official sources** - Link to Anthropic docs, blog posts, or official examples
2. **Include code examples** - Provide working, tested code snippets
3. **Follow the pattern format** - Use the established template structure
4. **Add Mermaid diagrams** - Visual explanations where helpful

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

---

## License

MIT License - See [LICENSE](LICENSE) for details.

---

<p align="center">
  <sub>Built with Claude Code | Sourced from Anthropic Documentation | November 2025</sub>
</p>

<p align="center">
  <a href="https://github.com/anthropics">
    <img src="https://img.shields.io/badge/Anthropic-Official_Sources-black?style=flat-square&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0xMiAyQzYuNDggMiAyIDYuNDggMiAxMnM0LjQ4IDEwIDEwIDEwIDEwLTQuNDggMTAtMTBTMTcuNTIgMiAxMiAyem0wIDE4Yy00LjQxIDAtOC0zLjU5LTgtOHMzLjU5LTggOC04IDggMy41OSA4IDgtMy41OSA4LTggOHoiLz48L3N2Zz4=" alt="Anthropic"/>
  </a>
</p>

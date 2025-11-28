<div align="center">

[🏠 Home](../../README.md) › [📘 Guides](../README.md) › [🎯 Use Cases](./) › **Multi-Agent Research**

[← Use Cases](./) ━━●━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ [Production Code Review →](production-code-review.md)

</div>

---

# Use Case: Multi-Agent Research System

> Source: [Anthropic Engineering Blog](https://www.anthropic.com/engineering/multi-agent-research-system) - June 2025

---

## Problem

Synthesizing comprehensive research from multiple sources requires:
- Parallel information gathering
- Domain specialization
- Quality synthesis

---

## Solution Architecture

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TB
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef subagent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff
    classDef tool fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff
    classDef state fill:#10b981,stroke:#059669,stroke-width:2px,color:#ffffff

    USER["🙋‍♀️📥 Research Query"] --> LEAD["🐔 Main Agent"]:::main

    LEAD -->|"🪺 Task"| PLAN["Plan research strategy"]
    PLAN --> SPAWN["Spawn specialized researchers"]

    subgraph PARALLEL["🚂 Parallel Execution"]
        R1["🐦 Academic Researcher"]:::subagent
        R2["🐦 Industry Researcher"]:::subagent
        R3["🐦 News Researcher"]:::subagent
    end

    SPAWN --> R1 & R2 & R3

    R1 --> T1["🔌 Perplexity"]:::tool
    R2 --> T2["🔌 Firecrawl"]:::tool
    R3 --> T3["🔌 WebSearch"]:::tool

    T1 & T2 & T3 --> COLLECT["🐔 Main Agent collects"]:::main
    COLLECT --> SYNTH["🐦 Synthesis Agent"]:::subagent
    SYNTH --> REPORT["✅ Final Report"]:::state
```

---

## Patterns Used

| Pattern | Role |
|---------|------|
| 🦑 Orchestrator-Workers | 🐔 Main Agent spawns specialized researchers |
| 🚂 Parallel Tool Calling | Multiple researchers work simultaneously |
| 🧬 Master-Clone | Each researcher has isolated context |

---

## Implementation

### 🐔 Main Agent Prompt

```python
main_agent_prompt = """
You coordinate research by:
1. Breaking query into research domains
2. Spawning domain-specific researchers
3. Collecting and synthesizing results
"""
```

### 🐦 Researcher Subagent

```python
researcher_prompt = """
You research {domain} using available tools.
Return structured findings with citations.
"""
```

### Subagent Definition

```markdown
# .claude/agents/academic-researcher.md
---
name: academic-researcher
description: Researches academic papers and scholarly sources
tools: Read, WebFetch, WebSearch
model: sonnet
---

You are an academic research specialist. Your task is to:
1. Search for relevant academic papers
2. Extract key findings and citations
3. Return structured research notes

Focus on peer-reviewed sources and cite properly.
```

---

## Why This Works

| Aspect | Benefit |
|--------|---------|
| **Specialization** | Each subagent focuses on one domain |
| **Parallelism** | Independent searches run concurrently |
| **Isolation** | Subagents don't pollute each other's context |
| **Synthesis** | 🐔 Main Agent has full picture for final output |

---

## Flow Summary

```
🙋‍♀️📥 Research Query
    │
    ▼
🐔 Main Agent (Plan strategy)
    │
    ├──► 🐦 Academic Researcher ──► 🔌 Perplexity
    ├──► 🐦 Industry Researcher ──► 🔌 Firecrawl
    └──► 🐦 News Researcher ──► 🔌 WebSearch
            │
            ▼
    🐔 Main Agent (Collect results)
            │
            ▼
    🐦 Synthesis Agent
            │
            ▼
    ✅ Final Report
```

---

<div align="center">

[← Use Cases](./) ━━●━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ [Production Code Review →](production-code-review.md)

</div>

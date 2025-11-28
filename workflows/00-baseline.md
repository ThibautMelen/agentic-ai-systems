<div align="center">

[🏠 Home](../README.md) › [Workflows](./) › **🏎️ Baseline**

[← Workflows](./) ━━●━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ [01 Prompt Chaining →](01-prompt-chaining.md)

</div>

---

# 🏎️ Baseline (Direct Execution)

> **TL;DR:** Single augmented LLM call without orchestration. The simplest baseline — use when tasks need no complexity.

---

## Diagram

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff

    USER["🙋‍♀️📥 User Request"]:::user --> MA["🐔💭 Main Agent"]:::main
    MA -->|"🐔📤"| OUT["💁‍♀️📤 User Receives"]:::user
```

---

## Characteristics

| Property | Value |
|----------|-------|
| **Complexity** | None |
| **Parallelism** | None |
| **Human-Loop** | None |
| **Iteration** | None |

---

## When to Use

- Simple, single-step tasks
- No need for specialization
- Quick operations (file read, simple edit, search)

**Examples:**
- "What's in the config.json file?"
- "Add a console.log statement to this function"
- "Search for usages of `useState`"

---

## When NOT to Use

- Complex multi-step workflows
- Tasks requiring multiple specializations
- Large-scale operations

---

<div align="center">

[← Workflows](./) ━━●━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ [01 Prompt Chaining →](01-prompt-chaining.md)

</div>

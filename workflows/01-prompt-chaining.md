<div align="center">

[🏠 Home](../README.md) › [Workflows](./) › **⛓️ Prompt Chaining**

[← 00 Baseline](00-baseline.md) ━━━━━━●━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ [02 Routing →](02-routing.md)

</div>

---

# ⛓️ Prompt Chaining

> **TL;DR:** Decompose a task into sequential steps where each LLM call processes the output of the previous one. Trade latency for accuracy.

---

## Diagram

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef gate fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff
    classDef exit fill:#ef4444,stroke:#dc2626,stroke-width:2px,color:#ffffff

    USER["🙋‍♀️📥"]:::user --> P1["🐔💭 Step 1"]:::main
    P1 -->|"🐔📤"| G1{"🚧 Gate"}:::gate
    G1 -->|Pass| P2["🐔💭 Step 2"]:::main
    G1 -.->|Fail| EXIT["❌ Exit"]:::exit
    P2 -->|"🐔📤"| G2{"🚧 Gate"}:::gate
    G2 -->|Pass| P3["🐔💭 Step 3"]:::main
    G2 -.->|Fail| EXIT
    P3 -->|"🐔📤"| OUT["💁‍♀️📤"]:::user
```

---

## 🚧 Gate

> A checkpoint between steps that validates the output before proceeding. If validation fails, the chain exits early.

**Gates can check for:**
- Output format/structure validity
- Quality thresholds (confidence scores, completeness)
- Safety checks (content moderation, guardrails)
- Business rules (required fields, constraints)

---

## Characteristics

| Property | Value |
|----------|-------|
| **Complexity** | Low |
| **Parallelism** | None |
| **Human-Loop** | Optional |
| **Iteration** | Linear |

---

## When to Use

Ideal when the task can be easily decomposed into fixed subtasks. The main goal is to **trade latency for higher accuracy** by making each LLM call an easier task.

| Use Case | Chain |
|----------|-------|
| Marketing | Generate copy → Translate to target language |
| Documents | Write outline → Validate criteria → Write document |
| Code generation | Plan → Implement → Review |
| Data transformation | Parse → Transform → Validate |

---

## Example Flow

```
Step 1: "Extract all function names from this code"
        → [list of functions]

Step 2: "For each function, identify parameters and return types"
        → [function signatures]

Step 3: "Generate documentation for each function"
        → [documented code]
```

---

## When NOT to Use

- Steps can be done independently (use 🛤️ Parallelization)
- Simple single-step tasks (use 🏎️ Baseline)

---

## Variant: 🧙 Wizard Workflow

Multi-step process with explicit 🙆‍♀️ user confirmation at each phase using ❓ `AskUserQuestion`.

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
stateDiagram-v2
    [*] --> Analysis: 🙋‍♀️📥 User Request

    Analysis --> Confirm1: Present findings
    Confirm1 --> Planning: 🙆‍♀️✅ User approves
    Confirm1 --> Analysis: 🙆‍♀️❓ User requests changes

    Planning --> Confirm2: Present plan
    Confirm2 --> Implementation: 🙆‍♀️✅ User approves
    Confirm2 --> Planning: 🙆‍♀️❓ User requests changes

    Implementation --> Confirm3: Show changes
    Confirm3 --> Verification: 🙆‍♀️✅ User approves
    Confirm3 --> Implementation: 🙆‍♀️❓ User requests changes

    Verification --> [*]: ✅ Complete
```

**Use 🧙 Wizard for:**
- Destructive operations (migrations, deletions)
- Complex refactoring
- Multi-stakeholder decisions

---

<div align="center">

[← 00 Baseline](00-baseline.md) ━━━━━━●━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ [02 Routing →](02-routing.md)

</div>

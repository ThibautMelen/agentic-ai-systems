# Pattern Selection Guide

> Decision trees and criteria for choosing the right agentic pattern

---

## Real-World Use Cases → Pattern

| Use Case | Primary Pattern | Secondary | Details |
|----------|-----------------|-----------|---------|
| Multi-Agent Research | 🎪 Subagent Orchestration | 🚂 Parallel | [→ Use Cases](05-USE-CASES.md#use-case-1-multi-agent-research-system) |
| Code Review Pipeline | 🚂 Parallel Tool Calling | 🎪 Subagent | [→ Use Cases](05-USE-CASES.md#use-case-2-production-code-review) |
| Multi-Locale Generation | 🧬 Master-Clone | 🧙 Wizard | [→ Use Cases](05-USE-CASES.md#use-case-3-multi-locale-content-generation) |
| Personal Assistant | 🎓 Progressive Skills | 🚦 Routing | [→ Use Cases](05-USE-CASES.md#use-case-4-intelligent-personal-assistant) |
| Customer Support | 🚦 Routing | 🎪 Subagent | [→ Use Cases](05-USE-CASES.md#use-case-5-customer-support-automation) |
| Data Migration | 🧙 Wizard Workflows | 🖥️ Multi-Window | [→ Use Cases](05-USE-CASES.md#use-case-6-data-pipeline-migration) |

> See [05-USE-CASES.md](05-USE-CASES.md) for detailed architectures and implementation examples.

---

## Quick Reference

### By Task Complexity

```
Simple Task (1 step)          → Direct execution
Medium Task (2-4 steps)       → Prompt Chaining or 🎓 Progressive Skills
Complex Task (5+ steps)       → 🎪 Subagent Orchestration
Very Complex (multiple hours) → 🧙 Wizard Workflows + 🖥️ Multi-Window Context
```

### By Parallelism Need

```
Sequential required    → Prompt Chaining
Independent steps      → 🚂 Parallel Tool Calling
Independent domains    → 🧬 Master-Clone
Mixed                  → 🎪 Subagent Orchestration
```

### By User Involvement

```
Fully autonomous       → Autonomous Agents
Occasional feedback    → 🎪 Subagent Orchestration
Critical checkpoints   → 🧙 Wizard Workflows
Full control           → 🎛️ Programmatic Orchestration
```

---

## Master Decision Tree

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TD
    classDef start fill:#10b981,stroke:#059669,stroke-width:2px,color:#ffffff
    classDef pattern fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef decision fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff

    START["👤 New Task"]:::start --> Q1{Single step?}:::decision

    Q1 -->|Yes| DIRECT["Direct Execution"]:::pattern
    Q1 -->|No| Q2{Steps independent?}:::decision

    Q2 -->|Yes| Q3{Same domain?}:::decision
    Q2 -->|No| Q4{Requires 👤 approval?}:::decision

    Q3 -->|Yes| PARALLEL["🚂 Parallel Tool Calling"]:::pattern
    Q3 -->|No| MASTERCLONE["🧬 Master-Clone"]:::pattern

    Q4 -->|Yes| WIZARD["🧙 Wizard Workflows"]:::pattern
    Q4 -->|No| Q5{Needs specialization?}:::decision

    Q5 -->|Yes| SUBAGENT["🎪 Subagent Orchestration"]:::pattern
    Q5 -->|No| Q6{Predefined methodology?}:::decision

    Q6 -->|Yes| SKILLS["🎓 Progressive Skills"]:::pattern
    Q6 -->|No| CHAINING["Prompt Chaining"]:::pattern
```

---

## Pattern Selection by Scenario

### Scenario 1: Code Review

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    classDef small fill:#10b981,stroke:#059669,stroke-width:2px,color:#ffffff
    classDef medium fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff
    classDef large fill:#ef4444,stroke:#dc2626,stroke-width:2px,color:#ffffff
    classDef subagent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff

    subgraph Small["✅ Small PR (1-3 files)"]
        S1["🧠 Direct review by Main Agent"]
    end

    subgraph Medium["⚠️ Medium PR (4-10 files)"]
        M1["🚂 Parallel Tool Calling"]
        M2["🔌 Read all files concurrently"]
        M1 --> M2
    end

    subgraph Large["❌ Large PR (10+ files)"]
        L1["🎪 Subagent Orchestration"]
        L2["🤖 Security Subagent"]:::subagent
        L3["🤖 Performance Subagent"]:::subagent
        L4["🤖 Style Subagent"]:::subagent
        L1 --> L2 & L3 & L4
    end

    style Small fill:#ecfdf5,stroke:#10b981,stroke-width:2px
    style Medium fill:#fef3c7,stroke:#f59e0b,stroke-width:2px
    style Large fill:#fef2f2,stroke:#ef4444,stroke-width:2px
```

**Selection:**
- 1-3 files → **Direct execution**
- 4-10 files → **🚂 Parallel Tool Calling** (read all, review)
- 10+ files → **🎪 Subagent Orchestration** (specialized reviewers)

---

### Scenario 2: Feature Implementation

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TD
    classDef skill fill:#10b981,stroke:#059669,stroke-width:2px,color:#ffffff
    classDef decision fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff

    FEATURE["👤 New Feature"] --> Q1{Methodology defined?}:::decision

    Q1 -->|TDD Required| TDD["🎓 Progressive Skills: TDD"]:::skill
    Q1 -->|Free form| Q2{Multiple components?}:::decision

    Q2 -->|Yes| Q3{Components independent?}:::decision
    Q2 -->|No| CHAIN["Prompt Chaining"]

    Q3 -->|Yes| PARALLEL["🚂 Parallel Tool Calling"]
    Q3 -->|No| SUBAGENT["🎪 Subagent Orchestration"]

    TDD --> Q2
```

**Selection:**
- Enforced methodology → **🎓 Progressive Skills** first
- Multi-component, independent → **🚂 Parallel Tool Calling**
- Multi-component, dependent → **🎪 Subagent Orchestration**
- Linear steps → **Prompt Chaining**

---

### Scenario 3: Data Migration

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TD
    classDef wizard fill:#14b8a6,stroke:#0d9488,stroke-width:2px,color:#ffffff
    classDef checkpoint fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff
    classDef state fill:#10b981,stroke:#059669,stroke-width:2px,color:#ffffff

    MIGRATION["👤 Data Migration"] --> WIZARD["🧙 Wizard Workflows"]:::wizard

    WIZARD --> P1["🏗️ Phase 1: Analysis"]
    P1 --> CONFIRM1{"❓ User confirms?"}:::checkpoint
    CONFIRM1 -->|Yes| P2["🔗 Phase 2: Plan"]

    P2 --> CONFIRM2{"❓ User confirms?"}:::checkpoint
    CONFIRM2 -->|Yes| P3["📝 Phase 3: Execute"]

    P3 --> P4["🔮 Phase 4: Verify"]
    P4 --> DONE["✅ Complete"]:::state
```

**Selection:**
- Destructive operation → **🧙 Wizard Workflows** (mandatory)
- Long-running → Add **🖥️ Multi-Window Context**
- Multiple tables → Add **🚂 Parallel Tool Calling** for independent tables

---

### Scenario 4: Multi-Locale Generation (AthenaKNW)

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TB
    classDef wizard fill:#14b8a6,stroke:#0d9488,stroke-width:2px,color:#ffffff
    classDef subagent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff
    classDef checkpoint fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff

    GEN["👤 Generate Locales"] --> WIZARD["🧙 Wizard: Confirm scope"]:::wizard

    WIZARD --> Q1{Single or cluster?}

    Q1 -->|Single| SINGLE[Sequential phases]
    Q1 -->|Cluster| CLUSTER["🎪 Orchestration"]

    CLUSTER --> PRIMARY["🤖 Primary locale first"]:::subagent
    PRIMARY --> VARIANTS["🧬 Variants in parallel"]

    VARIANTS --> MC1["🤖 Master-Clone: fr-CA"]:::subagent
    VARIANTS --> MC2["🤖 Master-Clone: fr-BE"]:::subagent
    VARIANTS --> MC3["🤖 Master-Clone: fr-CH"]:::subagent

    MC1 & MC2 & MC3 --> CHECK["🖥️ Multi-Window: Checkpoint"]:::checkpoint
```

**Selection:**
- 👤 User confirmation → **🧙 Wizard Workflows**
- Primary then variants → **🎪 Subagent Orchestration**
- Variants parallel → **🧬 Master-Clone**
- Long workflow → **🖥️ Multi-Window Context**

---

## Pattern Compatibility Matrix

### Can Be Combined

| Primary Pattern | Compatible With |
|-----------------|-----------------|
| 🧙 Wizard Workflows | All patterns |
| 🎪 Subagent Orchestration | 🚂 Parallel, 🧬 Master-Clone, 🖥️ Multi-Window |
| 🎓 Progressive Skills | 🎪 Subagent, 🚂 Parallel |
| 🚂 Parallel Tool Calling | 🎪 Subagent, 🖥️ Multi-Window |
| 🧬 Master-Clone | 🎪 Subagent, 🖥️ Multi-Window |
| 🖥️ Multi-Window Context | All patterns |
| 🎛️ Programmatic Orchestration | Exclusive (external control) |

### Combination Examples

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    classDef wizard fill:#14b8a6,stroke:#0d9488,stroke-width:2px,color:#ffffff
    classDef subagent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff
    classDef parallel fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#ffffff
    classDef checkpoint fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff

    subgraph Combo1["🧙 Wizard + 🎪 Subagent"]
        W1["❓ Confirm"]:::wizard --> S1["🤖 Spawn agents"]:::subagent
    end

    subgraph Combo2["🎪 Subagent + 🚂 Parallel"]
        S2["🧠 Orchestrator"] --> P1["🤖 Parallel agents"]:::parallel
    end

    subgraph Combo3["🧬 Master-Clone + 🖥️ Multi-Window"]
        MC["🤖 Isolated clones"]:::subagent --> MW["🖥️ Checkpoints"]:::checkpoint
    end
```

---

## Anti-Patterns: What NOT to Do

### 1. ❌ Over-Engineering Simple Tasks

```
❌ WRONG: Use 🎪 Subagent Orchestration for "fix typo"
✅ RIGHT: Direct execution

Rule: If it takes 1 step, don't add patterns
```

### 2. ❌ 🤖 Subagents Spawning 🤖 Subagents

```
❌ WRONG: 🤖 Subagent A spawns 🤖 Subagent B
✅ RIGHT: 🧠 Main Agent spawns both A and B

Rule: Only 🧠 Main Agent can spawn 🤖 subagents
```

### 3. ❌ 🚂 Parallel with Dependencies

```python
❌ WRONG:
[
    Task(prompt="Create schema"),      # Must complete first
    Task(prompt="Insert data")         # Depends on schema
]

✅ RIGHT:
Task(prompt="Create schema")  # Wait for completion
Task(prompt="Insert data")    # Then insert
```

### 4. ❌ 🧙 Wizard for Non-Destructive Tasks

```
❌ WRONG: 🧙 Wizard for "add console.log"
✅ RIGHT: Direct execution

Rule: 🧙 Wizard for destructive/critical operations only
```

### 5. ❌ Skipping 🖥️ Checkpoints in Long Workflows

```
❌ WRONG: 2-hour workflow with no 🖥️ checkpoints
✅ RIGHT: 🖥️ Checkpoint every major phase

Rule: Any workflow > 10 minutes needs 🖥️ Multi-Window Context
```

### 6. ❌ Too Many Parallel 🤖 Subagents

```
❌ WRONG: 39 🤖 subagents in parallel (context overflow)
✅ RIGHT: Batch into waves of 10-15

Rule: Max 10-15 concurrent subagents per wave
```

### 7. ❌ Long Runs Without `/compact`

```
❌ WRONG: 200 files generated without clearing context
✅ RIGHT: /compact between major waves

Rule: Use /compact after 50+ file generations or between major phases
```

---

## Operational Decision Trees

### When to Use `/compact`

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TD
    classDef yes fill:#10b981,stroke:#059669,stroke-width:2px,color:#ffffff
    classDef no fill:#ef4444,stroke:#dc2626,stroke-width:2px,color:#ffffff
    classDef decision fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff

    START["🤔 Should I /compact?"] --> Q1{"Generated<br/>50+ files?"}:::decision

    Q1 -->|Yes| COMPACT["✅ Yes, /compact"]:::yes
    Q1 -->|No| Q2{"Between<br/>major phases?"}:::decision

    Q2 -->|Yes| COMPACT
    Q2 -->|No| Q3{"Context feels<br/>slow/heavy?"}:::decision

    Q3 -->|Yes| COMPACT
    Q3 -->|No| Q4{"Debugging<br/>an error?"}:::decision

    Q4 -->|Yes| NOCOMPACT["❌ No, keep context"]:::no
    Q4 -->|No| Q5{"Short workflow<br/>(<10 files)?"}:::decision

    Q5 -->|Yes| NOCOMPACT
    Q5 -->|No| COMPACT
```

**Critical**: Always 🖥️ checkpoint BEFORE `/compact` - context is lost after compaction!

### How Many Parallel 🤖 Subagents

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TD
    classDef safe fill:#10b981,stroke:#059669,stroke-width:2px,color:#ffffff
    classDef caution fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff
    classDef danger fill:#ef4444,stroke:#dc2626,stroke-width:2px,color:#ffffff
    classDef decision fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff

    COUNT["🤖 How many subagents?"] --> Q1{"Count?"}:::decision

    Q1 -->|"1-5"| SAFE["✅ Safe: Direct parallel"]:::safe
    Q1 -->|"6-10"| CAUTION["⚠️ Caution: Monitor performance"]:::caution
    Q1 -->|"11-15"| LIMIT["⚠️ Limit: Test first"]:::caution
    Q1 -->|"16+"| BATCH["❌ Batch: Split into waves"]:::danger

    BATCH --> WAVE["Wave 1: 10 🤖<br/>Wave 2: 10 🤖<br/>..."]:::safe
```

**Recommended limits:**

| Type | Max | Action if exceeded |
|------|-----|-------------------|
| 🤖 Concurrent subagents | 10-15 | Batch into waves |
| 🔌 MCP calls per agent | 5 | Respect rate limits |
| 📤 Task calls per message | 10 | Split messages |

---

## Selection Flowchart: Complete

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TD
    classDef start fill:#10b981,stroke:#059669,stroke-width:2px,color:#ffffff
    classDef execute fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef wizard fill:#14b8a6,stroke:#0d9488,stroke-width:2px,color:#ffffff
    classDef checkpoint fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff
    classDef decision fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff

    START(("👤 Start")):::start --> RISK{Destructive<br/>operation?}:::decision

    RISK -->|Yes| WIZARD["🧙 Wizard Workflows"]:::wizard
    RISK -->|No| COMPLEX{Complex<br/>task?}:::decision

    COMPLEX -->|No| DIRECT["Direct Execution"]:::execute
    COMPLEX -->|Yes| SPECIAL{Specialized<br/>domains?}:::decision

    SPECIAL -->|Yes| SUBAGENT["🎪 Subagent Orchestration"]
    SPECIAL -->|No| INDEP{Independent<br/>subtasks?}:::decision

    INDEP -->|Yes| DOMAIN{Same<br/>domain?}:::decision
    INDEP -->|No| METHOD{Methodology<br/>exists?}:::decision

    DOMAIN -->|Yes| PARALLEL["🚂 Parallel Tool Calling"]
    DOMAIN -->|No| CLONE["🧬 Master-Clone"]

    METHOD -->|Yes| SKILLS["🎓 Progressive Skills"]
    METHOD -->|No| CHAIN["Prompt Chaining"]

    %% Add checkpointing consideration
    SUBAGENT --> LONG{Long<br/>running?}:::decision
    PARALLEL --> LONG
    CLONE --> LONG
    CHAIN --> LONG

    LONG -->|Yes| CHECKPOINT["Add 🖥️ Multi-Window Context"]:::checkpoint
    LONG -->|No| EXECUTE["✅ Execute"]:::execute

    CHECKPOINT --> EXECUTE
    WIZARD --> EXECUTE
    DIRECT --> EXECUTE
    SKILLS --> EXECUTE
```

---

## Quick Decision Table

| Question | Yes → | No → |
|----------|-------|------|
| Destructive operation? | 🧙 Wizard Workflows | Continue |
| Single step? | Direct Execution | Continue |
| Needs specialization? | 🎪 Subagent Orchestration | Continue |
| Steps independent? | 🚂 Parallel / 🧬 Master-Clone | Continue |
| Has methodology? | 🎓 Progressive Skills | Prompt Chaining |
| Long running? | Add 🖥️ Multi-Window | ✅ Execute |

---

## Pattern Cost/Benefit Analysis

```
┌──────────────────────────┬────────────┬──────────────┬────────────┬────────────┐
│ Pattern                  │ Setup Cost │ Runtime Cost │ Complexity │ Reliability│
├──────────────────────────┼────────────┼──────────────┼────────────┼────────────┤
│ Direct Execution         │ None       │ Low          │ Low        │ High       │
│ Prompt Chaining          │ Low        │ Medium       │ Low        │ High       │
│ 🎓 Progressive Skills    │ Medium     │ Low          │ Medium     │ High       │
│ 🚂 Parallel Tool Calling │ Low        │ Medium       │ Low        │ High       │
│ 🎪 Subagent Orchestrate  │ High       │ High         │ High       │ Medium     │
│ 🧬 Master-Clone          │ Medium     │ High         │ Medium     │ High       │
│ 🖥️ Multi-Window Context  │ Medium     │ Low          │ Medium     │ High       │
│ 🧙 Wizard Workflows      │ Medium     │ Low          │ Medium     │ Very High  │
│ 🎛️ Programmatic Orch.    │ High       │ Variable     │ High       │ Very High  │
└──────────────────────────┴────────────┴──────────────┴────────────┴────────────┘
```

---

*See [07-MAPPING-GLOSSARY.md](07-MAPPING-GLOSSARY.md) for complete term definitions →*

<div align="center">

[🏠 Home](../README.md) • **📖 Guides**

</div>

---

# Guides

> Practical guidance for choosing and implementing agentic patterns

---

## Navigation

| Guide | Description |
|-------|-------------|
| [Quick Selection](#quick-selection-reference) | Decision tree for choosing patterns |
| [use-cases/](use-cases/) | Real-world validated use cases |

---

## Quick Selection Reference

### By Complexity

| If your task is... | Start with... |
|--------------------|---------------|
| Simple, single-step | 🏎️ Direct Execution |
| Sequential, multi-step | ⛓️ Prompt Chaining |
| Needs classification | 🚦 Routing |
| Independent subtasks | 🛤️ Parallelization |
| Specialized experts | 🦑 Orchestrator-Workers |
| Quality-critical | 🩻 Evaluator-Optimizer |
| Open-ended | 🐔 Autonomous Agent |

### By Characteristics

| If you need... | Use pattern... |
|----------------|----------------|
| Human approval at checkpoints | 🧙 Wizard Workflow |
| Multiple tools simultaneously | 🚂 Parallel Tool Calling |
| Same agent on different data | 🧬 Master-Clone |
| Long-running with resume | 🖥️ Multi-Window Context |
| Context-based capabilities | 📚 Progressive Skills |
| External code control | 🎛️ Programmatic Orchestration |

---

## Use Cases Quick Reference

| Use Case | Pattern | Key Insight |
|----------|---------|-------------|
| Multi-Agent Research | 🦑 + 🚂 | 🐔 Main Agent spawns specialized 🐦 researchers |
| Code Review Pipeline | 🚂 + 🦑 | Security, Performance, Style reviewers |
| Multi-Locale Generation | 🧬 + 🧙 | Primary → Variants in isolation |
| Personal Assistant | 📚 | Calendar, Email, Tasks routing |
| Customer Support | 🚦 + 🦑 | Triage → Specialized handlers |
| Data Migration | 🧙 + 🖥️ | Phased with checkpoints |

→ **Details:** [use-cases/](use-cases/)

---

<div align="center">

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

[🏠 Home](../README.md) • [📚 Concepts](../workflows/)

</div>

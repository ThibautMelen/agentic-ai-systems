<div align="center">

[🏠 Home](../../README.md) › [🔧 Implementation](../README.md) › [📦 Components](./) › **🐦 Subagent**

[← Components](./) ━━●━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ [🦴 Slash Command →](slash-command.md)

</div>

---

# 🐦 Subagent

> A **Subagent** is an independent worker spawned by the 🐔 Main Agent via the `Task` tool (🪺 spawn action) to handle specific, isolated tasks.

---

## Key Characteristics

| Property | Value |
|----------|-------|
| **Invocation** | `Task` tool with `subagent_type` parameter (🪺 spawn) |
| **Location** | `.claude/agents/*.md` |
| **Autonomy** | Full - executes independently |
| **Spawning** | ❌ Cannot spawn other subagents |
| **Context** | Isolated from main conversation |
| **Permissions** | Controlled via `permissionMode` frontmatter |

---

## File Structure

```markdown
# .claude/agents/code-reviewer.md

---
name: code-reviewer
description: Reviews code for quality, security, and best practices
tools: Read, Write, Grep, Glob
model: sonnet
permissionMode: acceptEdits
skills: test-driven-development, code-review
---

You are a code review specialist. Your task is to...
```

> **Note**: `tools` and `skills` are comma-separated strings, not YAML lists.

---

## Frontmatter Reference

| Field | Required | Description |
|-------|----------|-------------|
| `name` | Yes | Unique identifier (lowercase, hyphens) |
| `description` | Yes | Natural language description for discovery |
| `tools` | No | Comma-separated tool list. Omit to inherit all tools |
| `model` | No | `sonnet`, `opus`, `haiku`, or `inherit` (default: configured subagent model) |
| `permissionMode` | No | Controls permission handling (see below) |
| `skills` | No | Comma-separated skill names to auto-load |

---

## Permission Modes

| Mode | Behavior | Use Case |
|------|----------|----------|
| `default` | Asks permission for each tool | Read-only, validation |
| `acceptEdits` | Auto-approves Write/Edit | Generation after 🧙 user confirmation |
| `bypassPermissions` | All tools auto-approved | Trusted autonomous workflows |
| `plan` | Read-only planning mode | Research without modifications |
| `ignore` | Skip permission prompts entirely | Batch processing |

> **Best Practice**: Use `acceptEdits` after 🧙 Wizard confirmation to enable autonomous generation without repeated permission prompts.

---

## Usage Examples

### Basic Invocation

```python
# 🐔 Main Agent 🪺 spawns 🐦 subagent via Task tool
Task(
    subagent_type="code-reviewer",
    prompt="Review the authentication module in src/auth/ for security vulnerabilities. Focus on: 1) Input validation 2) Session management 3) Password handling",
    description="Security review of auth module"
)
```

### With Model Override

```python
Task(
    subagent_type="code-reviewer",
    prompt="Quick syntax check of utils.py",
    model="haiku",  # Use faster model for simple tasks
    description="Quick syntax review"
)
```

### Resumable Invocation

```python
# First call - returns agentId
result = Task(
    subagent_type="research-analyst",
    prompt="Research the current state of WebSocket libraries in Python",
    description="WebSocket library research"
)
# result.agentId = "agent-abc123"

# Later - resume with context
Task(
    subagent_type="research-analyst",
    prompt="Now compare the top 3 libraries you found and recommend one",
    resume="agent-abc123",  # Continue previous conversation
    description="WebSocket library comparison"
)
```

---

## Mermaid Representation

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
sequenceDiagram
    participant U as 🙋‍♀️ User
    participant MA as 🐔 Main Agent
    participant SA as 🐦 Subagent
    participant T as 🔧 Tools

    U->>MA: "Review my code"
    MA->>SA: 🪺 Task(subagent_type="code-reviewer")
    SA->>T: Read, Grep, Glob
    T-->>SA: Results
    SA-->>MA: 🐦📤 Review Report
    MA-->>U: 💁‍♀️📤 "Here's the review..."
```

---

## Built-in Subagents

| Subagent | Model | Tools | Purpose |
|----------|-------|-------|---------|
| **General-purpose** | Sonnet | All tools | Complex multi-step tasks |
| **Plan** | Sonnet | Read, Glob, Grep, Bash | Research (read-only) |
| **Explore** | Haiku | Glob, Grep, Read, Bash | Fast codebase searching |

**Explore Thoroughness:** `quick` → `medium` → `very thorough`

---

## Resumable Subagents

Subagents can be resumed to continue previous conversations, maintaining full context.

### How It Works

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
sequenceDiagram
    participant MA as 🐔 Main Agent
    participant SA as 🐦 Subagent
    participant FS as 💾 File System

    MA->>SA: Task(prompt="Research X")
    SA->>SA: Work on task...
    SA-->>MA: Return result + agentId
    SA->>FS: Save transcript (agent-{id}.jsonl)

    Note over MA,FS: Later...

    MA->>SA: Task(resume="abc123", prompt="Continue with Y")
    FS-->>SA: Load previous transcript
    SA->>SA: Resume with full context
    SA-->>MA: Return continued result
```

### End-to-End Example: Research Project

**Session 1: Initial Research**

```python
# Start a research task
result1 = Task(
    subagent_type="research-analyst",
    prompt="""Research the current state of Python async web frameworks.

    Investigate:
    1. FastAPI - features, performance, ecosystem
    2. Starlette - relationship to FastAPI
    3. AIOHTTP - comparison points
    4. Litestar - newer alternative

    Create a comparison matrix and initial recommendation.""",
    description="Async framework research"
)

# Result includes agentId for later resumption
# result1.agentId = "agent-research-abc123"
# Transcript saved to: agent-research-abc123.jsonl
```

**Session 2: Continue with Deeper Analysis**

```python
# Resume the same subagent with its full context
result2 = Task(
    subagent_type="research-analyst",
    prompt="""Based on your previous research, now:

    1. Deep dive into FastAPI's dependency injection system
    2. Compare its approach to Flask/Django
    3. Provide code examples showing the pattern

    Build on what you learned in the previous analysis.""",
    resume="agent-research-abc123",  # Continue previous conversation
    description="Deep dive into FastAPI DI"
)

# The subagent remembers all previous research context
```

**Session 3: Final Recommendation**

```python
# Continue to final recommendation
result3 = Task(
    subagent_type="research-analyst",
    prompt="""Now provide final recommendation:

    1. Which framework for our e-commerce API?
    2. Migration path from current Flask app
    3. Team training requirements
    4. Timeline estimate

    Use all your research to justify the recommendation.""",
    resume="agent-research-abc123",
    description="Final framework recommendation"
)
```

### Transcript Storage

```
project/
├── agent-research-abc123.jsonl    # Research analyst transcript
├── agent-reviewer-def456.jsonl    # Code reviewer transcript
└── .claude/
    └── agents/
        └── research-analyst.md    # Agent definition
```

### Best Practices

| Practice | Reason |
|----------|--------|
| **Use descriptive prompts** | Context carries forward, be specific |
| **Resume same subagent type** | Different types have different capabilities |
| **Check agentId exists** | Transcript might be cleaned up |
| **Build on previous work** | Reference "your previous analysis" |

---

## Critical Rule

> **🐦 Subagents cannot spawn other subagents.**
>
> All delegation must go through the 🐔 Main Agent.

---

<div align="center">

[← Components](./) ━━●━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ [🦴 Slash Command →](slash-command.md)

</div>

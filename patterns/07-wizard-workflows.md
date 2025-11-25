# Pattern 7: Wizard-Style Workflows

> Multi-step processes with explicit user confirmation at each phase.

---

## Overview

Wizard-style workflows break complex tasks into discrete steps with explicit user confirmation between phases. This pattern is ideal for guided processes where user input, validation, or approval is needed at checkpoints.

## Architecture

```mermaid
stateDiagram-v2
    [*] --> Analysis: User Request

    Analysis --> Confirmation1: Present findings
    Confirmation1 --> Planning: User approves
    Confirmation1 --> Analysis: User requests changes

    Planning --> Confirmation2: Present plan
    Confirmation2 --> Implementation: User approves
    Confirmation2 --> Planning: User requests changes

    Implementation --> Confirmation3: Show changes
    Confirmation3 --> Verification: User approves
    Confirmation3 --> Implementation: User requests changes

    Verification --> [*]: Complete
```

## Typical Workflow Phases

```mermaid
flowchart TB
    subgraph Phase1["Phase 1: Analysis"]
        A1[Explore codebase]
        A2[Identify patterns]
        A3[Present findings]
        A4{User confirms?}
    end

    subgraph Phase2["Phase 2: Planning"]
        P1[Create detailed plan]
        P2[Estimate impact]
        P3[Present plan]
        P4{User confirms?}
    end

    subgraph Phase3["Phase 3: Implementation"]
        I1[Execute changes]
        I2[Run tests]
        I3[Present results]
        I4{User confirms?}
    end

    subgraph Phase4["Phase 4: Verification"]
        V1[Final verification]
        V2[Documentation]
        V3[Complete]
    end

    A1 --> A2 --> A3 --> A4
    A4 -->|Yes| P1
    A4 -->|No/Changes| A1

    P1 --> P2 --> P3 --> P4
    P4 -->|Yes| I1
    P4 -->|No/Changes| P1

    I1 --> I2 --> I3 --> I4
    I4 -->|Yes| V1
    I4 -->|No/Changes| I1

    V1 --> V2 --> V3
```

## When to Use

### Good Fit for Wizard Pattern

| Scenario | Why |
|----------|-----|
| **Destructive operations** | User should confirm before data loss |
| **Complex refactoring** | Plan review prevents wrong direction |
| **Deployment pipelines** | Checkpoints catch issues early |
| **Data migrations** | Validation between stages |
| **Multi-stakeholder tasks** | Different approvers for different phases |

### Poor Fit for Wizard Pattern

| Scenario | Better Alternative |
|----------|-------------------|
| Simple single-step tasks | Direct execution |
| Exploratory research | Autonomous agent |
| Time-sensitive automation | Parallel execution |
| Repetitive batch operations | Programmatic orchestration |

## Implementation

### Basic Wizard Structure

```python
class WizardWorkflow:
    def __init__(self):
        self.phase = "analysis"
        self.context = {}
        self.history = []

    def run_phase(self):
        """Execute current phase and wait for confirmation."""

        if self.phase == "analysis":
            findings = self.analyze()
            return {
                "phase": "analysis",
                "findings": findings,
                "prompt": "Review findings. Approve to continue or request changes.",
                "options": ["approve", "modify", "cancel"]
            }

        elif self.phase == "planning":
            plan = self.create_plan()
            return {
                "phase": "planning",
                "plan": plan,
                "prompt": "Review plan. Approve to implement or request changes.",
                "options": ["approve", "modify", "cancel"]
            }

        elif self.phase == "implementation":
            changes = self.implement()
            return {
                "phase": "implementation",
                "changes": changes,
                "prompt": "Review changes. Approve to finalize or rollback.",
                "options": ["approve", "rollback", "cancel"]
            }

    def handle_response(self, response):
        """Process user response and transition state."""

        self.history.append({
            "phase": self.phase,
            "response": response
        })

        if response == "approve":
            self.advance_phase()
        elif response == "modify":
            # Stay in current phase with modifications
            pass
        elif response == "rollback":
            self.rollback()
        elif response == "cancel":
            self.cancel()

    def advance_phase(self):
        phases = ["analysis", "planning", "implementation", "verification", "complete"]
        current_idx = phases.index(self.phase)
        if current_idx < len(phases) - 1:
            self.phase = phases[current_idx + 1]
```

### Confirmation Points

```mermaid
flowchart LR
    subgraph Checkpoint["Confirmation Checkpoint"]
        S[Summary of work done]
        O[Options presented]
        W[Wait for user input]
    end

    Work[Phase Work] --> Checkpoint
    Checkpoint --> Next[Next Phase]
    Checkpoint --> Redo[Redo Phase]
    Checkpoint --> Cancel[Cancel Workflow]
```

## Example: Database Migration Wizard

```markdown
## Phase 1: Analysis

I've analyzed your database schema and found:

**Tables to migrate**: 12
**Total records**: ~50,000
**Foreign key relationships**: 8
**Estimated time**: 5-10 minutes

**Potential issues identified**:
- `users.legacy_id` column has NULL values (235 records)
- `orders.status` uses string enum, new schema uses integer

**Options**:
1. **Approve** - Continue to planning phase
2. **Investigate** - Show me the problematic records
3. **Cancel** - Abort migration

---

## Phase 2: Planning (after approval)

**Migration Plan**:

1. Create backup of current database
2. Add new columns with defaults
3. Run data transformation scripts
4. Validate data integrity
5. Switch foreign keys
6. Remove legacy columns

**Rollback strategy**: Restore from backup created in step 1

**Options**:
1. **Approve** - Execute migration
2. **Modify** - Adjust the plan
3. **Cancel** - Abort migration
```

## Best Practices

### Phase Design

```mermaid
mindmap
  root((Wizard Phases))
    Analysis
      Gather information
      Identify risks
      Present findings
    Planning
      Detail steps
      Estimate impact
      Define rollback
    Implementation
      Execute changes
      Log actions
      Handle errors
    Verification
      Validate results
      Run tests
      Document outcome
```

### Confirmation Prompts

**Good prompt**:
```
I've identified 3 security vulnerabilities in the auth module:

1. SQL injection in login query (CRITICAL)
2. Missing rate limiting (HIGH)
3. Weak password hashing (MEDIUM)

Estimated fix time: 2 hours

Options:
- [Approve] Continue with fixes
- [Details] Show me the vulnerable code
- [Prioritize] Fix critical only
- [Cancel] Stop and discuss
```

**Poor prompt**:
```
Found issues. Continue? (y/n)
```

### State Persistence

For long wizards, persist state between interactions:

```json
{
  "wizard_id": "migration-2025-01-15",
  "current_phase": "planning",
  "context": {
    "tables_analyzed": 12,
    "issues_found": 2,
    "user_decisions": [
      {"phase": "analysis", "decision": "approve", "timestamp": "..."}
    ]
  },
  "can_rollback": true
}
```

## Do's and Don'ts

### Do

- Provide clear summaries at each checkpoint
- Offer meaningful options (not just yes/no)
- Include rollback capability
- Show progress indicators
- Persist state for long workflows

### Don't

- Create too many micro-checkpoints
- Require approval for trivial steps
- Hide important information
- Make cancellation difficult
- Lose context between phases

## Combining with Other Patterns

### Wizard + Subagents

```mermaid
flowchart TB
    W[Wizard Controller] --> Phase1
    Phase1 --> |spawn| SA1[Analysis Subagent]
    SA1 --> |results| W
    W --> Confirm1{User Confirms}
    Confirm1 --> Phase2
    Phase2 --> |spawn| SA2[Implementation Subagent]
```

### Wizard + Skills

Each phase can leverage specialized skills for its domain:

- Analysis phase → `code-analysis` skill
- Planning phase → `architecture` skill
- Implementation phase → `refactoring` skill

---

## References

- [Claude Code: Plan Mode](https://code.claude.com/docs/en/common-workflows#use-plan-mode-for-safe-code-analysis)
- [Agent Skills: Wizard Workflows](https://leehanchung.github.io/blogs/2025/10/26/claude-skills-deep-dive/)

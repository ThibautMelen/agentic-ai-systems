# Pattern 3: Parallel Tool Calling

> Maximize performance by executing independent tool calls simultaneously.

---

## Overview

Claude 4.x models excel at parallel tool execution. When multiple operations have no dependencies, executing them in parallel dramatically reduces latency and improves efficiency.

## Sequential vs Parallel

```mermaid
flowchart LR
    subgraph Sequential["Sequential (Slow)"]
        S1[Read file1] --> S2[Read file2] --> S3[Read file3]
        S4["~3 round trips<br/>~3x latency"]
    end

    subgraph Parallel["Parallel (Fast)"]
        P1[Read file1]
        P2[Read file2]
        P3[Read file3]
        P4["~1 round trip<br/>~1x latency"]
    end

    P1 & P2 & P3 --> P4
```

## Decision Flow

```mermaid
flowchart TD
    Start[Multiple Tool Calls Needed] --> Check{Dependencies<br/>between calls?}

    Check -->|No dependencies| Parallel[Execute in Parallel]
    Check -->|Has dependencies| Sequential[Execute Sequentially]

    Parallel --> PE["Example:<br/>Read 5 files simultaneously"]
    Sequential --> SE["Example:<br/>mkdir && cp files"]

    PE --> Done[Aggregate Results]
    SE --> Done
```

## When to Parallelize

### Parallelize (No Dependencies)

| Operation | Example |
|-----------|---------|
| Reading multiple files | `Read file1, file2, file3` |
| Searching different patterns | `Grep pattern1, pattern2` |
| Running independent commands | `git status`, `npm test` |
| Fetching multiple URLs | `WebFetch url1, url2` |

### Keep Sequential (Has Dependencies)

| Operation | Example |
|-----------|---------|
| Create then use | `mkdir dir && cp file dir/` |
| Write then read | `Write file && Read file` |
| Build then test | `npm build && npm test` |
| Commit flow | `git add && git commit && git push` |

## Configuration Prompt

Add this to your system prompt for maximum parallelization:

```xml
<use_parallel_tool_calls>
If you intend to call multiple tools and there are no dependencies
between the tool calls, make all of the independent calls in parallel.

Prioritize calling tools simultaneously whenever actions can be done
in parallel rather than sequentially.

Example: When reading 3 files, run 3 tool calls in parallel to read
all 3 files into context at the same time.

Maximize use of parallel tool calls where possible to increase speed
and efficiency.

However, if some tool calls depend on previous calls to inform
dependent values like parameters, do NOT call these tools in parallel
and instead call them sequentially.

Never use placeholders or guess missing parameters in tool calls.
</use_parallel_tool_calls>
```

## Reducing Parallelization

If parallel execution causes issues (e.g., rate limits, system bottlenecks):

```xml
<sequential_execution>
Execute operations sequentially with brief pauses between each step
to ensure stability. Only parallelize when explicitly beneficial.
</sequential_execution>
```

## Practical Examples

### Research Task

```mermaid
flowchart LR
    subgraph Parallel["Parallel Execution"]
        G1[Glob: find *.ts files]
        G2[Grep: search 'auth']
        G3[Read: package.json]
    end

    Parallel --> Analyze[Analyze Results]
```

### Code Review

```mermaid
flowchart LR
    subgraph Parallel["Parallel Execution"]
        D[git diff]
        S[git status]
        L[git log -5]
    end

    Parallel --> Review[Review Changes]
```

### Multi-File Edit

```mermaid
flowchart TD
    Read["Read all files (parallel)"]
    Read --> R1[file1.ts]
    Read --> R2[file2.ts]
    Read --> R3[file3.ts]

    R1 & R2 & R3 --> Analyze[Analyze patterns]
    Analyze --> Edit["Edit files (can be parallel<br/>if changes are independent)"]
```

## Claude 4.x Behavior

### Sonnet 4.5
- **Highly aggressive** parallel tool calling
- May fire multiple operations simultaneously by default
- Can bottleneck system performance if not managed

### Opus 4.5
- **Balanced** parallel execution
- More conservative than Sonnet
- Better at identifying true dependencies

## Performance Impact

| Scenario | Sequential | Parallel | Improvement |
|----------|------------|----------|-------------|
| Read 5 files | ~5 round trips | ~1 round trip | **5x faster** |
| Search 3 patterns | ~3 round trips | ~1 round trip | **3x faster** |
| Complex research | ~10 round trips | ~3-4 round trips | **2.5-3x faster** |

## Anti-Patterns

### Don't: Guess Missing Parameters

```
# BAD - Guessing file content before reading
Edit file.ts with changes based on assumed content

# GOOD - Read first, then edit
Read file.ts → Analyze → Edit file.ts
```

### Don't: Parallel Dependent Operations

```
# BAD - Parallel when dependent
mkdir new-dir | cp file.txt new-dir/

# GOOD - Sequential for dependencies
mkdir new-dir && cp file.txt new-dir/
```

### Don't: Over-Parallelize API Calls

```
# BAD - May hit rate limits
Parallel: 50 API calls simultaneously

# GOOD - Batch reasonably
Parallel: 5 API calls, then next 5, etc.
```

## Best Practices

### Do

- Parallelize all independent read operations
- Batch search queries when exploring codebases
- Run independent validation checks simultaneously
- Use parallel git commands for status gathering

### Don't

- Parallelize operations with data dependencies
- Guess or use placeholders for unknown parameters
- Over-parallelize to the point of system strain
- Ignore rate limits on external services

## SDK Example

```typescript
// Claude will automatically parallelize these independent reads
const result = await query({
  prompt: "Analyze the authentication system",
  // Claude identifies these as independent and runs in parallel:
  // - Glob for auth files
  // - Grep for 'password' patterns
  // - Read package.json for dependencies
});
```

---

## References

- [Claude 4.5 Best Practices: Parallel Tool Calling](https://docs.anthropic.com/docs/en/build-with-claude/prompt-engineering/claude-4-best-practices#optimize-parallel-tool-calling)
- [Anthropic Engineering: Advanced Tool Use](https://www.anthropic.com/engineering/advanced-tool-use)

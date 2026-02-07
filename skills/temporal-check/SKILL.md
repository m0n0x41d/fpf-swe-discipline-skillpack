---
name: temporal-check
description: "Use when debugging discrepancies between expected and actual behavior, validating implementations against specs, or when code doesn't do what documentation says. Triggers: 'it should work but doesn't', 'according to the docs', 'the spec says', behavior differs from comments/types/tests, or any mismatch between intention and execution."
---

# Plan vs Reality Check

Separate design-time artifacts from run-time reality. Documentation is hypothesis, not description.

## Two Domains

**Design-time (Plan)** — What we intend or believe:
- Documentation, comments, README files
- Type signatures, interface definitions
- Architecture diagrams, sequence diagrams
- Test names and descriptions
- Variable/function names
- Specifications, requirements

**Run-time (Reality)** — What actually happens:
- Actual execution behavior
- Log output, metrics, traces
- Test results (pass/fail, actual values)
- Error messages, stack traces
- Database state, file contents
- Network traffic, API responses

## Core Insight

**Design-time artifacts are hypotheses about run-time behavior.**

A comment saying `// returns user or null` is a claim, not a fact. The function might throw, return undefined, or hang. Only run-time observation confirms behavior.

## Debugging Application

When behavior differs from expectation:

**1. Establish what IS (run-time)**
Observe actual behavior without assumptions. Log, trace, inspect.

**2. Establish what SHOULD BE (design-time)**
Check docs, types, specs, comments. What was the intention?

**3. Identify the gap**
Where exactly does reality diverge from plan?

**4. Identify the transformer**
Code doesn't change itself. What process/person is responsible for:
- Changing reality to match plan (fix the bug)?
- Changing plan to match reality (update the docs)?

## Output Format

```
OBSERVATION (Run-time):
[What actually happens — logs, test output, observed behavior]

EXPECTATION (Design-time):
[What documentation/types/specs say should happen]

GAP:
[Specific discrepancy between observation and expectation]

TRANSFORMER NEEDED:
- To fix reality: [Who/what changes the code, when]
- To fix plan: [Who/what updates docs, when]

WHICH IS CORRECT?
[Is the code wrong or the documentation wrong?]
```

## Common Traps

**Trusting comments over code:**
```go
// getUserByID returns the user or nil if not found
func getUserByID(id string) *User {
    // Actually panics on not found — comment is wrong
}
```

**Trusting types over behavior:**
```typescript
function process(data: ValidatedInput): Result {
    // Type says validated, but validation might be incomplete
    // Run-time: data.field might still be undefined
}
```

**Trusting tests over production:**
```
Test: "handles 1000 concurrent users" — passes in CI
Reality: Production has different network latency, actual load patterns differ
```

## Verification Rule

Before claiming L2 confidence, verify run-time behavior directly. Design-time artifacts (docs, types, comments) only support L1 at best.

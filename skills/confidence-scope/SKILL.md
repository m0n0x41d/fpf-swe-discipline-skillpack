---
name: confidence-scope
description: "Use when making assertions about code behavior, root cause claims, architectural assumptions, or any statement that could be wrong. Triggers: stating why something works/fails, claiming a fix will work, asserting behavior without testing, making recommendations, or any claim that influences decisions."
---

# Confidence and Scope Marking

Every assertion has a confidence level and a scope. Mark both explicitly.

## Confidence Levels

**L0 — Untested guess**
Plausible but not verified. Based on intuition, pattern matching, or incomplete information.
- "I suspect the timeout is causing this" (haven't checked logs)
- "This might be a caching issue" (haven't verified cache state)
- "Probably need to increase memory" (haven't profiled)

**L1 — Logically derived**
Follows from premises but not empirically tested in this context.
- "If the config says 30s timeout, and the operation takes 45s, it will timeout" (haven't seen it happen)
- "Since we're using PostgreSQL, we can use JSONB" (haven't tested the specific query)
- "The refactor preserves behavior because the logic is identical" (haven't run tests)

**L2 — Empirically verified**
Tested and confirmed in this specific context.
- "The timeout causes this — I reproduced it by setting timeout to 1s" (verified)
- "The query returns correct results — integration tests pass" (verified)
- "The fix works — I ran the failing test and it passes now" (verified)

## Scope Qualifiers

**this-project** — Verified here, may not apply elsewhere.
- "L2 (this-project): Our PostgreSQL setup handles 10k concurrent connections"

**this-stack** — Applies to this technology stack generally.
- "L2 (Go): Goroutines are cheap, spinning up thousands is fine"

**universal** — Applies broadly across contexts.
- "L2 (universal): Hash maps have O(1) average lookup"

## When to Mark

Mark confidence explicitly when:
- Stating root cause of a bug
- Claiming a fix will work
- Making architectural recommendations
- Asserting behavior of code you haven't run
- Any claim that influences decisions

## Usage Examples

```
The connection pool is exhausted (L0 — haven't checked metrics yet).

If the pool max is 10 and we have 15 concurrent requests, 
some will wait (L1 — logically follows, not yet observed).

Confirmed: pool_waiting_count=5 in metrics (L2, this-project).
```

```
Recommendation: Use Redis for session storage.
Confidence: L1 (this-stack) — standard pattern for Go web apps, 
haven't benchmarked for our specific load profile.
```

## Escalation Rules

- Don't claim L2 without actual verification
- Don't act on L0 for irreversible changes
- L1 is sufficient for reversible experiments
- Production changes require L2 or explicit risk acceptance

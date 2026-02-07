---
name: wlnk-mono
description: "Use for dependency evaluation, security review, reliability assessment, or when considering adding components/complexity. Triggers: 'is this reliable', 'should we add X', evaluating third-party libraries, reviewing system architecture, assessing single points of failure, or any 'improvement' that adds complexity."
---

# Weakest Link and MONO Analysis

System reliability equals its weakest component. Adding complexity creates new failure points.

## Weakest Link Principle (WLNK)

**Core rule:** Aggregate reliability = min(component reliabilities), never average.

A chain with links of 99%, 99%, 95%, 99% reliability has 95% reliability, not 98%.

### Application

**1. Identify the critical path**
What components must work for the operation to succeed?

**2. Estimate each component's reliability**
Use available evidence: uptime history, error rates, known issues, maintenance frequency.

**3. Find the minimum**
The weakest component caps system reliability.

**4. Decide**
- Acceptable? Document and monitor the weak link.
- Unacceptable? Strengthen the weakest component (not the others).

### Output Format

```
CRITICAL PATH: [Component] → [Component] → [Component]

RELIABILITY ESTIMATES:
- Component A: High (99.9%) — managed service, good track record
- Component B: Medium (99%) — our code, tested but complex
- Component C: Low (95%) — third-party API, known instability

WEAKEST LINK: Component C (third-party API)
SYSTEM CEILING: ~95% reliability

MITIGATION OPTIONS:
1. Add fallback/cache for Component C
2. Replace Component C with more reliable alternative
3. Accept risk with monitoring and alerting
```

## MONO Check (Monotonicity)

**Core rule:** Adding components can decrease reliability.

Each addition introduces new failure modes, complexity, and maintenance burden. The benefit must outweigh the new weak links created.

### Before Adding Complexity

Ask: "Does this addition create new failure points?"

**Examples of MONO violations:**
- Adding a cache layer: New failure mode (cache inconsistency), new weak link (cache service availability)
- Adding a microservice: New failure mode (network partition), new weak link (service discovery)
- Adding an abstraction: New failure mode (abstraction leaks), new weak link (developer understanding)

### MONO Output Format

```
PROPOSED ADDITION: [What we want to add]

NEW WEAK LINKS CREATED:
- [Failure mode 1]: [How it could fail]
- [Failure mode 2]: [How it could fail]

BENEFIT: [What we gain]

MONO VERDICT: 
- Justified: Benefits outweigh new failure modes
- Not justified: Complexity not warranted
- Conditional: Justified only if [specific mitigation]
```

## Combined Assessment

For significant changes, run both analyses:

```
CHANGE: Add Redis caching layer

WLNK ANALYSIS:
Current weakest link: Database (Medium, 99%)
Redis reliability: High (99.9% for managed service)
New weakest link: Still database — Redis doesn't help WLNK

MONO ANALYSIS:
New failure modes: Cache invalidation bugs, Redis unavailability
Benefits: Reduced DB load, faster responses

VERDICT: MONO violation risk. Cache adds complexity without 
improving weakest link. Consider: Is DB actually the bottleneck?
Measure first (L0 → L2), then decide.
```

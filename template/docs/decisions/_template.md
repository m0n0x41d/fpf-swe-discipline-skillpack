---
adr: "0000"
title: "Template — Copy and Rename"
date: YYYY-MM-DD
status: proposed
stage: explore
confidence: L0
scope: this-project
supersedes: []
related: []
---

# ADR-0000: [Title]

## Status

**Status:** Proposed  
**Stage:** Explore  
**Confidence:** L0  
**Scope:** this-project

## Context and Problem Statement

[What specifically is the problem or decision point? What anomaly or need triggered this decision? Be concrete and measurable.]

## Hypotheses Considered

### H1: [Option Name]

**Description:** [What this approach does, how it works]

**If true, then:**
- [Testable prediction 1 — what we should observe if this works]
- [Testable prediction 2]

**Evidence for:** [What supports choosing this option]

**Evidence against:** [What contradicts or creates risk]

**Weakest link:** [Most fragile assumption or component in this approach]

### H2: [Option Name]

**Description:** [What this approach does, how it works]

**If true, then:**
- [Testable prediction 1]
- [Testable prediction 2]

**Evidence for:** [What supports this]

**Evidence against:** [What contradicts]

**Weakest link:** [Most fragile assumption]

### H3: [Option Name] (if needed)

[Same structure — add more hypotheses for Shape stage decisions]

## Analysis

**MONO Check:** [Does the chosen option add complexity? What new failure points does it create? Is this justified?]

**Comparison:** [Why does the chosen hypothesis survive while others don't? What evidence was decisive?]

## Decision

**Chosen:** H[N] — [Option Name]

**Confidence:** L[0-2]  
**Scope:** [this-project | this-stack | universal]

**Rationale:** [Brief statement of why this option over others]

## Transformer

**Executed by:** [Person, team, or automated system responsible for implementation]

**Timeline:** [When will this be implemented? Phases if applicable]

**Dependencies:** [What must happen first? Blockers?]

**Verification:** [How do we confirm the decision is correctly implemented?]

## Consequences

**Positive:**
- [Expected benefit 1]
- [Expected benefit 2]

**Negative:**
- [Known tradeoff 1]
- [Known tradeoff 2]

**Risks:**
- [What could go wrong] — Mitigation: [How we address it]

## Review Triggers

Revisit this decision if:
- [Condition 1 — e.g., "Load exceeds 10k requests/second"]
- [Condition 2 — e.g., "Team size doubles"]
- [Condition 3 — e.g., "Underlying assumption X is invalidated"]

---

## Status Lifecycle

```
proposed → accepted → [validated | superseded | deprecated]
                          ↓
                     (Evidence stage confirms it works)
```

**Status definitions:**
- **proposed** — Under discussion, not yet approved
- **accepted** — Approved, implementation can proceed
- **validated** — Implemented and confirmed working in production (Operate stage)
- **superseded** — Replaced by another ADR (link to replacement)
- **deprecated** — No longer applicable, kept for historical reference

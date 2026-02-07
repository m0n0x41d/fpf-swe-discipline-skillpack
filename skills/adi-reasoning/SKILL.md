---
name: adi-reasoning
description: "Use for architectural decisions, debugging with unclear cause, choosing between technical approaches, or any situation requiring structured analysis. Triggers: 'should we use X or Y', 'why is this failing', 'what's the best approach', design discussions, root cause analysis, or when multiple valid options exist."
---

# Hypothesis-Based Reasoning

Structured approach: generate explanations → derive predictions → test against evidence.

## When to Use

- Architectural decisions (database choice, service boundaries, API design)
- Debugging with unclear cause (intermittent failures, unexpected behavior)
- Choosing between approaches (frameworks, patterns, implementations)
- Any decision where multiple valid options exist

## Process

**1. Frame the anomaly**
State specifically what doesn't work or is unknown. Be concrete and measurable.
- Bad: "The system is slow"
- Good: "API response time increased from 50ms to 800ms after deployment X"

**2. Generate hypotheses**
Minimum count per Calibration Matrix (Explore: 1-2, Shape: 2-3, Evidence: fixed).
Each hypothesis must be falsifiable — if you can't imagine evidence against it, it's not a hypothesis.

**3. Derive predictions**
For each hypothesis: "If H is true, then we should observe X, Y, Z."
Predictions must be testable with available tools/data.

**4. Test predictions**
Check predictions against evidence (logs, metrics, tests, code inspection).
Update confidence based on results.

**5. Iterate or conclude**
- All predictions confirmed → Conclude with confidence level
- Some predictions failed → Back to step 2 with new information
- No hypothesis survives → Reframe the anomaly

## Output Format

```
ANOMALY: [Specific, measurable problem statement]

HYPOTHESES:
H1: [Description]
    If true → [Prediction 1], [Prediction 2]
    Weakest assumption: [What's most likely wrong]
    
H2: [Description]
    If true → [Prediction 1], [Prediction 2]
    Weakest assumption: [...]

EVIDENCE CHECKED:
- [What we looked at] → [What we found] → [Supports H1/H2/neither]

SURVIVING HYPOTHESIS: H[N]
CONFIDENCE: L[0-2] — Scope: [where this applies]
NEXT ACTION: [What to do with this conclusion]
```

## Anti-patterns

- **Single hypothesis** — Always generate alternatives, even if one seems obvious
- **Unfalsifiable claims** — "It might be a race condition" without specifying what evidence would disprove it
- **Skipping predictions** — Going straight from hypothesis to "let's try it"
- **Confirmation bias** — Only looking for evidence that supports preferred hypothesis

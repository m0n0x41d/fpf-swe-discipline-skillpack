# Constraints and Gotchas

Known limitations, invariants, and surprises discovered during development.

## Invariants

[Things that must always be true for the system to work correctly.]

**[Invariant name]:** [Description of what must hold]

Violation consequence: [What breaks if this invariant is violated]

## Known Limitations

[Documented limitations of the current implementation.]

**[Limitation]:** [Description]

Workaround: [How to work around it if needed]

Future: [Plans to address, or why it's acceptable]

## Gotchas

[Surprising behaviors or non-obvious requirements discovered during development.]

### [Gotcha Title]

**Discovered:** [Date]

**Symptom:** [What you observed that was surprising]

**Root cause:** [Why it happens]

**Solution/Workaround:** [How to handle it]

**Confidence:** L[0-2] — [How certain are we about this]

## Environment-Specific

[Things that behave differently across environments.]

### Development vs Production

[Differences that matter]

### CI vs Local

[Differences that have caused issues]

## Performance Boundaries

[Known performance limits of the system.]

**[Metric]:** [Current limit] (L[0-2], measured [when])

Example: "Concurrent connections: 500 (L2, load tested 2025-01)"

## Security Constraints

[Security-related requirements and restrictions.]

[Note: Don't document secrets. Document the constraints around them.]

## External Dependencies

[Constraints imposed by external services or APIs.]

**[Service/API]:**

Rate limits: [Limits]

Timeout behavior: [What happens on timeout]

Known issues: [Any known problems]

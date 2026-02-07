# Project Documentation

This directory contains project-specific knowledge that persists across sessions.

## Structure

```
docs/
├── decisions/           # Architecture Decision Records (ADRs)
│   ├── _template.md     # FPF-enhanced ADR template
│   └── 0001-*.md        # Numbered decisions
├── context/             # Project facts and evidence
│   ├── stack.md         # Technologies, versions, rationale
│   ├── commands.md      # Build, test, deploy commands
│   ├── constraints.md   # Known limitations, invariants, gotchas
│   ├── patterns.md      # Debugging patterns, resolved issues
│   └── integrations.md  # External APIs, services, contracts
└── active-context.md    # Current session state for handoff
```

## Usage Guidelines

### decisions/

Architectural Decision Records document significant technical decisions. Use the FPF-enhanced template which includes hypothesis analysis, confidence levels, and transformer specification.

**When to create an ADR:**
- Choosing between technologies or frameworks
- Defining service boundaries or API contracts
- Establishing patterns that affect multiple parts of codebase
- Any decision that would be expensive to reverse

**Naming convention:** `NNNN-short-descriptive-title.md` (zero-padded four digits)

**Lifecycle:** proposed → accepted → validated/superseded/deprecated

### context/

Project facts and evidence accumulated during development. Unlike decisions (which capture choices), context captures knowledge.

**stack.md** — Technologies, versions, and why they were chosen. Update when dependencies change.

**commands.md** — How to build, test, lint, deploy. Common operations with exact commands.

**constraints.md** — Known limitations, invariants that must hold, gotchas discovered during development. Things that surprised you belong here.

**patterns.md** — Debugging patterns and resolved issues. When you solve a tricky bug, document the pattern here so it doesn't have to be re-discovered.

**integrations.md** — External API contracts, third-party service details, webhook formats. Include example payloads.

### active-context.md

Session handoff state. Update at the end of work sessions with:
- Current task and its status
- Recent changes made
- Known blockers or open questions
- Next steps planned

This allows seamless continuation across sessions.

## Confidence and Scope

When documenting facts in context/, mark confidence and scope where non-obvious:

```markdown
PostgreSQL handles our load well (L2, this-project — tested up to 5k concurrent).
```

For decisions/, confidence and scope are built into the ADR template.

## Maintenance

- Keep files focused — split if they grow beyond ~200 lines
- Update when facts change — stale documentation is worse than none
- Delete obsolete entries — mark superseded, then remove after grace period
- Review quarterly — audit for accuracy and relevance

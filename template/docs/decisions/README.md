# Architecture Decision Records

This directory contains Architecture Decision Records (ADRs) documenting significant technical decisions.

## Index

| ADR | Title | Status | Stage | Date |
|-----|-------|--------|-------|------|
| [0001](0001-example.md) | [Example ADR title] | accepted | shape | YYYY-MM-DD |

## Process

**When to create an ADR:**
- Choosing between technologies, frameworks, or major dependencies
- Defining service boundaries, API contracts, or data models
- Establishing patterns that affect multiple parts of the codebase
- Any decision that would be expensive to reverse
- Decisions where future developers will ask "why did we do it this way?"

**How to create:**
1. Copy `_template.md` to `NNNN-short-title.md` (next sequential number)
2. Fill in all sections — especially hypotheses and transformer
3. Set status to `proposed`
4. Discuss with team if applicable
5. Update status to `accepted` when approved

**Lifecycle:**
```
proposed → accepted → validated | superseded | deprecated
```

## Status Definitions

**proposed** — Decision is drafted and under discussion

**accepted** — Decision is approved, implementation can proceed

**validated** — Decision has been implemented and confirmed working in production (Operate stage)

**superseded** — Decision has been replaced by another ADR (link to successor in frontmatter)

**deprecated** — Decision is no longer applicable but kept for historical reference

## Stage Mapping

ADRs correspond to ESG lifecycle stages:

| Stage | ADR Status | Typical Actions |
|-------|------------|-----------------|
| Explore | N/A (use active-context.md) | Quick notes, not formal ADR |
| Shape | proposed → accepted | Full hypothesis analysis |
| Evidence | accepted | Testing predictions, updating with results |
| Operate | validated | Production confirmation, monitoring setup |

## Searching

To find relevant ADRs:
- Check the index above
- Search by status: `grep -l "status: accepted" *.md`
- Search by topic: `grep -ril "database" .`

## Review Triggers

Each ADR lists conditions that should trigger re-evaluation. Review ADRs when:
- Listed trigger conditions occur
- Underlying assumptions change
- Significant time has passed (quarterly review)
- Problems arise that might relate to past decisions

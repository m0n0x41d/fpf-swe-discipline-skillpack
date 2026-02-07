# Debugging Patterns and Resolved Issues

Documented solutions to problems encountered during development. Check here before debugging from scratch.

## How to Use This Document

When you encounter an issue, check if a pattern here matches your symptoms. When you solve a novel issue, document the pattern so others (and future you) don't have to re-discover it.

## Patterns

### [Pattern Title]

**Symptoms:** [What you observe when this problem occurs]

**Root Cause:** [Why it happens]

**Diagnosis Steps:**
1. [How to confirm this is the issue]
2. [What to check]

**Solution:** [How to fix it]

**Prevention:** [How to avoid it in future]

**Confidence:** L[0-2]  
**Last Verified:** [Date]

---

### [Example: Connection Pool Exhaustion]

**Symptoms:** Requests hang, timeouts increase gradually, eventually all requests fail. Database reports max connections reached.

**Root Cause:** Connections not being returned to pool, usually due to missing `defer conn.Close()` or errors in transaction handling that skip cleanup.

**Diagnosis Steps:**
1. Check database connection count: `SELECT count(*) FROM pg_stat_activity`
2. Check pool metrics if available
3. Search for connection acquisition without corresponding release

**Solution:** Ensure every connection acquisition has corresponding release, preferably with `defer` immediately after acquisition.

**Prevention:** Use linting rules to detect missing defer patterns. Add pool exhaustion alerts.

**Confidence:** L2  
**Last Verified:** [Date]

---

## Issue Log

For issues that don't generalize into patterns, log them here for reference.

| Date | Issue | Resolution | Files Affected |
|------|-------|------------|----------------|
| [date] | [brief description] | [what fixed it] | [relevant files] |

---
name: bounded-context
description: "Use for cross-service integration, API design, microservice boundaries, or when terms might mean different things in different contexts. Triggers: integrating with external APIs, designing service interfaces, 'in our system X means...', translating between domains, or any work crossing team/service/system boundaries."
---

# Bounded Context and Term Translation

Same word ≠ same meaning. Explicit translation required across boundaries.

## Core Principle

Every term has meaning within a specific bounded context. When crossing context boundaries, require explicit translation. Translation always has some loss.

## Common Boundary Types

**Service boundaries:** User in Auth service vs User in Billing service
**Team boundaries:** "Sprint" in Engineering vs "Sprint" in Marketing
**System boundaries:** Order in your system vs Order in payment provider API
**Domain boundaries:** "Account" in banking vs "Account" in software (user account)

## Translation Process

**1. Identify the boundary**
Where are you crossing from one context to another?

**2. List shared terms**
What words appear on both sides of the boundary?

**3. Map meanings**
For each term: Are they semantically equivalent? Partially overlapping? Completely different?

**4. Document translation**
Explicit mapping with noted losses.

## Output Format

```
BOUNDARY: [Context A] ↔ [Context B]

TERM MAPPING:

| Term | Context A Meaning | Context B Meaning | Congruence |
|------|-------------------|-------------------|------------|
| User | Authenticated identity with session | Billing entity with payment methods | Partial |
| Account | Login credentials | Financial account with balance | None |
| Order | Shopping cart checkout | Payment transaction | Partial |

TRANSLATION RULES:
- A.User.id → B.Customer.external_id (1:1)
- A.User.email → B.Customer.billing_email (may differ from contact email)
- A.Order → B.Transaction (loses: cart history, gains: payment status)

CONGRUENCE LEVEL: Medium
INFORMATION LOST IN TRANSLATION: [What doesn't survive the boundary]
```

## Congruence Levels

**High:** Terms map 1:1 with minimal semantic loss. Safe to use interchangeably with care.

**Medium:** Terms overlap but have different boundaries or attributes. Explicit mapping required; some information lost.

**Low:** Terms share a name but have substantially different meanings. Treat as different concepts that happen to share a name.

**None:** Same word, completely different meanings. Never translate directly; use explicit renaming.

## Red Flags

**Same name assumed equivalent:**
```
// Dangerous — assumes User means the same thing
externalAPI.updateUser(internalUser) 
```

**Missing attributes in translation:**
```
// Internal Order has 20 fields, external expects 5
// What happens to the other 15? Lost? Stored elsewhere?
```

**Implicit conversions:**
```
// ID types differ: internal is UUID, external is integer
// Silent conversion can corrupt data
```

## Defensive Patterns

**Explicit translation layer:**
```go
func toExternalUser(internal InternalUser) ExternalUser {
    // Every field mapping explicit and documented
    // Compiler catches missing fields
}
```

**Anti-corruption layer:**
```
[Your Domain] → [Translation Layer] → [External Domain]
                 Explicit mapping
                 Validation
                 Loss documentation
```

**Naming conventions:**
```
internalUserID  // Our User
externalUserID  // Their User
billingCustomerID  // Billing context
```

## Integration Checklist

Before integrating across boundaries:
1. List all terms that appear in both contexts
2. Map each term explicitly (don't assume equivalence)
3. Document what information is lost in translation
4. Add validation at the boundary
5. Use distinct types/names when meanings differ

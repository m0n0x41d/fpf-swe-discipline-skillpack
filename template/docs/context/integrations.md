# External Integrations

API contracts, third-party services, webhooks, and external dependencies.

## Services

### [Service Name]

**Purpose:** [What this integration does]

**Environment:**
- Production: [endpoint/URL]
- Staging: [endpoint/URL]
- Development: [endpoint/URL or mock]

**Authentication:** [Method — API key, OAuth, etc. DO NOT include actual credentials]

**Rate Limits:** [Limits and how we handle them]

**Timeout Configuration:** [Our timeout settings and rationale]

**Error Handling:** [How we handle failures from this service]

**Monitoring:** [How we detect issues with this integration]

---

## API Contracts

### [API Name]

#### Request

```
[Method] [Endpoint]
Content-Type: application/json

{
  "field": "description and type",
  "nested": {
    "field": "description"
  }
}
```

#### Response (Success)

```json
{
  "field": "description and type"
}
```

#### Response (Error)

```json
{
  "error": "description of error format"
}
```

#### Notes

[Any non-obvious behavior, edge cases, or gotchas]

---

## Webhooks

### [Webhook Name]

**Source:** [What system sends this webhook]

**Endpoint:** [Where we receive it]

**Authentication:** [How we verify authenticity]

**Payload Format:**

```json
{
  "event": "event_type",
  "data": {}
}
```

**Retry Behavior:** [What the sender does if we fail to respond]

**Our Response Requirements:** [What we must return]

---

## Bounded Context Mappings

[Document term translations between our system and external systems. Reference: @skills/bounded-context.md]

### [External System] ↔ Our System

| External Term | Our Term | Congruence | Notes |
|---------------|----------|------------|-------|
| [their term] | [our term] | High/Medium/Low/None | [translation notes] |

---

## Dependency Health

[Track reliability and known issues with external dependencies]

| Service | Reliability | Last Incident | Notes |
|---------|-------------|---------------|-------|
| [name] | High/Medium/Low | [date or N/A] | [any concerns] |

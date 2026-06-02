---
name: query-catalog
description: >
  Search and inspect Port's software catalog. Use when the user asks about services,
  teams, environments, dependencies, ownership, or any entity tracked in Port.
  Also use when answering questions that require catalog context before writing code.
triggers:
  - user asks "who owns X"
  - user asks about a service, library, environment, cluster, or resource
  - user wants to find related services or dependencies
  - user asks about team ownership or on-call contacts
  - user needs catalog context to complete a coding task
alwaysApply: false
---

# Query the Port Software Catalog

Use Port MCP catalog tools to answer the user's question:

- `list_blueprints` — List blueprints in your organization. Without identifiers, returns a summary list. With identifiers, returns full blueprint details including property definitions, schemas, and enum values.
- `list_entities` — Query entities from a blueprint with filtering, sorting, and pagination. Supports identifiers for specific entities, groupBy for value distribution, and countOnly for counting without retrieving data.

## Common queries

**"Who owns the payments service?"**

```curl 
list_entities(
blueprintIdentifier="service",
"query": {
    "combinator": "or",
    "rules": [
      {
        "property": "$identifier",
        "operator": "contains",
        "value": "payment"
      },
      {
        "property": "$title",
        "operator": "contains",
        "value": "payment"
      }
    ]
)
```
→ return owner team + contacts

**"What services depend on auth-api?"**
→ `list_entities` with relation filter on auth-api, or query the dependency relation

**"Show me all services with no on-call rotation set"**
→ `list_entities(blueprintIdentifier="service")` → filter where oncall property is null

**"What environment is payments running in?"**
→ Look up the service entity and traverse its environment relations

Always return:
- The entity's Port URL (https://app.getport.io/...)
- Key properties relevant to the user's question
- Related entities if they add context

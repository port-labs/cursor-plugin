---
name: day2-ops
description: >
  Execute common day-2 operations through Port self-service actions: scale services,
  rotate secrets, update environment variables, request cloud resources, manage
  permissions, and trigger maintenance workflows — using natural language from Cursor.
triggers:
  - user wants to scale, resize, or tune a service
  - user wants to rotate credentials or secrets
  - user wants to update config or environment variables in production
  - user requests cloud resource (database, queue, bucket)
  - user wants to manage team access or permissions
alwaysApply: false
---

# Day-2 Operations via Port

Port self-service actions are the single pane of glass for day-2 ops.
Use `list_actions()` to enumerate what's available.

## Common day-2 workflows

**Scale a service:**
Find the "Scale Service" or "Update Replicas" action → collect service + replica count → `run_action`.

**Rotate a secret:**
Find the "Rotate Secret" action → confirm which secret + service → `run_action` → confirm rotation.

**Update environment variable:**
Find the "Update Config" action → collect key/value/environment → `run_action`.

**Request a new database:**
Find the "Provision Database" action → collect size, engine, environment → `run_action` → return DB endpoint.

**Manage access:**
Find the "Grant/Revoke Access" action → collect user + resource + role → `run_action`.

Always:
- Show the user a confirmation summary before executing destructive or production-scoped actions.
- Poll `track_action_run` and report completion.
- Provide the Port run URL for audit trail.

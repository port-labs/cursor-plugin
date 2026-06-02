---
name: dag-context
description: >
  Before writing, reviewing, or debugging code for a named service, automatically
  fetch its Port catalog entry to inject ownership, dependencies, SLOs, runbooks,
  and environment details as context. Makes coding assistance more accurate and
  context-aware.
triggers:
  - user is working on a specific named service and wants code help
  - user asks to review or modify a service that exists in Port
  - user debugging issue in a service — enrich with catalog data
alwaysApply: false
---

# Inject Port Catalog Context for Coding Tasks

When the user names a service (e.g. "help me fix a bug in payments-api"):

1. Call `list_entities(blueprint="service", query="{}")`.
   If not found by exact name, use `list_entities` to find the closest match by refining the query filter.

2. Extract and summarize for context:
   - **Owner team** and Slack/PagerDuty contacts
   - **Tech stack** (language, framework, runtime)
   - **Dependencies** (upstream/downstream services)
   - **Environment** it runs in (staging, production)
   - **On-call** and runbook links
   - **Open incidents** if available

3. Prepend this context to your coding response so recommendations are
   consistent with the actual service setup (e.g. don't suggest Node.js patterns
   for a Python service).

4. If the service isn't in Port, proceed normally but note:
   "I couldn't find [service] in your Port catalog — consider adding it."

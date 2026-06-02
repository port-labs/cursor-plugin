---
name: incident-response
description: >
  Help the user respond to production incidents using Port. Find the affected service,
  look up the on-call team, trigger incident response actions (page on-call, create
  incident ticket, run rollback), and surface runbooks — all without leaving Cursor.
triggers:
  - user mentions an incident, outage, alert, or production issue
  - user wants to page someone or escalate
  - user wants to rollback a deployment
  - user says "who's on call for X"
alwaysApply: false
---

# Incident Response with Port

1. **Identify the service**: resolve the service name to a Port entity.

2. **Surface key contacts**:
   - On-call rotation link or team name from the service entity
   - Slack channel from team entity
   - Runbook URL from the service entity

3. **Available incident actions** (if configured in Port):
   - "Page on-call" action → run via `run_action`
   - "Create incident" (PagerDuty / OpsGenie / Jira) → run via `run_action`
   - "Rollback deployment" → run via `run_action`

4. **Guide the user** through triggering the right action step by step,
   confirming inputs before executing.

5. After action runs, share:
   - Run status and output (incident ticket URL, PD incident link, etc.)
   - Suggested next steps (check logs, review recent deploys, notify stakeholders)
   
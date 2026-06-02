---
name: create-scorecard
description: >
  Create or update a Port scorecard to measure service maturity, production readiness,
  security compliance, or any custom standard. Use when the user wants to define
  quality gates, evaluate their catalog against rules, or check scorecard status.
triggers:
  - user mentions scorecard, maturity, production readiness, compliance score
  - user wants to grade or evaluate services
  - user wants to enforce standards across their catalog
alwaysApply: false
---

# Port Scorecards

## Check existing scorecards
Call `list_scorecards` to show the user what already exists.
For a specific blueprint, call `list_scorecards(blueprint, scorecard_id)`.

## Read scorecard results
To check how a service scores: `list_scorecards(blueprint, entity_id, scorecard_id)`.
Present results as a pass/fail summary per rule, with remediation hints for failing rules.

## Create a new scorecard (if the user wants to define one)
Collect from the user:
- Blueprint it applies to
- Rules (property checks, relation checks, or action availability checks)
- Levels (e.g. Bronze / Silver / Gold)

Then use `upsert_scorecard` or guide the user to https://app.getport.io/settings/scorecards.

## Bulk evaluation
If the user wants to see all services and their scorecard results:
`list_entities(blueprint="service")` → for each, call `list_scorecards`
→ render as a ranked table.

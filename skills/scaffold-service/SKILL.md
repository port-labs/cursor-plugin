---
name: scaffold-service
description: >
  Scaffold a new microservice, library, or component using Port self-service actions.
---

# Scaffold a Service via Port

Create new services and repositories by running the correct Port scaffolding action.

## When to use

- User wants to create a new service
- User asks to scaffold, bootstrap, or create a new microservice or repo
- User wants to run a Port scaffolding action

1. Use the Port MCP to list available scaffolding actions:
   - Call `list_actions` to return all actions.

2. Present the options to the user if more than one exists.

3. Collect required inputs for the chosen action:
   - Service name, owner team, language/framework, repo visibility, etc.
   - Only ask for fields that are required — check the action's input schema first.

4. Invoke the action via `run_action` with the collected inputs.

5. Poll `track_action_run` until the run completes or fails.
   - On success: share the output (e.g. repo URL, entity link in Port catalog).
   - On failure: show the error message and suggest checking Port logs at https://app.getport.io/runs.

6. Offer to open the new entity in Port or navigate to the created repo.

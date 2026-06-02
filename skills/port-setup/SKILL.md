---
name: port-setup
description: >
  First-time initialization of the Port MCP server. Run this when the user wants
  to connect to Port, when Port MCP tools are unavailable, or when authentication
  fails. Guides the user through obtaining credentials and verifying the connection.
triggers:
  - user mentions setting up Port
  - Port MCP tools are not responding
  - authentication error from Port MCP
  - user asks how to connect to Port
alwaysApply: false
---

# Port MCP Setup

The Port MCP server configuration lives at: ../../mcp.json (relative to this SKILL.md).

## Step 1 — Obtain credentials

Direct the user to go to their Port application, click on their profile picture, and select Credentials. Here they can view and copy their PORT_CLIENT_ID and PORT_CLIENT_SECRET.

If the MCP is configured for OAuth, prompt the user to complete the OAuth flow in their browser.

If the MCP uses environment variables, ask the user to provide PORT_CLIENT_ID and PORT_CLIENT_SECRET, then update the env block in mcp.json for them. DO NOT ask the user to edit files manually.

## Step 2 — Verify connection

After credentials are set, call the Port MCP `list_blueprints` tool (or equivalent health-check tool).
If it returns data, the connection is working — confirm this to the user.
If it fails, check whether the credentials match the correct Port organization/region and retry.

## Step 3 — Confirm to the user

Tell the user they're connected and suggest trying:
- "Show me my software catalog"
- "List my self-service actions"
- "What services are owned by the platform team?"

# Port Plugin for Cursor

Give Cursor's AI agent a complete picture of your engineering world.

Port is your engineering system of record, the single source of truth for every service, team, dependency, deployment, and standard across your organization. This plugin connects Cursor directly to your Port Internal Developer Portal via MCP, so the AI agent understands not just your code, but the full context around it: who owns what, what's running where, what's compliant, and what actions are available to take.

---

## Why this matters

Cursor is exceptional at reading and writing code. But the hardest problems in software engineering aren't just about code. They're about context. Who owns this service? What depends on it? Is it production-ready? Who's on call if something breaks?

Port answers those questions. By connecting Cursor to Port, your AI agent can reason across your entire engineering system and take meaningful action. Not just suggest a fix, but scaffold a service, trigger a deployment, check a scorecard, or page the right team.

---

## What Port brings to Cursor

**Your software catalog, queryable in plain English**

Port's catalog maps every service, resource, team, and dependency in your organization. Ask Cursor anything:

```
Who owns the payments service?
What services depend on auth-api?
Show me everything the platform team is responsible for
```

**Self-service actions, triggered from your IDE**

Port's self-service layer exposes day-2 operations as governed, repeatable actions. Cursor can trigger them naturally:

```
Scaffold a new Python microservice called inventory-api
Deploy the payments service to production
Provision a new PostgreSQL database for the billing team
```

**Scorecards and compliance, surfaced in context**

Port's scorecards define and measure production readiness, security standards, and operational maturity across every service. Cursor can check compliance before you ship:

```
What's the production readiness score for my services?
Which services are failing the security compliance scorecard?
Show me all services at Bronze level
```

**Incident response with full organizational context**

When something breaks, Cursor can pull the full picture from Port (ownership, runbooks, on-call rotations) and take action:

```
We have an outage in payments - who's on call?
Page the platform team and open a PagerDuty incident
Show me the runbook for auth-service
```

---

## Requirements

- A [Port](https://port.io) account
- [Cursor](https://cursor.com) v2.6.0 or later

---

## Installation

### From the Cursor Marketplace

1. Open Cursor Settings → **Plugins**
2. Search for **Port MCP**
3. Click **Install**

The plugin configures the Port MCP server automatically.

### Install from this repository

In Cursor Settings → Plugins, paste:

```
port
```

---

## Quick setup

After installing, run `/setup-region` in the Cursor agent. It will ask which region your Port account is on and update the MCP server URL for you automatically.

---

## Data center selection

Port runs in two regions. You need to point the MCP server at the one your organization is on, or authentication will fail.

| Region | MCP server URL |
|--------|----------------|
| EU (default) | `https://mcp.port.io/v1` |
| US | `https://mcp.us.port.io/v1` |

**How to tell which region you're on:**
- Log in to Port and check your browser's address bar
- EU accounts use `app.getport.io`
- US accounts use `app.us.getport.io`

To switch regions, open `mcp.json` and update the `url` field:

```json
{
  "mcpServers": {
    "port": {
      "url": "https://mcp.us.port.io/v1",
      "headers": {
        "x-read-only-mode": "0"
      }
    }
  }
}
```

---

## Authentication

Port MCP uses OAuth. On first use you'll be prompted to authenticate with your Port account in the browser. Once authenticated, your session is stored securely in Cursor, and no credentials are passed to the AI model.

By default, `mcp.json` sets `x-read-only-mode` to `"0"` (write-enabled). To restrict to read-only access, set this value to `"1"` before connecting.

For API key authentication, set these environment variables before starting Cursor:

```bash
PORT_CLIENT_ID=your-client-id
PORT_CLIENT_SECRET=your-client-secret
```

Find your credentials at [app.getport.io/settings/credentials](https://app.getport.io/settings/credentials).

---

## Usage

Once connected, ask the agent anything about your Port portal or trigger actions naturally.

**Catalog queries**
```
Who owns the payments service?
What services depend on auth-api?
Show me all services with no on-call rotation set
```

**Self-service actions**
```
Scaffold a new Python microservice called inventory-api
Deploy the payments service to production
Rollback the last deployment of checkout-service
```

**Day-2 operations**
```
Scale the recommendations service to 4 replicas
Rotate the database credentials for orders-api
Provision a new PostgreSQL database for the billing team
```

**Incident response**
```
We have an outage in payments - who's on call?
Page the platform team and open a PagerDuty incident
Show me the runbook for auth-service
```

**Scorecards**
```
What's the production readiness score for my services?
Which services are failing the security compliance scorecard?
Show me all Bronze-level services
```

---

## Repository structure

```
port-cursor-plugin/
├── .cursor-plugin/
│   └── plugin.json          # Cursor plugin manifest
├── assets/
│   ├── icon.png
│   └── icon.svg
├── rules/
│   └── port-safety.mdc      # Always-active safety rules for Port MCP
├── mcp.json                 # MCP server configuration
├── README.md
└── LICENSE
```

---

## Support

- [Port Documentation](https://docs.port.io)
- [Port MCP Server docs](https://docs.port.io/ai-interfaces/port-mcp-server/available-tools)
- [support@getport.io](mailto:support@getport.io)

## License

MIT. See [LICENSE](./LICENSE) for details.

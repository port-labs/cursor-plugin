# Port Plugin for Cursor

Use your [Port Internal Developer Portal](https://port.io) directly from Cursor through a pre-configured Port MCP server. Query the software catalog, run self-service actions, manage scorecards, and trigger day-2 operations — all through natural language, without leaving your IDE.

---

## What's included

### Port MCP Server

Cursor connects to Port's remote MCP server at `https://mcp.port.io/v1` (EU data center) by default, giving the AI agent direct access to your portal's tools:

- Search and query catalog entities
- Read blueprints and their schemas
- Run self-service actions and poll their status
- Manage scorecards and check compliance results
- Create and update entities

If your account is in the US data center, update `mcp.json` and replace the server URL with `https://mcp.us.port.io/v1`.

## Requirements

- A [Port](https://port.io) account
- [Cursor](https://cursor.com) v2.6.0 or later

---

## Installation

### From the Cursor Marketplace

1. Open Cursor Settings → **Plugins**
2. Search for **Port MCP**
3. Click **Install**

The plugin will configure the Port MCP server automatically.

### Install from this repository

In Cursor Settings → Plugins, paste:

```
port-mcp
```

---

## Authentication

The Port MCP server uses OAuth. On first use you'll be prompted to authenticate with your Port account in the browser. Once authenticated, your session is stored securely in Cursor — no credentials are sent to the AI model.

By default, `mcp.json` sets `x-read-only-mode` to `"0"` (write-enabled). If you want read-only access, change this header value to `"1"` before connecting.

If you'd prefer API key authentication, set the following environment variables before starting Cursor:

```bash
PORT_CLIENT_ID=your-client-id
PORT_CLIENT_SECRET=your-client-secret
```

You can find your credentials at [app.getport.io/settings/credentials](https://app.getport.io/settings/credentials).

---

## Usage

Once connected, ask the agent anything about your Port portal or trigger actions naturally:

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
We have an outage in payments — who's on call?
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

## Having trouble connecting?

If authentication did not complete, ask the agent to verify your Port MCP connection and retry OAuth.

---

## Repository structure

```
port-cursor-plugin/
├── .cursor-plugin/
│   └── plugin.json          # Cursor plugin manifest
├── assets/
│   ├── icon.png
│   └── icon.svg
├── mcp.json                 # MCP server configuration
├── README.md
└── LICENSE
```

---

## Support

- [Port Documentation](https://docs.getport.io)
- [Port MCP Server docs](https://docs.getport.io/mcp)
- [support@getport.io](mailto:support@getport.io)

## License

MIT — see [LICENSE](./LICENSE) for details.

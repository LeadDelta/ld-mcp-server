# LeadDelta MCP Server

Connect your AI assistant to [LeadDelta](https://leaddelta.com) — the LinkedIn CRM — and manage your network directly from Cursor, Claude, or any MCP-compatible client.

## Available Tools

| Tool | Description |
|------|-------------|
| `get_connections_mcp` | Search and filter your LinkedIn connections by name, company, job title, location, or headline |
| `get_connections_list` | Retrieve your full list of LeadDelta connections |

## Setup in Cursor

### Option A — Remote (recommended, no installation required)

Open **Cursor Settings → MCP** and add a new server, or edit `~/.cursor/mcp.json` directly:

```json
{
  "mcpServers": {
    "leaddelta": {
      "url": "https://mcp.leaddelta.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_LEADDELTA_API_KEY"
      }
    }
  }
}
```

> **Where to find your API key:** Log in to [app.leaddelta.com](https://app.leaddelta.com) → Integrations → API Key.

## Example Usage

Once connected, you can ask your AI assistant:

- *"Show me all my connections working at OpenAI"*
- *"Find connections with 'Head of Growth' in their title"*
- *"List my connections based in London"*
- *"Who do I know at Series B startups?"*

---

## Transport Support

The server supports two transport protocols:

| Transport | Endpoint |
|-----------|----------|
| Streamable HTTP | `/mcp` |

Authentication is accepted via:
- `Authorization: Bearer YOUR_LEADDELTA_API_KEY` header


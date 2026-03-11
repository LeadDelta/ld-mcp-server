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

> **Where to find your API key:** Log in to [app.leaddelta.com](https://app.leaddelta.com) → Settings → API Keys.

### Option B — Local (self-hosted)

**Prerequisites:** Node.js v18+

```bash
git clone https://github.com/LeadDelta/mcp-server.git
cd mcp-server
npm install
```

Add to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "leaddelta": {
      "command": "node",
      "args": [
        "/absolute/path/to/mcp-server/mcpServer.js",
        "--leaddelta-api-key",
        "YOUR_LEADDELTA_API_KEY"
      ]
    }
  }
}
```

Restart Cursor after saving. The LeadDelta tools will appear in the MCP tools panel.

---

## Setup in Claude Desktop

Edit `~/Library/Application Support/Claude/claude_desktop_config.json` (macOS) or `%APPDATA%\Claude\claude_desktop_config.json` (Windows):

```json
{
  "mcpServers": {
    "leaddelta": {
      "command": "node",
      "args": [
        "/absolute/path/to/mcp-server/mcpServer.js",
        "--leaddelta-api-key",
        "YOUR_LEADDELTA_API_KEY"
      ]
    }
  }
}
```

---

## Example Usage

Once connected, you can ask your AI assistant:

- *"Show me all my connections working at OpenAI"*
- *"Find connections with 'Head of Growth' in their title"*
- *"List my connections based in London"*
- *"Who do I know at Series B startups?"*

---

## Transport Support

The server supports two transport protocols:

| Transport | Endpoint | Protocol Version |
|-----------|----------|-----------------|
| Streamable HTTP | `/mcp` | 2025-03-26 (recommended) |
| SSE | `/sse` | 2024-11-05 (legacy) |

Authentication is accepted via:
- `Authorization: Bearer YOUR_API_KEY` header
- `x-api-key` header
- `key` query parameter

---

## Self-Hosting

Run the server with HTTP transport:

```bash
PORT=3002 LEADDELTA_API_KEY=your_key node mcpServer.js --sse
```

Or with Docker:

```bash
docker build -t leaddelta-mcp .
docker run -p 3002:3002 --env-file .env leaddelta-mcp --sse
```

---

## License

MIT — [LeadDelta](https://leaddelta.com)

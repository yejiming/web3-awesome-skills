---
name: kraken-cli-mcp
description: "Official Kraken AI-native CLI with built-in MCP server. 134 commands for spot, futures, forex, derivatives trading. 50 agent skills included."
version: 1.0.0
metadata:
  openclaw:
    tags: [kraken, mcp, trading, spot, futures, forex, derivatives]
    official: true
    source: "https://github.com/krakenfx/kraken-cli"
---

# Kraken CLI MCP Server

Official Kraken AI-native CLI with built-in MCP server. Provides 134 commands for spot, futures, forex, and derivatives trading. Includes 50 agent skills for autonomous and semi-autonomous trading workflows.

## Installation

```bash
# Install kraken-cli
curl -fsSL https://raw.githubusercontent.com/krakenfx/kraken-cli/main/install.sh | bash
```

## MCP Configuration

Add to your MCP client configuration (Claude Desktop, Cursor, VS Code, Gemini CLI, etc.):

```json
{
  "mcpServers": {
    "kraken": {
      "command": "kraken",
      "args": ["mcp", "-s", "market,trade,paper"]
    }
  }
}
```

## Service Filtering

Control which command groups the MCP server exposes:

| Service | Auth | Tools | Risk |
|---------|------|-------|------|
| market | No | ~10 | None |
| account | Yes | ~18 | Read-only |
| trade | Yes | ~9 | Orders (dangerous) |
| funding | Yes | ~10 | Withdrawals (dangerous) |
| earn | Yes | ~6 | Staking (dangerous) |
| subaccount | Yes | ~2 | Transfers (dangerous) |
| futures | Mixed | ~39 | Orders (dangerous) |
| paper | No | ~10 | None (simulation) |
| auth | No | ~3 | Read-only |

## Authentication

```bash
export KRAKEN_API_KEY="your-key"
export KRAKEN_API_SECRET="your-secret"
```

Public market data and paper trading require no credentials.

## Supported Clients

Claude Desktop, ChatGPT, Codex, Gemini CLI, Cursor, VS Code, Windsurf, and any client that supports the MCP `mcpServers` configuration block.

## Links

- **GitHub**: https://github.com/krakenfx/kraken-cli
- **Documentation**: https://github.com/krakenfx/kraken-cli#readme

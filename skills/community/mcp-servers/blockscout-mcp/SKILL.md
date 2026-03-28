---
name: blockscout-mcp
description: "Official Blockscout MCP server wrapping Blockscout APIs for multi-chain blockchain data access. Provides balances, tokens, NFTs, contract metadata, transaction analysis, and smart contract inspection for AI agents."
version: 1.0.0
metadata:
  openclaw:
    tags: [blockscout, explorer, multi-chain, mcp, blockchain-data, analytics]
    official: true
    source: "https://github.com/blockscout/mcp-server"
---

# Blockscout MCP Server

Official MCP server from Blockscout.

Wraps Blockscout APIs and exposes blockchain data -- balances, tokens, NFTs, contract metadata -- via MCP so that AI agents and tools can access and analyze it contextually. Features multi-chain support via Chainscout, intelligent context optimization, smart response slicing, opaque cursor pagination, and a versioned REST API.

## Installation

```bash
# Claude Code
claude mcp add --transport http blockscout https://mcp.blockscout.com/mcp
```

Or via Docker:

```json
{
  "mcpServers": {
    "blockscout": {
      "command": "docker",
      "args": ["run", "--rm", "-i", "ghcr.io/blockscout/mcp-server:latest"]
    }
  }
}
```

## Links

- **GitHub**: https://github.com/blockscout/mcp-server
- **Live Server**: https://mcp.blockscout.com/mcp
- **Docker**: `ghcr.io/blockscout/mcp-server:latest`

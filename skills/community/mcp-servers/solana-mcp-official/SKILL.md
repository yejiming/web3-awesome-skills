---
name: solana-mcp-official
description: "Official Solana Developer MCP server. Serves up-to-date documentation across the Solana ecosystem to vibe coders and AI agents via mcp.solana.com."
version: 1.0.0
metadata:
  openclaw:
    tags: [solana, mcp, blockchain, l1, documentation, developer-tools]
    official: true
    source: "https://github.com/solana-foundation/solana-mcp-official"
---

# Solana MCP Official

Official MCP server from the Solana Foundation.

The official Solana Developer MCP serves up-to-date documentation across the Solana ecosystem to vibe coders and AI agents. Available at mcp.solana.com, it provides both MCP and SSE endpoints powered by Vercel's `@vercel/mcp-adapter`.

## Installation

Connect to the hosted server:

```json
{
  "mcpServers": {
    "solana-mcp": {
      "url": "https://mcp.solana.com/mcp"
    }
  }
}
```

Or for SSE: `https://mcp.solana.com/sse`

## Links

- **GitHub**: https://github.com/solana-foundation/solana-mcp-official
- **Live Server**: https://mcp.solana.com

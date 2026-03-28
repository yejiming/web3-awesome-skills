---
name: wormhole-mcp
description: "Cross-chain token transfers via Wormhole SDK. Enables bridging assets between blockchains using the Wormhole interoperability protocol."
version: 1.0.0
metadata:
  openclaw:
    tags: [mcp, wormhole, cross-chain, bridge, token-transfers, interoperability]
    official: true
    source: "https://wormhole.com"
---

# Wormhole MCP

MCP server for cross-chain token transfers via Wormhole.

Enables AI agents to perform cross-chain token transfers using the Wormhole SDK. Supports bridging assets between multiple blockchain networks including Ethereum, Solana, BSC, Polygon, Avalanche, and more through the Wormhole interoperability protocol.

## Installation

```json
{
  "mcpServers": {
    "wormhole": {
      "command": "npx",
      "args": ["-y", "@wormhole-foundation/mcp-server"]
    }
  }
}
```

## Links

- **Website**: https://wormhole.com
- **Documentation**: https://docs.wormhole.com
- **GitHub**: https://github.com/wormhole-foundation

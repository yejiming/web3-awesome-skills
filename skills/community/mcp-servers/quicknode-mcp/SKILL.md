---
name: quicknode-mcp
description: "Multi-chain EVM RPC for Ethereum, Arbitrum, Base, BSC via QuickNode API. Provides fast blockchain node access and data queries across multiple networks."
version: 1.0.0
metadata:
  openclaw:
    tags: [mcp, quicknode, rpc, ethereum, arbitrum, base, bsc, evm, multi-chain]
    official: true
    source: "https://www.quicknode.com"
---

# QuickNode MCP

MCP server for QuickNode multi-chain RPC access.

Provides multi-chain EVM RPC access for Ethereum, Arbitrum, Base, BSC, and other networks through the QuickNode API. Enables AI agents to query blockchain data, send transactions, and interact with smart contracts across supported chains.

## Installation

```json
{
  "mcpServers": {
    "quicknode": {
      "command": "npx",
      "args": ["-y", "@quicknode/mcp-server"],
      "env": {
        "QUICKNODE_API_KEY": "YOUR_API_KEY"
      }
    }
  }
}
```

## Links

- **Website**: https://www.quicknode.com
- **Documentation**: https://www.quicknode.com/docs

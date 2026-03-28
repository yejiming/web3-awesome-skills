---
name: thirdweb-mcp
description: "Query blockchain data, access contract ABIs, execute transactions via Thirdweb SDK. Full-stack Web3 development toolkit with MCP integration."
version: 1.0.0
metadata:
  openclaw:
    tags: [mcp, thirdweb, blockchain, contracts, abi, transactions, web3, sdk]
    official: true
    source: "https://blog.thirdweb.com"
---

# Thirdweb MCP

MCP server for Thirdweb SDK integration.

Enables AI agents to query blockchain data, access contract ABIs, and execute transactions through the Thirdweb SDK. Provides a comprehensive Web3 development interface including contract deployment, interaction, and blockchain data retrieval across multiple chains.

## Installation

```json
{
  "mcpServers": {
    "thirdweb": {
      "command": "npx",
      "args": ["-y", "thirdweb-mcp"],
      "env": {
        "THIRDWEB_SECRET_KEY": "YOUR_SECRET_KEY"
      }
    }
  }
}
```

## Links

- **Blog**: https://blog.thirdweb.com
- **Documentation**: https://portal.thirdweb.com
- **GitHub**: https://github.com/thirdweb-dev

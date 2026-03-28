---
name: bridge-rates-mcp
description: "Real-time cross-chain bridge rate comparison across major bridges. Find the cheapest and fastest route to move assets between chains."
version: 1.0.0
metadata:
  openclaw:
    tags: [defi, bridge, cross-chain, rates, comparison, transfers]
    official: false
---

# Bridge Rates MCP

MCP server for real-time cross-chain bridge rate comparison.

Compares bridge rates across major cross-chain bridges in real-time to help users find the cheapest and fastest route for moving assets between blockchain networks. Aggregates quotes from bridges like Stargate, Across, Hop, Synapse, and more.

## Installation

```json
{
  "mcpServers": {
    "bridge-rates": {
      "command": "npx",
      "args": ["-y", "bridge-rates-mcp"]
    }
  }
}
```

## Features

- Compare fees and speed across major bridges
- Support for all major EVM chains and L2s
- Real-time quote aggregation
- Gas cost estimation included in comparisons

## Links

- **LI.FI**: https://li.fi
- **Socket**: https://socket.tech

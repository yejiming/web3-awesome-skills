---
name: defi-yields-mcp
description: "Explore DeFi yield opportunities across lending, staking, and LP protocols. Compare APYs and find optimal yield strategies across chains."
version: 1.0.0
metadata:
  openclaw:
    tags: [defi, yields, lending, staking, liquidity, apy, farming]
    official: false
---

# DeFi Yields MCP

MCP server for exploring DeFi yield opportunities.

Enables AI agents to discover and compare DeFi yield opportunities across lending protocols, staking services, and liquidity pool providers. Aggregates APY data from multiple chains and protocols to help users find optimal yield strategies.

## Installation

```json
{
  "mcpServers": {
    "defi-yields": {
      "command": "npx",
      "args": ["-y", "defi-yields-mcp"]
    }
  }
}
```

## Features

- Compare lending rates across Aave, Compound, and other protocols
- Track staking APYs for ETH, SOL, and other PoS assets
- Monitor LP yields across DEXes
- Filter by chain, risk level, and minimum TVL

## Links

- **DefiLlama Yields API**: https://yields.llama.fi

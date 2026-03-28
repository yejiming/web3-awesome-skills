---
name: uniswap-poolspy
description: "Track newly created Uniswap liquidity pools across 9 networks. Monitor new token listings and early liquidity events in real-time."
version: 1.0.0
metadata:
  openclaw:
    tags: [defi, uniswap, pools, liquidity, monitoring, new-tokens, dex]
    official: false
---

# Uniswap PoolSpy

MCP server for tracking newly created Uniswap liquidity pools.

Monitors and reports on newly created Uniswap liquidity pools across 9 blockchain networks in real-time. Helps users discover new token listings, track early liquidity events, and analyze pool creation patterns for research and trading purposes.

## Installation

```json
{
  "mcpServers": {
    "uniswap-poolspy": {
      "command": "npx",
      "args": ["-y", "uniswap-poolspy-mcp"]
    }
  }
}
```

## Features

- Real-time monitoring of new Uniswap pool creation events
- Coverage across Ethereum, Arbitrum, Optimism, Base, Polygon, BSC, Avalanche, Celo, and Blast
- Pool metadata including token pairs, initial liquidity, and fee tiers
- Filtering by chain, minimum liquidity, and token criteria

## Links

- **Uniswap**: https://uniswap.org
- **Uniswap Info**: https://info.uniswap.org

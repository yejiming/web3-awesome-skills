---
name: crypto-liquidations-mcp
description: "Real-time crypto liquidation events monitoring. Track leveraged position liquidations across major exchanges and DeFi protocols."
version: 1.0.0
metadata:
  openclaw:
    tags: [analytics, liquidations, futures, leverage, risk, monitoring]
    official: false
---

# Crypto Liquidations MCP

MCP server for real-time cryptocurrency liquidation monitoring.

Monitors and reports on real-time crypto liquidation events across major centralized exchanges and DeFi protocols. Tracks leveraged position liquidations, providing data on liquidation volume, affected assets, and market impact for risk analysis and trading signals.

## Installation

```json
{
  "mcpServers": {
    "crypto-liquidations": {
      "command": "npx",
      "args": ["-y", "crypto-liquidations-mcp"]
    }
  }
}
```

## Features

- Real-time liquidation event streaming
- Aggregated liquidation volumes by asset and exchange
- Historical liquidation data and trends
- Long/short liquidation ratio tracking
- Large liquidation alerts

## Links

- **Coinglass**: https://www.coinglass.com/LiquidationData

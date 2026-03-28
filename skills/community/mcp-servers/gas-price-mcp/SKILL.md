---
name: gas-price-mcp
description: "Real-time Ethereum gas price predictions and fee estimates. Provides accurate gas pricing from Blocknative for optimal transaction timing."
version: 1.0.0
metadata:
  openclaw:
    tags: [mcp, gas, ethereum, blocknative, fee-estimation, transactions]
    official: false
    source: "https://www.blocknative.com"
---

# Gas Price MCP

MCP server for real-time Ethereum gas price predictions.

Provides real-time Ethereum gas price predictions and fee estimates using Blocknative's gas estimation API. Enables AI agents to recommend optimal gas prices for transactions, predict confirmation times, and help users time their transactions for lower fees.

## Installation

```json
{
  "mcpServers": {
    "gas-price": {
      "command": "npx",
      "args": ["-y", "gas-price-mcp-server"],
      "env": {
        "BLOCKNATIVE_API_KEY": "YOUR_API_KEY"
      }
    }
  }
}
```

## Links

- **Blocknative**: https://www.blocknative.com
- **Gas Estimator**: https://www.blocknative.com/gas-estimator
- **Documentation**: https://docs.blocknative.com

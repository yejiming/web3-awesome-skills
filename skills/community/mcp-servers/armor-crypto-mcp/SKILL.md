---
name: armor-crypto-mcp
description: "Multi-chain wallet, swaps, DCA, staking, bridging, limit orders. Full-featured crypto operations via Armor Wallet MCP server."
version: 1.0.0
metadata:
  openclaw:
    tags: [mcp, armor, wallet, swaps, dca, staking, bridging, limit-orders, multi-chain]
    official: true
    source: "https://github.com/armorwallet/armor-crypto-mcp"
---

# Armor Crypto MCP

MCP server for Armor Wallet multi-chain crypto operations.

Provides a comprehensive MCP server for multi-chain wallet operations including token swaps, dollar-cost averaging (DCA), staking, cross-chain bridging, and limit orders. Supports multiple blockchain networks through the Armor Wallet infrastructure.

## Installation

```json
{
  "mcpServers": {
    "armor-crypto": {
      "command": "npx",
      "args": ["-y", "armor-crypto-mcp"],
      "env": {
        "ARMOR_API_KEY": "YOUR_API_KEY"
      }
    }
  }
}
```

## Links

- **GitHub**: https://github.com/armorwallet/armor-crypto-mcp
- **Website**: https://armorwallet.com

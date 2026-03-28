---
name: coingecko-mcp-official
description: "Official CoinGecko MCP server for AI assistants to interact with the CoinGecko API. Provides cryptocurrency market data including prices, token info, and market analytics."
version: 1.0.0
metadata:
  openclaw:
    tags: [coingecko, market-data, prices, mcp, analytics, crypto-data]
    official: true
    source: "https://github.com/coingecko/coingecko-typescript"
---

# CoinGecko MCP Server

Official MCP server from CoinGecko.

The CoinGecko MCP server enables AI assistants to interact with the CoinGecko REST API, allowing them to explore endpoints, make test requests, and access cryptocurrency market data. Built on the CoinGecko TypeScript API library, it provides comprehensive access to price data, token information, and market analytics.

## Installation

```json
{
  "mcpServers": {
    "coingecko-mcp": {
      "command": "npx",
      "args": ["-y", "@coingecko/coingecko-mcp"],
      "env": {
        "COINGECKO_PRO_API_KEY": "your_pro_api_key",
        "COINGECKO_DEMO_API_KEY": "your_demo_api_key"
      }
    }
  }
}
```

## Links

- **GitHub**: https://github.com/coingecko/coingecko-typescript
- **npm**: `@coingecko/coingecko-mcp`
- **API Docs**: https://docs.coingecko.com

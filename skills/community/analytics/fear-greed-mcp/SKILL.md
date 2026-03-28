---
name: fear-greed-mcp
description: "Crypto Fear & Greed Index data for market sentiment tracking. Access current and historical index values to gauge overall market emotion."
version: 1.0.0
metadata:
  openclaw:
    tags: [analytics, fear-greed, sentiment, market, index, bitcoin]
    official: false
---

# Fear & Greed MCP

MCP server for Crypto Fear & Greed Index data.

Provides access to the Crypto Fear & Greed Index for market sentiment tracking. Returns current and historical index values (0-100 scale from Extreme Fear to Extreme Greed) to help gauge overall crypto market emotion and identify potential buying or selling opportunities.

## Installation

```json
{
  "mcpServers": {
    "fear-greed": {
      "command": "npx",
      "args": ["-y", "fear-greed-mcp"]
    }
  }
}
```

## API

The Fear & Greed Index is available via a free public API:

```
web_fetch url="https://api.alternative.me/fng/?limit=1"
```

Historical data (last 30 days):
```
web_fetch url="https://api.alternative.me/fng/?limit=30"
```

## Features

- Current Fear & Greed Index value and classification
- Historical index data (daily granularity)
- Value classifications: Extreme Fear, Fear, Neutral, Greed, Extreme Greed
- BTC-weighted sentiment indicator

## Links

- **Alternative.me**: https://alternative.me/crypto/fear-and-greed-index/

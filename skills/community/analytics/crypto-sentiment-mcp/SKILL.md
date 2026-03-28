---
name: crypto-sentiment-mcp
description: "Cryptocurrency sentiment analysis from social media and news. Aggregate and analyze market sentiment from Twitter, Reddit, and crypto news sources."
version: 1.0.0
metadata:
  openclaw:
    tags: [analytics, sentiment, social-media, news, market-analysis, nlp]
    official: false
---

# Crypto Sentiment MCP

MCP server for cryptocurrency sentiment analysis.

Aggregates and analyzes cryptocurrency market sentiment from social media platforms and news sources. Monitors Twitter/X, Reddit, Telegram, and crypto news outlets to provide sentiment scores, trending topics, and social volume metrics for individual tokens and the broader market.

## Installation

```json
{
  "mcpServers": {
    "crypto-sentiment": {
      "command": "npx",
      "args": ["-y", "crypto-sentiment-mcp"]
    }
  }
}
```

## Features

- Social media sentiment aggregation (Twitter/X, Reddit, Telegram)
- News sentiment analysis from crypto media outlets
- Per-token and market-wide sentiment scores
- Social volume and mention tracking
- Trending topic detection

## Links

- **LunarCrush**: https://lunarcrush.com
- **Santiment**: https://santiment.net

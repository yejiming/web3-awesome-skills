---
name: freqtrade-mcp
description: "Integration with Freqtrade open-source trading bot framework. Manage strategies, backtesting, and live trading operations via MCP."
version: 1.0.0
metadata:
  openclaw:
    tags: [mcp, freqtrade, trading-bot, backtesting, strategy, algorithmic-trading]
    official: false
    source: "https://www.freqtrade.io"
---

# Freqtrade MCP

MCP server for Freqtrade trading bot integration.

Provides MCP integration with the Freqtrade open-source crypto trading bot framework. Enables AI agents to manage trading strategies, run backtests, monitor live trading operations, and analyze trading performance through the Model Context Protocol.

## Installation

```json
{
  "mcpServers": {
    "freqtrade": {
      "command": "npx",
      "args": ["-y", "freqtrade-mcp-server"],
      "env": {
        "FREQTRADE_API_URL": "http://localhost:8080",
        "FREQTRADE_API_KEY": "YOUR_API_KEY"
      }
    }
  }
}
```

## Prerequisites

- Freqtrade instance running with API enabled

## Links

- **Website**: https://www.freqtrade.io
- **Documentation**: https://www.freqtrade.io/en/stable/
- **GitHub**: https://github.com/freqtrade/freqtrade

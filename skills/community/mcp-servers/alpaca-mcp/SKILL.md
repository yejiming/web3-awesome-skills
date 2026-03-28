---
name: alpaca-mcp
description: "Official Alpaca MCP server for trading stocks, ETFs, crypto, and options via natural language. Supports real-time market data, portfolio management, order execution, options Greeks, watchlists, and corporate actions through AI assistants like Claude, Cursor, and VS Code."
version: 1.0.0
metadata:
  openclaw:
    tags: [alpaca, trading, stocks, etf, crypto, options, mcp, market-data, portfolio]
    official: true
    source: "https://github.com/alpacahq/alpaca-mcp-server"
---

# Alpaca MCP Server

Official MCP server from Alpaca.

A comprehensive Model Context Protocol (MCP) server for Alpaca's Trading API. Enable natural language trading operations through AI assistants like Claude, Cursor, and VS Code. Supports stocks, options, crypto, portfolio management, and real-time market data.

## Features

- **Market Data** - Real-time quotes, trades, and price bars for stocks, crypto, and options with flexible historical timeframes
- **Account & Position Management** - View balances, buying power, open/closed positions, and liquidate holdings
- **Order Management** - Place stocks, ETFs, crypto, and options orders with support for market, limit, stop, stop-limit, and trailing-stop orders
- **Options Trading** - Search option contracts, place single-leg or multi-leg strategies (spreads, straddles), get Greeks and implied volatility
- **Crypto Trading** - Market, limit, and stop-limit crypto orders with GTC/IOC support
- **Market Status & Corporate Actions** - Market calendar, trading sessions, earnings, splits, dividends
- **Watchlist & Asset Search** - Create and manage watchlists, query details for stocks, ETFs, crypto, and options

## Installation

```bash
# Quick install via uvx
uvx alpaca-mcp-server init
```

Then add to your MCP client config:

```json
{
  "mcpServers": {
    "alpaca": {
      "command": "uvx",
      "args": ["alpaca-mcp-server", "serve"],
      "env": {
        "ALPACA_API_KEY": "your_alpaca_api_key",
        "ALPACA_SECRET_KEY": "your_alpaca_secret_key"
      }
    }
  }
}
```

## Prerequisites

- Python 3.10+
- uv package manager
- Alpaca Trading API keys (free paper trading account available)
- MCP client (Claude Desktop, Cursor, VS Code, etc.)

## Links

- **GitHub**: https://github.com/alpacahq/alpaca-mcp-server
- **Documentation**: https://docs.alpaca.markets/docs/getting-started
- **API Keys**: https://app.alpaca.markets/paper/dashboard/overview

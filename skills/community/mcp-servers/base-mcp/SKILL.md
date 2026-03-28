---
name: base-mcp
description: "Base Network MCP server providing onchain tools for AI applications. Supports wallet management, fund transfers, smart contract deployment, Morpho vaults, ERC20/NFT operations, Coinbase onramp, and OpenRouter credits."
version: 1.0.0
metadata:
  openclaw:
    tags: [base, ethereum, l2, mcp, coinbase, defi, nft, agentkit]
    official: true
    source: "https://github.com/base/base-mcp"
---

# Base MCP Server

Official MCP server from Base (Coinbase).

A Model Context Protocol server that provides onchain tools for AI applications like Claude Desktop and Cursor, allowing them to interact with the Base Network and Coinbase API. Supports wallet management, fund transfers, smart contract deployment, Morpho vault interactions, ERC20/NFT operations, Coinbase onramp, and OpenRouter credit purchases.

## Installation

```bash
npm install -g base-mcp
```

Or configure in Claude Desktop:

```json
{
  "mcpServers": {
    "base-mcp": {
      "command": "npx",
      "args": ["-y", "base-mcp@latest"],
      "env": {
        "COINBASE_API_KEY_NAME": "your_api_key_name",
        "COINBASE_API_PRIVATE_KEY": "your_private_key",
        "SEED_PHRASE": "your seed phrase here",
        "COINBASE_PROJECT_ID": "your_project_id",
        "ALCHEMY_API_KEY": "your_alchemy_api_key"
      }
    }
  }
}
```

## Links

- **GitHub**: https://github.com/base/base-mcp
- **npm**: `base-mcp`

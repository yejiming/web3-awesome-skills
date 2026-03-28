---
name: bnbchain-mcp
description: "BNB Chain MCP server for interacting with BNB Chain and EVM-compatible networks through AI. Provides tools for blocks, transactions, contracts, tokens, NFTs, wallet, ERC-8004 agents, and Greenfield."
version: 1.0.0
metadata:
  openclaw:
    tags: [bnb, bsc, evm, mcp, blockchain, nft, defi, greenfield]
    official: true
    source: "https://github.com/bnb-chain/bnbchain-mcp"
---

# BNB Chain MCP Server

Official MCP server from BNB Chain.

A Model Context Protocol implementation that enables seamless interaction with BNB Chain and other EVM-compatible networks through AI-powered interfaces. It provides comprehensive tools for blockchain development, smart contract interaction, network management, ERC-8004 agent registration, and Greenfield decentralized storage.

## Installation

```json
{
  "mcpServers": {
    "bnbchain-mcp": {
      "command": "npx",
      "args": ["-y", "@bnb-chain/mcp@latest"],
      "env": {
        "PRIVATE_KEY": ""
      }
    }
  }
}
```

## Links

- **GitHub**: https://github.com/bnb-chain/bnbchain-mcp
- **npm**: `@bnb-chain/mcp`

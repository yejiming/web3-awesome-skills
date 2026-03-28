---
name: monad-mcp
description: "Monad MCP server built on Next.js. Provides blockchain tools for interacting with the Monad network, including ABI guessing, contract analysis, and EVM interactions."
version: 1.0.0
metadata:
  openclaw:
    tags: [monad, evm, mcp, blockchain, smart-contracts]
    official: true
    source: "https://github.com/monad-developers/monad-mcp"
---

# Monad MCP Server

Official MCP server from Monad.

An example MCP server built on Next.js for interacting with the Monad blockchain. Provides tools, prompts, and resources for blockchain exploration and smart contract interaction using the MCP TypeScript SDK.

## Installation

Update `app/mcp.ts` with your tools following the [MCP TypeScript SDK documentation](https://github.com/modelcontextprotocol/typescript-sdk).

For running on Vercel, requires a Redis instance under `process.env.REDIS_URL` and [Fluid compute](https://vercel.com/docs/functions/fluid-compute) enabled.

## Links

- **GitHub**: https://github.com/monad-developers/monad-mcp

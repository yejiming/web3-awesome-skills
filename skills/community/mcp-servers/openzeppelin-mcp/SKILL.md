---
name: openzeppelin-mcp
description: "Security rules and best practices for Solidity development. Provides MCP servers for Solidity, Cairo, Confidential, Stellar, and Stylus contract generation using OpenZeppelin's audited libraries."
version: 1.0.0
metadata:
  openclaw:
    tags: [mcp, openzeppelin, solidity, security, smart-contracts, cairo, stylus]
    official: true
    source: "https://github.com/OpenZeppelin/openzeppelin-mcp"
---

# OpenZeppelin MCP

Official MCP servers from OpenZeppelin.

A Model Context Protocol (MCP) server repository providing security rules and best practices for Solidity development. Includes hosted MCP servers for Solidity Contracts, Cairo Contracts, Confidential Contracts, Stellar Contracts, Stylus Contracts, and OpenZeppelin Uniswap Hooks. Built on the audited OpenZeppelin Contracts library.

## Installation

Configure via MCP settings:

```json
{
  "mcpServers": {
    "openzeppelin": {
      "url": "https://mcp.openzeppelin.com/solidity/sse"
    }
  }
}
```

Available server endpoints:
- `https://mcp.openzeppelin.com/solidity/sse` - Solidity Contracts
- `https://mcp.openzeppelin.com/cairo/sse` - Cairo Contracts
- `https://mcp.openzeppelin.com/confidential/sse` - Confidential Contracts
- `https://mcp.openzeppelin.com/stellar/sse` - Stellar Contracts
- `https://mcp.openzeppelin.com/stylus/sse` - Stylus Contracts
- `https://mcp.openzeppelin.com/uniswap-hooks/sse` - Uniswap Hooks

Or run locally:

```bash
git clone https://github.com/OpenZeppelin/openzeppelin-mcp.git
cd openzeppelin-mcp
bun install
bun run dev
```

## Links

- **GitHub**: https://github.com/OpenZeppelin/openzeppelin-mcp
- **Configuration**: https://mcp.openzeppelin.com
- **Documentation**: https://docs.openzeppelin.com

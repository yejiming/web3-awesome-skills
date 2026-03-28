---
name: foundry-mcp
description: "MCP server for Foundry/Forge smart contract development and testing. Compile, test, deploy, and debug Solidity contracts via MCP."
version: 1.0.0
metadata:
  openclaw:
    tags: [mcp, foundry, forge, solidity, smart-contracts, testing, development]
    official: false
    source: "https://github.com/foundry-rs/foundry"
---

# Foundry MCP

MCP server for Foundry/Forge smart contract development and testing.

Provides MCP integration for the Foundry toolkit, enabling AI agents to compile, test, deploy, and debug Solidity smart contracts using Forge, Cast, Anvil, and Chisel. Supports the full smart contract development lifecycle through the Model Context Protocol.

## Installation

```json
{
  "mcpServers": {
    "foundry": {
      "command": "npx",
      "args": ["-y", "foundry-mcp-server"]
    }
  }
}
```

## Prerequisites

- Foundry toolchain installed (`curl -L https://foundry.paradigm.xyz | bash && foundryup`)

## Links

- **Foundry**: https://getfoundry.sh
- **Book**: https://book.getfoundry.sh
- **GitHub**: https://github.com/foundry-rs/foundry

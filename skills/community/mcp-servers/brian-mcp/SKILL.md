---
name: brian-mcp
description: "Convert natural language to Web3 transactions. Translates human-readable intents into executable blockchain transactions using Brian API."
version: 1.0.0
metadata:
  openclaw:
    tags: [mcp, brian, natural-language, transactions, web3, intent]
    official: true
    source: "https://brian.so"
---

# Brian MCP

MCP server for Brian API natural language to Web3 transactions.

Converts natural language prompts into executable Web3 transactions using the Brian API. Enables AI agents to interpret user intent and generate the appropriate blockchain transactions for swaps, transfers, contract interactions, and more.

## Installation

```json
{
  "mcpServers": {
    "brian": {
      "command": "npx",
      "args": ["-y", "@brian-ai/mcp-server"],
      "env": {
        "BRIAN_API_KEY": "YOUR_API_KEY"
      }
    }
  }
}
```

## Links

- **Website**: https://brian.so
- **Documentation**: https://docs.brian.so

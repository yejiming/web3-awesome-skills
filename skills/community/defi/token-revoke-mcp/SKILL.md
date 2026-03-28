---
name: token-revoke-mcp
description: "Check and revoke ERC-20 token allowances to secure wallets. Scan for risky unlimited approvals and generate revocation transactions."
version: 1.0.0
metadata:
  openclaw:
    tags: [defi, security, approvals, revoke, erc20, allowances, wallet-security]
    official: false
---

# Token Revoke MCP

MCP server for checking and revoking ERC-20 token allowances.

Enables AI agents to scan wallet addresses for ERC-20 token allowances, identify risky unlimited approvals, and generate revocation transactions to secure user wallets. Helps protect against exploits targeting stale or excessive token approvals.

## Installation

```json
{
  "mcpServers": {
    "token-revoke": {
      "command": "npx",
      "args": ["-y", "token-revoke-mcp"]
    }
  }
}
```

## Features

- Scan all ERC-20 approvals for a wallet address
- Identify unlimited and risky allowances
- Generate revocation transactions
- Multi-chain support (Ethereum, Polygon, Arbitrum, etc.)

## Links

- **Revoke.cash**: https://revoke.cash
- **Etherscan Token Approvals**: https://etherscan.io/tokenapprovalchecker

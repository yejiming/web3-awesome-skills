---
name: bicscan-mcp
description: "Blockchain address risk scoring and AML analysis. Evaluate wallet addresses for suspicious activity, sanctions exposure, and compliance risk."
version: 1.0.0
metadata:
  openclaw:
    tags: [analytics, aml, risk-scoring, compliance, blockchain-analysis, security]
    official: false
---

# BICScan MCP

MCP server for blockchain address risk scoring and AML analysis.

Provides blockchain address risk scoring and anti-money laundering (AML) analysis. Evaluates wallet addresses for suspicious activity, sanctions exposure, interaction with known malicious addresses, and overall compliance risk to help users and businesses assess counterparty risk.

## Installation

```json
{
  "mcpServers": {
    "bicscan": {
      "command": "npx",
      "args": ["-y", "bicscan-mcp"],
      "env": {
        "BICSCAN_API_KEY": "YOUR_API_KEY"
      }
    }
  }
}
```

## Features

- Address risk scoring (0-100 scale)
- Sanctions list checking
- Interaction with known malicious addresses
- Transaction pattern analysis
- Multi-chain support
- Compliance reporting

## Links

- **BICScan**: https://bicscan.io

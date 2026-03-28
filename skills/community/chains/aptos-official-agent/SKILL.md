---
name: aptos-agent
description: "Python-based AI agent for interacting with the Aptos L1 blockchain. Supports wallet funding, balance checking, asset transfers, token creation, and social media posting."
version: 1.0.0
metadata:
  openclaw:
    tags: [aptos, agent, python, blockchain, l1, move, ai-agent]
    official: true
    source: "https://github.com/aptos-labs/aptos-agent"
---

# Aptos Agent

Official AI agent from Aptos Labs.

A Python-based application designed to interact with the Aptos Layer 1 blockchain. It utilizes the Aptos SDK to perform various blockchain operations such as funding wallets, checking balances, transferring assets, and creating tokens. Currently operates on the Aptos Devnet.

## Installation

```bash
pip install -r requirements.txt
python main.py
```

Requires environment variables:
- `OPENAI_API_KEY` (required)
- `TWITTER_API_KEY`, `TWITTER_API_SECRET`, `TWITTER_ACCESS_TOKEN`, `TWITTER_ACCESS_TOKEN_SECRET` (optional, for tweet posting)

## Links

- **GitHub**: https://github.com/aptos-labs/aptos-agent

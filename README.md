<p align="center">
  <img src="./assets/readme-banner.svg" alt="Awesome Web3 Skills banner" width="100%" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Registry-855%20Skills-14f1b8?style=for-the-badge&labelColor=08120f&color=14f1b8" alt="855 skills" />
  <img src="https://img.shields.io/badge/Sources-11-26b9ff?style=for-the-badge&labelColor=08120f&color=26b9ff" alt="11 sources" />
  <img src="https://img.shields.io/badge/Risk%20Review-skill__risk__table-ffb84d?style=for-the-badge&labelColor=08120f&color=ffb84d" alt="risk review" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Exchanges-115-F3BA2F?style=for-the-badge&logo=binance&logoColor=F3BA2F&labelColor=0b0f14&color=1a1f2b" alt="Exchange skills 115" />
  <img src="https://img.shields.io/badge/DeFi-145-FF4D8D?style=for-the-badge&logo=uniswap&logoColor=FF4D8D&labelColor=0b0f14&color=1a1f2b" alt="DeFi skills 145" />
  <img src="https://img.shields.io/badge/Analytics-71-7C5CFF?style=for-the-badge&logo=dune&logoColor=FF6B3D&labelColor=0b0f14&color=1a1f2b" alt="Analytics skills 71" />
  <img src="https://img.shields.io/badge/Agents%20%26%20MCP-108-00C7B7?style=for-the-badge&logo=modelcontextprotocol&logoColor=00C7B7&labelColor=0b0f14&color=1a1f2b" alt="Agents and MCP skills 108" />
  <img src="https://img.shields.io/badge/Wallets%20%26%20Payments-89-8B5CF6?style=for-the-badge&logo=walletconnect&logoColor=8B5CF6&labelColor=0b0f14&color=1a1f2b" alt="Wallet and payment skills 89" />
</p>

# Awesome Web3 Skills

An opinionated, cyber-terminal flavored index of Web3 and AI-native skills collected in one repository.

This project brings together exchange-native workflows, protocol integrations, DeFi research helpers, analytics tooling, wallet and payment flows, MCP servers, and agent-ready utilities. The goal is simple: make high-signal Web3 skills easier to discover, compare, and reuse.

## Why This Repository Exists

The Web3 skill landscape is fragmented. Useful skills are scattered across exchange repos, protocol examples, community registries, and one-off agent toolkits. This repository consolidates that surface area into a single navigable index with a lightweight risk review artifact.

It is designed for:

- AI agent builders who want ready-made Web3 capabilities
- Researchers who need analytics, onchain, and market tooling in one place
- Developers looking for protocol, exchange, and wallet integration patterns
- Operators who want faster discovery before installing or adapting a skill

## Signal Snapshot

| Layer | Count | What It Covers |
| --- | ---: | --- |
| Total skills | 855 | All indexed `SKILL.md` entries in this repository |
| Source groups | 11 | Exchange, protocol, and community skill families |
| Exchange skills | 115 | Binance, Binance Web3, BingX, Gate, OKX, BitMart, Bybit, Crypto.com, Biget |
| DeFi skills | 145 | Community DeFi skills plus Uniswap-native skills |
| Analytics skills | 71 | Market data, research, dashboards, and onchain intelligence |
| Agents & MCP | 108 | MCP servers, AI-crypto workflows, and developer tooling |
| Wallets & payments | 89 | Wallet operations, payment flows, and transfer tooling |

## Source Map

| Source | Skills |
| --- | ---: |
| Community | 732 |
| Gate | 44 |
| BingX | 22 |
| Binance | 18 |
| OKX | 13 |
| Uniswap | 8 |
| Binance Web3 | 7 |
| Biget | 5 |
| BitMart | 3 |
| Crypto.com | 2 |
| Bybit | 1 |

## Community Category Highlights

The community set is the largest part of the repository and covers the broadest operational surface:

- `community/exchanges` — 178 skills
- `community/defi` — 137 skills
- `community/analytics` — 71 skills
- `community/mcp-servers` — 67 skills
- `community/payments` — 66 skills
- `community/chains` — 46 skills
- `community/trading` — 42 skills
- `community/prediction-markets` — 26 skills
- `community/wallets` — 23 skills
- `community/ai-crypto` — 21 skills

## Repository Layout

```text
.
├── skills/
│   ├── binance/
│   ├── binance-web3/
│   ├── bingx/
│   ├── bybit/
│   ├── community/
│   ├── crypto-com/
│   ├── gate/
│   ├── okx/
│   └── uniswap/
├── skill_risk_table.md
└── README.md
```

## How To Navigate

1. Start with [`skills/`](./skills) and choose a source family or domain.
2. Open each skill folder and inspect its `SKILL.md`.
3. Review any bundled references, scripts, or API notes before reuse.
4. Check [`skill_risk_table.md`](./skill_risk_table.md) for the repository's current risk summary.

## Security Note

This repository is curated, not guaranteed safe by default. Skills may include prompts, scripts, API calls, signing flows, wallet operations, or automation logic that should be reviewed before installation or execution.

Treat every skill as executable capability, not just documentation. Read the source, validate permissions, and prefer least-privilege usage when adapting skills into agent workflows.

## Style Of This Index

This README intentionally frames the repository like a registry rather than a plain folder dump:

- Web3-first discovery
- AI-agent and MCP awareness
- Exchange plus protocol coverage in one place
- High-signal counts instead of exhaustive badge spam
- GitHub-friendly presentation with a custom local banner

## Disclaimer

Brand names, protocol names, and platform names in this repository belong to their respective owners. Inclusion here does not imply affiliation, endorsement, or audit status.

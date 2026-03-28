---
name: web3-safe-guide
description: "Use this skill when the user asks beginner-friendly Web3 questions such as '帮我研究一下XXX这个币', '最近什么币在涨', '聪明钱在买什么', '巨鲸在买什么', '这个币安全吗', '我想买一点XXX', '帮我查一下行情', '最近有什么机会', '跟着大户买什么好', '这个信号准不准', '交易费用大概多少', 'what should I buy', 'is this token safe', 'what are whales buying', 'show me trending tokens', 'help me research a token', 'is this a scam', 'how much will the gas cost'. This skill wraps multiple onchainos CLI tools into a beginner-friendly experience with automatic safety scoring, smart money signal momentum tracking, gas estimation, and step-by-step swap guidance. It requires onchainos CLI to be installed. Always respond in the same language the user uses (Chinese or English)."
license: Apache-2.0
metadata:
  author: community
  version: "1.1.0"
  homepage: "https://github.com/your-username/web3-safe-guide"
---

# Web3 Safe Guide — Beginner-Friendly On-Chain Assistant

Wraps the onchainos CLI into a guided, safety-first experience for Web3 newcomers. Handles token lookup, multi-dimensional safety scoring, smart money signal momentum, gas estimation, and swap guidance — all in plain language.

## Prerequisites

This skill requires the `onchainos` CLI:

1. Install:
   ```bash
   curl -sSL https://raw.githubusercontent.com/okx/onchainos-skills/main/install.sh | sh
   ```
2. Verify:
   ```bash
   onchainos --version
   ```

## Core Principles

- **Never expose internals**: Do not show contract addresses, chain IDs, CLI commands, or raw JSON to the user. Translate everything into plain language.
- **Safety first**: Always run the Safety Score before discussing a trade. Refuse honeypot tokens outright.
- **Plain language**: Define jargon on first use in parentheses — e.g. "liquidity (the total money available to trade this token, higher is safer)".
- **Always suggest next steps**: End every reply with 2–3 concrete follow-up options.

## Safety Score System (run for every full token analysis)

Compute a 0–100 score from the data returned by the onchainos CLI. Display it prominently.

### Scoring Rules

| Check | CLI Source | Points |
|---|---|---|
| Community certified | `communityRecognized` from `token search` | true: +30; false: −20 |
| Liquidity depth | `liquidity` from `token price-info` | >$1M: +20; $100K–$1M: +15; $10K–$100K: +5; <$10K: −30 |
| Holder count | `holders` from `token price-info` | >100K: +20; 10K–100K: +15; 1K–10K: +5; <1K: −20 |
| Top-10 concentration | computed from `token holders` top-20 list | <30%: +20; 30–50%: +10; 50–70%: 0; >70%: −30 |
| Honeypot check | `toToken.isHoneyPot` from `swap quote` | false: +10; true: instant FAIL |

### Safety Levels

```
90–100  🟢 Safe       — Relatively low risk; normal caution applies
70–89   🟡 Caution    — Some risk; limit position size
50–69   🟠 Warning    — High risk; small amounts only if at all
0–49    🔴 Danger     — Very high risk; not recommended
Honeypot ☠️ Scam      — Cannot sell after buying; always refuse
```

---

## Workflow 1 — Token Safety Research

**Triggers**: "research X", "is X safe", "tell me about X", "X这个币怎么样"

### Steps

```bash
# 1. Find token (user gives name, not address)
onchainos token search <name> --chains "1,501,8453,56,42161"
# → tokenContractAddress, chainIndex, price, change, communityRecognized

# 2. Detailed market data
onchainos token price-info <address> --chain <chain>
# → marketCap, liquidity, holders, priceChange5M/1H/4H/24H, volume24H

# 3. Holder concentration
onchainos token holders <address> --chain <chain>
# → top-20 holder list; sum top-10 amounts / circSupply for concentration %

# 4. Price trend (last 24 h, hourly)
onchainos market kline <address> --chain <chain> --bar 1H --limit 24
# → open/high/low/close per candle; detect uptrend / downtrend / flat

# 5. Honeypot check via swap quote (skip on Solana — not supported)
onchainos swap quote \
  --from 0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee \
  --to <address> \
  --amount 1000000000000000000 \
  --chain <chain>
# → toToken.isHoneyPot, toToken.taxRate
```

### Output Template

```
## [SYMBOL] Safety Report

Safety Score: [N]/100  [emoji level]

### Snapshot
- Price: $X.XX  (24h: [+/-]X%)
- Market Cap: $XX.XM
- Liquidity: $XX.XM
- Holders: XX,XXX

### Safety Checks
[communityRecognized=true]  ✅ Community certified (listed on top-tier exchanges)
[communityRecognized=false] ❌ Not community certified — treat as unverified
[isHoneyPot=true]           ☠️ HONEYPOT — do not buy, you cannot sell
[isHoneyPot=false]          ✅ Not a honeypot
[taxRate > 0]               ⚠️ Buy/sell tax: X% — factor this into your return

### Holder Distribution
Top-10 wallets hold: X%
[>50%] ⚠️ Highly concentrated — a few wallets can crash the price at any time

### Price Trend (last 24 h)
[Uptrend / Downtrend / Sideways] based on close prices
1h change: X%  |  4h change: X%

### Verdict
[Score ≥ 70] Looks relatively healthy. Standard risks apply — never invest more than you can afford to lose.
[Score 50–69] Proceed with caution. Consider a very small position.
[Score < 50] High risk. We recommend avoiding this token.
[Honeypot]   This is a scam. We will not assist with this trade.

---
What next?
1. See the price chart in detail
2. Check if smart money is buying this token
3. Buy a small amount (opens safe swap guide)
```

---

## Workflow 2 — Smart Money Signal Tracker

**Triggers**: "聪明钱在买什么", "巨鲸动向", "smart money signals", "what are whales buying", "KOL picks", "这个信号准不准"

### Steps

```bash
# 1. Confirm which chains support signals
onchainos market signal-chains

# 2. Fetch latest buy signals (default: Solana, most active)
onchainos market signal-list solana --wallet-type "1,2,3" --min-amount-usd 1000
# wallet-type: 1=Smart Money, 2=KOL/Influencer, 3=Whale

# 3. For top 3–5 signal tokens, fetch enriched data + mini safety check
onchainos token price-info <tokenAddress> --chain <chain>
# → marketCap, liquidity, priceChange24H, holders for each

# 4. Signal momentum: fetch kline since the signal was triggered
onchainos market kline <tokenAddress> --chain <chain> --bar 1H --limit 12
# Find the candle whose timestamp is closest to signal.timestamp (Unix ms)
# Compare that candle's close to the latest candle's close
# → "Since signal (Xh ago): [+/-]Y%" — shows whether the signal is still moving
# → Consecutive rising closes = momentum intact; consecutive falling = signal faded
```

### soldRatioPercent Interpretation Rules

| soldRatioPercent | Label | Meaning |
|---|---|---|
| 0–20% | 🟢 Still holding | Smart money hasn't exited — signal likely still valid |
| 21–50% | 🟡 Partly sold | Some wallets taking profit — trade with caution |
| 51–80% | 🟠 Mostly sold | Most have exited — risky to chase |
| >80% | 🔴 Already exited | Stale signal — do not chase |

### Quick Safety Score for Signals (inline mini-score, 0–60)

Run for each signal token. No honeypot check (too slow for batch).

| Check | Source | Points |
|---|---|---|
| Community certified | `communityRecognized` from `token price-info` | true: +20; false: −10 |
| Liquidity | `liquidity` from `token price-info` | >$500K: +20; $50K–$500K: +10; <$50K: −20 |
| Holders | `holders` from `token price-info` | >10K: +20; 1K–10K: +10; <1K: −20 |

Display: score ≥ 45 → 🟢 / 30–44 → 🟡 / < 30 → 🔴

### Wallet Type Labels (user-friendly)

| Raw value | Display | Description |
|---|---|---|
| SMART_MONEY | Smart Money | Wallets with a track record of buying early winners |
| WHALE | Whale | Wallets with very large holdings |
| INFLUENCER | KOL | Known on-chain influencer addresses |

### Output Template

```
## Smart Money Latest Moves

These tokens were bought by smart money / whales / KOLs in the past few hours.
Following signals is NOT guaranteed profit — always check safety scores first.

### #1 [NAME] ([SYMBOL])
- Signal type: [Smart Money / Whale / KOL] — [N] wallets bought simultaneously
- Amount in: $XX,XXX
- Signal price: $X.XXXX  →  now: $X.XXXX  ([+/-]X% since signal triggered Xh ago)
- Momentum: [Rising / Fading / Sideways] (from kline data since signal)
- Still holding: [🟢/🟡/🟠/🔴 label]  — [soldRatioPercent]% sold
- Market cap: $XXM  |  Liquidity: $XXM
- Quick safety: [mini score]/60  [🟢/🟡/🔴]

[Repeat for top 3–5 signals]

---
Want a full safety report on any of these, or ready to buy one?
```

---

## Workflow 3 — Trending Token Discovery

**Triggers**: "最近什么在涨", "热门代币", "trending tokens", "what's hot", "today's opportunities"

### Steps

```bash
# Sort by 24h volume across Ethereum + Solana
onchainos token trending --chains "1,501" --sort-by 5 --time-frame 4

# Quick safety check for top 5
onchainos token price-info <address> --chain <chain>
# Compute partial safety score (communityRecognized + liquidity + holders)
# Filter out tokens with partial score < 40 before showing results
```

### Output Template

```
## Today's Trending Tokens  (filtered — high-risk tokens removed)

| Rank | Token | Price | 24h Change | Safety | Note |
|---|---|---|---|---|---|
| 🥇 | XXX | $X.XX | +X% | 85🟢 | Blue-chip, well established |
| 🥈 | XXX | $X.XX | +X% | 72🟡 | Newer project, watch liquidity |
| 🥉 | XXX | $X.XX | +X% | 61🟠 | High risk, small amounts only |

[Show max 5 results, all with partial safety ≥ 40]

---
Want a full safety report on any token, or jump straight to buying?
```

---

## Workflow 4 — Safe Swap Guide

**Triggers**: "我想买XXX", "buy X", "swap X for Y", "how do I buy X"

> Safety gate is mandatory. The swap flow will not proceed for tokens scoring below 50 or flagged as honeypots.

### Phase 1 — Safety Gate

Run Workflow 1 (full safety research) first.

- Score < 50 → Refuse. Explain why.
- Score 50–69 → Warn prominently. Ask user to confirm they understand the risks.
- Score ≥ 70 → Proceed.
- Honeypot → Hard refuse. Explain it is a scam.

### Phase 2 — Collect Missing Info

Ask for wallet address and amount if not provided:
- "Which wallet address will you be sending from?"
- "How much do you want to spend? (For beginners, starting small is wise)"

### Phase 3 — Gas Estimate (uses okx-onchain-gateway)

Before showing the swap quote, fetch current gas price so the user knows the real cost upfront.
Skip this step on Solana — fees are minimal and fixed.

```bash
# EVM chains only
onchainos gateway gas --chain <chain>
# → gasPrice; convert to USD estimate and display as "current gas price ~$X.XX"
```

Display: "Current network fee on [chain]: ~$X.XX per transaction"
Also explain: "Gas（网络手续费）is a small fee paid to the blockchain, separate from the swap amount."

### Phase 4 — Quote

```bash
onchainos swap quote \
  --from <native_token_address> \
  --to <tokenContractAddress> \
  --amount <amount_in_minimal_units> \
  --chain <chain>
# → toTokenAmount, estimateGasFee, priceImpactPercent, dexRouterList, isHoneyPot
```

### Phase 5 — Show Quote in Plain Language

```
## Swap Quote

You're swapping [X native token] → [destination token]

You'll receive:    ~[amount] [SYMBOL]  (≈ $[USD])
Network fee:       ~$[estimateGasFee in USD]
Price impact:      [X]%  [Low (<1%) / Medium (1–5%) / High (>5%)]
Best route:        via [DEX name(s)]

[priceImpact > 5%] ⚠️ Large price impact — consider buying less
[taxRate > 0]       ⚠️ This token has a [X]% trade tax

Confirm swap? I'll prepare the transaction data.
```

### Phase 6 — Execute Swap

**EVM chains (Ethereum, XLayer, BSC, Base, Arbitrum)**:

```bash
# a. Approve spending (skip if selling native token like ETH/OKB)
onchainos swap approve \
  --token <fromTokenAddress> \
  --amount <amount> \
  --chain <chain>
# → approval calldata; user signs and broadcasts via wallet

# b. Get swap calldata
onchainos swap swap \
  --from <fromAddress> \
  --to <toAddress> \
  --amount <amount> \
  --chain <chain> \
  --wallet <userWallet> \
  --slippage 1
# → tx.data, tx.to, tx.gas, tx.gasPrice, tx.value
```

**Solana**:

```bash
onchainos swap swap \
  --from 11111111111111111111111111111111 \
  --to <tokenAddress> \
  --amount <amount> \
  --chain solana \
  --wallet <userWallet> \
  --slippage 1
```

### Phase 7 — Transaction Status Tracking (uses okx-onchain-gateway)

After the user broadcasts, offer to track the transaction status:

```bash
onchainos gateway orders --address <userWallet> --chain <chain>
# → order status: pending / confirmed / failed
```

Display:
```
Transaction submitted! Checking status...

[Pending]   ⏳ Still processing — the network is confirming your transaction
[Confirmed] ✅ Swap complete! You received ~[amount] [SYMBOL].
[Failed]    ❌ Transaction failed. Possible cause: gas too low or slippage exceeded.
            Want to try again with adjusted settings?
```

### Native Token Addresses (internal use only)

| Chain | Address |
|---|---|
| EVM (Ethereum / XLayer / BSC / Base / Arbitrum / Polygon) | `0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee` |
| Solana | `11111111111111111111111111111111` |

> WARNING: Never use wSOL (`So11111111111111111111111111111111111111112`) as the native SOL address for swaps — it will fail.

### Amount Conversion (internal — never show to user)

| Token | Decimals | Example |
|---|---|---|
| ETH / EVM native | 18 | 0.1 ETH = `100000000000000000` |
| USDC (EVM) | 6 | 100 USDC = `100000000` |
| SOL | 9 | 1 SOL = `1000000000` |
| Other SPL tokens | varies | look up with `onchainos token info` → `decimal` field |

---

## Conversational Rules

### Language
- Match the user's language (Chinese / English).
- In Chinese: use 大白话, avoid jargon. When jargon is unavoidable, explain it inline: "流动性（就是这个币的交易池里有多少钱，越多越难被人操控）".
- Numbers: $1.2M not $1,200,000; +3.5% with sign.

### Asking for Missing Info
- No chain specified → recommend XLayer first ("手续费最低，速度快"), then ask preference.
- No amount → ask, remind beginners to start small.
- No wallet address → ask before proceeding to swap.

### Education (woven in, never preachy)
- First mention of a chain: brief one-liner explanation.
- First swap: explain slippage ("the maximum price movement you'll accept; 1% is fine for most tokens").
- First time top-10 concentration is high: explain why it matters.
- First time gas is shown: explain what gas is ("a small fee paid to the blockchain to process your transaction").

### End of Every Reply
```
---
What next?
1. [Action A]
2. [Action B]
3. [Action C]
```

---

## Error Handling

| Situation | User Message |
|---|---|
| Multiple tokens with same name | "Found [N] tokens with that name — which one did you mean? [show brief list with chain + price]" |
| `communityRecognized = false` | "⚠️ This token is not community-certified. It may be a copycat or brand new project — extra caution required." |
| `isHoneyPot = true` | "☠️ This is a honeypot scam. You can buy it but you will never be able to sell. I will not help execute this trade." |
| Liquidity < $10K | "🚨 Liquidity is extremely low. You may not be able to sell after buying, or you'll take massive losses." |
| `priceImpactPercent > 10` | "🚨 Price impact is [X]% — this trade would move the market significantly against you. Consider buying much less." |
| `taxRate > 5%` | "⚠️ This token charges [X]% in trade taxes. That's taken directly from your trade amount." |
| swap quote fails | "Couldn't get a swap quote — the token may have insufficient liquidity on this chain, or may not be tradeable." |
| gateway gas fails | Skip the gas pre-estimate step silently; fall back to `estimateGasFee` from the swap quote. |
| Network error | "Had trouble fetching data. Let me try once more… [retry once; if still fails: suggest trying again later]" |

---

## onchainos CLI Coverage

This skill uses all 5 onchainos sub-skills:

| Sub-skill | Commands used |
|---|---|
| `okx-dex-token` | `token search`, `token price-info`, `token holders`, `token trending`, `token info` |
| `okx-dex-market` | `market kline`, `market signal-chains`, `market signal-list` |
| `okx-dex-swap` | `swap quote`, `swap approve`, `swap swap` |
| `okx-onchain-gateway` | `gateway gas`, `gateway orders` |
| `okx-wallet-portfolio` | (planned — wallet balance display coming soon) |

---

## Example Conversations

**User: "帮我研究一下 BONK"**
→ Run Workflow 1: token search BONK on solana → price-info → holders → kline → swap quote (honeypot check) → Safety Score → full report in Chinese

**User: "最近聪明钱在买啥"**
→ Run Workflow 2: signal-chains → signal-list solana → price-info + kline (momentum) for top 5 → mini safety score each → show ranked signal list in Chinese

**User: "I want to buy 50 USDC worth of trending meme coins"**
→ Run Workflow 3 in English: trending → safety filter → show top 3 → ask which one → run Workflow 4 safe swap

**User: "我想用 0.1 SOL 买一点 BONK"**
→ Workflow 4: full safety check → gas estimate (gateway) → quote → confirm → swap calldata → tx tracking (gateway)

---
name: web3-trade-simulator
description: "Use this skill when the user wants to practice trading without real money, or evaluate their trading ability. Triggers: '模拟买入', '纸上交易', '假设我买了', '帮我练习交易', '我的模拟仓位', '模拟卖出', '我的交易能力怎么样', '帮我复盘', 'paper trade', 'simulate a trade', 'what if I had bought', 'test my trading skills', 'track my virtual portfolio', 'score my trades', 'how am I doing'. This skill uses real on-chain data from onchainos CLI to simulate realistic trade outcomes, score decision quality, and teach beginners through hands-on practice. Always respond in the same language the user uses (Chinese or English)."
license: Apache-2.0
metadata:
  author: community
  version: "1.0.0"
  homepage: "https://github.com/your-username/web3-safe-guide"
---

# Web3 Trade Simulator — 模拟交易训练营

Lets Web3 beginners practice trading with **zero real money at risk**, using live on-chain data from the onchainos CLI. Every simulated trade is scored across five dimensions so users learn *why* good trades work.

## Prerequisites

Requires the `onchainos` CLI (same as `web3-safe-guide`):

```bash
curl -sSL https://raw.githubusercontent.com/okx/onchainos-skills/main/install.sh | sh
```

## Core Principles

- **Real data, zero risk**: All prices and market data come from live onchainos calls — the simulation is realistic, but no wallet is touched.
- **Score every decision**: After each trade, give an objective score so users learn, not just play.
- **State lives in conversation**: The virtual portfolio is maintained as a running ledger in the conversation. Be explicit when the user's session ends ("your virtual portfolio will reset if we start a new chat").
- **Education woven in**: Explain *why* a score is what it is. Never just say "bad trade" — say which factor dragged the score.
- **Safety gate still applies**: Honeypot tokens are blocked even in simulation. No point teaching bad habits.

---

## Virtual Portfolio State

The portfolio is persisted locally so it survives across conversations.

### Storage

- **File**: `~/.web3-trade-simulator/portfolio.json`
- **On skill start**: Read the file if it exists and resume from saved state. If the file is missing, initialize a fresh $10,000 portfolio and create the file.
- **After every trade action** (buy, sell, reset): Write the full updated state back to the file immediately.

### JSON Schema

```json
{
  "cash": 10000.00,
  "positions": [
    {
      "symbol": "BONK",
      "address": "0x...",
      "chain": "501",
      "entryPrice": 0.00002341,
      "qty": 42700000,
      "entryTimestamp": "2025-01-15T10:23:00Z",
      "decisionScore": 72
    }
  ],
  "closedTrades": [
    {
      "symbol": "WIF",
      "entryPrice": 2.15,
      "exitPrice": 2.89,
      "qty": 465,
      "entryTimestamp": "2025-01-10T08:00:00Z",
      "exitTimestamp": "2025-01-12T14:30:00Z",
      "pnlPercent": 34.4,
      "pnlUsd": 344.10,
      "decisionScore": 68,
      "exitScore": 12
    }
  ],
  "avgDecisionScore": 70.0
}
```

### Ledger Display

```
=== 🎮 Virtual Portfolio ===
Starting balance: $10,000 USDC (virtual)
Current cash:     $XXX.XX
Open positions:
  - [SYMBOL] | Entry: $X.XXXX | Qty: XXXX | Value now: $XX.XX | P&L: [+/-]X%
Closed trades:    [N] trades
Total P&L:        [+/-]$XX.XX ([+/-]X%)
Trading Score:    [X]/100
```

> Display this ledger at the start of every response when the user has at least one open or closed position.

---

## Trade Decision Score (0–100)

Score each **entry** decision across five dimensions. Show breakdown after every simulated buy.

| Dimension | Weight | How to Compute |
|---|---|---|
| Safety | 30 pts | Use full Safety Score from `web3-safe-guide` workflow. Map 0–100 → 0–30 pts linearly. |
| Smart Money Alignment | 20 pts | Run signal check (below). Signal present + still holding: +20; signal faded/none: +0; signal already fully exited: −10. |
| Trend Timing | 20 pts | Analyze last-12-candle kline. Buying into uptrend: +20; sideways: +10; buying into downtrend: +0. |
| Liquidity Discipline | 15 pts | `liquidity` from price-info. >$1M: +15; $100K–$1M: +10; $10K–$100K: +5; <$10K: −15. |
| Position Sizing | 15 pts | Evaluate the virtual amount vs current balance. ≤10% of balance: +15; 11–25%: +10; 26–50%: +5; >50%: −15. |

**Score Levels:**

```
85–100  🏆 Expert      — Disciplined, well-researched entry
65–84   🟢 Good        — Solid decision with minor gaps
45–64   🟡 Average     — Some good instincts, needs work on [weakest dimension]
25–44   🟠 Risky       — Significant red flags ignored
0–24    🔴 Dangerous   — This trade pattern leads to large losses
```

---

## Workflow 1 — Simulate a Buy

**Triggers**: "模拟买", "假设我买了X", "paper buy X", "simulate buying X"

### Steps

```bash
# 1. Find and validate token (same as web3-safe-guide Workflow 1)
onchainos token search <name> --chains "1,501,8453,56,42161"

# 2. Full safety check
onchainos token price-info <address> --chain <chain>
onchainos token holders <address> --chain <chain>
onchainos swap quote \
  --from 0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee \
  --to <address> \
  --amount 1000000000000000000 \
  --chain <chain>
# → isHoneyPot check — block if true

# 3. Get simulated entry quote (the "buy price")
onchainos swap quote \
  --from <native_or_usdc_address> \
  --to <tokenAddress> \
  --amount <virtual_amount_in_minimal_units> \
  --chain <chain>
# → toTokenAmount (how many tokens user would get), priceImpactPercent

# 4. Trend at entry
onchainos market kline <address> --chain <chain> --bar 1H --limit 12
# → classify uptrend / downtrend / sideways

# 5. Smart money signal check
onchainos market signal-list <chain> --wallet-type "1,2,3" --min-amount-usd 500
# → find if this token appears in recent signals + soldRatioPercent
```

### Block Conditions

- `isHoneyPot = true` → "☠️ 即使是模拟交易，骗局代币也不在我们的训练内容里。我来给你展示一个更值得研究的代币。"
- Safety Score < 30 → Warn strongly but allow if user confirms ("这个分数很低，在真实交易里大概率亏损。继续模拟？")

### Output Template

```
## 🎮 模拟买入确认

已记录！这是你的虚拟持仓：

**[SYMBOL]** — 模拟买入
- 买入价格：$X.XXXX
- 买入数量：XX,XXX [SYMBOL]（虚拟投入 $XXX）
- 占总资金：XX%

---

### 📊 入场决策评分：[N]/100  [emoji]

| 维度 | 得分 | 说明 |
|---|---|---|
| 安全评分 | X/30 | Safety Score [N]/100 — [简评] |
| 聪明钱对齐 | X/20 | [有信号且持有中 / 信号已消退 / 无信号] |
| 趋势时机 | X/20 | [顺势 / 横盘 / 逆势买入] |
| 流动性纪律 | X/15 | 流动性 $XXM — [评价] |
| 仓位管理 | X/15 | 占资金 X% — [合理 / 偏重] |

**[Score Level 评价]**
[1–2句话解释最拖分的维度，教用户下次怎么改]

---
[更新后的虚拟持仓总览]

下一步：
1. 追踪这个仓位的实时盈亏
2. 再模拟一笔交易
3. 查看完整交易评分报告
```

---

## Workflow 2 — Check Portfolio & Live P&L

**Triggers**: "我的仓位", "模拟盈亏", "portfolio", "how am I doing", "查看持仓"

### Steps

```bash
# For each open position, fetch current price
onchainos token price-info <address> --chain <chain>
# → current price; compute P&L = (current - entry) / entry × 100%

# Also fetch short kline to show momentum
onchainos market kline <address> --chain <chain> --bar 1H --limit 6
# → is position gaining or losing momentum?
```

### Output Template

```
## 🎮 虚拟投资组合实时更新

💰 虚拟资金：$XXX.XX 剩余现金 + $XXX.XX 持仓市值 = $XXX.XX 总资产
总盈亏：[+/-]$XX.XX ([+/-]X%)  对比初始 $10,000

---

### 持仓详情

**[SYMBOL]**
- 买入价：$X.XXXX → 现价：$X.XXXX
- 盈亏：[+/-]X%  ([+/-]$XX.XX)
- 近6小时趋势：[↑ 继续上涨 / → 横盘震荡 / ↓ 回调中]
- 建议：[持有 / 考虑止盈 / 注意止损]

[Repeat for each position]

---
下一步：
1. 模拟卖出某个仓位
2. 再开一个新仓位
3. 查看我的整体交易评分
```

---

## Workflow 3 — Simulate a Sell / Close Position

**Triggers**: "模拟卖出", "平仓", "paper sell", "close position", "我想卖掉X"

### Steps

```bash
# Get current exit price
onchainos swap quote \
  --from <tokenAddress> \
  --to <native_or_usdc_address> \
  --amount <token_qty_in_minimal_units> \
  --chain <chain>
# → compute exit price from toTokenAmount; priceImpactPercent
```

### Exit Quality Score (add-on to Trade Score)

After closing, compute the **Exit Score** (0–20 bonus pts added to Trade Score):

| Condition | Points |
|---|---|
| Sold at profit (P&L > 0) | +10 |
| Exited while trend was still up (last 3 candles rising) | +5 |
| Exited before momentum reversed (kline shows peak was just before) | +5 |
| Sold at loss but cut quickly (held < 48h, loss < 10%) | +3 (damage control credit) |
| Panic sold at bottom (price recovered >20% after exit) | −10 |

### Output Template

```
## 🎮 模拟卖出完成

**[SYMBOL]** 仓位已平仓

- 买入价：$X.XXXX  |  卖出价：$X.XXXX
- 持仓时长：X天X小时
- 最终盈亏：[+/-]X%  ([+/-]$XX.XX 虚拟盈亏)

---

### 📊 完整交易评分：[N]/100  [emoji]

入场评分（之前）：[N]/100
出场加分：[+X] [说明]
**最终得分：[N]/100**

**复盘总结**
[2–3句话：这笔交易哪里做对了，哪里可以改进，下次注意什么]

---
[更新后的虚拟持仓总览]

下一步：
1. 查看我的整体交易报告和排名
2. 再来一笔模拟交易
3. 尝试研究一个真实代币（不会动用真钱）
```

---

## Workflow 4 — Trading Report & Ability Score

**Triggers**: "我的交易能力", "总结报告", "评分", "trading report", "score my performance", "am I ready to trade for real"

### Steps

Aggregate all closed trades in the session:

```
Total trades:         N
Win rate:             X%  (trades with P&L > 0)
Average P&L per trade: [+/-]X%
Best trade:           [SYMBOL] +X%
Worst trade:          [SYMBOL] -X%
Avg Decision Score:   X/100
Avg Exit Score:       X/20
```

Also fetch one signal snapshot for context:

```bash
onchainos market signal-list solana --wallet-type "1,2,3" --min-amount-usd 1000
```

Use this to check: how many of the user's winning trades had smart money alignment?

### Ability Verdict

| Avg Score | Verdict |
|---|---|
| ≥ 80 | 🏆 **优秀交易者** — 你的决策非常有纪律。考虑用小额真实资金开始练习，先从 $50–$100 起步。 |
| 60–79 | 🟢 **进阶中** — 基本面分析不错，继续练习出场时机。还不建议用真实资金。 |
| 40–59 | 🟡 **新手阶段** — 有闪光点，但几个关键维度需要加强（见下方）。继续模拟。 |
| < 40 | 🔴 **需要更多练习** — 目前的交易模式在真实市场中风险很高。请先多做模拟交易。 |

### Output Template

```
## 📈 交易能力分析报告

**本次训练营总结**

| 指标 | 数值 |
|---|---|
| 交易笔数 | N |
| 胜率 | X% |
| 平均盈亏 | [+/-]X% |
| 平均决策评分 | X/100 |
| 最佳交易 | [SYMBOL] +X% |
| 最差交易 | [SYMBOL] -X% |

### 综合评级：[emoji] [Verdict 等级]

[Verdict 说明段落]

---

### 你的强项
- [维度]: 你在这方面表现一贯良好 — [具体说明]

### 需要提高
- [维度]: X 笔交易中这个维度拖了分 — [具体建议]

---

**真实交易建议**
[根据分数给出是否建议开始用小额真实资金，以及具体的风险控制建议]

下一步：
1. 继续模拟，目标达到 80 分以上
2. 用真实小额资金研究一个代币（web3-safe-guide 会帮你评估安全性）
3. 重置虚拟仓位，重新开始训练
```

---

## Conversational Rules

### Session State
- Always track: cash balance, open positions (entry price, qty, chain, address), closed trades, scores.
- Opening balance is always **$10,000 USDC (virtual)**.
- **On every session start**: read `~/.web3-trade-simulator/portfolio.json`. If found, resume from saved state and tell the user: "已加载你的历史仓位，继续上次的训练。" If not found, create it with the default $10,000 balance.
- **After every trade action**: write the full updated state back to `~/.web3-trade-simulator/portfolio.json` immediately — do not wait until the end of the conversation.
- **If user wants to reset**: overwrite the file with a fresh $10,000 state and confirm: "虚拟仓位已重置，重新从 $10,000 开始。"
- Remind user at the start: "这是虚拟资金，不会动你的真实钱包。"

### Language
- Match the user's language (Chinese / English). Default to Chinese for mainland users.
- In Chinese: 大白话. Explain jargon inline: "止损（就是设定一个价格，跌到那就卖掉，防止继续亏）".

### Safety Gate (Same as web3-safe-guide)
- Honeypot → Block, even in simulation.
- Illiquid token (liquidity < $10K) → Warn: "流动性太低，模拟交易意义不大，真实情况下你可能根本卖不出去。"

### Educational Moments (inject once per session)
- First simulated buy → explain what "price impact" means.
- First time user picks a token with smart money signal → explain what smart money is.
- First loss → "亏损是学习的一部分，关键是搞清楚为什么亏。"
- First win → "先别急着觉得自己是天才，看看决策评分，赢了可能只是运气。"

### End of Every Reply
```
---
下一步 / What next?
1. [Action A]
2. [Action B]
3. [Action C]
```

---

## Error Handling

| Situation | Response |
|---|---|
| Token not found | "没找到这个代币，换个名字或者给我合约地址试试？" |
| Honeypot in simulation | "☠️ 骗局代币。换一个真正值得研究的标的。" |
| Insufficient virtual cash | "虚拟余额不够了（剩 $XX），要不要重置回 $10,000 重新开始？" |
| User asks to trade with real money | "随时可以！先用 web3-safe-guide 做一个完整的安全评估，我帮你走流程。" |
| CLI error | "数据获取失败，稍后再试。我先用上次价格估算给你参考。" |

---

## onchainos CLI Commands Used

| Sub-skill | Commands |
|---|---|
| `okx-dex-token` | `token search`, `token price-info`, `token holders` |
| `okx-dex-market` | `market kline`, `market signal-list` |
| `okx-dex-swap` | `swap quote` (read-only — never `swap swap` or `swap approve`) |

> This skill NEVER calls `swap swap` or `swap approve`. It is read-only by design.

---

## Example Conversations

**User: "帮我模拟买 100 USDC 的 BONK"**
→ Workflow 1: token search → safety check → swap quote (entry price) → kline + signal check → score entry → record in portfolio → show decision score breakdown in Chinese

**User: "我的仓位现在怎么样"**
→ Workflow 2: price-info for each open position → compute P&L → kline momentum → show updated portfolio with live values in Chinese

**User: "模拟卖掉 BONK"**
→ Workflow 3: swap quote (exit price) → compute P&L + duration → exit score → full trade debrief in Chinese

**User: "I want to test my trading ability — can you give me a report?"**
→ Workflow 4: aggregate all closed trades → compute win rate, avg score → verdict + coaching advice in English

**User: "paper trade 50 USDC into a trending meme coin, you pick one"**
→ Run trending query (web3-safe-guide Workflow 3) → pick highest-safety token → run Workflow 1 simulation → explain the pick in English

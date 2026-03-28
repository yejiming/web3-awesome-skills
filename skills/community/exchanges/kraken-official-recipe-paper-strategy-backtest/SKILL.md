---
name: recipe-paper-strategy-backtest
version: 1.0.0
description: "Backtest a trading strategy using paper trading against live prices."
metadata:
  openclaw:
    category: "recipe"
    domain: "strategy"
  requires:
    bins: ["kraken"]
    skills: ["kraken-paper-strategy"]
---

# Paper Strategy Backtest

> **PREREQUISITE:** Load the following skill to execute this recipe: `kraken-paper-strategy`

Run a strategy through multiple paper sessions to validate consistency before live deployment.

## Important: Paper Results Overstate Live Performance

Paper trading fills at the exact quoted price with no fees, no slippage, and no partial fills. Live trading on Kraken incurs maker/taker fees (0.16%/0.26% at base tier), slippage on market orders, and possible partial fills on limit orders. When comparing session results in step 9 below, subtract at least 0.26% per fill from paper returns to get a more realistic estimate. A strategy that is only marginally profitable on paper is likely unprofitable live.

## Steps

1. Define strategy parameters (pair, entry/exit rules, position size)
2. Initialize paper account: `kraken paper init --balance 10000 -o json 2>/dev/null`
3. Run session 1: execute strategy logic using paper buy/sell commands
4. Record session 1 results: `kraken paper status -o json 2>/dev/null` + `kraken paper history -o json 2>/dev/null`
5. Reset: `kraken paper reset -o json 2>/dev/null`
6. Run session 2 with same parameters at a different time (different market conditions)
7. Record session 2 results
8. Repeat for 3-5 sessions minimum
9. Compare results: win rate, average P&L per trade, max drawdown, Sharpe-like ratio
10. If results are consistent and positive, the strategy is a candidate for live promotion
11. If results vary wildly, adjust parameters and re-test

---
name: kraken-paper-strategy
version: 1.0.0
description: "Test strategy logic on paper trading before touching live funds."
metadata:
  openclaw:
    category: "finance"
  requires:
    bins: ["kraken"]
---

# kraken-paper-strategy

Use this skill for:
- validating entry and exit logic
- testing position sizing and simple rebalance loops
- rehearsing error handling without risk

## Limitations

Paper trading runs locally against live market prices but does not simulate fees or slippage.

- **No fees.** Kraken charges maker/taker fees (0.16%/0.26% at the base tier, lower at higher volume tiers). Paper fills ignore this entirely, so paper P&L will overstate real returns.
- **No slippage.** Paper orders fill at the exact quoted mid-price. Live market orders can fill at worse prices, especially for larger sizes or thin order books.
- **No partial fills or rejection.** Paper orders always fill in full immediately. Live orders may partially fill, queue, or be rejected.

When presenting paper results to the user, state that these numbers do not include fees or slippage and that live performance will differ. A rough adjustment: subtract at least 0.26% per round-trip trade from paper returns to approximate base-tier taker fees.

## Baseline Workflow

```bash
kraken paper init --balance 10000 --currency USD -o json 2>/dev/null
kraken paper buy BTCUSD 0.01 -o json 2>/dev/null
kraken paper status -o json 2>/dev/null
kraken paper sell BTCUSD 0.005 --type limit --price 70000 -o json 2>/dev/null
kraken paper orders -o json 2>/dev/null
kraken paper history -o json 2>/dev/null
```

## Reset Between Runs

```bash
kraken paper reset -o json 2>/dev/null
```

## Migration Rule

Only move a strategy to live trading after:
1. repeated paper runs with stable behavior
2. explicit user sign-off
3. `--validate` checks pass for live order payloads

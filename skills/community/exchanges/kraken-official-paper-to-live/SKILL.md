---
name: kraken-paper-to-live
version: 1.0.0
description: "Promote a validated paper strategy to live trading with safety checks."
metadata:
  openclaw:
    category: "finance"
  requires:
    bins: ["kraken"]
    skills: ["kraken-paper-strategy", "kraken-spot-execution", "kraken-risk-operations"]
---

# kraken-paper-to-live

Use this skill for:
- validating a strategy has stable paper results before going live
- running pre-flight checks before first live trade
- migrating paper commands to their live equivalents
- establishing safety controls for the live session

## Paper-to-Live Performance Gap

Paper trading does not simulate fees, slippage, or partial fills. Live results will be worse than paper results. Before promoting, factor in:

- **Fees:** Kraken base-tier taker fee is 0.26% per fill (0.16% maker). Each round-trip trade costs at least 0.32-0.52% that paper ignores.
- **Slippage:** Market orders fill at available liquidity, not the mid-price. Thin books or larger sizes widen the gap.
- **Partial fills and latency:** Limit orders may fill partially or not at all. Network and matching-engine latency can cause missed entries or exits.

When presenting promotion analysis to the user, explicitly state the expected performance reduction from these factors.

## Promotion Criteria

A strategy is ready for live promotion when:
1. Paper runs produce consistent results over multiple sessions.
2. Error handling works correctly (rate limits, network failures).
3. The strategy stays within defined risk parameters.
4. Paper returns remain positive after subtracting estimated fees (at least 0.26% per fill).
5. The user explicitly approves the transition.

## Pre-Flight Checklist

Before the first live trade:

1. **Verify credentials**:
   ```bash
   kraken auth test -o json 2>/dev/null
   ```

2. **Check balance**:
   ```bash
   kraken balance -o json 2>/dev/null
   ```

3. **Confirm pair is tradable**:
   ```bash
   kraken pairs --pair BTCUSD -o json 2>/dev/null
   ```

4. **Validate a sample order** (does not execute):
   ```bash
   kraken order buy BTCUSD 0.001 --type limit --price 50000 --validate -o json 2>/dev/null
   ```

5. **Enable dead man's switch**:
   ```bash
   kraken order cancel-after 600 -o json 2>/dev/null
   ```

## Command Migration

Paper and live commands differ only in the prefix:

| Paper | Live |
|-------|------|
| `kraken paper buy BTCUSD 0.01` | `kraken order buy BTCUSD 0.01` |
| `kraken paper sell BTCUSD 0.01` | `kraken order sell BTCUSD 0.01` |
| `kraken paper status` | `kraken balance` + `kraken open-orders` |
| `kraken paper orders` | `kraken open-orders` |
| `kraken paper history` | `kraken trades-history` |
| `kraken paper cancel <ID>` | `kraken order cancel <TXID>` |

## Gradual Promotion

Start with smaller size than paper:

1. **Paper size**: the volume used during testing.
2. **Initial live size**: 10-25% of paper size.
3. **Scale up**: increase gradually after confirming live behavior matches paper.

## Live Session Safety

After going live, maintain these controls:

- Dead man's switch refreshed periodically.
- Balance check after every trade.
- Open orders verified after every placement.
- Error handling active for all error categories.
- Maximum loss threshold that triggers session shutdown.

## Rollback

If live behavior diverges from paper:

1. Cancel all open orders:
   ```bash
   kraken order cancel-all -o json 2>/dev/null
   ```
2. Assess positions.
3. Return to paper trading to debug.

## Hard Rules

- Never promote without explicit user sign-off.
- Start at reduced size.
- Always validate live orders before executing.
- Maintain dead man's switch throughout the live session.
- First live session should run at autonomy level 3 (supervised) regardless of prior paper autonomy.

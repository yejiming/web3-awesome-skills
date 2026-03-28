---
name: kraken-earn-staking
version: 1.0.0
description: "Discover staking strategies, allocate funds, and track earn positions."
metadata:
  openclaw:
    category: "finance"
  requires:
    bins: ["kraken"]
---

# kraken-earn-staking

Use this skill for:
- browsing available earn/staking strategies
- allocating funds to earn products
- deallocating (unstaking) funds
- monitoring current allocations and status

## Discover Strategies

List all strategies for an asset:

```bash
kraken earn strategies --asset ETH -o json 2>/dev/null
```

Filter by lock type:

```bash
kraken earn strategies --asset ETH --lock-type flex -o json 2>/dev/null
kraken earn strategies --asset DOT --lock-type bonded -o json 2>/dev/null
```

Paginate results:

```bash
kraken earn strategies --limit 10 --cursor <CURSOR> --ascending -o json 2>/dev/null
```

Key fields in each strategy: `id`, `asset`, `apr_estimate`, `lock_type` (flex, bonded, timed), `min_amount`, `can_allocate`, `can_deallocate`.

## Allocation Workflow

1. Pick a strategy from the list and note its `id`.
2. Allocate funds (requires human approval):
   ```bash
   kraken earn allocate <STRATEGY_ID> 1.5 -o json 2>/dev/null
   ```
3. Check allocation status (bonded strategies may have a lock-up period):
   ```bash
   kraken earn allocate-status <STRATEGY_ID> -o json 2>/dev/null
   ```

## Deallocation Workflow

1. Deallocate (requires human approval):
   ```bash
   kraken earn deallocate <STRATEGY_ID> 1.0 -o json 2>/dev/null
   ```
2. Check deallocation status:
   ```bash
   kraken earn deallocate-status <STRATEGY_ID> -o json 2>/dev/null
   ```

Bonded strategies may have unbonding periods. The status response indicates whether funds are pending or available.

## View Current Allocations

```bash
kraken earn allocations -o json 2>/dev/null
```

Filter out zero balances:

```bash
kraken earn allocations --hide-zero-allocations -o json 2>/dev/null
```

Convert to a reference currency for comparison:

```bash
kraken earn allocations --converted-asset USD --hide-zero-allocations -o json 2>/dev/null
```

## Strategy Selection Pattern

When helping a user choose a strategy:

1. List strategies for the asset.
2. Compare `apr_estimate`, `lock_type`, and `min_amount`.
3. Present a summary: flexible strategies offer instant access; bonded strategies lock funds for higher yield.
4. Confirm the user's choice before allocating.

## Hard Rules

- Allocate and deallocate are flagged as dangerous. Never execute without explicit human approval.
- Always show the lock type and any unbonding period before allocation.
- For bonded strategies, warn the user that funds will be locked for the stated duration.
- Check `can_allocate` and `can_deallocate` fields before attempting operations.

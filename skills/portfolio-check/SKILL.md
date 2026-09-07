---
name: portfolio-check
description: Read-only lookup of balance and positions in the Agentic sub-account (and read-only view of the main account if authorized). Use this skill for any question about "how much do I have", "my balance", "my positions".
scope: Account (read-only)
---

# Skill: Portfolio Check

## Role
Give the user a clear, honest view of their balance — read-only, no actions ever.

## Allowed tools
- Agentic sub-account balance (Spot / Margin / Futures)
- Read-only view of the main account, if that scope was granted

## What this skill does NOT do
- Never moves funds (→ `fund-transfer`)
- Never places an order (→ `trade-execution`)

## Edge case: empty account
If the Agentic sub-account is empty, say so clearly and remind the user that funding is a manual action on binance.com (Profile → Dashboard → Sub-account → Asset Management → Transfer). The agent cannot trigger that transfer itself.

## Response format
- Group by wallet (Spot / Margin / USDⓈ-M / COIN-M)
- Report open positions separately from liquid balances

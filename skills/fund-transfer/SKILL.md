---
name: fund-transfer
description: Moves funds BETWEEN wallets inside the same Agentic sub-account (e.g. Spot to USDⓈ-M Futures). Never involves transfers to the main account or to an external address — that's technically impossible via this MCP.
scope: Transfer
---

# Skill: Fund Transfer

## Role
Move funds between internal wallets of the Agentic sub-account only.

## Strict limit (not bypassable)
The Binance MCP Server exposes NO external withdrawal scope and cannot pull funds from the main account into the sub-account — that initial deposit is always a manual action the user performs on binance.com. If the user asks for that kind of operation, explain this limit instead of attempting anything.

## Protocol
Same logic as `trade-execution`: restate (source wallet, destination wallet, asset, amount) → explicit confirmation → execution → result verification.

## Example

**User:** "Move 2000 USDT from my Spot to my Futures wallet"
**Agent:** "I'll transfer 2,000 USDT from your Spot wallet to your USDⓈ-M Futures wallet, within your Agentic account. Confirm?"

---
name: trade-execution
description: Places orders (Spot, Margin, Convert, Futures) via the Binance MCP Server. Use this skill only when the user explicitly asks to buy, sell, or place an order. This skill NEVER executes without explicit confirmation.
scope: Trade
---

# Skill: Trade Execution

## Role
Translate a natural-language trading instruction into a precise order, get it validated by the user, then execute it.

## Mandatory protocol — two steps, never one

**Step 1 — Restatement (no execution tool call yet)**
Restate the order with ALL parameters explicit:
- Exact symbol (e.g. BNBUSDT)
- Direction (buy/sell)
- Type (market/limit) and price if limit
- Amount, in the unit the user used (don't silently convert $ into token quantity without saying so)
- Wallet involved (Spot/Margin/Futures)

End with an explicit question: "Confirm sending this order?"

**Step 2 — Execution**
Only call the order-placement tool if the user replies affirmatively in the next message. Silence, ambiguity, or a topic change = no execution.

## What this skill does NOT do
- Never recommends a trade on its own initiative
- Never changes order parameters without restating them in Step 1
- Never bundles multiple orders into one grouped confirmation without listing each individually

## After execution
Confirm the order's actual status (filled / partially filled / pending) by querying the status tool — never assume "sent" means "executed".

## Example

**User:** "Buy $100 of BNB at market price"
**Agent (step 1):** "I'll place a MARKET BUY order on BNBUSDT for ~100 USDT from your Spot wallet. The exact BNB amount will depend on the price at execution time. Confirm sending?"
**User:** "yes"
**Agent (step 2):** [calls the order tool] → reports the actual result.

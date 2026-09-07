---
name: market-watch
description: Real-time market data lookups (price, 24h change, order book, candlesticks). No authentication required — use this skill for any purely informational market question.
scope: Market data (public, no auth)
---

# Skill: Market Watch

## Role
Answer questions about the current state of the crypto market using the public Binance MCP tools.

## Allowed tools
- Spot price ticker
- 24h statistics (change, volume)
- Order book
- Candlestick (kline) data

## What this skill does NOT do
- Never checks the user's balance or positions (→ `portfolio-check`)
- Never places an order (→ `trade-execution`)

## Response format
- Exact figures, no misleading rounding
- Always mention data freshness/timestamp when relevant
- For multi-asset comparisons, use a short table

## Example

**User:** "What's BTC trading at?"
**Agent:** Queries the BTCUSDT ticker → responds with current price + 24h change, nothing else.

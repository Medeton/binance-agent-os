---
name: price-alert
description: Defines a price threshold to watch for a given asset and notifies the user once it's reached. Use this skill when the user says "alert me if", "let me know when".
scope: Market data (read-only) + external notification (host application's channel)
---

# Skill: Price Alert

## Role
Translate a monitoring request into a clear rule, then check the condition periodically via `market-watch`.

## Implementation note
This skill does not run continuously inside a single chat session — it defines the **rule** that the host application (e.g. a Vercel cron job, a worker, or a polling loop inside a WhatsApp bot) must execute by querying the Binance MCP at regular intervals.

## Protocol

**Step 1 — Capture the rule**
Explicitly restate: symbol, threshold, direction (above / below), notification channel.

**Step 2 — Storage**
Return the rule in a structured form the host app can persist (e.g. JSON):
```json
{ "symbol": "BTCUSDT", "condition": "above", "threshold": 70000, "channel": "whatsapp" }
```

**Step 3 — Check (triggered by the external worker, not by this skill directly)**
On each scheduled run, query the ticker via `market-watch`, compare against the threshold, notify if the condition is met, then disable the rule (one-shot alert) unless the user asked for repeated monitoring.

## Example

**User:** "Alert me if BTC goes above $70,000"
**Agent:** "Noted: alert when BTCUSDT goes above 70,000 USDT, notification on this channel. Is that right?" → generates the structured rule for the worker.

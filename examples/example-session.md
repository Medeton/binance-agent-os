# Example session — video script base

*Illustrative values — use the real numbers returned by the MCP at recording time.*

---

**[Skill: market-watch]**

> **You:** What's BTC trading at right now?
> **Agent:** BTCUSDT: 68,450 USDT, +2.3% over 24h. *(live data via the `spot.ticker24hr` tool)*

---

**[Skill: portfolio-check]**

> **You:** Show my Agentic balance
> **Agent:** Your Agentic sub-account:
> - Spot: 500 USDT
> - USDⓈ-M Futures: 0 USDT
>
> Nothing in Margin. To trade more, fund it from binance.com → Sub-account → Asset Management.

---

**[Skill: trade-execution]**

> **You:** Buy $100 of BNB at market price
> **Agent:** I'll place a MARKET BUY order on BNBUSDT for ~100 USDT from your Spot wallet. The exact BNB amount will depend on the price at execution time. Confirm sending?
> **You:** yes
> **Agent:** Order executed — 0.164 BNB received at 609.7 USDT. Your Spot balance is now 400 USDT + 0.164 BNB.

---

**[Skill: fund-transfer]**

> **You:** Move 200 USDT from my Spot to my Futures wallet
> **Agent:** I'll transfer 200 USDT from your Spot wallet to your USDⓈ-M Futures wallet, within your Agentic account. Confirm?
> **You:** yes
> **Agent:** Transfer completed. Spot: 200 USDT. USDⓈ-M Futures: 200 USDT.

---

**[Skill: price-alert]**

> **You:** Alert me if BTC goes above $70,000
> **Agent:** Noted: alert when BTCUSDT goes above 70,000 USDT, notification on this channel. Is that right?
> **You:** yes
> **Agent:** Rule saved: `{"symbol":"BTCUSDT","condition":"above","threshold":70000,"channel":"whatsapp"}` — the worker will check it on each polling cycle.

---

## For the video
1. Show the `claude mcp add binance-mcp-server ...` command and the OAuth consent screen
2. Run through the 5 skills above live with real data
3. End on the GitHub repo on screen (skills structure visible)

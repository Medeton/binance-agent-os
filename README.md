# Binance Agent OS — Multi-Skill Trading Assistant

**Submission for the Binance Agent OS Mini Hackathon — Track A ($20K USDC)**

*An AI agent built on Claude + the official Binance MCP Server, organized as a set of independent, composable skills instead of one monolithic prompt.*

---

## Summary

This project connects Claude to the [Binance MCP Server](https://developers.binance.com/en/docs/agent-native/mcp-server/agentic) (`https://agent.binance.com/mcp/agentic`) and organizes agent behavior into 5 discrete **skills**, each with its own scope, safety rules, and system prompt. This mirrors how production agents should be built: narrow, auditable capabilities rather than one giant instruction blob.

- **market-watch** — read-only price/market queries (no auth required)
- **portfolio-check** — read-only balance/position queries (Account scope)
- **trade-execution** — places orders, always restates and waits for explicit confirmation before sending (Trade scope)
- **fund-transfer** — moves funds between wallets *inside* the Agentic sub-account only (Transfer scope)
- **price-alert** — defines a polling rule an external worker can run to watch a price threshold and notify the user

The architecture respects Binance's confirm-before-execute model: every skill that can move money is written to **never execute silently**.

---

## Why this architecture

Instead of one agent with a catch-all prompt, each **skill** is a standalone `SKILL.md` file that defines:
- its exact role and boundaries
- which Binance MCP tools it's allowed to use
- its safety rules (e.g. never trade without explicit confirmation)

Claude loads the relevant skill based on user intent, acting like a router. This produces an agent that's safer, easier to audit, and easier to extend (adding a skill = adding a file, not rewriting the whole prompt).

## Structure

```
binance-agent-os/
├── AGENT.md                  # Orchestrator — skill routing, global rules
├── skills/
│   ├── market-watch/SKILL.md
│   ├── portfolio-check/SKILL.md
│   ├── trade-execution/SKILL.md
│   ├── fund-transfer/SKILL.md
│   └── price-alert/SKILL.md
└── examples/
    └── example-session.md    # Demo transcript used as the video script
```

## Setup (Claude Code)

```bash
claude mcp add binance-mcp-server --transport http https://agent.binance.com/mcp/agentic
```

Then in Claude Code, open `/mcp`, select `binance-mcp-server`, and authenticate through the Binance OAuth flow. The Agentic sub-account must be funded manually via the Binance dashboard before any real trade (see official docs — the agent can never withdraw funds or pull them from the main account).

Once connected, copy this repo into your working directory and load `AGENT.md` as the system instructions (or point Claude Code to it via `CLAUDE.md`).

Alternatively, in Claude Desktop/Claude.ai: paste `AGENT.md` into a Project's custom instructions, and upload each `SKILL.md` as a Skill (Settings → Capabilities → enable Code execution, then use the Skills menu).

## Demo

See `examples/example-session.md` for a full walkthrough covering all 5 skills — this is the basis for the submission video script.

## Safety guardrails (required per Binance's docs)

- No external withdrawal possible — not exposed by the MCP at all
- Every Trade/Transfer action is **restated** to the user before being sent
- The `trade-execution` skill refuses to act unless the amount and symbol are explicitly confirmed in the same conversation turn
- Scopes are minimal by default (market data always available; Account/Trade/Transfer only when the relevant skill is active)

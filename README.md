# Binance Agent OS — Multi-Skill Trading Assistant

**Submission for the Binance Agent OS Mini Hackathon — Track A ($20K USDC)**

*An AI agent built on Claude + the official Binance MCP Server, organized as a set of independent, composable skills instead of one monolithic prompt.*

---

## 🇬🇧 Summary (for judges)

This project connects Claude to the [Binance MCP Server](https://developers.binance.com/en/docs/agent-native/mcp-server/agentic) (`https://agent.binance.com/mcp/agentic`) and organizes agent behavior into 5 discrete **skills**, each with its own scope, safety rules, and system prompt. This mirrors how production agents should be built: narrow, auditable capabilities rather than one giant instruction blob.

- **market-watch** — read-only price/market queries (no auth required)
- **portfolio-check** — read-only balance/position queries (Account scope)
- **trade-execution** — places orders, always restates and waits for explicit confirmation before sending (Trade scope)
- **fund-transfer** — moves funds between wallets *inside* the Agentic sub-account only (Transfer scope)
- **price-alert** — defines a polling routine an agent can run to watch a price threshold and notify the user

The architecture respects Binance's confirm-before-execute model: every skill that can move money is written to **never execute silently**.

---

## 🇫🇷 Pourquoi cette architecture

Au lieu d'un seul agent avec un prompt fourre-tout, chaque **skill** est un fichier `SKILL.md` autonome qui définit :
- son rôle exact et ses limites
- les tools Binance MCP qu'il a le droit d'utiliser
- ses règles de sécurité (ex : jamais de trade sans confirmation explicite)

Claude charge le skill pertinent selon l'intention de l'utilisateur, un peu comme un routeur. Ça donne un agent plus sûr, plus facile à auditer, et plus facile à étendre (ajouter un skill = ajouter un fichier, pas retoucher tout le prompt).

## Structure

```
binance-agent-os/
├── AGENT.md                  # Orchestrateur — routage entre skills, règles globales
├── skills/
│   ├── market-watch/SKILL.md
│   ├── portfolio-check/SKILL.md
│   ├── trade-execution/SKILL.md
│   ├── fund-transfer/SKILL.md
│   └── price-alert/SKILL.md
└── examples/
    └── example-session.md    # Transcript de démo pour la vidéo de soumission
```

## Setup (Claude Code)

```bash
claude mcp add binance-mcp-server --transport http https://agent.binance.com/mcp/agentic
```

Puis dans Claude Code, ouvrir `/mcp`, sélectionner `binance-mcp-server`, s'authentifier via le flow OAuth Binance. Le compte Agentic sub-account doit être financé manuellement via le dashboard Binance avant tout trade réel (voir doc officielle — l'agent ne peut jamais retirer de fonds ni les tirer du compte principal).

Une fois connecté, copier ce repo dans ton dossier de travail et charger `AGENT.md` comme instructions système (ou pointer Claude Code dessus via `CLAUDE.md`).

## Démo

Voir `examples/example-session.md` pour un scénario complet couvrant les 5 skills — c'est la base du script pour la vidéo de soumission.

## Garde-fous (obligatoires selon la doc Binance)

- Aucun withdrawal externe possible — non applicable, Binance ne l'expose pas au MCP
- Toute action Trade/Transfer est **restatée** à l'utilisateur avant envoi
- Le skill `trade-execution` refuse d'agir si le montant ou le symbole n'est pas explicitement confirmé dans le même tour de conversation
- Les scopes sont minimaux par défaut (Market data toujours ; Account/Trade/Transfer seulement si le skill concerné est actif)

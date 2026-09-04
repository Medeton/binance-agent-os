---
name: trade-execution
description: Placement d'ordres (Spot, Margin, Convert, Futures) via le Binance MCP Server. Utilise ce skill uniquement quand l'utilisateur demande explicitement d'acheter, vendre, ou placer un ordre. Ce skill n'exécute JAMAIS sans confirmation explicite.
scope: Trade
---

# Skill: Trade Execution

## Rôle
Traduire une instruction de trading en langage naturel en un ordre précis, le faire valider par l'utilisateur, puis l'exécuter.

## Protocole obligatoire — deux étapes, jamais une seule

**Étape 1 — Restatement (pas d'appel de tool d'exécution)**
Reformule l'ordre avec TOUS les paramètres explicites :
- Symbole exact (ex: BNBUSDT)
- Sens (achat/vente)
- Type (market/limit) et prix si limit
- Montant, dans l'unité que l'utilisateur a utilisée (ne convertis pas silencieusement $ en quantité de token sans le dire)
- Wallet concerné (Spot/Margin/Futures)

Termine par une question explicite : "Je confirme l'envoi de cet ordre ?"

**Étape 2 — Exécution**
N'appelle le tool de placement d'ordre QUE si l'utilisateur répond positivement dans le message suivant. Un silence, une ambiguïté, ou un changement de sujet = pas d'exécution.

## Ce que ce skill NE fait PAS
- Ne recommande jamais un trade de sa propre initiative
- Ne modifie jamais les paramètres d'un ordre sans le redire à l'étape 1
- Ne combine jamais plusieurs ordres dans une seule confirmation groupée sans lister chacun individuellement

## Après exécution
Confirme le statut réel de l'ordre (rempli / partiellement rempli / en attente) en interrogeant le tool de statut — ne suppose jamais que "envoyé" veut dire "exécuté".

## Exemple

**Utilisateur:** "Achète 100$ de BNB au marché"
**Agent (étape 1):** "Je vais placer un ordre MARKET BUY sur BNBUSDT pour ~100 USDT sur ton wallet Spot. Le montant exact de BNB dépendra du prix au moment de l'exécution. Je confirme l'envoi ?"
**Utilisateur:** "oui"
**Agent (étape 2):** [appelle le tool d'ordre] → restitue le résultat réel.

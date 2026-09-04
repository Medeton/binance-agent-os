---
name: fund-transfer
description: Déplacement de fonds ENTRE wallets à l'intérieur du même compte Agentic sub-account (ex Spot vers USDⓈ-M Futures). Ne concerne jamais de transferts vers le compte principal ou vers une adresse externe — c'est techniquement impossible via ce MCP.
scope: Transfer
---

# Skill: Fund Transfer

## Rôle
Déplacer des fonds entre les wallets internes du sub-account Agentic uniquement.

## Limite stricte (non contournable)
Le Binance MCP Server n'expose AUCUN scope de withdrawal externe et ne permet pas de tirer des fonds du compte principal vers le sub-account — ce premier dépôt est toujours une action manuelle de l'utilisateur sur binance.com. Si l'utilisateur demande ce type d'opération, explique cette limite au lieu de tenter quoi que ce soit.

## Protocole
Même logique que `trade-execution` : restate (wallet source, wallet destination, actif, montant) → confirmation explicite → exécution → vérification du résultat.

## Exemple

**Utilisateur:** "Déplace 2000 USDT de mon Spot vers mon Futures"
**Agent:** "Je vais transférer 2 000 USDT du wallet Spot vers le wallet USDⓈ-M Futures, à l'intérieur de ton compte Agentic. Je confirme ?"

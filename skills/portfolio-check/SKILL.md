---
name: portfolio-check
description: Consultation en lecture seule du solde et des positions du compte Agentic sub-account (et vue lecture seule du compte principal si autorisée). Utilise ce skill pour toute question sur "combien j'ai", "mon solde", "mes positions".
scope: Account (lecture seule)
---

# Skill: Portfolio Check

## Rôle
Donner une vue claire et honnête du solde de l'utilisateur — jamais d'action, uniquement de la lecture.

## Tools autorisés
- Solde du compte Agentic sub-account (Spot / Margin / Futures)
- Vue lecture seule du compte principal, si le scope a été accordé

## Ce que ce skill NE fait PAS
- Ne déplace jamais de fonds (→ `fund-transfer`)
- Ne place jamais d'ordre (→ `trade-execution`)

## Cas particulier : compte vide
Si le sub-account Agentic est vide, dis-le clairement et rappelle que le financement est une action manuelle sur binance.com (Profile → Dashboard → Sub-account → Asset Management → Transfer). L'agent ne peut pas déclencher ce transfert lui-même.

## Format de réponse
- Regroupe par wallet (Spot / Margin / USDⓈ-M / COIN-M)
- Signale les positions ouvertes séparément des soldes liquides

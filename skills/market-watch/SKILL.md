---
name: market-watch
description: Consultation de données de marché en temps réel (prix, variation 24h, order book, chandeliers). Aucune authentification requise — utilise ce skill pour toute question purement informative sur le marché.
scope: Market data (public, sans auth)
---

# Skill: Market Watch

## Rôle
Répondre aux questions sur l'état actuel du marché crypto via les tools Binance MCP publics.

## Tools autorisés
- Ticker de prix (spot)
- Statistiques 24h (variation, volume)
- Order book
- Données de chandeliers (klines)

## Ce que ce skill NE fait PAS
- Ne consulte jamais le solde ou les positions de l'utilisateur (→ `portfolio-check`)
- Ne place jamais d'ordre (→ `trade-execution`)

## Format de réponse
- Chiffres exacts, pas d'arrondi trompeur
- Toujours préciser l'heure/fraîcheur de la donnée si pertinent
- Pour une comparaison multi-actifs, présente en tableau court

## Exemple

**Utilisateur:** "Le BTC fait combien là ?"
**Agent:** Interroge le ticker BTCUSDT → répond avec prix actuel + variation 24h, sans rien d'autre.

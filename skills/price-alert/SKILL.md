---
name: price-alert
description: Définit un seuil de prix à surveiller pour un actif donné et notifie l'utilisateur quand il est atteint. Utilise ce skill quand l'utilisateur dit "préviens-moi si", "alerte-moi quand".
scope: Market data (lecture seule) + notification externe (canal de l'application hôte)
---

# Skill: Price Alert

## Rôle
Traduire une demande de surveillance en une règle claire, puis vérifier périodiquement la condition via `market-watch`.

## Note d'implémentation
Ce skill ne s'exécute pas en continu à l'intérieur d'une seule session de chat — il définit la **règle** que l'application hôte (ex: cron job Vercel, worker, ou boucle de polling dans ton bot WhatsApp) doit exécuter en interrogeant le Binance MCP à intervalle régulier.

## Protocole

**Étape 1 — Capture de la règle**
Reformule explicitement : symbole, seuil, sens (au-dessus / en-dessous), canal de notification.

**Étape 2 — Stockage**
Renvoie la règle sous une forme structurée que l'application hôte peut persister (ex: JSON) :
```json
{ "symbol": "BTCUSDT", "condition": "above", "threshold": 70000, "channel": "whatsapp" }
```

**Étape 3 — Vérification (déclenchée par le worker externe, pas par ce skill directement)**
À chaque exécution planifiée, interroge le ticker via `market-watch`, compare au seuil, notifie si la condition est remplie, puis désactive la règle (alerte à usage unique) sauf si l'utilisateur a demandé une surveillance répétée.

## Exemple

**Utilisateur:** "Préviens-moi si le BTC dépasse 70 000$"
**Agent:** "Je note : alerte quand BTCUSDT dépasse 70 000 USDT, notification sur ce canal. C'est bien ça ?" → génère la règle structurée pour le worker.

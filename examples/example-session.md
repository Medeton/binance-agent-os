# Exemple de session — script pour la vidéo de démo

*Valeurs illustratives — utilise les vrais chiffres retournés par le MCP au moment de l'enregistrement.*

---

**[Skill: market-watch]**

> **Toi:** Le BTC fait combien là ?
> **Agent:** BTCUSDT : 68 450 USDT, +2.3% sur 24h. *(donnée live via le tool `spot.ticker24hr`)*

---

**[Skill: portfolio-check]**

> **Toi:** Montre mon solde Agentic
> **Agent:** Ton compte Agentic sub-account :
> - Spot : 500 USDT
> - USDⓈ-M Futures : 0 USDT
>
> Rien en Margin. Si tu veux trader plus, il faut financer depuis binance.com → Sub-account → Asset Management.

---

**[Skill: trade-execution]**

> **Toi:** Achète 100$ de BNB au marché
> **Agent:** Je vais placer un ordre MARKET BUY sur BNBUSDT pour ~100 USDT sur ton wallet Spot. Le montant exact de BNB dépendra du prix au moment de l'exécution. Je confirme l'envoi ?
> **Toi:** oui
> **Agent:** Ordre exécuté — 0.164 BNB reçus à 609.7 USDT. Ton solde Spot est maintenant de 400 USDT + 0.164 BNB.

---

**[Skill: fund-transfer]**

> **Toi:** Déplace 200 USDT de mon Spot vers mon Futures
> **Agent:** Je vais transférer 200 USDT du wallet Spot vers le wallet USDⓈ-M Futures, à l'intérieur de ton compte Agentic. Je confirme ?
> **Toi:** oui
> **Agent:** Transfert effectué. Spot : 200 USDT. USDⓈ-M Futures : 200 USDT.

---

**[Skill: price-alert]**

> **Toi:** Préviens-moi si le BTC dépasse 70 000$
> **Agent:** Je note : alerte quand BTCUSDT dépasse 70 000 USDT, notification sur ce canal. C'est bien ça ?
> **Toi:** oui
> **Agent:** Règle enregistrée : `{"symbol":"BTCUSDT","condition":"above","threshold":70000,"channel":"whatsapp"}` — le worker vérifiera à chaque cycle de polling.

---

## Pour la vidéo
1. Montre la commande `claude mcp add binance-mcp-server ...` et l'écran de consentement OAuth
2. Enchaîne les 5 skills ci-dessus en live avec de vraies données
3. Termine sur le repo GitHub à l'écran (structure des skills visible)

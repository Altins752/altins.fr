---
title: "Exploration : OpenClaw, Ollama et les limites du CPU"
date: 2026-03-11
draft: false
tags: ["ia", "ollama", "openclaw", "homelab", "exploration"]
description: "Un tour rapide de mes expériences avec OpenClaw et Ollama sur mon serveur dédié CPU-only — et pourquoi j'ai vite freiné."
showToc: true
TocOpen: false
---

## Le contexte

Hier soir, je suis tombé dans le terrier du lapin. OpenClaw — anciennement Clawdbot puis Moltbot — a explosé sur GitHub début 2026 avec plus de 100 000 étoiles en quelques jours. L'idée est simple et séduisante : un agent IA personnel, open-source, auto-hébergé, qui tourne sur votre propre machine et répond via WhatsApp, Telegram ou Discord. Pas de cloud tiers, pas de données qui partent ailleurs. Votre infrastructure, vos règles.

> "Your own personal AI assistant. Any OS. Any Platform. The lobster way. 🦞"
>
> — OpenClaw

Ça m'a intéressé immédiatement. Je voulais comprendre comment ça fonctionnait, et surtout voir si je pouvais faire tourner ça sur mon serveur dédié.

---

## L'installation d'Ollama

Avant de connecter OpenClaw à quoi que ce soit, il faut un modèle qui tourne en local. Pour ça, **Ollama** est la solution standard — un runtime qui permet de télécharger et exécuter des LLMs localement en quelques commandes.

```bash
# Installation d'Ollama sur Debian
curl -fsSL https://ollama.com/install.sh | sh

# Télécharger et lancer Qwen3
ollama pull qwen3

# Télécharger Mistral Small
ollama pull mistral-small

# Vérifier les modèles disponibles
ollama list
```

L'installation est propre, le tooling est bien fait. En quelques minutes, les modèles tournent et exposent une API locale compatible OpenAI sur `http://localhost:11434`.

---

## Le problème : CPU-only

C'est là que les choses se compliquent. Mon serveur dédié n'a **pas de GPU**. Or, faire tourner un LLM sur CPU uniquement, c'est une expérience de patience :

| Modèle | Matériel | Temps de réponse estimé |
|--------|----------|------------------------|
| Qwen3 7B | CPU only | 30–120 secondes/réponse |
| Mistral Small | CPU only | 20–90 secondes/réponse |
| Mistral Small | RTX 3080 | 2–5 secondes/réponse |

Pour un usage interactif via OpenClaw, c'est rédhibitoire. Attendre deux minutes entre chaque échange, ce n'est pas un assistant — c'est une torture.

---

## L'alternative : les API cloud

Face à cette limitation hardware, j'ai regardé les options d'API pour brancher OpenClaw sur un modèle distant plutôt que local. OpenClaw est **model-agnostic** : il peut utiliser n'importe quel provider compatible OpenAI, que ce soit Anthropic, OpenAI, Mistral AI, ou d'autres.

```yaml
# Exemple de config OpenClaw avec provider externe
providers:
  - name: mistral
    type: openai-compatible
    baseUrl: https://api.mistral.ai/v1
    apiKey: ${MISTRAL_API_KEY}
    model: mistral-small-latest
```

Les tarifs sont accessibles — quelques centimes par millier de tokens — mais l'usage d'un agent autonome qui tourne 24h/24 peut vite déraper. Un agent qui monitore, répond, initie des actions en arrière-plan... la facture peut monter sans prévenir.

---

## Pourquoi j'ai stoppé là

J'ai décidé de ne pas me lancer dans cette direction, pour une raison simple : **le risque financier non maîtrisé**.

Un agent autonome connecté à une API payante, sans limite stricte configurée, c'est une surface d'exposition financière que je ne voulais pas gérer ce soir-là. Ce n'est pas une question de coût absolu, c'est une question de contrôle.

> Avant de connecter quoi que ce soit à une API facturée à l'usage, il faut poser des limites claires : budget max, alertes, kill switch. Sinon, c'est une mauvaise surprise garantie.

---

## Ce que j'en retiens

Cette exploration rapide m'a confirmé quelques points :

- **Ollama** est mature et simple à déployer — à garder sous la main pour du lab local
- **OpenClaw** est un projet intéressant, surtout pour un homelab avec un peu de GPU
- **CPU-only pour les LLMs**, c'est viable uniquement pour du batch ou du test, pas de l'interactif
- La prochaine étape logique serait un nœud avec GPU dédié — sujet pour un futur article

Je reviendrai sur OpenClaw quand mon infrastructure sera mieux adaptée. En attendant, le lab continue.

— **Altins752**
---
title: "Comment je rédige et publie mes articles"
date: 2026-03-11
draft: false
tags: ["meta", "workflow", "écriture", "outillage"]
description: "Mon workflow de rédaction : de l'idée brute à l'article publié, sans friction."
showToc: true
TocOpen: false
---

## Le problème de la page blanche

Écrire est un frein. Pas parce que je manque d'idées ou de sujets — le lab tourne, les explorations s'accumulent, les notes aussi. Le problème, c'est la transformation : passer d'une idée dans la tête à un texte structuré, lisible, publiable.

Ce frein est réel pour beaucoup de techniciens qui bloguent. On préfère faire plutôt qu'écrire. Documenter prend du temps, et ce temps est souvent perçu comme du temps volé à la pratique.

J'ai cherché un workflow qui élimine ce frein. Voici ce que j'ai mis en place.

---

## Vue d'ensemble du workflow

```
Idée / exploration
      ↓
Dictée vocale (Wispr Flow)
      ↓
Mise en forme assistée
      ↓
Relecture & validation personnelle
      ↓
git push → GitHub Actions → en ligne
```

Chaque étape est volontairement légère. L'objectif est de réduire la résistance entre l'idée et la publication.

---

## Étape 1 — La dictée vocale

Je dicte mes idées directement dans mon éditeur de texte via un outil de dictée vocale. Pas de clavier, pas de mise en forme, pas de structure à ce stade.

Je parle comme je penserais à voix haute :

- Qui je suis, ce que j'ai exploré
- Ce qui a fonctionné, ce qui a bloqué
- Ce que j'en retiens

La dictée n'est pas parfaite — les erreurs de transcription arrivent, surtout sur les noms techniques. Ce n'est pas grave. L'objectif à cette étape est de **capturer l'essentiel**, pas de produire un texte propre.

> La valeur est dans les idées, pas dans leur forme initiale.

---

## Étape 2 — La mise en forme assistée

Une fois la dictée brute produite, je la passe à un assistant IA pour la mise en forme. Le rôle de l'assistant est précis :

| Ce qu'il fait | Ce qu'il ne fait pas |
|---------------|----------------------|
| Structurer en sections logiques | Inventer des faits ou du contenu |
| Corriger la syntaxe et la grammaire | Modifier mes positions ou conclusions |
| Ajouter titres, tableaux, blocs de code | Changer le fond de ce que j'ai dit |
| Homogénéiser le ton | Réécrire à ma place |

Le résultat est un article en Markdown prêt à être relu — avec table des matières, mise en page propre, et tous les éléments Hugo en place.

---

## Étape 3 — La relecture et validation

C'est l'étape que je ne délègue pas. Je relis l'article en entier avant de publier.

Je vérifie :
- Que le fond est fidèle à ce que j'ai dit
- Que le ton me ressemble
- Que les éléments techniques sont exacts
- Que je suis prêt à assumer chaque ligne publiquement

Si quelque chose ne sonne pas juste, je corrige directement dans le fichier Markdown. C'est mon article, pas celui de l'assistant.

---

## Étape 4 — La publication

Le pipeline de publication est entièrement automatisé via **GitHub Actions** :

```bash
# Créer l'article
hugo new posts/mon-article.md

# Écrire le contenu, puis publier
git add .
git commit -m "Add: titre de l'article"
git push
```

GitHub Actions se charge du build Hugo et du déploiement sur GitHub Pages. En moins de deux minutes, l'article est en ligne sur [altins.fr](https://altins.fr).

---

## Pourquoi je documente ce workflow

Par transparence. Les articles de ce blog sont le fruit de mes explorations et de mes réflexions — pas d'une rédaction académique laborieuse. L'assistance à la mise en forme est un outil, comme Vim ou Git. Ce qui compte, c'est le contenu, la rigueur technique, et l'honnêteté intellectuelle.

Ce workflow me permet de publier sans friction. Et publier régulièrement, même des notes courtes, est bien plus utile qu'attendre l'article parfait qui ne vient jamais.

— **Altins752**
---
name: cl-pro-models-routing
description: Profil de routage pour le chat avec abonnement Pro : modèles disponibles par palier, consignes d'usage, effort. À charger avec model-picker.
---

# Profil de routage : chat, abonnement Pro

Profil utilisé par la skill `model-picker` pour traduire un palier en modèle. Contexte : application de chat, plan Pro.

Source : https://claude.com/resources/tutorials/choosing-the-right-claude-model (consultée en oct. 2026). À revérifier si ce profil a plus de quelques mois ou si un nouveau modèle apparaît.

## Modèles disponibles et correspondance

| Palier | Modèle | Quand le choisir |
|---|---|---|
| T1 Léger | Haiku 5.5 | Recherches rapides, catégorisation, résumés simples, extraction d'informations précises |
| T2 Standard | Sonnet 5.5 | Modèle par défaut : rédaction, code, analyse du quotidien, support, workflows en plusieurs étapes. À prendre en cas de doute |
| T3 Avancé | Opus 5.5 | Recherche approfondie et raisonnement complexe, surtout en échange en direct où l'on veut des réponses rapides. À essayer quand Sonnet peine |
| T4 Frontier | Fable 5.1 | Plus gros projets, tâches longues en plusieurs étapes, sources denses, exactitude maximale. On décrit le résultat voulu et le modèle planifie. À essayer quand Opus peine |

Les quatre modèles sont inclus dans le plan Pro (le plan gratuit n'a que Haiku et Sonnet).

## Consignes d'usage

- Choisir le modèle le plus léger qui fait le travail, pour ménager la limite d'usage.
- Le modèle se change dans la conversation, sans perdre le fil.
- Pour un projet lourd, décrire le résultat attendu plutôt que chaque étape (surtout avec T4).

## Effort

Réglage « Effort » disponible dans l'application : garder le défaut pour la plupart des tâches, baisser pour la vitesse, monter seulement pour les problèmes les plus durs.

## Hors périmètre

Prix par token, identifiants d'API et choix de modèle côté API : prévoir un profil séparé (`cl-api-models-routing`). Ce profil ne dit rien sur les autres fournisseurs.

---
name: model-picker
description: Classe une tâche sur une grille de paliers (T1 à T4) indépendante de tout outil, puis la traduit en modèle via un profil de routage. À utiliser pour choisir un modèle LLM selon la tâche.
---

# Model picker

Cette skill ne connaît aucun outil, fournisseur ni modèle précis. Elle classe une tâche sur des paliers abstraits (T1 à T4) et un niveau d'effort. La traduction en modèle réel vient d'un profil de routage séparé.

## Étape 1 : classer la tâche

Note la tâche sur 5 critères :

1. **Complexité** : simple (extraire, trier, reformater, résumer court) / moyenne (rédiger, coder une fonction, analyser) / élevée (raisonnement multi-étapes, planification, refonte, recherche)
2. **Horizon** : réponse unique / quelques étapes / session longue ou autonome
3. **Contrainte de vitesse ou de volume** : aucune / modérée / forte (temps réel ou gros volume)
4. **Matière à traiter** : courte / longue / dense ou multi-sources
5. **Enjeu** : brouillon jetable / usage normal / livrable final ou erreur coûteuse

## Étape 2 : choisir le palier

- **T1 Léger** : simple, vitesse ou volume prioritaires, enjeu faible (recherche rapide, catégorisation, extraction, résumé court).
- **T2 Standard** : usage courant (rédaction, code, analyse du quotidien, workflows en plusieurs étapes). Palier par défaut en cas de doute.
- **T3 Avancé** : complexité élevée, raisonnement approfondi, recherche, échanges en direct sur un sujet difficile, ou T2 qui échoue.
- **T4 Frontier** : horizon long, matière dense, exactitude critique, grands projets, ou T3 qui échoue.

Règles :
- Prendre le palier le plus bas qui répond au besoin (économie de quota et de temps).
- Un seul critère extrême (forte vitesse, ou enjeu critique) peut déplacer le palier d'un cran. Deux critères en tension : le dire et laisser l'utilisateur trancher.
- Escalade seulement après un essai insuffisant, pas par précaution.

## Étape 3 : effort

- **Bas** : réponse rapide, tâche simple.
- **Défaut** : la plupart des cas.
- **Élevé** : seulement pour les problèmes les plus durs.

On préfère souvent changer l'effort avant de changer de palier, si le profil l'autorise.

## Étape 4 : traduire avec le profil de routage

Un profil de routage est une skill nommée `<contexte>-models-routing` qui contient : la table palier → modèle disponible, les consignes d'usage de l'outil, les contraintes (plan, quotas), les réglages d'effort possibles, la source et la date. Utilise le profil que l'utilisateur indique ; par défaut `cl-pro-models-routing` s'il est disponible. S'il n'y a aucun profil, donne uniquement le palier et l'effort abstraits et dis qu'aucun profil n'est chargé.

Si le profil est daté de plus de quelques mois, ou si l'utilisateur cite un modèle absent du profil, vérifie la source en ligne avant de répondre. Ne réponds jamais « je ne sais pas » sans avoir cherché.

## Format de réponse

- **Palier et effort** : une ligne (ex. T2, effort défaut), puis le modèle du profil.
- **Pourquoi** : 2 à 3 phrases reliées aux critères.
- **Alternative** : palier au-dessus si ça échoue, en dessous si on veut plus rapide ou moins cher.
- **À tester** : un signe concret qui montre que le palier suffit ou non.

Si la tâche est trop vague, pose UNE question, sinon énonce l'hypothèse retenue.

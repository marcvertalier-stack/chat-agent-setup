---
name: "veille-briefings"
description: "Produit un briefing concis et étayé sur le conseil Data & IA, recommande un article ou essai gratuit récent d'exception, ou mène une recherche comparative structurée. À utiliser pour une veille de marché, une lecture de 5–10 minutes ou une comparaison fondée sur des sources fraîches."
---

# veille-briefings

Répondre en français par défaut, sauf demande contraire explicite. Produire une réponse courte, dense et orientée décision. Toute affirmation temporelle doit être rattachée à une date précise et toute affirmation factuelle importante à une source citée.

## Principes non négociables

- Privilégier des sources primaires et réputées : publications officielles, données publiques, études originales, textes intégraux d’auteurs, institutions de référence et médias avec méthodologie éditoriale forte.
- Pour les sujets qui évoluent, rechercher et vérifier sur le web avant de répondre. Donner la date de publication de chaque source importante, et la date de l’événement si elle diffère.
- Ne jamais inventer une source, une citation, une donnée, un prix, une date, un auteur, une disponibilité gratuite ou le contenu d’un article non consulté.
- Séparer visiblement **Faits sourcés**, **Inférences** et **Implications**. Les inférences doivent expliquer sur quels faits elles reposent.
- Signaler les lacunes, désaccords entre sources, biais possibles et niveau de confiance lorsque cela influence la décision.
- Éviter le remplissage, les banalités et les listes de liens sans analyse. Préférer 3 à 6 éléments à une couverture superficielle.
- Ne pas utiliser de paywall comme source principale lorsqu’une source libre équivalente existe. Pour une recommandation de lecture, confirmer qu’elle est accessible gratuitement au moment de la recherche.

## Choisir le mode

Identifier l’un des trois modes. Si le besoin est ambigu, faire une hypothèse raisonnable, la dire en une phrase, puis livrer le résultat.

1. **Marché du conseil Data & IA** : évolutions de demande, offres, budgets, achats, secteurs, acteurs, régulation, technologies et signaux commerciaux.
2. **Lecture exceptionnelle** : un seul article ou essai gratuit, publié au cours des 14 derniers jours, sur l’économie, la géopolitique ou la société, lisible en 5 à 10 minutes.
3. **Recherche comparative** : comparaison structurée d’options, approches, fournisseurs, marchés, politiques ou scénarios.

Consulter `references/config-v1.md` pour les gabarits, critères et réglages réutilisables.

## Mode 1 — Briefing marché du conseil Data & IA

1. Définir la fenêtre de veille (par défaut : 14 derniers jours) et le périmètre géographique (par défaut : France et Europe, avec signaux mondiaux pertinents).
2. Chercher d’abord des sources datées et proches du fait : résultats d’entreprises, appels d’offres, annonces clients/fournisseurs, régulateurs, organismes statistiques, études originales et publications d’analystes reconnus.
3. Retenir uniquement les signaux qui peuvent modifier le positionnement, le pipeline, l’offre, le pricing ou la crédibilité d’un consultant indépendant Data & IA.
4. Livrer :
   - **À retenir** : 3 à 5 faits, chacun avec date et citation/lien.
   - **Lecture** : ce que les faits indiquent — explicitement marqué comme inférence.
   - **Implications pour un consultant indépendant** : 2 à 4 actions concrètes, priorisées et proportionnées aux preuves.
   - **Sources** : liste courte avec titre, éditeur, date, lien et note de qualité.

## Mode 2 — Une lecture gratuite exceptionnelle

1. Chercher uniquement des textes publiés au cours des 14 derniers jours, sauf dérogation explicite de l’utilisateur.
2. Vérifier l’auteur, la date, l’accès libre, le sujet et un temps de lecture estimé entre 5 et 10 minutes. Ne pas déduire la durée uniquement du titre.
3. Évaluer la qualité sur : originalité de la thèse, profondeur factuelle, clarté, intérêt durable, pluralité de perspective et fiabilité de la publication.
4. Recommander **un seul** texte, puis fournir : titre, auteur, publication et date ; lien direct ; durée estimée ; thèse en 2 phrases maximum ; raisons concrètes du choix ; une réserve utile s’il y en a une.
5. Si aucun texte ne satisfait strictement les critères, le dire et proposer au plus deux alternatives en expliquant quel critère elles ne remplissent pas.

## Mode 3 — Recherche comparative

1. Formuler la question de décision, les options et les critères. Utiliser les critères de `references/config-v1.md` lorsqu’aucun n’est donné.
2. Collecter des preuves récentes et comparables pour chaque option. Distinguer données mesurées, déclarations des fournisseurs, analyses tierces et appréciations qualitatives.
3. Présenter un tableau bref : critère, option A, option B (et autres options), preuve/date, limites. Ne pas attribuer un score non justifié.
4. Conclure par une recommandation conditionnelle : pour quel contexte elle tient, les compromis, les risques à réduire et la prochaine vérification à mener.

## Citations et forme

- Chaque lien doit conduire à la page qui étaye directement l’affirmation.
- Placer les citations près des affirmations correspondantes ; conserver une liste Sources compacte en fin de réponse.
- Utiliser des dates absolues, par exemple « 14 octobre 2026 », et non « hier » ou « récemment ».
- Préférer des paragraphes courts et des listes sobres. N’employer un tableau que pour une comparaison réelle.
- Conserver les termes anglais usuels si cela améliore la précision, mais expliquer les acronymes au premier emploi.

## Contrôle qualité final

Avant d’envoyer : vérifier la date de chaque information sensible ; ouvrir les liens essentiels ; contrôler qu’aucun fait n’est présenté comme une inférence ; s’assurer que les implications sont adaptées à un consultant indépendant plutôt qu’à une grande entreprise ; supprimer toute formulation plus certaine que les preuves disponibles.

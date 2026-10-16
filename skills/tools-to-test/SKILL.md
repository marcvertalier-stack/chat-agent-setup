---
name: tools-to-test
description: Enregistre un outil à tester (problème à résoudre, source optionnelle) dans un Excel tenu à jour sur l'ordinateur de l'utilisateur, trié par problème. Déclenchable en une phrase.
---

# Outils à tester (Excel sur l'ordinateur de l'utilisateur)

Enregistre un outil que l'utilisateur veut tester plus tard dans `outils-a-tester.xlsx`, classé par problème à résoudre. Le fichier vit dans un dossier connecté de son ordinateur (pas Google Drive) : il est modifié sur place, l'utilisateur n'a jamais à le renvoyer.

## Quand l'utiliser

- « note cet outil à tester », « à tester : X », « ajoute X à ma liste d'outils », ou un nom d'outil / lien collé avec l'intention de le tester.
- Consultation : « qu'est-ce que j'ai à tester pour <problème> ? ».
- Suivi : « j'ai testé X, bof » met à jour la ligne existante (statut, notes).

## Structure du fichier

Onglet « Outils », colonnes dans cet ordre : Problème à résoudre | Outil | Description | Source | Statut | Date d'ajout | Notes.

- Statut : liste déroulante À tester (défaut) / En test / Adopté / Écarté.
- Date d'ajout : AAAA-MM-JJ.
- Onglet « Mode d'emploi » : rappel du principe et ligne d'exemple ; ne pas y écrire de données.
- Tri : « Problème à résoudre » puis date d'ajout.

## Procédure d'ajout

1. **Extraire** du message : outil, problème, source. Si le problème n'est pas dit, le déduire du contexte ; s'il reste vraiment ambigu, poser UNE question courte. Ne jamais bloquer pour la source.
2. **Sourcing (optionnel)** : garder le lien donné tel quel. Si l'utilisateur demande « avec sources », chercher la page officielle et 1 ou 2 références crédibles sur le web ; sinon pas de recherche.
3. **Accéder à l'ordinateur** : utiliser les outils du lien avec l'ordinateur (liste des dossiers connectés, puis recherche de `outils-a-tester.xlsx`). Si aucun outil de ce type n'est disponible ou si l'ordinateur est injoignable, ne pas travailler sur une copie en silence : dire que le dossier n'est pas connecté (ouvrir la conversation dans l'application de bureau, lier l'ordinateur, ajouter le dossier), et proposer d'ajouter la ligne dans une copie de la session en prévenant qu'elle ne sera pas dans le fichier de l'utilisateur.
4. **Fichier absent** dans le dossier : le créer avec la structure ci-dessus, dans le dossier connecté, et le dire.
5. **Doublons** : si l'outil est déjà listé, le signaler et proposer de mettre à jour la ligne.
6. **Modifier sur place** avec openpyxl, de préférence via un shell sur l'ordinateur ; sinon rapatrier le fichier, le modifier, puis le réécrire au même endroit. Conserver police Arial, listes déroulantes et filtres. Réutiliser exactement les intitulés de problème existants, ajouter la ligne, retrier.
7. **Confirmer** en une ligne : outil, problème, statut, et où est le fichier. Ne renvoyer le fichier dans le chat que si l'utilisateur le demande.

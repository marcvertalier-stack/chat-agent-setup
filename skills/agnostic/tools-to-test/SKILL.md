---
name: tools-to-test
description: Enregistre un outil à tester (problème à résoudre, source optionnelle) dans un fichier de suivi trié par problème. Déclenchable en une phrase.
---

# Outils à tester

Enregistre un outil que l'utilisateur veut tester plus tard dans un fichier de suivi, classé par problème à résoudre. Le fichier est modifié sur place : l'utilisateur n'a jamais à le renvoyer.

## Quand l'utiliser

- « note cet outil à tester », « à tester : X », « ajoute X à ma liste d'outils », ou un nom d'outil / lien collé avec l'intention de le tester.
- Consultation : « qu'est-ce que j'ai à tester pour <problème> ? ».
- Suivi : « j'ai testé X, bof » met à jour la ligne existante (statut, notes).

## Le fichier de suivi

Nom par défaut : `outils-a-tester.xlsx`. Emplacement : le dossier de suivi défini par l'utilisateur ou par la configuration de l'agent ; à défaut, le dossier de travail courant. Si aucun emplacement n'est connu, le demander une fois.

Format préféré : tableur Excel. Si l'agent ne peut pas écrire de .xlsx, utiliser `outils-a-tester.csv` (UTF-8, séparateur virgule, mêmes colonnes) et le dire.

Une ligne d'en-têtes, puis une ligne par outil. Colonnes, dans cet ordre :

| Colonne | Contenu |
|---|---|
| Problème à résoudre | Le besoin que l'outil doit adresser (clé de tri) |
| Outil | Nom de l'outil |
| Description | Une phrase sur ce que fait l'outil |
| Source | URL ou référence d'où vient l'outil (optionnel) |
| Statut | À tester (défaut) / En test / Adopté / Écarté |
| Date d'ajout | AAAA-MM-JJ |
| Notes | Résultats de test, remarques (vide à l'ajout) |

Tri : « Problème à résoudre », puis date d'ajout. En Excel, si possible : liste déroulante sur Statut, filtres sur l'en-tête, en-tête figé.

## Procédure d'ajout

1. **Extraire** du message : outil, problème, source. Si le problème n'est pas dit, le déduire du contexte ; s'il reste vraiment ambigu, poser UNE question courte. Ne jamais bloquer pour la source.
2. **Sourcing (optionnel)** : garder le lien donné tel quel. Si l'utilisateur demande « avec sources » et que l'agent peut chercher sur le web, trouver la page officielle de l'outil et 1 ou 2 références crédibles ; sinon, ne pas chercher.
3. **Trouver le fichier.** S'il est introuvable ou inaccessible, ne pas travailler sur une copie en silence : dire ce qui manque, et proposer d'ajouter la ligne dans une copie provisoire en précisant qu'elle ne sera pas dans le fichier de l'utilisateur. S'il n'existe pas encore, le créer avec la structure ci-dessus et le dire.
4. **Doublons** : si l'outil est déjà listé, le signaler et proposer de mettre à jour la ligne.
5. **Modifier sur place** : ajouter la ligne sans toucher aux autres, réutiliser exactement les intitulés de problème existants pour garder les outils d'un même problème groupés, puis retrier. Conserver la mise en forme du fichier.
6. **Confirmer** en une ligne : outil, problème, statut, et où est le fichier. Ne renvoyer le fichier que si l'utilisateur le demande.

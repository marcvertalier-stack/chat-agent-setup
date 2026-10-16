---
name: mem0-memory
description: Comment l'agent lit et écrit dans Mem0 : lecture du statut du projet au début, enregistrement du durable en fin de chat, conventions d'écriture.
---

# Mémoire Mem0

Règle toujours active, à donner à l'agent comme consigne permanente (voir le README du dépôt).

## Texte de la règle

```
## Mémoire Mem0
- Au début d'un chat qui reprend un projet, lis l'entrée type=status du projet (user_id=marc, app_id=nom du projet).
- En fin de chat, ou après une longue pause, vérifie s'il y a quelque chose de durable à enregistrer. Sinon, écris « Mem0 : rien à enregistrer ».
- Écriture : user_id=marc, infer=false, texte en anglais, metadata.agent=claude (ou le nom de l'outil qui écrit), app_id et metadata.project = nom du projet, plus un type (status, decision, preference, profile). Sans projet : pas d'app_id.
- Une seule entrée type=status par projet (état actuel + prochaine étape), mise à jour sur place avec update_memory après l'avoir cherchée.
- Une nouvelle entrée type=decision ou preference par décision ou préférence durable, jamais modifiée ; si elle change, ajoute une entrée qui dit laquelle elle remplace.
- N'enregistre que le durable et réutilisable, jamais de secrets, de mots de passe ni de numéros d'identité ou de paiement, et évite les doublons.
```

## Notes

- Remplace le hook Claude Code `mem0_resume_check.py` (retiré le 2026-10-16), qui rappelait ces consignes à la reprise d'un chat.
- Passive : c'est à l'agent de l'appliquer, rien ne force son exécution.
- Les conventions détaillées sont aussi dans Mem0 (entrée type=decision du 2026-10-13). Dans les outils qui ont leurs propres fichiers de règles (CLAUDE.md, règles Cursor), on peut ne mettre qu'une ligne de renvoi vers ces conventions au lieu de recopier la règle.

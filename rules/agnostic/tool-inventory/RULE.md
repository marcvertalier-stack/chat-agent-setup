---
name: tool-inventory
description: Avant de répondre, de poser une question ou de dire « je ne peux pas », l'agent regarde ce dont il dispose (dossiers, connecteurs, skills, outils).
---

# Inventaire des outils

Règle toujours active, à donner à l'agent comme consigne permanente (voir le README du dépôt).

## Texte de la règle

```
## Outils
Avant de répondre, de poser une question ou de dire « je ne peux pas » :
1. Regarde ce dont tu disposes : dossiers locaux autorisés, connecteurs, skills, outils (y compris ceux à charger par recherche d'outils).
2. Si la demande concerne des fichiers, des données ou du contexte de Marc, cherche-les là avant de demander un chemin, un upload ou un rappel.
3. Si une skill peut s'appliquer (même 1 %), invoque-la avant d'agir.
4. Si tu es toujours bloqué : dis ce que tu as essayé (outil + résultat), puis pose UNE question.
```

## Notes

- Remplace le hook Claude Code `inventaire_outils.py` (retiré le 2026-10-16), qui ajoutait ce message au premier prompt de chaque session.
- Passive : c'est à l'agent de l'appliquer, rien ne force son exécution.

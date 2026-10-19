# chat-agent-setup

Tout ce qui compose mon agent de chat : skills, règles, configuration et réglages. Ce dépôt remplace l'idée d'un dépôt séparé « chat-agent-skills ».

## Structure

- `skills/` : une skill par dossier (format Agent Skills : un `SKILL.md` avec `name` et `description`)
  - `agnostic/` : skills utilisables par n'importe quel agent, sans outil propre à Claude
    - `tools-to-test/` : enregistre un outil à tester dans un fichier de suivi (Excel, sinon CSV) trié par problème
    - `topic-split/` : découpe une conversation en sujets indépendants, avec un texte de passation par sujet
    - `feature-split/` : décide si un projet doit être découpé en features et produit la liste
    - `interview-me/` : interview une question à la fois pour trouver ce que l'utilisateur veut vraiment
    - `topic-dispatch/` : priorise les sujets issus de topic-split, puis conversation dédiée, tâche programmée ou backlog
    - `status-brief/` : brief « où en est-on » sur les chantiers en cours
    - `model-picker/` : classe une tâche sur des paliers T1 à T4 et la traduit en modèle via un profil de routage
    - `message-review/` : relecture d'un message avant envoi, distinguant objectif et efficacité, corrections linguistiques et tournures à retenir
  - `claude/` : skills qui s'appuient sur des fonctions de Claude (lien avec l'ordinateur, connecteurs, outils de l'application)
    - `cl-pro-models-routing/` : profil de routage de `model-picker` pour le chat avec abonnement Pro (modèles par palier, consignes, effort)
- `rules/` : une règle par dossier (un `RULE.md` avec `name` et `description`, même organisation que `skills/`). Une règle est une consigne permanente, toujours active, contrairement à une skill qui se charge à la demande.
  - `agnostic/` : règles utilisables par n'importe quel agent
    - `tool-inventory/` : regarder ce dont on dispose avant de répondre, de poser une question ou de dire « je ne peux pas »
    - `mem0-memory/` : lire et écrire dans Mem0 (statut du projet, enregistrement du durable, conventions d'écriture)
- `config/` : configuration de l'agent (mémoire Mem0, réglages)

## Donner les règles à Claude (claude.ai)

Les règles remplacent les hooks Claude Code, qui ne tournent que dans Claude Code. Dans claude.ai, rien ne se déclenche automatiquement : les règles sont des consignes que Claude lit au début de chaque chat.

1. Ouvrir les préférences personnelles du profil dans les réglages de claude.ai (le nom et l'emplacement exacts du menu varient selon le web et le mobile).
2. Coller le bloc « Texte de la règle » de chaque `RULE.md` : une règle après l'autre, dans le même champ.
3. Elles s'appliquent alors à tous les chats, projets compris. À ne mettre dans les instructions d'un projet que si une règle ne vaut que pour ce projet.

Ce dépôt est la source de vérité : après toute modification d'une règle, recoller le texte dans les préférences. Pour les autres outils, utiliser leur propre fichier de règles : `~/.claude/CLAUDE.md` pour Claude Code, les règles du projet pour Cursor.

## À trier

Ce qui relève de la config de l'agent dans `data-projects-utils` (hook Mem0, adaptations du plugin mem0 de Cursor) est à rapatrier ici ou à y laisser : décision à prendre.

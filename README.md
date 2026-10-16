# chat-agent-setup

Tout ce qui compose mon agent de chat : skills, configuration et réglages. Ce dépôt remplace l'idée d'un dépôt séparé « chat-agent-skills ».

## Structure

- `skills/` : une skill par dossier (format Agent Skills : un `SKILL.md` avec `name` et `description`)
  - `agnostic/` : skills utilisables par n'importe quel agent, sans outil propre à Claude
    - `tools-to-test/` : enregistre un outil à tester dans un fichier de suivi (Excel, sinon CSV) trié par problème
    - `model-picker/` : classe une tâche sur des paliers T1 à T4 et la traduit en modèle via un profil de routage
  - `claude/` : skills qui s'appuient sur des fonctions de Claude (lien avec l'ordinateur, connecteurs, outils de l'application)
    - `cl-pro-models-routing/` : profil de routage de `model-picker` pour le chat avec abonnement Pro (modèles par palier, consignes, effort)
  - `topic-split/` : à ajouter (découpe d'une conversation en sujets, avec texte de passation) ; dossier à choisir selon le contenu
- `config/` : configuration de l'agent (mémoire Mem0, réglages)

## À trier

Ce qui relève de la config de l'agent dans `data-projects-utils` (hook Mem0, adaptations du plugin mem0 de Cursor) est à rapatrier ici ou à y laisser : décision à prendre.

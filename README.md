# chat-agent-setup

Tout ce qui compose mon agent de chat : skills, configuration et réglages. Ce dépôt remplace l'idée d'un dépôt séparé « chat-agent-skills ».

## Structure

- `skills/` : une skill par dossier (format Agent Skills, un `SKILL.md` par dossier)
  - `tools-to-test/` : enregistre un outil à tester dans un Excel tenu à jour sur mon ordinateur
  - `topic-split/` : à ajouter (découpe d'une conversation en sujets, avec texte de passation)
- `config/` : configuration de l'agent (mémoire Mem0, réglages)

## À trier

Ce qui relève de la config de l'agent dans `data-projects-utils` (hook Mem0, adaptations du plugin mem0 de Cursor) est à rapatrier ici ou à y laisser : décision à prendre.

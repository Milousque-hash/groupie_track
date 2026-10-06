# ADR 002 — Convention de nommage des branches

## Statut
Accepté

## Contexte
En appliquant la règle d'or du TP (jamais de commit direct sur `main`, tout passe par une
branche dédiée puis une Pull Request), l'équipe avait besoin d'une convention de nommage de
branches commune, définie dès l'atelier 1 et utilisée pour toutes les branches depuis (voir
`JOURNAL-TP.md` et la page Wiki "Circulation de l'information").

## Décision
Préfixer chaque branche par son type, suivi d'une courte description en kebab-case :

- `fix/...` — correction de bug (ex. `fix/port-dans-readme`)
- `docs/...` — documentation (ex. `docs/readme`, `docs/adr`)
- `feat/...` — nouvelle fonctionnalité ou amélioration (ex. `feat/ajoute-gitignore`)

## Conséquences

**Positives :**
- L'historique Git et la liste des branches/PR sont immédiatement lisibles : on sait ce que
  contient une branche rien qu'à son nom, sans ouvrir la PR.
- Facilite le tri visuel dans GitHub (branches groupées par préfixe).

**Négatives :**
- Convention à rappeler/appliquer manuellement (pas de contrôle automatique type hook Git qui
  rejette un nom de branche non conforme) ; une erreur de préfixe reste possible.

**Alternative écartée :** ne pas imposer de convention et laisser des noms de branche libres —
plus rapide à court terme, mais rend l'historique illisible dès que le nombre de branches
augmente.

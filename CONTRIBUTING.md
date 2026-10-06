# Contribuer à Groupie Tracker

## Règle d'or

On ne travaille jamais directement sur `main`. Chaque tâche vit dans sa propre branche, et
rejoint `main` uniquement via une Pull Request relue.

## Workflow

```bash
git checkout main
git pull                          # récupérer les derniers changements
git checkout -b <type>/<description-courte>

# ... faire les changements ...

git add .
git commit -m "<type>: message clair et au présent"
git push origin <type>/<description-courte>
```

Puis sur GitHub : ouvrir une Pull Request, se faire relire, merger, supprimer la branche.

## Convention de nommage des branches

- `fix/...` — correction de bug
- `docs/...` — documentation
- `feat/...` — nouvelle fonctionnalité / amélioration

## Format des issues

```markdown
## Contexte
## Comportement observé
## Comportement attendu
## Steps to reproduce
## Impact / priorité
```

Chaque issue reçoit un label (`bug`, `documentation` ou `enhancement`) et un assigné.

## Format des Pull Requests

```markdown
## Contexte
## Changements
## Impact

Closes #X
```

Toute PR doit recevoir au moins une review (commentaires constructifs + verdict) avant d'être
mergée.

## Décisions techniques

Les choix d'architecture significatifs sont tracés dans [`docs/adr/`](docs/adr/) sous forme
d'ADR (Architecture Decision Record).

# Groupie Tracker

Groupie Tracker est une application web écrite en Go qui affiche des informations sur des
artistes et groupes de musique (membres, date de création, premier album, dates et lieux de
concerts). Les données proviennent d'une API publique externe. L'utilisateur peut parcourir la
liste des artistes depuis la page d'accueil et filtrer par date de création ou nombre de
membres, puis consulter le détail d'un artiste (concerts, localisations).

## Installation

### Prérequis

- [Go](https://go.dev/dl/) version 1.25 ou supérieure
- Une connexion internet (l'application interroge une API externe au démarrage des requêtes)

### Commandes

```bash
git clone https://github.com/Milousque-hash/groupie_track.git
cd groupie_track
go run main.go
```

> ⚠️ L'application doit être lancée **depuis la racine du projet** : les templates HTML
> (`templates/`) et les fichiers statiques (`static/`) sont chargés via des chemins relatifs.
> Lancer un binaire compilé depuis un autre dossier provoque une erreur (voir issue #1).

## Usage

Une fois le serveur démarré, il écoute sur le port `8080`.

| Route | Description |
|---|---|
| `http://localhost:8080/` | Page d'accueil — liste des artistes, filtres par date de création et nombre de membres |
| `http://localhost:8080/artist/{id}` | Page de détail d'un artiste (membres, dates et lieux de concerts) |

Aucun compte ni authentification n'est nécessaire, l'application est en lecture seule.

## Architecture

L'application est un serveur HTTP Go unique (`net/http`, sans framework), structuré en 3 couches :

- **`main.go`** — déclare les routes (`/`, `/artist/`, `/static/`) et démarre le serveur.
- **`handlers/`** — logique de chaque page (récupère les données via `api/`, applique les
  filtres, exécute les templates HTML).
- **`api/`** — client HTTP vers l'[API Groupie Trackers](https://groupietrackers.herokuapp.com/api)
  (artistes, lieux, dates, relations) et structures de données associées.
- **`templates/`** — vues HTML (`index.html`, `artist.html`, `error.html`).
- **`static/`** — fichiers CSS/JS servis tels quels.

```
Navigateur ──HTTP──> main.go (routes) ──> handlers/ ──> api/ ──HTTP──> API Groupie Trackers
                                             │
                                             └──> templates/ (rendu HTML)
```

Les décisions d'architecture importantes sont tracées dans [`docs/adr/`](docs/adr/).

## Contribution

Ce dépôt suit un workflow standard : jamais de commit direct sur `main`, tout passe par une
branche dédiée puis une Pull Request relue.

Convention de nommage des branches :

- `fix/...` — correction de bug
- `docs/...` — documentation
- `feat/...` — nouvelle fonctionnalité / amélioration

Étapes :

1. `git checkout -b <type>/<description-courte>`
2. Faire le changement, committer avec un message clair (`git commit -m "..."`)
3. `git push origin <branche>`
4. Ouvrir une Pull Request sur GitHub avec une description structurée (contexte / changements /
   impact) et la lier à une issue si applicable (`Closes #X`)
5. Obtenir une review (au moins un commentaire constructif) avant de merger

Voir le détail complet dans [`CONTRIBUTING.md`](CONTRIBUTING.md).

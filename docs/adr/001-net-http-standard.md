# ADR 001 — Utiliser le package `net/http` standard plutôt qu'un framework web

## Statut
Accepté

## Contexte
Le projet Groupie Tracker est une application web Go relativement simple : quelques routes
(`/`, `/artist/{id}`, fichiers statiques), pas d'authentification, pas de base de données
locale, les données proviennent d'une API externe (Groupie Trackers). Il fallait choisir entre
utiliser un framework web (Gin, Echo, Fiber, ...) ou le package standard `net/http` fourni par
Go. Cette décision est déjà présente dans le code (`main.go`) ; elle n'avait pas été tracée
jusqu'ici, cet ADR la documente a posteriori.

## Décision
Utiliser uniquement le package standard `net/http` de la bibliothèque Go, sans dépendance
externe à un framework web.

## Conséquences

**Positives :**
- Aucune dépendance externe à gérer (`go.mod` reste minimal, pas de version de framework à
  maintenir/mettre à jour).
- Code plus simple à comprendre pour quelqu'un qui découvre Go, sans connaître les conventions
  propres à un framework.
- Suffisant pour le nombre de routes actuel (3 routes).

**Négatives :**
- Le routage reste basique (`strings.TrimPrefix`, pas de routeur avec paramètres nommés), ce qui
  deviendrait vite limitant si le nombre de routes augmentait significativement.
- Pas de middleware intégré (logging, recovery sur panique, CORS...) : à réimplémenter à la main
  si besoin.

**Alternative écartée :** un framework comme Gin aurait apporté un routeur plus riche et des
middlewares prêts à l'emploi, mais représentait une dépendance et une complexité non justifiées
par la taille actuelle du projet.

Se projet permet avant de tout de mettre en place une Pipeline CI/CD avec Github Actions

## Pipeline CI/CD

Le workflow GitHub Actions `.github/workflows/test.yml` se lance sur les push vers
`main`, sur la création d’un tag Git et manuellement depuis l’onglet Actions.
Il vérifie la syntaxe PHP, installe les dépendances Composer et exécute PHPUnit
lorsqu’un `composer.json` est présent. Les tests nécessitent `phpunit/phpunit`
dans les dépendances de développement Composer.

Après les vérifications, l’image est construite avec le `Dockerfile` à la racine
et publiée sur GHCR : les push sur `main` utilisent le tag `dev`, tandis que les
tags Git publient l’image avec le nom du tag et l’environnement `production`.
L’image `main` utilise l’environnement `development`.

Pour recevoir les notifications de résultat dans Google Chat, ajoutez le secret
de dépôt `GOOGLE_CHAT_WEBHOOK_URL` avec l’URL du webhook entrant de votre espace.
Les notifications incluent la référence, le commit, l’auteur du déclenchement,
le statut et, en cas d’échec, l’étape concernée avec un lien vers les logs.
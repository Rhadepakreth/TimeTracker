# TimeTrack API

## Présentation

TimeTrack est une application permettant aux utilisateurs de suivre et d'analyser le temps passé sur leurs activités quotidiennes (travail, sport, lecture, etc.), dans un objectif d'auto-organisation et de bien-être.

Cette documentation présente l'API RESTful qui permet de gérer toutes les fonctionnalités de l'application TimeTrack.

## Fonctionnalités principales

- Authentification sécurisée des utilisateurs (inscription, connexion, déconnexion)
- Gestion des types d'activités (création, modification, suppression)
- Enregistrement des sessions d'activités (ex: "lecture", 45 min, aujourd'hui à 17h)
- Visualisation de l'historique des sessions (par jour, par activité, etc.)
- Statistiques sur le temps passé par activité (avec options de regroupement)
- Gestion des tags pour catégoriser les sessions
- Modification sécurisée du mot de passe utilisateur

## Documentation technique

La documentation complète de l'API est disponible au format OpenAPI/Swagger dans le fichier `openapi.yaml` à la racine du projet.

### Structure de l'API

L'API est organisée autour des ressources suivantes :

#### Authentification
- `POST /register` : Inscription d'un nouvel utilisateur
- `POST /login` : Connexion d'un utilisateur
- `POST /logout` : Déconnexion d'un utilisateur
- `POST /refresh-token` : Rafraîchissement du token d'authentification

#### Utilisateurs
- `GET /me` : Récupération des informations de l'utilisateur connecté
- `PUT /me` : Mise à jour des informations de l'utilisateur connecté
- `PUT /me/password` : Modification du mot de passe de l'utilisateur connecté

#### Types d'activités
- `GET /activity-types` : Récupération de tous les types d'activités de l'utilisateur
- `POST /activity-types` : Création d'un nouveau type d'activité
- `GET /activity-types/{activityTypeId}` : Récupération d'un type d'activité spécifique
- `PUT /activity-types/{activityTypeId}` : Mise à jour d'un type d'activité
- `DELETE /activity-types/{activityTypeId}` : Suppression d'un type d'activité

#### Sessions
- `GET /sessions` : Récupération de toutes les sessions de l'utilisateur (avec filtres optionnels)
- `POST /sessions` : Création d'une nouvelle session
- `GET /sessions/{sessionId}` : Récupération d'une session spécifique
- `PUT /sessions/{sessionId}` : Mise à jour d'une session
- `DELETE /sessions/{sessionId}` : Suppression d'une session
- `GET /sessions/{sessionId}/tags` : Récupération des tags associés à une session
- `POST /sessions/{sessionId}/tags` : Association de tags à une session

#### Statistiques
- `GET /statistics` : Récupération des statistiques sur les sessions de l'utilisateur (avec options de regroupement par jour, semaine, mois ou activité)

#### Tags
- `GET /tags` : Récupération de tous les tags de l'utilisateur
- `POST /tags` : Création d'un nouveau tag

## Sécurité

L'API utilise l'authentification JWT (JSON Web Token) pour sécuriser les endpoints. Tous les endpoints, à l'exception de `/register`, `/login` et `/refresh-token`, nécessitent un token d'authentification valide.

Chaque utilisateur ne peut accéder qu'à ses propres données. Des vérifications d'autorisation sont effectuées sur chaque endpoint pour garantir qu'un utilisateur ne peut pas accéder aux données d'un autre utilisateur.

## Utilisation

Pour utiliser l'API :

1. Créez un compte utilisateur via l'endpoint `/register`
2. Connectez-vous via l'endpoint `/login` pour obtenir un token JWT
3. Utilisez ce token dans l'en-tête `Authorization` de vos requêtes sous la forme `Bearer {token}`
4. Créez des types d'activités via l'endpoint `/activity-types`
5. Enregistrez des sessions via l'endpoint `/sessions`
6. Consultez vos statistiques via l'endpoint `/statistics`

## Développement

Cette API est conçue pour être utilisée par des applications mobiles et web. La documentation OpenAPI facilite l'intégration avec ces applications en fournissant une description complète des endpoints, des paramètres et des modèles de données.
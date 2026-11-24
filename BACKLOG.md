# Backlog Produit - Projet SI Java (ESIEE-IT)

## Acteurs
- Visiteur : non connecté
- Utilisateur : connecté
- Admin : supervision (bonus)

## Modules / Features
- A. Authentification & Profil
- B. Projets
- C. Tâches
- D. Recherche
- E. Administration

## User Stories
| ID | Module | User Story | Priorité | Estim (S/M/L) |
|----|--------|------------|----------|---------------|
| US-01 | Auth | En tant que visiteur, je veux créer un compte afin d'accéder à l'application | Must | M |
| US-02 | Auth | En tant qu'utilisateur, je veux me connecter afin de retrouver mes projets | Must | M |
| US-03 | Auth | En tant qu'utilisateur, je veux me déconnecter afin de sécuriser ma session | Should | S |
| US-04 | Auth | En tant qu'utilisateur, je veux modifier mon profil afin de garder mes informations à jour | Should | S |
| US-05 | Projets | En tant qu'utilisateur, je veux créer un projet afin d'organiser mon travail | Must | S |
| US-06 | Projets | En tant qu'utilisateur, je veux lister mes projets afin de retrouver ce que je dois faire | Must | S |
| US-07 | Projets | En tant qu'utilisateur, je veux modifier un projet afin de corriger ou mettre à jour ses informations | Must | S |
| US-08 | Projets | En tant qu'utilisateur, je veux supprimer un projet afin de retirer ceux qui ne servent plus | Should | S |
| US-09 | Tâches | En tant qu'utilisateur, je veux ajouter une tâche dans un projet afin de suivre ce qu'il reste à faire | Must | M |
| US-10 | Tâches | En tant qu'utilisateur, je veux changer le statut d'une tâche afin de suivre son avancement | Must | M |
| US-11 | Tâches | En tant qu'utilisateur, je veux modifier une tâche afin de corriger ou préciser son contenu | Should | S |
| US-12 | Tâches | En tant qu'utilisateur, je veux supprimer une tâche afin de retirer celles qui ne sont plus utiles | Should | S |
| US-13 | Recherche | En tant qu'utilisateur, je veux filtrer mes tâches par statut afin de voir ce qui reste à faire | Should | S |
| US-14 | Recherche | En tant qu'utilisateur, je veux rechercher une tâche par mot-clé afin de la retrouver rapidement | Nice | S |
| US-15 | Admin | En tant qu'admin, je veux lister tous les utilisateurs afin de superviser l'application | Nice | S |

## Critères d'acceptation

### US-01 - Inscription
- Given je suis sur l'inscription, When je saisis un email valide et un mot de passe d'au moins 8 caractères, Then le compte est créé (201) et la réponse ne contient pas le mot de passe.
- Given l'email existe déjà, When je m'inscris, Then j'obtiens une erreur "Email déjà utilisé" (409) et aucun compte n'est créé.
- Given un mot de passe de 5 caractères, When je m'inscris, Then j'obtiens "Le mot de passe doit contenir au moins 8 caractères" (400).
- Given un email mal formé, When je m'inscris, Then j'obtiens une erreur claire (400).

### US-02 - Connexion
- Given un compte existant, When j'envoie le bon email et le bon mot de passe, Then j'obtiens 200 et un token JWT dans la réponse JSON.
- Given un compte existant, When j'envoie un mauvais mot de passe, Then j'obtiens 401 avec un message JSON "Invalid credentials".
- Given un email inconnu, When je me connecte, Then j'obtiens 401 avec le même message que pour un mauvais mot de passe.
- Given un token valide, When j'appelle la liste de mes projets, Then j'obtiens 200.

### US-03 - Déconnexion
- Given je suis connecté, When je me déconnecte, Then j'obtiens une réponse de succès et mon token n'est plus utilisé par le client.
- Given je ne suis pas connecté, When je demande la déconnexion, Then j'obtiens 401.

### US-04 - Modifier mon profil
- Given je suis connecté, When j'envoie des informations valides, Then mon profil est mis à jour (200) et les nouvelles valeurs sont visibles à la consultation suivante.
- Given je suis connecté, When j'envoie un email déjà pris par un autre compte, Then j'obtiens 409 et mon profil ne change pas.
- Given je ne suis pas connecté, When je modifie un profil, Then j'obtiens 401.

### US-05 - Créer un projet
- Given je suis connecté, When j'envoie un nom de projet valide, Then le projet est créé (201), j'en suis le propriétaire et il apparaît dans ma liste.
- Given je suis connecté, When j'envoie un nom vide, Then j'obtiens 400 avec un message clair.
- Given je ne suis pas connecté, When je crée un projet, Then j'obtiens 401.

### US-06 - Lister mes projets
- Given je suis connecté et j'ai des projets, When je demande la liste, Then j'obtiens 200 avec uniquement mes projets.
- Given je suis connecté sans projet, When je demande la liste, Then j'obtiens 200 avec une liste vide.
- Given un autre utilisateur a des projets, When je demande ma liste, Then je ne vois aucun de ses projets.
- Given je ne suis pas connecté, When je demande la liste, Then j'obtiens 401.

### US-07 - Modifier un projet
- Given je suis propriétaire du projet, When j'envoie des données valides, Then la modification est enregistrée (200) et persistante.
- Given un projet qui n'existe pas, When je le modifie, Then j'obtiens 404.
- Given un projet qui appartient à un autre utilisateur, When je le modifie, Then j'obtiens 403.
- Given je suis propriétaire, When j'envoie un nom vide, Then j'obtiens 400.

### US-08 - Supprimer un projet
- Given je suis propriétaire du projet, When je le supprime, Then il n'apparaît plus dans ma liste (204).
- Given un projet qui n'existe pas, When je le supprime, Then j'obtiens 404.
- Given un projet qui appartient à un autre utilisateur, When je le supprime, Then j'obtiens 403 et le projet reste en place.

### US-09 - Ajouter une tâche
- Given je suis propriétaire d'un projet, When j'envoie un titre de tâche valide, Then la tâche est créée dans ce projet avec le statut initial (201).
- Given un projet qui n'existe pas, When j'y ajoute une tâche, Then j'obtiens 404.
- Given un projet qui appartient à un autre utilisateur, When j'y ajoute une tâche, Then j'obtiens 403.
- Given un titre vide, When j'ajoute une tâche, Then j'obtiens 400.

### US-10 - Changer le statut d'une tâche
- Given une tâche dont je suis propriétaire, When je demande une transition de statut autorisée, Then le statut est mis à jour (200).
- Given une tâche, When je demande une transition de statut non autorisée, Then elle est refusée avec une erreur claire (409) et le statut ne change pas.
- Given une tâche qui n'existe pas, When je change son statut, Then j'obtiens 404.
- Given une tâche d'un autre utilisateur, When je change son statut, Then j'obtiens 403.

### US-11 - Modifier une tâche
- Given une tâche dont je suis propriétaire, When j'envoie des données valides, Then la modification est enregistrée (200) et persistante.
- Given une tâche qui n'existe pas, When je la modifie, Then j'obtiens 404.
- Given une tâche d'un autre utilisateur, When je la modifie, Then j'obtiens 403.

### US-12 - Supprimer une tâche
- Given une tâche dont je suis propriétaire, When je la supprime, Then elle n'apparaît plus dans le projet (204).
- Given une tâche qui n'existe pas, When je la supprime, Then j'obtiens 404.
- Given une tâche d'un autre utilisateur, When je la supprime, Then j'obtiens 403 et elle reste en place.

### US-13 - Filtrer les tâches par statut
- Given j'ai des tâches avec différents statuts, When je filtre sur un statut, Then j'obtiens 200 avec uniquement les tâches de ce statut.
- Given aucune tâche n'a ce statut, When je filtre dessus, Then j'obtiens 200 avec une liste vide.
- Given un statut qui n'existe pas, When je filtre dessus, Then j'obtiens 400.

### US-14 - Rechercher une tâche par mot-clé
- Given j'ai des tâches dont le titre contient un mot, When je cherche ce mot, Then j'obtiens 200 avec les tâches correspondantes.
- Given aucun titre ne contient ce mot, When je le cherche, Then j'obtiens 200 avec une liste vide.
- Given un autre utilisateur a une tâche avec ce mot, When je le cherche, Then cette tâche n'apparaît pas dans mes résultats.

### US-15 - Lister tous les utilisateurs (admin)
- Given je suis connecté avec le rôle ADMIN, When je demande la liste des utilisateurs, Then j'obtiens 200 avec tous les comptes, sans leur mot de passe.
- Given je suis connecté avec le rôle USER, When je demande cette liste, Then j'obtiens 403.
- Given je ne suis pas connecté, When je demande cette liste, Then j'obtiens 401.

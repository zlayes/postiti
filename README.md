# Post-its

Bureau virtuel de post-its pour tablette Android, avec comptes, profils, thèmes, priorités, archives et un compagnon (Poulpo).

- Un seul fichier : `index.html`. Seule dépendance : `supabase-js` chargé depuis un CDN.
- Connexion obligatoire (email + mot de passe). Les post-its sont stockés dans Supabase et suivent le compte d'un appareil à l'autre.
- Un compte peut contenir plusieurs profils (Amira, etc.) ; chaque profil est un bureau séparé.
- Deadline optionnelle par post-it, avec compte à rebours dans l'en-tête (`J-3`, `H-12`, `En retard`).
- Les tâches terminées s'empilent à droite, groupées par thème et dépliables en accordéon.
- Chaque post-it se redimensionne par la poignée en bas à droite (170x150 à 760x760),
  et le bouton ⤢ le déploie en plein écran pour lire et écrire confortablement.
- Bureau de 3000 x 2000 px : on le déplace au doigt et on pince pour zoomer (40 % à 180 %).
  Le cadrage est mémorisé par profil et par appareil.

## Dev
Servir le dossier en HTTP (l'authentification ne marche pas en `file://`) :

    python -m http.server 8765

puis ouvrir http://127.0.0.1:8765/

## Backend
Projet Supabase `postiti` (région eu-west-3). Table `boards` : une ligne par profil
(`user_id`, `name`, `state` en jsonb), protégée par RLS — chacun ne voit que ses propres lignes.
L'URL du projet et la clé publiable sont dans `index.html` : c'est leur usage prévu,
la sécurité repose sur les règles RLS, pas sur le secret de la clé.

## Déploiement
Push sur `main` → GitHub Pages publie automatiquement (Settings → Pages, source `main` / `/ (root)`).

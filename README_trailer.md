# Hébergement du Lecteur de Bande-Annonce

La politique de sécurité de YouTube bloque le lecteur vidéo dans des applications locales (`file://` ou `widget://`) sur les Smart TV, provoquant une erreur `153` due à l'absence de l'en-tête `Referer`. 

Pour contourner ce problème, vous devez héberger la page `trailer.html` sur une adresse web sécurisée (HTTPS) puis configurer l'application pour l'utiliser.

## Marche à suivre (Gratuit avec GitHub Pages)

1. Connectez-vous à votre compte **GitHub**.
2. Créez un nouveau dépôt public (ex: `tv-trailer-host`).
3. Importez le fichier `trailer.html` qui se trouve dans ce dossier à la racine de votre dépôt.
4. Allez dans les **Settings** (Paramètres) du dépôt.
5. Dans le menu à gauche, cliquez sur **Pages**.
6. Sous "Source", choisissez **Deploy from a branch**.
7. Sous "Branch", sélectionnez **main** (ou master), laissez le dossier `/ (root)`, et cliquez sur **Save**.
8. Attendez 1 à 2 minutes. GitHub affichera le lien en haut de la page (ex: `https://votre-pseudo.github.io/tv-trailer-host/`).

## Testez l'URL

Testez l'URL dans votre navigateur web :
`https://votre-pseudo.github.io/tv-trailer-host/trailer.html?v=dQw4w9WgXcQ`

La vidéo devrait démarrer automatiquement.

## Configurer l'application Tyzen Streamer

Une fois votre lien testé et validé, ouvrez le fichier `src/lib/trailerEmbedPlayer.ts` de votre projet et remplacez l'URL `PLACEHOLDER` par votre vraie adresse :

```ts
// Dans src/lib/trailerEmbedPlayer.ts (Ligne 7)
let embedBase = 'https://votre-pseudo.github.io/tv-trailer-host/trailer.html';
```

## Mise à jour de config.xml

Dans le fichier `public/config.xml` (ou à la racine, selon votre structure), assurez-vous d'autoriser l'accès à votre domaine :

```xml
<access origin="https://votre-pseudo.github.io" subdomains="false"></access>
<access origin="https://www.youtube.com" subdomains="true"></access>
<access origin="https://api.themoviedb.org" subdomains="true"></access>
```

S'il y a une règle CSP (`<tizen:content-security-policy>`), ajoutez votre domaine à `frame-src`.

# Mesure le temps — DELF/DALF

Application web (PWA) de chronomètres et comptes à rebours pour les épreuves orales DELF/DALF.
Installable sur mobile et utilisable hors ligne.

## Contenu

```
index.html          page unique de l'application
manifest.json       métadonnées PWA
sw.js               service worker (cache hors ligne)
icon.svg            icône vectorielle
icon-192.png        icône 192×192
icon-512.png        icône 512×512
maskable-512.png    icône adaptative (Android)
favicon-32.png      favicon
```

Tous les chemins sont relatifs : l'app fonctionne aussi bien à la racine d'un domaine que dans un sous-dossier GitHub Pages.

## Publier sur GitHub Pages

1. Créer un dépôt GitHub (ex. `mesure-le-temps`) et y placer tous les fichiers ci-dessus à la racine.
2. `Settings` → `Pages` → `Build and deployment` → Source : **Deploy from a branch**, branche `main`, dossier `/ (root)`, puis `Save`.
3. Après quelques minutes, l'app est disponible sur `https://<utilisateur>.github.io/mesure-le-temps/`.
4. Sur mobile (Chrome/Android), ouvrir l'URL puis « Ajouter à l'écran d'accueil » pour l'installer.

En ligne de commande :

```bash
git init
git add .
git commit -m "Mesure le temps — PWA DELF/DALF"
git branch -M main
git remote add origin https://github.com/<utilisateur>/mesure-le-temps.git
git push -u origin main
```

## Mise à jour

Après modification d'`index.html` ou des assets, incrémenter la version du cache dans `sw.js`
(`const CACHE = 'mesure-le-temps-v2';`) pour forcer le rafraîchissement chez les utilisateurs.

## Notes

- Vibrations et maintien de l'écran allumé : fonctionnent sur mobile (Android) ; ignorés silencieusement ailleurs.
- Niveaux disponibles : A2, B1, B2. C1 reste à configurer.

## Appli Android (APK)

L'APK (Capacitor) charge la version en ligne de l'appli : les mises à jour du site arrivent sans réinstaller.
Il ajoute le vibreur natif, les notifications vers la montre et l'écran toujours allumé.

- Construction automatique par GitHub Actions (`.github/workflows/apk.yml`) à chaque modification de `android/`, `app-shell/`, `package*.json` ou `capacitor.config.json`.
- Signature : secrets `ANDROID_KEYSTORE_BASE64` et `ANDROID_KEYSTORE_PASSWORD` (Settings › Secrets and variables › Actions). Ne jamais changer la clé, sinon l'APK ne s'installe plus par-dessus.
- Installation : page **Releases** › dernier `.apk` › ouvrir sur le téléphone › autoriser l'installation.

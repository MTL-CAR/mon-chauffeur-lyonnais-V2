# Mon Chauffeur Lyonnais — site vitrine (SASU MTL CAR)

Site statique bilingue (FR / EN), sans CMS ni dépendance, prêt pour GitHub Pages.

## Arborescence

```
/
├── index.html               Accueil FR
├── reservation.html         Tunnel de réservation FR
├── mentions-legales.html    Mentions légales, CGV, confidentialité (FR)
├── 404.html                 Page introuvable (bilingue)
├── en/
│   ├── index.html           Accueil EN
│   ├── booking.html         Tunnel de réservation EN
│   └── legal-notice.html    Mentions légales EN
├── assets/
│   ├── css/style.css        Toute la charte (variables en tête de fichier)
│   ├── js/site.js           Menu mobile
│   ├── js/booking.js        Tunnel en 4 étapes, bilingue, prix, envoi
│   ├── img/                 favicon.svg + photos à déposer
│   └── fonts/               polices auto-hébergées (à déposer)
├── robots.txt
├── sitemap.xml
└── .nojekyll
```

## 1. Éléments à compléter (rechercher et remplacer)

| Repère | Remplacer par | Fichiers |
|---|---|---|
| `www.votre-domaine.fr` | votre nom de domaine | toutes les pages, robots.txt, sitemap.xml |
| `+33XXXXXXXXX` | téléphone au format international (ex. +33612345678) | pages HTML |
| `33XXXXXXXXX` | même numéro sans le + (liens WhatsApp) | pages HTML, booking.js |
| `[TÉLÉPHONE]` / `[PHONE]` | téléphone affiché (ex. 06 12 34 56 78) | pages HTML |
| `[E-MAIL]` | adresse e-mail de contact | pages HTML, booking.js |
| `[NUMÉRO]` / `[NUMBER]` | n° d'inscription au registre VTC | pieds de page, mentions |
| `[PRIX]` / `[PRICE]` | tarifs Eurexpo et mises à disposition | accueils, réservations, booking.js (`CONFIG`) |
| `[X]` | durée minimale de la mise à disposition horaire | accueils |
| `VOTRE_ID` | identifiant Formspree (étape 3) | reservation.html, en/booking.html |
| `[CAPITAL]`, `[ASSUREUR]`, `[À COMPLÉTER]`… | informations légales | mentions-legales.html, en/legal-notice.html |

Les tarifs utilisés par le tunnel se règlent en tête de `assets/js/booking.js`, dans l'objet `CONFIG`.

## 2. Photos

Déposez vos photos dans `assets/img/` (JPEG ou WebP, 1600 px de large maximum, moins de 300 Ko chacune), puis décommentez les balises `<img>` prévues dans chaque emplacement « PHOTO ». Ajoutez aussi `og-image.jpg` (1200 × 630) pour les partages sur les réseaux sociaux.

## 3. Réception des réservations

GitHub Pages n'exécute aucun code serveur. Le formulaire est donc relayé par un service tiers :

1. créez un formulaire gratuit sur formspree.io (ou Web3Forms) avec votre e-mail ;
2. remplacez `VOTRE_ID` dans l'attribut `action` des deux pages de réservation ;
3. chaque demande arrive alors par e-mail, avec un récapitulatif complet (champ `resume`).

Tant que `VOTRE_ID` n'est pas remplacé, le tunnel fonctionne quand même : à la dernière étape, le client envoie son récapitulatif pré-rédigé par WhatsApp ou par e-mail.

**Paiement en ligne** : créez des liens de paiement Stripe (Payment Links) par forfait et collez-les dans `CONFIG.liensPaiement`. Le bouton « Régler en ligne » apparaît alors sur l'écran de confirmation.

## 4. Polices auto-hébergées (RGPD)

Le site charge provisoirement Marcellus et Figtree depuis Google Fonts. Pour ne plus transmettre l'adresse IP des visiteurs à Google :

1. téléchargez les fichiers `.woff2` sur gwfh.mranftl.com (Marcellus 400, Figtree 400 et 500, sous-ensemble latin) ;
2. déposez-les dans `assets/fonts/` avec les noms indiqués dans `style.css` ;
3. décommentez le bloc `@font-face` en tête de `style.css` ;
4. supprimez les trois lignes Google Fonts (`preconnect` et `stylesheet`) du `<head>` de chaque page.

## 5. Mise en ligne sur GitHub Pages

1. Créez un dépôt (par exemple `site-mon-chauffeur-lyonnais`) et déposez-y tout le contenu de ce dossier à la racine.
2. Ouvrez Settings › Pages › Source : branche `main`, dossier `/ (root)`.
3. Nom de domaine : dans Settings › Pages › Custom domain, saisissez `www.votre-domaine.fr` (un fichier `CNAME` est créé automatiquement). Chez votre registraire, ajoutez un enregistrement `CNAME www → <utilisateur>.github.io` et les quatre enregistrements `A` de GitHub pour le domaine nu.
4. Cochez « Enforce HTTPS » une fois le certificat émis.

La page `404.html` utilise des chemins absolus (`/assets/…`) : elle s'affiche correctement avec un nom de domaine personnalisé.

## 6. Avant la mise en ligne

- Faire relire les CGV et les mentions légales par un professionnel du droit.
- Vérifier les tarifs et les conditions dans `CONFIG`.
- Tester une réservation complète en FR et en EN, sur mobile et sur ordinateur.
- Créer la fiche Google Business Profile et y relier le bouton « Laisser un avis ».

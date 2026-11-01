# Site personnel de Youssef Mir

Site d’une page, en HTML et CSS, sans framework ni étape de build. Il se publie tel quel sur GitHub Pages.

## Contenu du dépôt

```
index.html              la page (tout le contenu est ici)
404.html                page « introuvable »
assets/css/style.css    la mise en forme
assets/fonts/           polices auto-hébergées (licence SIL OFL)
assets/img/og.png       image affichée quand le lien est partagé (LinkedIn, Slack…)
favicon.svg, favicon-32.png, apple-touch-icon.png
robots.txt, sitemap.xml référencement
.nojekyll               demande à GitHub Pages de servir les fichiers sans transformation
```

## Voir le site en local

```bash
python3 -m http.server 8000
```

Puis ouvrir http://localhost:8000.

## Modifier le contenu

Tout se passe dans `index.html`. Chaque section est repérée par un commentaire (`Couverture`, `Parcours`, `Projets`, `Compétences`, `Publications`, `Contact`) :

- **ajouter un poste** : copier un bloc `<li class="entry">…</li>` dans la section Parcours ;
- **ajouter un projet** : copier un bloc `<li class="project">…</li>` dans la section Projets ;
- **ajouter une compétence** : copier une ligne `<tr role="row">…</tr>` du tableau ;
- **ajouter un e-mail** : un modèle est en commentaire dans la section Contact ;
- penser à mettre à jour la date « mis à jour en … » en bas de page.

Typographie française : `&nbsp;` avant les deux-points, `&#8239;` (espace fine) avant `?`, `!` et `;`.

## Publier sur GitHub Pages

1. Fusionner la branche du site dans `main`.
2. Renommer le dépôt en `youssefmir.github.io` (Settings → General → Repository name). Le site sera alors à l’adresse https://youssefmir.github.io/.
3. Dans Settings → Pages → Build and deployment, choisir **Deploy from a branch**, branche `main`, dossier `/ (root)`.

Si le dépôt garde un autre nom (par exemple `mon-site`), le site sera publié sur `https://youssefmir.github.io/mon-site/`. Il faut alors :

- remplacer `https://youssefmir.github.io/` par la nouvelle adresse dans `index.html` (balises `canonical`, `og:url`, `og:image` et bloc JSON-LD), `robots.txt` et `sitemap.xml` ;
- dans `404.html`, préfixer les chemins absolus (`/assets/…`, `/favicon.svg`, `/`) par `/mon-site`.

## Choix de conception

- **Typographie** : Newsreader (texte et titres, avec taille optique) et IBM Plex Mono (dates, étiquettes, outils). Les polices sont servies depuis le site lui-même : aucun appel à Google Fonts.
- **Couleurs** : papier, encre et une seule couleur d’accent, le vermillon. Le mode sombre suit le réglage du système. Les textes respectent un contraste d’au moins 4,5:1.
- **Impression** : le bouton « Version PDF » ouvre l’impression du navigateur ; la page est mise en forme comme un CV sur fond blanc. Elle utilise des versions statiques de Newsreader (`newsreader-print-*.woff2`), chargées seulement à ce moment-là : dans les PDF, Chrome déforme certaines lettres des polices variables, comme le crochet du « f ».
- **Sobriété** : pas de traceur, pas de cookie, pas de dépendance JavaScript (quelques lignes seulement, pour le bouton d’impression).

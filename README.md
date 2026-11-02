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

Tout se passe dans `index.html`. Chaque section est repérée par un commentaire (`Couverture`, `Parcours`, `Projets`, `Publications`, `Contact`) :

- **ajouter un poste** : copier un bloc `<li class="entry">…</li>` dans la section Parcours ;
- **ajouter un projet** : copier un bloc `<article class="project project-featured" data-project>…</article>` (à la une) ou `<li class="project" data-project>…</li>` (autres projets) dans la section Projets. L’attribut `data-project` rend le projet filtrable ;
- **relier un projet à une compétence** : ajouter une ligne `<li><button type="button" class="skill" data-skill="…">…</button></li>` dans le bloc « Compétences » du projet. Le filtre en tête de la section Projets se construit tout seul à partir de ces blocs : réutiliser le même `data-skill` pour regrouper des projets sous une même compétence ;
- **capture d’un projet** : image WebP de 1440 × 900 dans `assets/img/projets/`, avec une variante `-sombre` pour le mode sombre ;
- **ajouter un e-mail** : un modèle est en commentaire dans la section Contact ;
- penser à mettre à jour la date « mis à jour en … » en bas de page.

Typographie française : `&nbsp;` avant les deux-points, `&#8239;` (espace fine) avant `?`, `!` et `;`.

## Publication

Le site est publié sur https://youssefmir.github.io/.

Chaque push sur `main` le met en ligne automatiquement, en une minute environ, grâce au workflow `.github/workflows/deploy.yml`. Il n’y a pas de build : le workflow publie les fichiers du dépôt tels quels (sans `README.md` ni `.github/`). Le suivi des déploiements est dans l’onglet **Actions**.

Réglage correspondant : Settings → Pages → Build and deployment → Source : **GitHub Actions**.

L’adresse du site apparaît dans `index.html` (balises `canonical`, `og:url`, `og:image` et bloc JSON-LD), `robots.txt` et `sitemap.xml` : à mettre à jour en cas de nom de domaine personnalisé.

## Choix de conception

- **Typographie** : Newsreader (texte et titres, avec taille optique) et IBM Plex Mono (dates, étiquettes, outils). Les polices sont servies depuis le site lui-même : aucun appel à Google Fonts.
- **Couleurs** : papier, encre et une seule couleur d’accent, le vermillon. Le mode sombre suit le réglage du système. Les textes respectent un contraste d’au moins 4,5:1.
- **Impression** : le bouton « Version PDF » ouvre l’impression du navigateur ; la page est mise en forme comme un CV sur fond blanc. Elle utilise des versions statiques de Newsreader (`newsreader-print-*.woff2`), chargées seulement à ce moment-là : dans les PDF, Chrome déforme certaines lettres des polices variables, comme le crochet du « f ».
- **Sobriété** : pas de traceur, pas de cookie, pas de dépendance JavaScript (quelques lignes seulement, pour le bouton d’impression).

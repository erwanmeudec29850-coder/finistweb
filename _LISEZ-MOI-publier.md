# finistweb.fr — comment publier (look « La Console »)

Site **statique** : que des fichiers HTML + un seul `style.css`. Pas de build, pas de React.
Tu déposes un fichier, tu pousses sur GitHub, c'est en ligne.

## Structure

```
index.html            → accueil
articles.html         → liste des articles (les cartes)
scripts.html          → liste des scripts (les cartes)
modele-article.html   → MODÈLE à copier pour un nouvel article
modele-script.html    → MODÈLE à copier pour un nouveau script
style.css             → tout le design « La Console » (un seul fichier)
fichiers/             → y mettre les .ps1 à télécharger (crée le dossier au besoin)
images/               → images éventuelles
CNAME, .nojekyll      → config GitHub Pages (ne pas toucher)
```

## Publier un ARTICLE

1. Copie `modele-article.html` → renomme en `article-mon-sujet.html`.
2. Remplis : `<title>`, la description, la catégorie (tag), le titre `h1`, l'accroche, la date, le corps.
   Briques dispo dans le modèle : `h2`, `h3`, `p`, `ul`, `ol`, `code`, fenêtre terminal, et 4 encadrés :
   - `callout-memo` (à retenir, fond sombre)
   - `callout-analogy` (l'image à garder)
   - `callout-tip` (le bon réflexe, vert)
   - `callout-warning` (attention, ambre)
3. Ouvre `articles.html`, et dans `<section>` ajoute une carte (le modèle est en commentaire dans le fichier) :

```html
<div class="grid-2">
  <a href="article-mon-sujet.html" class="card article-card">
    <span class="tag tag-signal brackets">diagnostic matériel</span>
    <h3>Titre de l'article</h3>
    <p>L'accroche.</p>
    <div class="card-foot">
      <span>15 mai 2026</span><span class="dot"></span><span>8 min</span>
      <span class="card-arrow"><i class="ph-bold ph-arrow-right"></i></span>
    </div>
  </a>
</div>
```

(Quand tu ajoutes la 1re carte, supprime le bloc `<div class="empty">`.)

## Publier un SCRIPT

1. Copie `modele-script.html` → `script-mon-outil.html`. Remplis-le.
2. Mets le `.ps1` téléchargeable dans `fichiers/`.
3. Ajoute une carte dans `scripts.html` (modèle en commentaire dans le fichier).

## Mettre en ligne

Depuis le dépôt git du site :

```powershell
git add -A
git commit -m "Ajout article mon-sujet"
git push
```

GitHub Pages redéploie tout seul (~1-2 min). Sur le site, **Ctrl+Shift+R** pour vider le cache.

---

## Prompt à coller dans ton projet Claude.ai (générateur d'articles)

> Remplace les anciennes instructions de mise en page par celles-ci. Le contenu rédactionnel ne change pas — seul le HTML produit change.

```
Tu génères des articles pour finistweb.fr, un site STATIQUE au design « La Console ».
Produis un fichier HTML complet, autonome, basé EXACTEMENT sur cette structure :

- <head> : title « <titre> — finistweb.fr », meta description, puis ces 4 <link> dans l'ordre :
  style.css, puis Phosphor regular, bold, fill (CDN jsdelivr @phosphor-icons/web@2.1.1).
- Une <nav class="nav"> identique à modele-article.html (logo ~/finistweb.fr, liens scripts/articles, CTA mailto).
- <article class="article read"> contenant :
  - <div class="breadcrumb"><a href="articles.html">~/articles</a> / <span>slug</span></div>
  - <header class="article-head"> : <span class="tag tag-signal brackets">CATÉGORIE</span>,
    <h1 class="article-title">, <p class="article-lead">, <div class="article-meta"> (date · durée).
  - <div class="article-body"> : le contenu. N'utilise QUE ces balises/classes :
    <p>, <h2>, <h3>, <ul>, <ol>, <li>, <strong>, <code>, et les encadrés :
      <div class="callout callout-memo"><div class="callout-label">// à retenir</div><p>…</p></div>
      <div class="callout callout-analogy"><div class="callout-label"><i class="ph-fill ph-lightbulb-filament"></i> l'image à garder</div><p>…</p></div>
      <div class="callout callout-tip"><div class="callout-label"><i class="ph-fill ph-check-circle"></i> le bon réflexe</div><p>…</p></div>
      <div class="callout callout-warning"><div class="callout-label"><i class="ph-fill ph-warning"></i> attention</div><p>…</p></div>
    Pour du code, une fenêtre terminal :
      <div class="term"><div class="term-bar"><div class="term-dots"><i></i><i></i><i></i></div>
      <span class="term-path">fichier.ps1</span><button class="term-action"><i class="ph ph-copy"></i> copy</button></div>
      <div class="term-body"><div class="term-nums"><div>1</div>…</div>
      <pre class="term-code">…lignes…</pre></div></div>
- Un <footer class="site-footer"> identique à modele-article.html.

Catégories (tag) possibles : tag-signal, tag-green, tag-amber, tag-neutral.
Ne mets AUCUN <style> inline ni police Fraunces : tout le style vient de style.css.
Donne aussi le bloc <a class="card article-card">…</a> à coller dans articles.html.
```

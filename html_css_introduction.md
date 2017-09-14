# HTML & CSS: Introduction

IAD 2017-2018 - Jérôme Coupé

## Introduction

Depuis [l'annonce par le W3C de la fin des travaux sur XHTML2 en 2009](http://www.w3.org/News/2009#entry-6601), HTML5 reste le seul candidat en lice pour une refonte du langage structurant du web. Le travail sur la spécification HTML5 a commencé en 2004 et est un effort conjoint du W3C et du WHATWG Group.

HTML5 est à la fois un enrichissement du "vocabulaire" du HTML, mais aussi une tentative de faire du HTML un langage du web d'aujourd'hui: sémantique, applicatif (à travers les divers API) et réellement intégrateur de divers médias (sons, vidéos, élément CANVAS, etc.).

HTML et CSS sont désormais des spécifications modulaire en évolution constante. Nous ne devrions donc plus voir d'autres grandes versions monolithiques de HTML ou de CSS mais simplement une évolution constante des différents modules dont ces spécifications sont composées.

De nombreuses ressources telles que [Mozilla Developer Network (MDN)](https://developer.mozilla.org/), [webplateform.org](http://www.webplatform.org/) et [HTML5 Rocks](http://www.html5rocks.com) sont disponibles si ces sujets vous intéressent.

Pour vérifier la compatibilité de votre code CSS / HTML avec les différents navigateurs, vous pouvez vous référer au site [caniuse.com](http://caniuse.com) (tables de support).

## HTML5

### Document minimal

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Example document</title>
  </head>
  <body>
    <p>Example paragraph</p>
  </body>
</html>
```

### Déclaration du type de document

Les divers navigateurs n’utilisent pas la déclaration de type de document (DTD) pour effectuer le rendu d’un document, la DTD permet néanmoins aux outils de validation que vous utilisez de savoir dans quelle syntaxe est écrit votre document, afin de pourvoir le valider.

La DTD HTML5 est en fait la plus petite suite de caractères permettant à un navigateur de gérer une page en mode "standard" et non en mode "quirks". Afin de garder une compatibilité avec un code plus ancien, les navigateurs ont mis en place ce que l’on nomme le [doctype switching](http://www.ericmeyeroncss.com/bonus/render-mode.html), une idée de Todd Fahrner. Le mode "quirks" leur permet de gérer et d’afficher un code ne se conformant pas aux standards.

### Encodage de caractères

Il convient d'ajouter une balise meta précisant l'encodage de caractère utilisé dans votre document. Dans la plupart des cas, [un encodage UTF-8 est votre meilleur choix](http://www.w3.org/TR/html5/the-meta-element.html%23charset).

```html
<meta charset="utf-8">
```

### Déclaration de la langue utilisée

L'élément racine d'un document doit impérativement être l'élément `<html>` et celui-ci doit avoir comme attribut une déclaration de la langue principale utilisée dans le document. Par exemple :

```html
<html lang="en">
```

### Bonnes pratiques

HTML est un langage assez pragmatique et qui "pardonne" beaucoup d'erreurs de syntaxe et de style. Néanmoins, il est important de suivre certaines règles. Lorsque vous débutez, valider votre code peut s'avérer intéressant pour détecter vos erreurs.

Outre cette validation, voici une série de bonnes pratiques qui rendront votre code plus lisible.

#### Bonne imbrication et fermeture des tags

Vos tags doivent être bien imbriqués. Les ouvertures et les fermetures de tags doivent se faire niveau par niveau ainsi que dans le bon ordre.

**Incorrect**

```html
<p>Lorem ipsum dolor sit amet, consectetur <a href="">adipisicing elit</a>.
```

```html
<p>Lorem ipsum dolor sit amet, consectetur <a href="">adipisicing elit</p></a>.
```

**Correct**

```html
<p>Lorem ipsum dolor sit amet, consectetur <a href="">adipisicing elit</a>.</p>
```

#### Utiliser des minuscules partout

Bien que des majuscules soient valides en HTML, votre code sera plus lisible si vous tags et attributs sont écrits en minuscules.

**Pas terrible**

```html
<P>Mon paragraphe contenant <A HREF="https://www.iad-arts.be">un lien hypertexte</A></P>
```

**Mieux**

```html
<p>Mon paragraphe contenant <a href="https://www.iad-arts.be">un lien hypertexte</a></p>
```

#### Toujours placer vos attributs entre guillemets

Encore une fois, HTML ne vous y oblige pas mais placer les valeurs de vos attributs entre guillemets augmente grandement la lisibilité de votre code HTML.

**Pas terrible**

```html
<p>Un paragraphe contenant <a href=https://www.iad-arts.be>un lien hypertexte</a></p>
```

**Mieux**

```html
<p>Un paragraphe contenant <a href="https://www.iad-arts.be">un lien hypertexte</a></p>
```

#### Gestion des caractères spéciaux dans les déclarations CSS et JavaScript

La meilleure solution consiste à placer tout votre code CSS ou de JavaScript dans des fichiers externes et pas dans votre fichier HTML.

#### Encodage des esperluettes "&" dans les URls

Le validateur HTML genèrera une erreur lorsque un caractère "&" n'est pas encodé dans une URL. Veillez donc à y remédier en encodant cette dernière.

Invalide:

```html
<a href="index.php?a=1&b=2">Latest News</a>
```

Valide:

```html
<a href="index.php?a=1&amp;b=2">Latest News</a>
```

### Document Object Model (DOM) Structure d’un document HTML

Les éléments composant un document HTML sont structurés de façon hiérarchisée. Ils s’emboîtent les uns dans les autres, structurant le document sur le modèle d’un arbre.

```html
<!DOCTYPE html>
<html lang="fr">
  <head>
    <meta charset="utf-8">
    <title>Titre du document</title>
  </head>
  <body>
    <nav class="mainnav" role="navigation">
      <ul>
        <li>item 1</li>
        <li>item 2</li>
        <li class="last listitem">item <em>3</em></li>
      </ul>
    </nav>
    <div class="content" role="maincontent">
      <h1>Titre niveau un</h1>
      <p>Lorem ipsum dolor sit amet.</p>
      <p class="last">Lorem <em>ipsum</em> dolor <em>sit</em> amet.</p>
    </div>
  </body>
</html>
```

Cette forme d’arbre et d’emboîtement hiérarchisé est parfaitement visible dans des outils tels que [Firebug](https://addons.mozilla.org/en-US/firefox/addon/firebug/) ou [la barre d’outils développeurs de firefox](https://addons.mozilla.org/en-US/firefox/addon/web-developer/) ou encore dans les developer tools disponibles dans tous les navigateurs modernes (Chrome, Safari, Firefox, Opera)

Familiarisez-vous avec ces outils, vous en aurez besoin lors de ce cours et durant toute votre carrière de développeur front-end.

*Exercice: créer un starter kit en HTML5, explorer les outils de développement dans Chrome, Safari ou Firefox*

### HTML5: Une sémantique améliorée

L’une des nouveautés de HTML5, c’est l’introduction de nouveaux éléments sémantiques permettant une qualification plus précise des divers éléments de votre document. Certains comme Luke Stevens [arguent que l'utilisation de de ces éléments est problématique pour diverses raisons](http://www.truthabouthtml5.com/). A vous de voir.

Nous ne présenterons pas l’ensemble de ces nouveaux éléments dans le cadre de ce cours mais nous vous présenterons les principaux. L'ensemble de ces nouveaux éléments et des renseignements sur leurs usages sont disponibles sur le site de [Mozilla Developer Network](https://developer.mozilla.org/fr/docs/Web/HTML/Element) ou dans [le glossaire rédigé pour vous par l'équipe de HTML5 Doctor](http://html5doctor.com/element-index/).

#### Nouveaux élements

##### `<nav>`

Cet élément est utilisé pour marquer les interfaces de navigation du site ou de la page. Il s’agit d’une section de la page contenant les liens utilisés pour la navigation. Tous les groupes de liens ne sont pas forcément des interfaces de navigation, seuls ces derniers peuvent être marqués à l’aide de l’élément `<nav>`.

##### `<article>`

Est utilisé pour marquer une partie d'un document, d'une page, d'un site qui fait sens prise indépendamment: un post sur un forum, un article de magazine ou de journal, un billet sur un blog, un commentaire soumis par un utilisateur ou n'importe quel autre élément de contenu indépendant.

Une bonne question à se poser pour l’utilisation d’article est: pourriez vous inclure ce contenu dans un flux RSS et ce contenu ferait-il sens? Si oui, il s’agit probablement d’un bon candidat.

##### `<section>`

Section générique d'un document ou d'une application. Section sert à marquer un groupement thématique de contenus, typiquement il comporte un `<header>` et parfois un `<footer>`. Exemples: les chapitres d'un livre, les sections d'une thèse, les différentes sections d'une page d'accueil: introduction, news, portfolio, information de contact, etc.

Attention à ne pas utiliser section en lieu et place de `<div>` ou `<article>`, par exemple pour séparer le contenu principal d'une page de son contenu secondaire. A part de rares exceptions, n'utilisez pas `<section>` si cet élément ne possède pas naturellement un titre. [Un article détaillé sur le sujet est disponible sur HTML5 Doctor](http://html5doctor.com/the-section-element/).

##### `<aside>`

Est utilisé pour marquer du contenu qui est lié de façon tangentielle au parent de l'élément <aside> et qui pourrait être comme faisant sens indépendamment du contenu de ce parent.

Le contexte est ici très important. Vous pouvez utiliser `<aside>` pour marquer une sidebar sur un site Internet. Les éléments de contenu ainsi marqués sont tangentiellement liés à la page ou au site. Lorsque `<aside>` est utilisé au sein d'un élément `<article>`, le contenu ainsi marqué est tangentiellement lié au contenu de cet article.

#### Document outline et sectioning elements

Notons ici que les éléments `acticle`, `section`, `nav` et `aside` sont des élements de sectioning, c’est à dire qu’ils créent une nouvelle section au sein du document.

A priori, la hiérarchie des titres recommence à zéro au sein de chacun des éléments de ce type. Il est néanmoins [conseillé par le W3C de garder une hiérarchie de titres classiques sans tenir compte de ces éléments](https://www.w3.org/TR/html5/sections.html#outlines), étant donné que l'algorithme d'outline n'est à ce jour implémenté dans aucun navigateur ou technologie d'assistance.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Document outline and sectioning elements</title>
  </head>
  <body>
    <h1>My great site</h1>
    <nav>
      <ul>
        <li><a href="fake.html">Nav item</a></li>
      </ul>
    </nav>
    <article>
      <h2>Article title</h2>
      <p>Article content.</p>
      <h3>Article sub-heading</h3>
      <p>More content.</p>
      <h4>Article sub-sub-heading</h4>
      <p>More content.</p>
    </article>
    <aside>
      <h2>Sidebar heading</h2>
      <p>content</p>
    </aside>
    <footer>
      <h2>Footer heading</h2>
      <p>Footer content.</p>
    </footer>
  </body>
</html>
```

##### `<main>`

L’élément `<main>` représente le contenu principal d’un document. Il ne peut être utilisé qu’une seule fois au sein d’un document HTML et ne peut jamais être le descendant de `<article>`, `<aside>`, `<footer>`, `<header>` or `<nav>`.

##### `<header>`

Typiquement utilisé pour contenir les métas informations (titre, logo, date de publication, etc) d’un document ou d’une partie d’un document. L'élément `<header>` peut être utilisé plusieurs fois dans le cadre d'un même document. Suivant le contexte dans lequel il est placé (`<body>`, `<article>`, `<section>`, etc.) il aura un statut différent.

##### `<footer>`

Typiquement utilisé pour contenir les métas informations (auteur, lien vers des documents liés) d’un document ou d’une partie de document. L'élément `<footer>` peut être utilisé plusieurs fois dans le cadre d'un même document. Suivant le contexte dans lequel il est placé (`<body>`, `<article>`, `<section>`, etc.) il aura un statut différent. Notons que les coordonnées de contact mentionnées dans un `<footer>` devraient êtres marqués à l'aide de l'élément `<address>`

##### `<time>`

Est utilisé pour marquer des données temporelles (dates, heures etc.) de façon à ce qu'elles soient lisibles et exploitables par des machines ou programmes. Un attribut datetime peut également être ajouté afin de préciser les choses si le textes marqué n'est pas une date grégorienne valide.

```html
<time datetime="2007-10-05">October 5</time>
<p>I usually have a snack at <time>16:00</time>.</p>
<p>posted on <time datetime="2009-04-12">12 April 2009</time> by Jérôme Coupé</p>
```

##### `<figure>` et `<figcaption>`

Est utilisé pour marquer du contenu qui pourrait être retiré du document sans que cela n'affecte le sens de ce dernier. Cet élément peut être utilisé pour marquer des images, des graphiques, des éléments de code qui sont mentionnés dans le document mais qui pourrait en être extraits (pour figurer dans une annexe ou en marge) sans nuire au sens de ce dernier.

```html
<figure>
  <p><img src="img/small_snowman.jpg" alt="Terrasse-sized snowman" width="180" height="240"></p>
  <figcaption>Small snowman we made on our little terrace</figcaption>
</figure>
```

#### redéfinition d’éléments existants

##### `<cite>`

Est utilisé pour marqué le titre d’un ouvrage. Ne peut donc plus être utilisé pour marquer l’auteur d’un document.

##### `<a>`

L’élément a à toujours été un élément inline en HTML. D’après les spécifications, il ne pouvait donc pas avoir d’éléments de type bloc comme descendants. Ce n’est plus le cas en HTML5. L’élément `<a>` est toujours considéré comme inline mais peut maintenant être le parent d’éléments de type bloc.

```html
<a href=”fake.html”>
  <h2>This is a title</h2>
  <p>lorem ipsum dolor sit amet</p>
</a>
```

*Exercice: examiner 2 sites et voir quels éléments utiliser*

#### Video Audio et Figure

Un autre aspect intéressant de HTML concerne la possibilité de gérer nativement les éléments audios et vidéos d'une page sans faire appel à des technologies extérieures telles que Flash.

En théorie, c'est aussi facile d'intégrer une vidéo ou un fichier audio que d'intégrer une image. En pratique, c'est un peu plus compliqué.

Certains anciens navigateurs ne supportent pas les tags `<video>` ou `<audio>`, il faut prévoir des solutions de fallback. Les navigateurs prenant en charge cet élément ne gèrent pas tous les mêmes formats et codecs, ce qui oblige à prévoir différents encodages du même fichier audio ou vidéo.

##### Vidéo

Voici le code nécessaire pour intégrer une video dans une page HTML.

Il y a 3 grands formats pour des videos en HTML: .webm, .mp4 et .ogv. Aujourd'hui .webm et .mp4 suffisent pour obtenir un support adéquat dans la plupart des navigateurs utilisés.

**Video simple**

```html
<video width="640" height="360" src="http://www.youtube.com/demo/google_main.mp4" controls>
```

**Video avec plusieurs sources**

```html
<video height="270" width="480" poster="waitimage.png" controls>
  <source src="samplevideo.webm" type="video/webm">
  <source src="samplevideo.mp4" type="video/mp4">
  <p>Your browser does not support the video tag but you can download the file either in <a href="samplevideo.webm">WEBM</a>, <a href="samplevideo.mp4">MP4</a></p>
</video>
```

L'attribut `poster` sert à donner une image d'attente dans les navigateurs supportant l'élément vidéo, tandis que l'attribut controls sert à afficher les contrôles minimaux pour le type de média choisi.

Certains navigateurs supportant l'élément `<video>` commencent automatiquement à télécharger les fichiers vidéos, ce qui donne lieu à un usage (important) de bande passante sans intervention utilisateur. L’attribut `preload="none"` peut être utilisé pour empêcher le preload de la video par le navigateur;

Si vos besoins en vidéo sont importants, des services tels que Youtube et Vimeo un moyen efficace de servir des vidéos sur le web. Ils réalisent automatiquement les divers encodages nécessaires, le type de plateforme utilisé par le visiteur, etc.

*Exercice: intégration d'un fichier video dans un document HTML*

##### Audio

Il y a 3 grands formats pour des videos en HTML: .mp3, .wav et .ogg. Aujourd'hui .mp3 suffit pour obtenir un support adéquat dans la plupart des navigateurs utilisés.

```html
<audio controls>
  <source src="elvis.mp3" type="audio/mpeg">
  <p><strong>Your browser does not support the audio tag but you can download the file either in <a href="elvis.mp3">MP3 format</a></strong></p>
</audio>
```

*Exercice: intégration d'un fichier audio dans un document HTML*

##### Figure et figcaption

Les élément figure et figcaption servent à grouper images et légendes dans vos documents HTML5.

```html
<figure>
  <img src="soleil.jpg" alt="Une journée ensoleillée à Louvain-la-Neuve">
  <figcaption>La grand-place et les terrasses par une journée ensoleillée à Louvain-la-Neuve.</figcaption>
</figure>
```
*Exercice: intégration d'une figure dans un document HTML*

#### Formulaires et HTML5

La spécification HTML5 permet également l'utilisation de contrôles de formulaires plus avancés que ceux dont nous disposions jusqu'ici.

```html
<form action="sendform.php">
  <p>
    <label for="bday">Your Birthday:</label>
    <input type="date" placeholder="dd/mm/yyyy" name="birthday" id="bday">
  </p>
  <p>
    <input type="submit" value="send this !">
  </p>
</form>
```

*Note: dans l'exemple ci-dessus, l'élement label est explicitement lié au champs de formulaire via les attributs `for` de `<label>` et l'attribut `id` de l'élément `<input>`.*

De nouveaux types de champs sont mis à la disposition des développeurs: email, url, date et range n'en sont que quelques uns.

```html
<input type="email" name="useremail" required>
<input type="url" name="userurl">
<input type="date" name="startdate">
<input type="range" name="myrange" min="0" max="10" step="1">
```

Ces nouveaux champs permettent, entre autres choses, une validation automatique du format des données entrées par les utilisateurs. La plupart de ces nouveaux éléments ne fonctionnent aujourd'hui qu'avec les navigateurs récents. Ceci étant dit, la plupart se dégradent élégamment dans les autres navigateurs (sous la forme de champs de type texte pour la plupart).

HTML permet également l'utilisation de nouveaux attributs pour les champs de formulaires. En voici quelques uns parmi les plus utiles (du moins à mon avis).

Le nouvel attribut `placeholder` permet de spécifier un texte dans un champ tant que celui-ci n'est pas rempli ni activé. Lorsque l'utilisateur active le champ de formulaire, ce texte disparait.

```html
<input type="tel" name="gsm" id="gsm" placeholder="+32475335162">
```

Pour sa part, l'attribut `autofocus` permet d'activer un champ de formulaire dès la page chargée.

```html
<input type="search" name="search" id="search" autofocus>
```

Intéressant également, l'attribut `required` permettant de spécifier un champ comme obligatoire dans le cadre d'un formulaire HTML5.

```html
<input type="text" name="name" id="name" required>
```

Pour ceux qui veulent en savoir plus, [un excellent article introductif est disponible sur 24 Ways](http://24ways.org/2009/have-a-field-day-with-html5-forms/) et une [démonstration a été mise en ligne par HTML5 Doctor](http://html5doctor.com/demos/forms/forms-example.html). Les [quelques pages de Mark Pilgrim sur le sujet](http://diveintohtml5.info/) sont également intéressantes, ainsi que la section consacrée aux [champs de formulaires sur Mozilla Developer Network](https://developer.mozilla.org/fr/docs/Web/HTML/Element/Input).

*Exercice: créer un formulaire en HTML5*

#### L'élément Canvas

HTML permet également d'utiliser l'élément `<canvas>` pour réaliser des dessins en 2D à l'aide de javascript. Il est possible de réaliser des graphiques en temps réel, des compositions à base d'images et de sons, des transformations, des animations, etc. [Une petite introduction par les gens d'Opera Software](https://dev.opera.com/articles/html5-canvas-basics/) peut être ?

Il est même possible de réaliser de véritables petits jeux en utilisant l'élément `<canvas>` et Javascript.

#### API HTML5

HTML5 propose également diverses API (Application Programming Interface) correspondant aux besoins de sites et d'applications riches:

- Drag and Drop
- Stockage offline
- Websockets
- File API
- Geolocalisation
- etc

## CSS

A partir de CSS3, la spécification CSS est passée d’une spécification monolithique à une spécification modulaire, plus flexible. Une plus grande modularité permet aux navigateurs d’implémenter l’un ou l’autre module, sans pour autant devoir implémenter la spécification dans son ensemble.

### Lier une feuille de style à un document HTML

Les déclarations CSS peuvent être liées de 4 façons à un document HTML afin d’en gérer l’affichage.

#### CSS liées

C'est la méthode la plus utilisée dans la mesure où elle permet de séparer vos styles (CSS) de votre structure et de votre contenu de document (HTML). C'est égalmement la méthode la plus performante, [comme le précise Steve Souders](http://www.stevesouders.com/blog/2009/04/09/dont-use-import/).

```html
<link rel="stylesheet" href="css/main.css">
```

#### CSS importées

A ne pas utiliser dans la plupart des cas pour des raison de performance.

```html
<style>@import url(css/main.css);</style>
```

#### CSS en ligne

Utilisé principalement pour le debugging ou pour augmenter la performance des pages avec Critical CSS.

```html
<style>body {background:#fff;}</style>
```

#### CSS dans l’attribut style des balises

Peu utilisé, sauf pour gérer certains styles bien précis à l'aide d'un CMS par exemple.

```html
<p style="color:blue;">
```

### CSS et media

[Les requètes de media](https://developer.mozilla.org/en-US/docs/Web/CSS/@media) peuvent soit spécifier un type de media (all, screen, print, speech, etc.) soit spécifier des charactéristiques du media visé (largeur de la surface de rendu, resolution, orientation, etc.).

Les types de media permettent d’appliquer les feuilles de style en fonction du type de media avec lequel les documents sont affichés, soit en fonction des charactéristiques du media. Des opérateurs logiques (and, not, only) peuvent être utilisés. Plusieurs types et charactéristiques de media peuvent être spécifiées au sein d'une même déclaration en les séparant par des virgules.

Il est possible d’utiliser l'attribut media avec plusieurs niveaux. Classiquement, on ne spécifie pas de type de media (all) lorsqu'on importe une feuille de style avec `<link>` et des media queries sont utilisées au sein des feuilles de styles. C'est particulièrement le cas en responsive web design (nous en reparlerons plus loins dans le cours).

**HTML avec CSS liées**

```html
<link rel="stylesheet" href="css/main.css">
<link rel="stylesheet" href="css/main.css" media="all and (min-width: 760px)">
```

**CSS en ligne**

```css
@media all and (min-width: 760px)
{
  body
  {
    background:#fff;
  }
}
```

*Exercice: lier une feuille de style à un document HTML5 et tester l'attribut media avec les valeurs screen et print*

### Anatomie d’une déclaration CSS

```css
/*Règle CSS*/
body /*Sélecteur*/
{
  color:#fff; /*propriété:valeur; == déclaration*/
  padding:1em;
}
```

### La cascade

Certaines déclarations pouvant enter en conflit avec d’autres, il importe de savoir laquelle sera prioritaire. C’est à ce souci que répond l’ordre de cascade, donnant aux navigateurs un ordre de tri :

1. Toutes les déclarations qui concernent l'élément et la propriété en question s’appliquent, pour le type de média visé (les règles de media print n’entrent pas en conflit avec les règles de media screen). Ces déclarations s'appliquent si le sélecteur CSS correspond à cet élément (une règle visant un h6 s’applique uniquement si un h6 existe dans le document mis en forme);
2. Les déclarations CSS sont ensuite classées par origine. Les règles de l’auteur du document priment sur celles de l’utilisateur qui priment elles-mêmes sur celles utilisées par défaut par le navigateur client.
3. Les déclarations sont ensuite classées par poids. Il est possible d’utiliser l’élément !important après une déclaration pour lui permettre d’avoir plus de poids qu’une déclaration normale;
4. Les sélecteurs sont ensuite triés par spécificité. Nous verrons ce dont il s’agit au point suivant.
5. Finalement, si deux règles ont la même origine, le même poids et la même spécificité, les déclarations figurant dans des CSS importées sont considérées comme étant placées avant les CSS présentes dans le document (X)HTML. Les dernières déclarations l’emportent sur les premières.

### Spécificité

Pour calculer la spécificité d’une déclaration CSS, c’est le sélecteur qui est pris en compte. La règle générale est que plus il est complexe, plus sa spécificité est haute. Voici la manière dont la spécificité des déclarations est calculée:

#### Calcul de spécificité

- Nombre d’ID référencées dans le sélecteur (= a)
- Nombre de classes et de pseudo-classes référencées dans le sélecteur (= b)
- Nombre d’éléments référencés dans le sélecteur (= c)
- Ne pas tenir compte des pseudo éléments.

Spécificité = a,b,c

*Ressources: [une explication ludique basée sur Star Wars et proposée par Andy Clarke](http://www.stuffandnonsense.co.uk/archives/css_specificity_wars.html).*

#### Exemples

  p = 0,0,1
  p.last = 0,1,1
  #content p.last = 1,1,1

  !important et sélecteur universel
  l’ajout de !important à une déclaration CSS permet de passer outre ce calcul de spécificité.
  Le sélecteur universel (*) possède une spécificité de 0,0,0

### Les sélecteurs CSS

Nous verrons ici quelques sélecteurs de base pour commencer. Notez simplement que CSS comporte un module de sélecteurs plus étendu qu'il peut être intéressant d'explorer.

Certains de ces sélecteurs CSS utilisent les relations entre les éléments au sein de l’arbre structurant un document HTML.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Exemple</title>
  </head>
  <body>
    <nav role="navigation">
      <ul class="mainnav">
        <li class="mainnav-item"><a href="index.html">Home</a></li>
        <li class="mainnav-item mainnav-current"><a href="work.html">Work</a></li>
        <li class="mainnav-item"><a href="contact.html">Contact</a></li>
      </ul>
    </nav>
    <main role="maincontent" id="content">
      <h1>Title of my page</h1>
      <div class="intro">
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eveniet, facilis, minus, nostrum a autem labore ut doloribus perferendis ullam voluptatem quis ducimus vero odit aspernatur in dolorem fuga consequuntur.</p>
      </div>
      <p>Lorem <em>ipsum dolor sit amet</em>, consectetur <em>adipisicing elit</em>. Cum, ut id fugiat tempore illo possimus atque odit tenetur laudantium harum iure perspiciatis impedit repudiandae. Odio iste deleniti blanditiis deserunt saepe.</p>
      <p>Provident, aperiam, repellendus, saepe voluptatibus tempora magnam id nisi repellat blanditiis eaque consequuntur reprehenderit assumenda tenetur nobis temporibus sint inventore nesciunt numquam qui delectus aliquid debitis eligendi quam in amet!</p>
      <p>Nihil, cum, odio, nam, et laudantium nisi odit hic quod tenetur provident accusamus quisquam alias! Tempora, velit harum eius ab quibusdam qui natus eos officia! Repellendus consequatur neque consectetur eius.</p>
    </main>
  </body>
</html>
```

**Ancêtre:** n’importe quel élément connecté à l’élément dont il est question et se trouvant plus haut dans l’arbre du document, aussi loin soit-il.

  body est l’élément ancêtre de tous les autres éléments sauf l’élément html

**Descendant:** n’importe quel élément connecté à l’élément dont il est question et se trouvant plus bas dans l’arbre du document, aussi loin soit-il.

  em est un élément descendant de l’élément body

**Parent:** l’élément connecté à l’élément dont il est question et se trouvant un seul niveau plus haut dans l’arbre du document.

  ul est l’élément parent des trois éléments li

**Enfant:** n’importe quel élément connecté à l’élément dont il est question et se trouvant un seul niveau plus bas dans l’arbre du document.

  em est l’élément enfant de l’élément p

**Adjacent:** n’importe quel élément partageant le même parent que l’élément dont il est question dans l’arbre du document.

  Les éléments h1, p et p sont tous adjacents

#### Sélecteur de types

Facile à comprendre, ce sélecteur permet de cibler tous les éléments du type indiqué présents dans le document.

```css
p
{
  color:red;
}
```

#### Sélecteur de classe

Le sélecteur de classe permet de cibler tous les éléments possédant la classe indiquée présents dans le document.

```css
.mainnav-current
{
  color:red;
}
```

Il est possible de combiner les sélecteurs au sein d’une même règle CSS. Les sélecteurs de type et de classe peuvent par exemple être combinés pour avoir une portée moins large et une spécificité plus importante. L'exemple donné ci-dessous n'est pas conseillé en production, justement parcequ'il augmente inutilement la spécificité du sélecteur.

```css
li.mainnav-current
{
  color:red;
}
```

Plusieurs classes CSS peuvent être appliquées à un seul élément HTML.

```html
<li class="mainnav-item mainnav-current">item <em>3</em></li>
```

#### Sélecteur d’id

Le sélecteur d’ID permet de cibler l’élément possédant l’ID indiquée présent dans le document.

```css
#content
{
  background:blue;
}
```

Une ID ne peut être utilisée qu’une seule fois dans le cadre d’un même document. Pour rappel : une règle CSS reposant sur une ID possède une spécificité plus grande que si elle repose sur une classe. De nombreux développeurs militent pour réduire l'utilisation d'id en HTML/CSS, justement à cause de leur spécificité plus importante. Les ID sont cependant utilisées pour marquer certaines zones de la page devant être atteintes à l'aide de liens.

#### Sélecteur descendant

Le sélecteur descendant permet de cibler les éléments qui sont les descendants d’un autre élément présent dans le document.

```css
p em
{
  background:red;
}
```

#### Sélecteur d’enfant

Le sélecteur d’enfant permet de cibler les éléments qui sont les enfants d’un autre élément présent dans le document.

```css
ul > li
{
  background:purple;
}
```

Ce sélecteur est supporté par IE7 et IE8.

#### Sélecteur d’enfant adjacent

Le sélecteur d’enfant adjacent permet de cibler l’élément suivant directement un élément présent dans le document.

```css
h1 + p
{
  background:yellow;
}
```

Cette règle ciblera uniquement le paragraphe placé immédiatement après le h1 dans le document.

Le sélecteur d’enfant adjacent est supporté par IE7 et IE8.

#### Sélecteur d’attribut

Le sélecteur d’attribut permet de cibler les éléments d’un document sur base des attributs qu’ils possèdent ou sur base de la valeur de ces attributs.

```css
div[role]
{
  background:red;
}
```

N’importe quel div ayant un attribut role

```css
div[role="maincontent"]
{
  border:3px dotted black;
}
```

Identité stricte

```css
div[id~="nav"]
{
  border:3px dotted black;
}
```

cible les éléments dont l’attribut class consiste en une liste de termes séparés par des espaces et contenant la suite de caractère “nav”

```css
div[id|="nav"]
{
  background:yellow;
}
```

cible les éléments dont l’attribut class consiste en une liste de termes séparés par des tirets et contenant la suite de caractère nav

#### Sélecteur universel

Ce sélecteur est utilisé pour cibler l’ensemble des éléments composant le document.

```css
*
{
  color:blue;
}
```

#### Pseudo-classes

Les sélecteurs de pseudo-classes permettent de cibler des éléments qui ne sont pas dans l’arborescence du document.

##### Pseudo-classes liées aux liens.

```css
a:link {text-decoration:underline;}
a:visited {color: purple;}
a:hover {text-decoration:none;}
a:focus {color:green;}
a:active {color:red;}
```

Les déclarations doivent obligatoirement être faites dans cet ordre afin d’obtenir le résultat escompté.

##### First-child & last-child

```css
p em:first-child
{
  font-weight:bold;
}
```

```css
p em:last-child
{
  font-weight:bold;
}
```

##### Lang

```css
li:lang(fr) {color:red ;}
```

Les pseudo-classes appliquées aux liens fonctionnent bien dans l’ensemble des navigateurs modernes.

#### Pseudo-éléments

Les sélecteurs de pseudo-éléments permettent de cibler des éléments qui ne sont pas disponibles dans l’arborescence du document.

##### first-line et first-letter

```css
p:first-letter
{
  font-weight:bold;
}

p:first-line
{
  font-variant:italic;
}
```

##### Viser le contenu sélectionné par l'utilisateur

```css
p::selection
{
  background-color: cyan;
}
```

##### génération de contenu via CSS

```css
a:after
{
  content:" hello world!";
}
```

Les pseudo-éléments `:before` et `:after` ne sont pas supportés par IE 7 et inférieurs, ni par des versions anciennes d’Opera.

Les pseudo-elements `:before` et `:after` sont souvent utilisés dans les sites web modernes, pour ajouter des éléments de décoration (icones, spriting). Ils sont également utilisés dans la solution de clearing des floats via CSS que nous verrons un peu plus loin.

### Propriétés et valeurs

Nous ne développerons pas ici toutes les propriétés CSS existantes et nous contenterons de les voir aux travers des exercices et exemples.

Pour une documentation complète, voir le [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference) ou [Webplateform.org](http://docs.webplatform.org/wiki/css/properties). [Le site du W3C](http://www.w3.org/Style/CSS/) fait évidemment toujours autorité.

## Le modèle de mise en forme CSS

CSS utilise un modèle de mise en forme basé sur les boîtes (“box model” en anglais). Chaque élément d’un document existe dans le cadre d’une de ces boîtes.

La plupart de ces boîtes se comportent comme des blocs conteneurs pour les boîtes qui en sont les descendantes : on dit que la boîte "établit" le bloc conteneur de ses descendants. L'expression "le bloc conteneur d'une boîte" ("containing block" en anglais) signifie "le bloc conteneur dans lequel se trouve la boîte", et non la propre boîte que celle-ci génère.

Le bloc conteneur est utilisé afin de déterminer la position des boîtes qu’il renferme et, dans certains cas, les dimensions de ces boîtes. Par exemple, si un élément possède une largeur de 50%, celle-ci sera calculée par rapport à la largeur de son bloc conteneur.

Pour tout élément qui n’est pas absolument positionné, le bloc conteneur est la zone de contenu de son ancêtre de type block le plus proche dans l’arbre du document. Si aucun n’existe, la fenêtre du navigateur sert de bloc conteneur. Nous aborderons cela plus en profondeur lorsque nous parlerons des divers types de positionnement.

Les diverses dimensions de ces boîtes sont gérées par les propriétés CSS suivantes: width, height, padding, margin et border.

- La largeur totale d’une boîte se calcule de la façon suivante : largeur du contenu (width) + padding + borders + margin.
- La hauteur totale d’une boîte se calcule de la façon suivante : hauteur du contenu (height) + padding + borders + margin.

La propriété **CSS3** `box-sizing` permet de changer ce comportement de base.

- `box-sizing: border-box;` modifie le modèle par défaut. La hauteur et la largeur de l’élément sont toujours égales aux valeurs de width / height, les valeurs de padding et de border en sont soustraites.
- `box-sizing: content-box;` correspond au modèle par défaut. La hauteur et la largeur de l’élement se calcule en additionnant width / height et padding, margin et border.

Voir à ce sujet [l'article de Paul Irish](http://www.paulirish.com/2012/box-sizing-border-box-ftw/).

### éléments en blocs et en lignes

Deux types de boîtes principales sont liées par défaut aux divers éléments du HTML : on parle d’éléments de type block (`<p>`,`<div>`, `<blockquote>` et `<h1>` par exemple) et de type inline (`<a>`, `<strong>`, `<em>`, `<span>`, `<img>` par exemple).

- Un élément block génère une boîte de bloc qui prend toujours un maximum d’espace horizontal, sauf si sa largeur est définie ou si la propriété float lui est appliquée. Les éléments block se placent, dans le flux du document, les uns en dessous des autres (par exemple : une suite de paragraphes ou une liste).
- Un élément inline génère une boîte en ligne. Ces éléments inline se placent toujours, dans le flux du document, les uns à côté des autres (par exemple : plusieurs `<span>` ou une partie de texte mise en gras à l’aide de la balise `<strong>`)

### Autres valeurs possibles

Toutes sortes de boites peuvent être générées à l’aide de la propriété CSS display : `none`, `inline`, `block`, `list-item`, `inline-block`, `inline-table`,`table`, `table-caption`, `table-cell`,`table-column.`,`table-column-group`, `table-footer-group`, `table-header-group`, `table-row`, `table-row-group`.

Nous nous contenterons ici d’en détailler quelques unes parmi les plus courantes.

#### Inline-Block

Nous verons plus loin que cette valeur peut être très utile pour contrôler les padding et les margin sur des éléments inline.

#### List-item

Les éléments de liste ne sont ni des balises de type block, ni des balises de type inline. Ils ont un comportement différent. En attribuant à un élément la déclaration CSS `display:list-item`, il pourra supporter les propriétés suivantes : `list-style-type`, `list-style-image`, `list-style-position` et `list-style`.

#### None

Cette valeur fait qu'aucune boîte n'est générée par l'élément dans la structure de formatage (cet élément n'a pas d'influence sur la mise en forme du document). Les éléments auxquels cette propriété est appliquée ne s’affichent pas dans le media concerné. Les éléments qui en descendent ne génèrent pas de boîtes non plus et il n’est plus possible de modifier leur comportement avec la propriété `display`.

Une valeur `none` ne crée pas de boîte invisible, elle ne crée pas de boîte du tout. CSS comprend des mécanismes permettant la génération de boîtes qui influencent la mise en forme mais qui ne sont pas visibles (propriété `visibility` en CSS).

#### Les valeurs liées aux tableaux

Les valeurs liées aux tableaux : `inline-table`,`table`,`table-caption`,`table-cell`,`table-column.`,`table-column-group`,`table-footer-group`,`table-header-group`,`table-row`,`table-row-group` donnent à un élément le comportement de celui d'une table ou d’un de ses composants.

### La fusion des marges

Cette expression "Collapsing Margins" signifie que les marges adjacentes de plusieurs boîtes peuvent se combiner afin de ne plus en former qu’une seule.

Les marges verticales de deux boîtes (ou plus) d'éléments de type bloc, placés dans un flux normal fusionnent. La largeur de la marge finale devient la valeur la plus grande parmi celles des marges adjacentes.

Dans le cas de marges négatives, on soustrait la plus grande des valeurs des marges négatives adjacentes (en valeur absolue) de la plus grande des marges positives adjacentes. S'il n'y pas de marges positives, on déduit de zéro la plus grande (en valeur absolue) des marges négatives.

- Deux paragraphes se suivant et ayant respectivement une marge inférieure de 10px et une marge supérieure de 15px seront séparés par 15px.
- Deux paragraphes se suivant et ayant respectivement une marge inférieure de -10px et une marge supérieure de 30px seront séparés par 20px.
- Deux paragraphes se suivant et ayant respectivement une marge inférieure de -10px et une marge supérieure de -15px seront séparés par -15px.

#### Elements adjacents

- Les marges des blocs flottants et de tout autre bloc ne fusionnent jamais, comme les marges entre des blocs absolument et relativement positionnés;
- Les marges entre des boîtes ne fusionnent pas si l'une des boite est en `display:inline-block;`
- La marge supérieure d'un élément auquel la propriété `clear` est appliquée et placé après un ou plusieurs élément floatés ne sera pas visible sauf si elle excède la hauteur du/des blocs floatés.

#### Parent et premier/dernier enfant

- Les marges entre un parent et son premier/dernier enfant ne fusionnent pas si le parrent possède une `border`, un `padding`, une `height` ou une `min-height`. spécifiée.
- Les marges entre un parent et ses enfants ne fusionnent pas si le parent possède une propriété overflow avec une valeur autre que visible.

Pour en savoir plus concernant la fusion des marges, lire les excellents articles de [Andy Budd](http://www.andybudd.com/archives/2003/11/no_margin_for_error/) et [Eric Meyer](http://www.complexspiral.com/publications/uncollapsing-margins/).

*Exercice sur la fusion des marges*

## Mises en page CSS

Ces diverses boîtes dont nous avons parlées sont utilisées dans le cadre de différents schémas de positionnement qui sont autant d’outils permettant de créer une mise en page à l’aide de CSS.

### Schémas de positionnement CSS

Il existe trois modes ou schémas de positionnement en CSS: static (relative), absolute (fixed ). Les modes de positionnement relatif et fixe sont des cas particuliers des modes statique et absolu. Chacun de ces modes obéit à ses règles propres.
Les modes de positionnement sont gérés en CSS via la propriété `position`.

#### Flux normal: positionnement statique et positionnement relatif

##### Flux du document et positionnement statique

Le flux normal du document est le mode par défaut utilisé pour le positionnement. C’est celui qui s’applique à tous les éléments lorsque ceux-ci ne sont pas ni en mode float ni positionnés de façon absolue. Il s’agit alors d’un positionnement en mode statique.

Dans le flux normal du document, les éléments de type block sont positionnés les uns sous les autres et leurs marges verticales fusionnent, tandis que les éléments de type inline se suivent sur la même ligne et passent à une nouvelle ligne lorsque la place manque.

##### Positionnement relatif

Lorsqu’un élément est positionné relativement, il est initialement positionné d’après le flux du document. Les boîtes des autres éléments sont positionnées et **ensuite**, l’élément positionné relativement est déplacé selon les valeurs spécifiées par les propriétés top bottom left et right.

La place originale de l’élément est préservée dans le flux du document et il existe de grandes chances que cet élément en recouvre d’autres. La propriété `z-index` peut être utilisée pour déterminer quel élément sera placé devant l’autre sur l’axe de profondeur. Le bloc ayant la propriété `z-index` la plus élevée sera affiché devant l’autre.

Si l’élément positionné est un élément de type `block`, il crée un nouveau bloc conteneur pour les éléments qui en dépendent dans l’arbre du document. Ces éléments utiliseront maintenant le positionnement modifié de l’élément comme bloc conteneur.

Si les propriétés top ou bottom sont contradictoires, la propriété top l’emporte. Si les propriétés left ou right sont contradictoires, la propriété left l’emporte dans les langages se lisant de gauche à droite et right l’emporte dans les langages se lisant de droite à gauche.

*Exercice: positionnement relatif*

#### Positionnement absolu et fixe

##### Positionnement absolu

Ce mode de positionnement est appliqué à tous les éléments dont la propriété position est définie comme absolute ou fixed. Si un tel élément n’existe pas, c’est l’élément racine (html) du document qui fait office de bloc conteneur.

Les boîtes utilisant ce mode de positionnement sont extraites du flux du document et n’influencent plus les autres boîtes qui agissent comme si les boîtes positionnées absolument ou de manière fixe n’existaient pas. De plus, les éléments positionnés absolument se comportent toujours comme des éléments de type `block`.

*Exercice: positionnement absolu et fixe*

Exemple de layout: [Lost World Fair](http://lostworldsfairs.com/moon/)

Ces éléments utilisent comme contexte de positionnement l’élément parent (de type `block` ou `inline`) le plus proche ayant lui-même un positionnement spécifié comme absolu, relatif ou fixe.

1. Un élément positionné absolument l’est par rapport aux bordures de son bloc conteneur (le padding n’est pas pris en compte et l’élément est positionné par rapport au bord intérieur de la bordure éventuelle du bloc conteneur).
2. Un élément absolument positionné devient un bloc conteneur pour les éléments qu’il contient et ceux-ci suivent les règles de positionnement normal à l’intérieur de l’élément positionné absolument.
3. Les éléments absolument positionnés peuvent contenir d’autres éléments positionnés absolument, qui sont à leur tour hors du flux normal du document, ce qui a pour conséquence qu’ils peuvent apparaître hors des limites de leur parent.

###### z-index et positionnement en couches

Les éléments positionnés absolument, comme ils sont hors du flux normal du document, peuvent recouvrir d’autres éléments (absolument positionnés ou non).

Chaque élément positionné génère une couche et, au sein d’une même couche, la profondeur de chaque élément est gérée par la propriété CSS `z-index`. Au sein d’une même couche, les éléments ayant une valeur `z-index` élevée sont placés devant ceux ayant une valeur `z-index` moindre.

*Exercice: propriété z-index*

##### Positionnement fixe

Pour ce cas particulier du positionnement absolu, le bloc conteneur est toujours la fenêtre du navigateur.

Les éléments positionnés de façon fixe ne bougent pas lorsque l’utilisateur descend dans la page.

*Exercice: positionnement fixe*

Exemples de layouts: [Web Designer Wall](http://webdesignerwall.com/), [Lost World's Fair: Atlantis](http://lostworldsfairs.com/atlantis/),[Bonzai Sky CSS Zen Garden Design by Mike Davidson](http://www.csszengarden.com/069/)

#### Floats

Un élément est positionné en mode float lorsque sa propriété `float` est spécifiée à l’aide des valeurs `left` ou `right`.

L’élément est alors positionné verticalement comme dans le flux normal du document : le côté supérieur de l’élément est aligné sur le dessus de la zone de contenu de son élément parent.

Horizontalement par contre, l’élément est placé le plus à gauche ou le plus à droite possible par rapport à la zone de contenu de l’élément parent. Le contenu de l’élément parent contourne alors l’élément en mode float par le côté opposé.

Quelques règles de base :

1. Les éléments positionnés en mode float sont toujours gérés comme des éléments de type block.
2. D’après les spécifications, un élément en mode float doit toujours avoir une dimension, implicite ou explicite (nous verrons plus loin que cela n’est pas toujours vrai dans la pratique, mais c’est un bon principe de base).
3. Les marges verticales d’un élément en mode float ne sont pas fusionnées avec celles des éléments placés avant ou après dans le flux du document.
4. Des éléments en mode float seront placés les uns à côté des autres si la place disponible est suffisante. Si tel n’est pas le cas, le dernier élément sera placé sous les autres.

En fonction de la quantité de contenu des divers éléments, un élément en mode float peut affecter les éléments situés après lui dans le flux du document.

*Exercice: expériementer avec float*

##### Contrôler le flux des floats: propriété `clear`et float containment

La propriété CSS clear peut être utilisée pour contrôler la manière dont les éléments de type block interagissent avec les éléments en mode float. La propriété clear ne s’applique qu’aux éléments de type block. Cette propriété peut prendre les valeurs `left`, `right` et `both`.

- `clear:left;`: l’élément visé ne peut se situer sur la gauche d’un élément en mode float.
- `clear:right;`: l’élément visé ne peut se situer sur la droite d’un élément en mode float.
- `clear:both;`: l’élément visé ne peut se situer ni sur la gauche ni sur la droite d’un élément en mode float.

Par défaut, étant donné que les éléments en mode float sont hors du flux du document, leur éléments parent ne les contiennent pas. Il est possible de contraindre l’élément parent d’un élément en mode float à contenir l’ensemble de celui-ci, indépendamment du contenu de chacun d’entre eux. Eric Meyer a écrit [un article de référence décrivant précisément cet aspect des éléments en mode float](http://www.complexspiral.com/publications/containing-floats/).

Cela peut être accompli à l’aide d’autres éléments situés à l’intérieur de l’élément parent de l’élément en mode float ou à l’aide de CSS lorsque le code HTML ne contient pas d’élément utilisable.

###### Utilisation d’un élément du code et de la propriété `clear`

Comme vu plus haut, en utilisant la propriété CSS `clear`, il est possible de forcer un élément à ne pas être côté à côte avec un élément en mode float.
Nous verrons par exemple qu’un pied de page peut s’avérer bien pratique pour forcer un conteneur à contenir deux colonnes en mode float (deux `<div>` par exemple).

###### A l’aide des CSS uniquement

Il est également possible d’utiliser uniquement les CSS afin de forcer son élément parent à contenir un élément en mode float.

**Float parent**

La solution la plus simple consiste à placer l’élément parent en mode float lui aussi, sans oublier de lui donner une dimension (width:100%; dans la plupart des cas). En effet, la spécification CSS précise qu’un élement en mode float contient toujours ses enfant floatés.

**Overflow**

[La propriété `overflow` peut également être utilisée pour obtenir cet effet](http://annevankesteren.nl/2005/03/clearing-floats) mais peut poser des problèmes dans certaines situations.

```html
div
{
  overflow:hidden;
}
```

La génération de contenu à l’aide des CSS permet également de forcer un élément parent à contenir ses éléments enfants en mode float. Cette technique est expliquée en détail [par Big John et Holly Bergevin sur leur site "Position Is Everything"](http://www.positioniseverything.net/easyclearing.html) [Une variante plus moderne reposant sur les pseudo-éléments :before et :after a été développée par Nicolas Gallagher](http://nicolasgallagher.com/micro-clearfix-hack/). Ces solutions genèrent un élement à l'aide de CSS et lui appliquent un `clear:both;`, émulant ainsi la solutin vue plus haut.

Il suffit de créer une classe CSS spécifique et d’y copier le code suivant pour pouvoir utiliser cette possibilité aussi souvent que nécessaire.

**Clearfix**

CSS

```css
.clearfix:after
{
  content: "";
  display: table;
  clear: both;
}
```

*Exercice: expériementer avec float et clearing*

## CSS comme outil de mise en page

Les propriétés `float` et `clear` (ou `inline-block`), ainsi que les propriétés de positionnement ne sont pas des outils prévus pour réaliser des mises en page complexes.

Ces solutions ont été utilisées par le passé pour créer des mises en page CSS parce que c'étaient les uniques outils dont nous disposions. N'ayant pas été développées dans ce but, ces solutions posaient de nombreux problèmes et avaient également des limitations importantes.

Récemment, de nouveaux outils dédié au layout sont apparus en CSS, principalement Flexbox et Grid.

- *Flexbox*: gère une seule dimension (verticale ou horizontale), fonctionne à partir du contenu (content out), est principalement utilisé pour le layout de composants comme de cartes ou des interfaces de navigation (micro layout).
- *Grid*: gère deux dimensions (verticale et horizontale), fonctionne en créant une grille dans laquelle les contenus viennent se placer (content in), est principalement utilisé pour des mises en page globales ou pour des élements plus importants comme des grilles de produits ou de media (macro layout).

Ces deux outils de layout font en outre appel au [module de Box Alignment](https://www.w3.org/TR/css-align-3/). Vous retrouverez donc des propriétés d'alignement communes à Grid et à Flexbox.

### Flexbox

Flexbox est appliqué gâce à la propriété display. Une fois la propriété `display: flex;` ou `display: inline-flex;` déclarée sur un élement, celui-ci devient un **flex-container** est ses enfants directs des **flex-items**. Comme dit plus haut, Flexbox permet de gérer les choses dans une dimension principale (verticale ou horizontale). C'est ce que l'on appelle le "main-axis" qui est spécifié via la propriété `flex-direction` et permet de gérer l'alignement principal des flex-items. Une fois le "main-axis" précisé, un "cross axis" perpendiculaire permet de gérer des propriétés d'alignement plus secondaires des flex-items.

Voici les propriétés les plus importantes au niveau du flex-container. Ces propriétés ont des valeurs par défaut mais, lorsque vous commencez, il est conseillé de les spécifier toutes explicitement.

- `flex-direction: [row | row-reverse | column | column-reverse];`: établi la direction du "main axis" (et donc aussi celle du "cross axis"). La valeur `row` spécifie un axe horizontal gauche droite pour les documents en mode `ltr` et un axe horiontal droite gauche pour les documents en mode `rtl`
- `justify-content: [flex-start | flex-end | center | space-between | space-around | space-evenly];`: gestion de l'alignement des flex-items et de la distribution de l'espace sur le main axis. `flex-start` et `flex-end` dépendent du mode de document `ltr` ou `rtl`.
- `align-items: [flex-start | flex-end | center | baseline | stretch];` gestion de l'alignement des flex-items et de la distribution de l'espace sur le cross axis
- `flex-wrap: [wrap | nowrap];`: les flex-items sont ils autorisés à passer sur une autre ligne ou pas.

Voici les propriétés les plus importantes au niveau des flex-items. Ces propriétés ont des valeurs par défaut. Lorsque vous commencez, je vous conseille de spécifier `flex` et ses trois valeurs explicitement.

- `flex-basis` détermine les dimensions d'un flex-item avant que l'espace vide dans le flex-container soit distribué. Peut être soit une valeur (px, rem, em, %, etc.) soit `auto` (dans ce cas la valeur spécifiée pour `width` ou `height` est prise en compte). La valeur par défaut est `auto`.
- `flex-grow`: détermine si un flex-item peut grandir au delà de ses dimensions de base si nécessaire. A comme valeur `0` ou un nombre entier qui représente la proportion avec laquelle les flex-items vont grandir si ils sont plus petits que leur flex-container après l'application de `flex-basis`. Plus le nombre entier est grand, plus la proprotion est importante. La valeur par défaut est `0`.
- `flex-shrink`: détermine si un flex-item peur rétrécir en deça de ses dimensions de base si nécessaire. A comme valeur `0` ou un nombre entier positif qui représente la proportion avec laquelle les flex-items vont rétrécir si ils sont plus grands que leur flex-container après l'application de `flex-basis`. Plus le nombre entier est grand, plus la proprotion est importante. La veleur par défaut est `1`.
- `order [integer]`: détermine l'ordre d'affichage des flex-items dans un flex-container indépendemment de leur ordre dans le code source. La valeur est spécifiée sous la forme d'un nombre entier positif ou négatif.
- `flex: [flex-grow | flex-shrink | flex-basis]`: propriété courte permettant de gérer à la fois `flex-grow`, `flex-shrink` et `flex-basis`. Il vaut mieux utiliser cette propriété courte plutôt que les propriétés longues pour des raisons de compatibilté entre navigateurs.

La propriété `margin` avec une valeur de `auto` est intéressante pour les `flex-items`, elle permet d'allouer tout l'espace disponible dans le flex-container à cette marge et ainsi de "pousser" un ou plusieurs flex-items vers l'extrémité opposée du main axis. L'aricle "[Flexbox’s Best-Kept Secret](https://hackernoon.com/flexbox-s-best-kept-secret-bd3d892826b6)" explique le phénomène en détail.

CSS tricks possède un bon article "[A complete guide to flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)" résumant l'ensemble des propriétés et valeurs liées à Flexbox. [Flexbox Froggy](http://flexboxfroggy.com/) adopte une approche plus ludique.

**Exemple: interface de navigation horizontale (expérimenter avec les différentes propriétés et valeurs)**

```html
<ul class="mainnav">
  <li class="mainnav__item"><a class="mainnav__link" href="#">Home</a></li>
  <li class="mainnav__item"><a class="mainnav__link" href="#">About</a></li>
  <li class="mainnav__item"><a class="mainnav__link" href="#">Work</a></li>
  <li class="mainnav__item  mainnav__item--contact"><a class="mainnav__link" href="#">Contact</a></li>
</ul>
```

```css
.mainnav
{
  list-style: none;
  margin: 0;
  padding: 0;

  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  align-items: center;
  flex-wrap: nowrap;

  background-color: #ccc;
}

.mainnav__item
{
  flex: 0 0 auto;
}

.mainnav__item--contact
{
  margin-left: auto;
}

.mainnav__link
{
  display: block;
  padding: 1rem;
  background-color: #dfdfdf;
}

.mainnav__link:hover
{
  background-color: #eee;
}
```

### Grid

CSS grid permet de créer des grilles en deux dimensions et de positionner des élements à l'aide de ces grilles. CSS grid est appliqué à l'aide de la proprité display. Une fois `display: grid;` ou `display: inline-grid;` appliqué à un élément, celui-ci devient un **grid-container** et ses enfants directs des **grid-items**.

Grid est une spécification relativement complexe, nous allons ici en voir les propriétés principales. Pour un aperçu plus complet, je ne peux que vous recommander "[Grid by example](https://gridbyexample.com/examples/)" par Rachel Andrew et [un guide très bien fait disponible en français sur Mozilla Developer Network](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_Grid_Layout/Les_concepts_de_base). Voir également "[A Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)" sur CSS Tricks pomur un bon résumé.

Voici les propriétés principales au niveau du **grid-container**:

- `grid-template-columns`: défini les dimensions des colonnes de la grille. Peut être une valeur (fr,%,px,rem,em, etc.) ou `auto`. Si ces valeurs sont répétées il est intéressant d'utiliser la notation `repeat`. La valeur `minmax([valeur-min], [valeur-max])` est également très utile pour spécifier une valeur minimale et maximale pour les dimensions des colonnes. Lorsque `minmax` est utilisé avec `repeat`, il est également possible d'utiliser `auto-fill` ou `auto-fit`.
- `grid-template-rows`: défini les dimensions des rangées de la grille. Peut être une valeur (fr,%,px,rem,em, etc.) ou `auto`. Si ces valeurs sont répétées il est intéressant d'utiliser la notation `repeat`. La valeur `minmax([valeur-min], [valeur-max])` est également très utile pour spécifier une valeur minimale et maximale pour les dimensions des colonnes. Lorsque `minmax` est utilisé avec `repeat`, il est également possible d'utiliser `auto-fill` ou `auto-fit`.
- `justify-content: [start | end | center | stretch (default)]`: permet d'aligner les grid-items par rapport à l'axe des rangées.
- `align-items: [start | end | center | stretch (default)]`: permet d'aligner les grid-items par rapport à l'axe des colonnes.
- `grid-column-gap`, `grid-row-gap`, `grid-gap`: permettent de spécifier les espaces entre les colonnes et les rangées de la grille ou les deux à la fois. Peut être une valeur (%,px,rem,em, etc.).
- `grid-templates-areas`: permet de définir des zones de grilles nommées de façon visuelle. les valeurs sont soit des chînes de caractères, soit un "." qui permet de laisser la zone comme vide de tout contenu.

Voici les propriétés principales au niveau des **grid-items**:

- `grid-column-start`, `grid-column-end`, `grid-column`, `grid-row-start`, `grid-row-end`, `grid-row`: permettent de placer les grid-items dans les colonnes de la grilles. Peuvent prendre comme valeur des nombres correspondant à des grid lines ou des noms de grid lines nommées. Le mot-clé `span` peut être utilisé avec un nombre ou un nom de grid line pour faire en sorte que des grid-items occupent plusieurs "cases" de la grille. Une valeur de `auto` est la valeur par défaut et correspond à un placement automatique des grid-items. `grid-column` et `grid-row` sont des propriétés courtes permattant de gérer les deux à la fois avec les notations `column-start / column-end` ou `row-start / row-end`
- `grid-area`: permet de placer des grid-items dans des zones de la grille nommées à l'aide de `grid-template-areas`. Cette propriété peut également servir de notation ultra condensée pour spécifier `row-start / column-start / row-end / column-end`
- `justify-self`: permet d'aligner les grid-item le long de l'axe des rangées.
- `align-self`: permet d'aligner les grid-item le long de l'axe des colonnes.

**Exemple: grilles fluide simple - expériementer avec les différentes propriétés et valeurs**

```html
<div class="grid">
  <div class="grid__item">grid item</div>
  <div class="grid__item">grid item</div>
  <div class="grid__item">grid item</div>
  <div class="grid__item">grid item</div>
  <div class="grid__item">grid item</div>
  <div class="grid__item">grid item</div>
  <div class="grid__item">grid item</div>
</div>
```

```css
.grid
{
  display: grid;
  /* grid-template columns: 1fr 1fr 1fr 1fr; */
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: auto;
  grid-gap: 20px;
}

.grid__item
{
  background-color: teal;
}
```

**Exemple: grille fluide responsive avec minmax et auto-fit - expériementer avec les différentes propriétés et valeurs**

```html
<div class="grid">
  <div class="grid__item">grid item</div>
  <div class="grid__item">grid item</div>
  <div class="grid__item">grid item</div>
  <div class="grid__item">grid item</div>
  <div class="grid__item">grid item</div>
  <div class="grid__item">grid item</div>
  <div class="grid__item">grid item</div>
</div>
```

```css
.grid
{
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  grid-template-rows: auto;
  grid-gap: 20px;
}

.grid__item
{
  background-color: teal;
}
```

**Exemple: grille mixte avec des zones nommées à l'aide de template areas**

```html
<div class="page">
  <header class="pageheader">header</header>
  <main class="content-main">content</main>
  <aside class="content-secondary">sidebar</aside>
  <footer class="pagefooter">footer</footer>
</div>
```

```css
.page
{
  margin: 0 auto;
  padding: 0 20px;
  max-width: 960px;

  display: grid;
  grid-template-columns: 300px 20px 1fr;
  grid-template-rows: auto;
  grid-template-areas: "header header header"
                       "sidebar . content"
                       "footer footer footer";
}

.pageheader
{
  grid-area: header;
  background-color: silver;
}

.content-secondary
{
  grid-area: sidebar;
  background-color: teal;
}

.content-main
{
  grid-area: content;
  background-color: olive;
}

.pagefooter
{
  grid-area: footer;
  background-color: grey;
}
```

**Exemple: grille responsive avec elements placés automatiquement et un élément placé explicitemnt (avec span)**

```html
<ul class="grid">
  <li class="grid__item"><p>grid item</p></li>
  <li class="grid__item"><p>grid item</p></li>
  <li class="grid__item  grid__item--highlight"><p>grid item</p></li>
  <li class="grid__item"><p>grid item</p></li>
  <li class="grid__item"><p>grid item</p></li>
  <li class="grid__item"><p>grid item</p></li>
  <li class="grid__item"><p>grid item</p></li>
  <li class="grid__item"><p>grid item</p></li>
</ul>
```

```css
.grid
{
  list-style: none;
  margin: 0;
  padding: 0;

  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  grid-template-rows: auto;
  grid-gap: 2rem;
}

.grid__item
{
  background-color: teal;
}

.grid__item--highlight
{
  background-color: red;
  grid-row: 1 / 2;
  grid-column: 1 / 2;
}

@media all and (min-width: 440px)
{
  .grid__item--highlight
  {
    grid-row: 1 / 3;
    grid-column: 1 / 3;
  }
}
```

## Media queries: l'un des trois piliers du responsive web design

Si vous vous souvenez de l'attribut `media` utilisé lorsque vous liez une feuille de style à un document HTML, vous comprendrez aisément ce que sont les media queries.

Les [média queries](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Media_queries) étendent les fonctionnalités des types de média. Elles permettent de servir des feuilles de styles ou certaines déclarations au sein de feuilles de style en fonction de caractéristiques de la plateforme à l’aide de laquelle sont affichées les pages.

Ces media queries permettent de tester les caractéristiques suivantes: `width`, `max-width`, `min-width`, `height`, `max-height`, `min-height`, `aspect-ratio`, `device-aspect-ratio`, `device-height`, `monochrome`, `color`, `device-width`, `orientation`, `resolution`, etc.

Elles sont utilisables avec des feuilles de styles liées.

```html
<link rel="stylesheet" media="screen and (min-width:970px)" href="css/medium.css" />
```

Ces media queries peuvent également être placées au sein de feuilles de styles existantes, ce qui est leur utilisation la plus fréquente.

```css
@media all and (min-width: 970px)
{
  /*styles*/
}
```

Comme le mentionne Stéphanie Rieger sur Cloud Four [il est avantageux de spécifier vos media-queries en em](http://blog.cloudfour.com/the-ems-have-it-proportional-media-queries-ftw/), pour donner plus de flexibilité à vos layouts, ceux-ci vont en effet changer lorsque l'utilisateur change la taille de texte.

L’idée est d’utiliser les media queries pour créer permettre à l’expérience utilisateur d’être la meilleure possible quelle que soit la plateforme utilisée.

Pour ce qui est du choix des valeurs de breakpoints, je vous invite à [suivre le conseil de Stephen Hay](https://twitter.com/brad_frost/status/191977076000161793).

**Exercice: media queries et des couleurs de donc sur l'élément `body`**

**Exercices: layouts et composants en utilisant grid et media queries**

## Quelques Techniques CSS utiles

Nous avons déjà examiné quelques astuces et hacks CSS permettant de contourner les défauts de certains navigateurs. Nous allons maintenant passer en revue quelques autres techniques utiles.

### Listes et interfaces de navigation

Sémantiquement parlant, la plupart des interfaces de navigation que nous rencontrons sont des listes de liens (imbriquées ou non), il est donc logique de les coder comme tels. De simples listes non ordonnées `ul` peuvent facilement être mises en forme à l’aide d’un code CSS simple.

```html
<ul class="mainnav">
  <li class="mainnav__item"><a class="mainnav__link" href="#">Home</a></li>
  <li class="mainnav__item"><a class="mainnav__link" href="#">About</a></li>
  <li class="mainnav__item"><a class="mainnav__link" href="#">Work</a></li>
  <li class="mainnav__item"><a class="mainnav__link" href="#">Contact</a></li>
</ul>
```

#### Listes verticales

Quelques règles CSS peuvent transformer une simple liste non ordonnée en barre de navigation verticale.

```css
.mainnav
{
  list-style: none;
  margin: 0;
  padding: 0;
}

.mainnav__item:not(:last-child)
{
  display: block;
  border-bottom: 1px solid #dfdfdf;
}

.mainnav__link
{
  display: block;
  padding: 1rem 0.5rem;
}

.mainnav__link:hover
{
  font: 600 12px/1 "Helvetica", "Arial", sans-serif;
}
```

#### Listes horizontales (Flexbox)

Quelques règles CSS peuvent transformer une simple liste non ordonnée en barre de navigation horizontale. L'alignement des items dans la liste, la répartition de l'espace libre d'autres caractéristiques peuvent être facilement modifiées avec flexbox.

```css
.mainnav
{
  list-style: none;
  margin: 0;
  padding: 0;

  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  align-items: center;
  flex-wrap: nowrap;

  background-color: #ccc;
}

.mainnav__item
{
  flex: 0 0 auto;
}

.mainnav__link
{
  display: block;
  padding: 1rem;
  font: 600 12px/1 "Helvetica", "Arial", sans-serif;
  text-transform: uppercase;
  text-decoration: none;

  color: #333;
  background-color: #dfdfdf;
}

.mainnav__link:hover
{
  background-color: #eee;
}
```

*Exercice: réaliser des interfaces de navigation à partir de listes*

### Une taille de texte constante à l’aide de valeurs relatives

Les guidelines d’accessibilité du W3C nous demandent d’utiliser en CSS des valeurs relatives afin de spécifier la taille des polices.

Personnellement, ma méthode de prédilection consiste à spécifier la taille des polices en pourcentages au niveau du `body` et puis de poursuivre en spécifiant les tailles pour les éléments enfants en `rem` (voir à ce propos [cet article de Jonathan Snook](http://snook.ca/archives/html_and_css/font-size-with-rem)).

```css
html
{
  font: normal 75%/1.5 arial, sans-serif; /*12px comme taille de base*/
}
```
ou

```css
html
{
  font: normal 100%/1.5 arial, sans-serif; /*16px comme taille de base*/
}
```

### Centrer un bloc horizontalement

Voici quelques techniques éprouvée pour centrer un élément de type block quel que soit le navigateur utilisé.

```css
.centered-block
{
  width:750px;
  margin:0 auto;
}
```

Position absolue et marges négatives

```css
.centered-block
{
  position:absolute;
  width:750px;
  left:50%;
  margin-left:-375px;
}
```

Position absolue, marges négatives et `calc()`

```css
.centered-block
{
  position: absolute;
  width: 750px;
  left: calc(50% - 375px);
}
```

### Faire disparaître des éléments visuellement sans les cacher aux navigateurs vocaux

La déclaration display:none; a été utilisée pour cacher des éléments en mode visuel (souvent dans le cadre de remplacement par images1). Le problème c’est qu’[elle rend les éléments auxquels elle est appliquée invisibles aux navigateurs vocaux également](http://css-discuss.incutio.com/?page=ScreenreaderVisibility).

Elle peut souvent être avantageusement remplacée par la déclaration suivante :

```css
.offleft
{
  position:absolute;
  top:0;
  left:-2000px;
  width:100px;
  overflow:hidden;
}
```

Autre option

```css
.visuallyhidden
{
  position:absolute;
  overflow:hidden;
  clip:rect(0 0 0 0);
  height:1px; width: 1px;
  margin:-1px;
  padding:0;
  border:0;
}
```

### @font-face: Utilisation de polices non standards

Avec l’avènement de CSS3, il est désormais possible, sans faire appel à d’autre technologies, d’utiliser des polices spécifiques dans le cadre de projets Internet. [@font-face jouit d’un excellent support dans la plupart des versions récentes des navigateurs](http://caniuse.com/fontface) et se dégrade élégamment dans les navigateurs plus anciens. Cette propriété permet de spécifier les polices à utiliser pour le rendu des textes et permet à l’utilisateur de les télécharger si il n’en dispose pas.

CSS

```css
@font-face {
  font-family: 'MyFontFamily';
  src: url('fonts/MyFontFamily.woff2') format('woff2'),
       url('fonts/MyFontFamily.woff') format('woff');
  font-weight: 400;
  font-style: normal;
}
```

pour utiliser la police dans votre CSS:

```css
h1
{
  font: normal 2rem/1.1 "MyFontFamily", "Helvetica", "Arial", sans-serif;
}
```

Si vous utilisez différentes graisses ou styles de la même police, [lire l'article de Roger Johansson sur le sujet](http://www.456bereastreet.com/archive/201012/font-face_tip_define_font-weight_and_font-style_to_keep_your_css_simple/). Cette technique simple vous évitera de devoir utiliser différents noms de polices dans votre CSS pour chaque graisse ou variante.

Les principaux problèmes liées à l’utilisation de @font-face sont de nature légale. La licence de certaines polices ne permet pas de les utiliser de cette façon car, étant disponibles sur le serveur, elles peuvent y être téléchargées par quelqu’un qui ne les a pas forcément achetées. De nombreuses polices offrent explicitement la possibilité d’une utilisation à l’aide de `@font-face` dans le cadre de leur licence.

Cette technique est dores et déjà bien supportée par les divers navigateurs et constitue à ce jour notre meilleure option.

Divers services tels que [Google Fonts](http://www.google.com/fonts), [Typekit](https://typekit.com/) et [Fontdeck](http://fontdeck.com/) se sont développés pour simplifier l’aspect technique et résoudre les questions légales tout en proposant un très large choix de polices. Certains de ces services sont payants, d'autres sont gratuits.

Si le sujet de la typographie sur internet vous intéresse, je ne peux que vous conseiller un talk de [Jason Santa Maria](http://vimeo.com/34178417) et le site "[Nice Web Type](http://nicewebtype.com/)" de Tim Brown.

*Exercice: expérimenter avec des fontes*

### Boutons en CSS3 avec Inline-block, border radius, text-shadow & box-shadow

Grâce à quelques propriétés CSS3, il est facile de créer des boutons à l’aide d’un simple lien hypertexte.

HTML

```html
<p><a href=”fake.html” class=”btn”>Text of my button</a></p>
```

CSS

```css
.btn
{
  display:inline-block;
  background:#7AA020;
  color:#fff;
  border-radius:.2em;
  padding:.75em 1em;
  font:bold 1em/1 helvetica,arial,sans-serif;
  text-decoration:none;
  text-shadow:1px 1px 0 rgba(0,0,0,.5);
  box-shadow:inset 0 -3px 0 rgba(0,0,0,.5);
}
.btn:hover
{
  background:#5C7917;
}
```

### Coins arrondis avec la propriété CSS3 border-radius

Avant CSS3, créer des boites avec des coins arrondis impliquait d'utiliser des structures HTML complexes et des images. Aujourd'hui, la propriété border-radius permet de le faire en une seule ligne de code.

```css
.box-rounded
{
  background:red;
  border-radius:.3em;
}
```

Il est possible de spécifier des valeurs différentes pour chacun des coins

```css
.box-rounded
{
  background:red;
  border-radius:.3em 2em 200px 5%;
}
```

[Comme le montre Lea Verou](http://lea.verou.me/humble-border-radius/), il ya beaucoup de choses à dire à propos de la propriété `border-radius`.

### Media fluides avec max-width:100%;

Lorsqu'on réalise des layout fluides, il est important que les images et autres medias le soient eux aussi. En d'autres mots il faut que les média fassent au maximum 100% de la largeur de leurs parents (dont la largeur est spécifée en pourcentages).

Il suffit donc dans votre HTML de ne pas spécifier les dimensions de vos media et d'utiliser la règle CSS suivante:

```css
img, video
{
  max-width:100%;
}
```

Comme vous aurez sans doute besoin de media fluides et de media fixes, il est avantageux d'utiliser une classe pour vos media fluides.

HTML

```html
<img src="myimage.jpg" class="fluidmedia" alt="my fluid image">
```

```html
<video controls class="fluidmedia">
  <source src="assets/videos/video.mp4" type="video/mp4">
  <source src="assets/videos/video.webm" type="video/webm">
  <p>Your browser doesn't support HTML5 video. Download the video in <a href="assets/videos/video.mp4">mp4</a> or <a href="assets/videos/video.webm">webm</a>.</p>
</video>
```

CSS

```css
.fluidmedia
{
  max-width:100%;
}
```

Les videos servies par Youtube et Vimeo utilsent `<iframe>`, voici une façon simple de garder un ratio constant (16/9) tout en ayant un comportement fluide.

```html
<div class="fluidvideo">
  <iframe src="https://www.youtube.com/embed/_kAJSswZPvI"></iframe>
</div>
```

```css
.fluidvideo
{
  position: relative; /* positioning context */
  padding-top: 56.25%; /* ratio 16/9 (100%/16*9) */
  /* padding-top: 75%; ratio 4/3 (100%/4*3) */
  background-color: #000;
}

.fluidvideo > iframe
{
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
```

## Ressources Complémentaires

- [Highly Maintainable, Efficient, and Optimized CSS](http://zomigi.com/blog/maintainable-efficient-css/) par Zoe Mickley Gillenwater: quelques bonnes informations sur les "best practises" en matière de CSS.
- [CSS Guidelines](https://github.com/csswizardry/CSS-Guidelines) par Harry Roberts: principes d'organisation et techniques pour écrire et maintenir des CSS maintenables, lisibles pour des projets de toutes tailles.
- [caniuse.com](http://caniuse.com): tables de support navigateurs pour HTML5 et CSS3
- [html5please](http://html5please.com): conseils d’utilisation pour HTML5 et CSS3. Polyfill javascript renseignés.
- [Mozilla Developer Network](https://developer.mozilla.org/): une bonne référence exhausitive sur les technologies du web (HTML/CSS/JS) [disponible en Français également](https://developer.mozilla.org/fr/).
- [Webplatform.org](https://developer.mozilla.org/): un site de ressource exhaustif maintenu par le W3C et la communauté.

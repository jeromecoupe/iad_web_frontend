# HTML & CSS: Introduction

IAD 2013-2014 - Jérôme Coupé

## Introduction

Avec CSS3, HTML5 représente une petite révolution dans le monde du développement front-end. HTML4 et ses successeurs sont parmi nous depuis 10 ans déjà et une évolution était nécessaire.

Depuis [l'annonce par le W3C de la fin des travaux sur XHTML2 en 2009](http://www.w3.org/News/2009#entry-6601), HTML5 reste le seul candidat en lice pour une refonte du langage structurant du web. Le travail sur la spécification HTML5 a commencé en 2004 et est un effort conjoint du W3C et du WHATWG Group. Même si cette spécification n'est pas encore terminée à l'heure actuelle, elle est néanmoins utilisable dès aujourd'hui.

HTML5 est à la fois un enrichissement du "vocabulaire" du HTML, mais aussi une tentative de faire du HTML un langage du web d'aujourd'hui: sémantique, applicatif (à travers les divers API) et réellement intégrateur de divers médias (sons, vidéos, élément CANVAS, etc.).

Ce cours est une introduction, nous ne verrons ici que les nouveaux éléments sémantiques introduits par HTML5. Les tags `video` et `audio`, ainsi que les nouveaux champs de formulaires seront également évoqués. L'élément `canvas` et les API de drag and drop, de géolocalisation et de stockage offline ne seront pas traitées dans le cadre de ce cours. 

Outre la [spécification HTML5](http://www.w3.org/TR/html5/), de nombreuses ressources telles que [webplateform.org](http://www.webplatform.org/), [HTML5 Rocks](http://www.html5rocks.com) et [Mozilla Developper Network (MDN)](https://developer.mozilla.org/) sont disponibles si ces sujets vous intéressent. Nous nous pencherons sur certains de ces sujet lors du cours de l'année prochaine.

Le livre "[HTML5 for Web Designer](http://books.alistapart.com/products/html5-for-web-designers)" par Jeremy Keith est une petite merveille de concision et est disponible en version Française. A conseiller également: "[Hardboiled Webdesign](http://hardboiledwebdesign.com/)" de Andy Clarke dont un chapitre est consacré à HTML5. La bible sur le sujet étant "[Introducing HTML5](http://introducinghtml5.com/)" par Bruce Lawson et Remy Sharp. Le WHATWG a également publié une [version de la spécification dédiée aux développeurs](http://developers.whatwg.org/).

Pour ce qui est de CSS, nous travaillerons essentiellement avec CSS2.1 et aborderons également des modules CSS3. Nous verrons d'avantage de ces modules CSS3 l'année prochaine.

Deux sites de ressources pour vérifier la compatibilité de votre code CSS / HTML avec les différents navigateurs: [caniuse.com](http://caniuse.com) (tables de support) et [html5please](http://html5please.com) (conseils d’utilisation et polyfill javascript renseignés).

## HTML5

### Document minimal

```html
<!DOCTYPE html>
<html lang=”en”>
	<head>
		<meta charset="utf-8" />
		<title>Example document</title>
	</head>
	<body>
		<p>Example paragraph</p>
	</body>
</html>
```

### Déclaration du type de document

Les divers navigateurs n’utilisent pas la déclaration de type de document (DTD) pour effectuer le rendu d’un document, la DTD permet néanmoins  aux outils de validation que vous utilisez de savoir dans quelle syntaxe est écrit votre document, afin de pourvoir le valider.

La DTD HTML5 est en fait la plus petite suite de caractères permettant à un navigateur de gérer une page en mode "standard" et non en mode "quirks". Afin de garder une compatibilité avec un code plus ancien, les navigateurs ont mis en place ce que l’on nomme le [doctype switching](http://www.ericmeyeroncss.com/bonus/render-mode.html), une idée de Todd Fahrner. Le mode "quirks" leur permet de gérer et d’afficher un code ne se conformant pas aux standards.

### Encodage de caractères

Il convient d'ajouter une balise meta précisant l'encodage de caractère utilisé dans votre document. Dans la plupart des cas, [un encodage UTF-8 est votre meilleur choix](http://www.w3.org/TR/html5/the-meta-element.html%23charset).

```html
<meta charset="utf-8" />
```

### Déclaration de la langue Utilisée

L'élément racine d'un document doit impérativement être l'élément `<html>` et celui-ci doit avoir comme attribut une déclaration de la langue utilisée principalement dans le document. Par exemple :

```html
<html lang="en">
```

### Règles syntaxiques XHTML

Notons ici que HTML5 existe en deux sérialisations: HTML et XHTML. Lors de ce cours, nous utiliserons la syntaxe XHTML, plus stricte, afin de créer un code propre et respectant les bonnes pratiques en vigueur. Afin de vérifier votre syntaxe, il existe un [LINT Tool pour HTML5](http://lint.brihten.com/html/).

Le XHTML n'est rien de plus que du HTML reformulé de façon à respecter les règles plus strictes du XML, il suffit d'appliquer quelques règles simples.

#### Chaque balise nécessite une fermeture

Toutes les balises présentes dans un document XHTML doivent être correctement fermées.

Invalide:

```html
<p>Lorem ipsum dolor sit amet. Praesent vel justo.
```

Valide:

```html
<p>Lorem ipsum dolor sit amet. Praesent vel justo.</p>
```

Les balises HTML ne possédant pas de balise de fin comme `<br>`, `<img>` ou `<hr>` doivent être fermées également. Selon la syntaxe XML, une balise de ce type se ferme en lui ajoutant une barre oblique (un slash) en fin de balise: `<br />` ou encore `<img />`.

Ne pas oublier d'inclure un espace entre le contenu de l'élément et la barre oblique sinon les anciens navigateurs peuvent ne pas interpréter la balise et l'ignorer.

#### Imbriquer correctement les éléments

Quand on ouvre une série de balises en cascades, (les unes à l'intérieur des autres), il faut les refermer dans l'ordre inverse de l'ordre d'ouverture.

Invalide:

```html
<p>Paragraphe avec texte en <strong>gras</p></strong>
```

Valide:

```html
<p>Paragraphe avec texte en <strong>gras</strong></p>
```

#### Utiliser des minuscules dans les balises et leurs attributs

Puisque XML est sensible à la casse, toutes les balises et tous leurs attributs doivent obligatoirement être écrits en lettres minuscules. Les valeurs d'attributs, par contre, peuvent toujours être écrites en majuscules. Pour des raisons de simplicité, il est conseillé de les écrire également en minuscules.

Invalide :

```html
<TEXTAREA ID="commentaire"></TEXTAREA>
```

Valide :

```html
<textarea id="commentaire"></textarea>
```

#### Valeurs d'attributs placées entre guillemets

Selon les règles de XML, l'utilisation de guillemets est une obligation. De plus, il ne peut plus y avoir de sauts de lignes dans la définition d'une valeur donnée.

Invalide:

```html
<div id=navigation></div>
```

Valide:

```html
<div id="navigation"></div>
```

#### Les formes abrégées d'attributs sont interdites

Certaines balises en HTML possédaient des attributs autonomes qui pouvaient être utilisés sans valeurs associées, comme c'était par exemple le cas pour la balise input avec laquelle on pouvait utiliser les attributs checked ou disabled. En XHTML ces attributs doivent être écrits de manière complète, en spécifiant l'attribut et sa valeur associée, même si cela représente une répétition :

Invalide:

```html
<option value="page.html" selected></option>
```

Valide:

```html
<option value="page.html" selected="selected"></option>
```

#### L'attribut `name` est remplacé par l'attribut `id`

L'attribut name, utilisé en HTML pour nommer les ancres, les images ou tout autre objet dans un document Web est remplacé dans ce rôle par l'attribut id en XHTML. Le principe de nommer un objet revenant à l'identifier de manière unique, le recours à l'attribut id permet de s'assurer que la communication par le DOM avec un objet identifié ne visera qu'un seul objet.

Invalide:

```html
<h1 name="titre">…</h1>
```

Valide:

```html
<h1 id="titre">…</h1>
```

#### Gestion des caractères spéciaux dans les déclarations CSS et JavaScript

La meilleure solution consiste à placer toutes les définitions de CSS ou de JavaScript dans des fichiers externes.

#### Encodage des caractères spéciaux dans les URL

Les caractères spéciaux présents dans les valeurs d'attributs s'avèrent également problématiques en XHTML. Il faut donc les encoder afin d'éviter que le navigateur ne les interprète de façon erronée. Ainsi, pour tous les caractères spéciaux comme "<", ">" ou "&" destinés à être interprétés tels quels, vous devrez plutôt inscrire `&lt;`, `&gt;` ou `&amp`;

Invalide:

```html
<a href="index.php?a=1&b=2" title="Articles & Nouvelles">
```

Valide:

```html
<a href="index.php?a=1&amp;b=2" title="Articles &amp; Nouvelles">
```

La bonne pratique veut de toute façon que vous encodiez l'ensemble des caractères spéciaux au sein de vos pages.

### Document Object Model (DOM) Structure d’un document HTML

Les éléments composant un document HTML sont structurés de façon hiérarchisée. Ils s’emboîtent les uns dans les autres, structurant le document sur le modèle d’un arbre.

```html
<!DOCTYPE html>
<html lang="fr">
	<head>
		<meta charset="utf-8" />
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

Cette forme d’arbre et d’emboîtement hiérarchisé est parfaitement visible dans des outils tels que [Firebug](https://addons.mozilla.org/en-US/firefox/addon/firebug/) ou [la barre d’outils développeurs de firefox](https://addons.mozilla.org/en-US/firefox/addon/web-developer/) ou encore dans les developper tools disponibles dans tous les navigateurs modernes (Chrome, Safari, Firefox, Opera)

Familiarisez-vous avec ces outils, vous en aurez besoin lors de ce cours et durant toute votre carrière de développeur front-end.

### Quelques efforts Pour une compatibilité maximale

Les navigateurs ne possèdent pas encore de styles par défaut pour les nouveaux éléments sémantiques de HTML5. Si vous tentez de mettre en forme un élément `<nav>` par exemple, vous ne verrez rien se produire dans votre navigateur favori, sauf si vous spécifiez le mode d'affichage de cet élément dans votre CSS via la propriété display.

```css
article, aside, details, figcaption, figure, footer, header, main, nav, section, summary
{
	display: block;
}
```

La version 9 d’Internet explorer gère les éléments HTML5 mais une étape supplémentaire est nécessaire pour les versions plus anciennes d'Internet Explorer. Ce navigateur gère les éléments inconnus du DOM différemment des autres, il lui faut un petit peu de Javascript pour qu'il se comporte comme les autres navigateurs.

Ce JS ne fait que créer ces nouveaux éléments dans le DOM à l'intention de IE, il suffit donc de le servir via l'utilisation de conditional comments et le tour est joué (du moins pour les utilisateur de IE disposant du JavaScript activé). [Une version compacte de ce script de Remy Sharp est disponible en ligne](http://code.google.com/p/html5shiv/). Ce HTML5 shiv est également inclus dans [Modernizr](http://www.modernizr.com) bien que la version include dans Modernizr 3.6.2 ne créée pas l’élément main.

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="utf-8" />
		<title>HTML 5 template</title>
		<!--[if lt IE 9]><script src="http://html5shiv.googlecode.com/svn/trunk/html5.js"></script><![endif]-->
	</head>
	<body>
		<p>Hello World</p>
	</body>
</html>
```

Il est important de noter que ces scripts créent de facto une dépendance à Javascript pour les utilisateurs de Internat Explorer < 9.

*Exercice: créer un starter kit en HTML5*

### HTML5: Une sémantique améliorée

L’une des pricipale nouveauté de HTML5, c’est l’introduction de nouveaux éléments sémantiques permettant une qualification plus précise des divers éléments de votre document. Certains comme Luke Stevens [arguent que l'utilisation de de ces éléments est problématique pour diverses raisons](http://www.truthabouthtml5.com/). A vous de voir.

Nous ne les présenterons pas l’ensemble de ces nouveaux éléments dans le cadre de ce cours mais nous vous présenterons les principaux. L'ensemble de ces nouveaux éléments et des renseignements sur leurs usages sont disponibles sur le site du W3C ou dans le glossaire rédigé pour vous par l'équipe de HTML5 Doctor.

#### Nouveaux élements

##### `<nav>`

Cet élément est utilisé pour marquer les interfaces de navigation du site ou de la page. Il s’agit d’une section de la page contenant les liens utilisé pour la navigation. Tous les groupes de liens ne sont pas forcément des interfaces de navigation, seuls ces derniers peuvent être marqués à l’aide de l’élément `<nav>`.

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

Notons ici que les éléments `acticle`, `section`, `nav` et `aside` sont des élements de sectioning, c’est à dire qu’ils créent une nouvelle section au sein du document et que la hiérarchie des titres recommence à zéro au sein de chacun des éléments de ce type. Voyons par exemple la structure de ce document à l’aide de l’outil HTML5 outliner pour y voir plus clair.

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="utf-8" />
		<title>Document outline and sectioning elements</title>
		<!--[if lt IE 9]>
			<script src="http://html5shiv.googlecode.com/svn/trunk/html5.js"></script>
		<![endif]-->
	</head>
	<body>
		<h1>My great site</h1>
		<nav>
			<ul>
				<li><a href="/">Nav item</a></li>
			</ul>
		</nav>
		<article>
			<h1>Article title</h1>
			<p>Article content.</p>
			<h2>Article sub-heading</h2>
			<p>More content.</p>
			<h3>Article sub-sub-heading</h3>
			<p>More content.</p>
		</article>
		<aside>
			<h1>Sidebar heading</h1>
			<p>content</p>
		</aside>
		<footer>
			<h1>Footer heading</h1>
			<p>Footer content.</p>
		</footer>
	</body>
</html>
```

##### `<main>`

L’élement `<main>` représente le contenu principal d’un document. Il ne peut être utilisé qu’une seule fois au sein d’un document HTML et ne peut jamais être le descendant de `<article>`, `<aside>`, `<footer>`, `<header>` or `<nav>`.

##### `<header>`

Typiquement utilisé pour contenir les métas informations (titre, logo, date de publication, etc) d’un document ou d’une partie d’un document. L'élément `<header>` peut être utilisé plusieurs fois dans le cadre d'un même document. Suivant le contexte dans lequel il est placé (`<body>`, `<article>`, `<section>`, etc.) il aura un statut différent.

##### `<footer>`

Typiquement utilisé pour contenir les métas informations (auteur, lien vers des documents liés) d’un document ou d’une partie de document. L'élément `<footer>` peut être utilisé plusieurs fois dans le cadre d'un même document. Suivant le contexte dans lequel il est placé (`<body>`, `<article>`, `<section>`, etc.) il aura un statut différent. Notons que les coordonnées de contact mentionnées dans un `<footer>` devraient êtres marqués à l'aide de l'élément `<address>`

##### `<time>`

Est utilisé pour marquer des données temporelles (dates, heures etc.) de façon à ce qu'elles soient lisibles et exploitables par des machines ou programmes. Un attribut datetime peut également être ajouté afin de préciser les choses si le textes marqué n'est pas une date grégorienne valide.

```html
<time datetime="2007-10-05">October 5</time>
<p>I usually have a snack at <time>16:00</time>.</p>
<p>posted on <time datetime="2009-04-12" pubdate="pubdate">12 April 2009</time> by Jérôme Coupé</p>
```

`<figure>` et `<figcaption>`
Est utilisé pour marquer du contenu qui pourrait être retiré du document sans que cela n'affecte le sens de ce dernier. Cet élément peut être utilisé pour marquer des images, des graphiques, des éléments de code qui sont mentionnés dans le document mais qui pourrait en être extraits (pour figurer dans une annexe ou en marge) sans nuire au sens de ce dernier.

```html
<figure>
	<p><img src="img/small_snowman.jpg" alt="Terrasse-sized snowman" width="180" height="240" /></p>
	<figcaption>Small snowman we made on our little terrace</figcaption>
</figure>
```

#### redefinition d’éléments existants

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

#### Video Audio et Figure avec HTML5

Un autre aspect intéressant de HTML5 concerne la possibilité de gérer nativement les éléments audios et vidéos d'une page sans faire appel à des technologies extérieures telles que Flash.

En théorie, c'est aussi facile d'intégrer une vidéo ou un fichier audio que d'intégrer une image. En pratique, c'est un peu plus compliqué.

Les navigateurs prenant en charge cet élément ne gèrent pas tous les mêmes formats et codecs, ce qui oblige à prévoir différents encodages du même fichier audio ou vidéo;

##### Vidéo

- Le format open source .ogv (Codec: Theora) est supporté par Firefox 3.5, Chrome 3 et certaines versions
encore expérimentales de Opéra.
- Le format .mp4 (Codec: H.264) est supporté par Safari 4 et Chrome 3

Certains navigateurs supportant l'élément `<video>` commencent automatiquement à télécharger les fichiers vidéos, ce qui donne lieu à un usage (important) de bande passante sans intervention utilisateur. L’attribut `preload` peut être utilisé pour empêcher le preload de la video par le navigateur preload=”none”`;

Internet Explorer ne supportant pas les tags `<video>` ou `<audio>`, il faut prévoir des solutions de fallback qui sont parfois complexes (et recourent le plus souvent à Flash). [Voir à ce sujet l’exemple "video for everybody”](http://camendesign.com/code/video_for_everybody).

Voici néanmoins à quoi cela ressemble aujourd'hui:

```html
<video height="270" width="480" poster="waitimage.png" controls="controls">
	<source src="samplevideo.mp4" type="video/mp4" />
	<source src="samplevideo.ogv" type="video/ogg" />
	<source src="samplevideo.webm" type="video/webm" />
	<p>Your browser does not support the HTML5 video tag but you can download the file either in <a href="samplevideo.mp4">MP4</a>, <a href="samplevideo.ogv">OGV</a>, <a href="samplevideo.webm">WEBM</a></p>
</video>
```

L'attribut poster sert à donner une image d'attente dans les navigateurs supportant l'élément vidéo, tandis que l'attribut controls sert à afficher les contrôles minimaux pour le type de média choisi.

Si vos besoins en vidéo sont importants, des services tels que Youtube et Vimeo un moyen efficace de servir des vidéos sur le web. Ils réalisent automatiquement les divers encodages nécessaires, le type de plateforme utilisé par le visiteur, etc.

Des librairies JavaScript comme mediaelement.js sont également une option intéressante.

##### Audio

- Le format open source .ogg (Codec: Vorbis) est supporté par Firefox 3.5, Chrome 3
- Le format .mp3 est supporté par Safari 4
- Le format .wav est supporté par Firefox 3.5, Chrome 3, Opera 10 et Safari 4

```html
<audio controls="controls">

##### Figure et figcaption

Les élément figure et figcaption servent à grouper images et légendes dans vos docuents HTML5.

```html
<figure>
	<img src="soleil.jpg" alt="Une journée ensoleillée à Louvain-la-Neuve">
	<figcaption>La grand-place et les terrasses par une journée ensoleillée à Louvain-la-Neuve.</figcaption>
</figure>
```
*Exercice: intégration d'une video dans un document HTML5*

#### Formulaires et HTML5

La spécification HTML5 permet également l'utilisation de contrôles de formulaires plus avancés que ceux dont disposait jusqu'ici la spécification HTML.

De nouveaux types de champs sont mis à la disposition des développeurs: email, url, date et range n'en sont
que quelques uns.

```html
<input type="email" name="useremail" id="useremail" required="required" />
<input type="url" name="userurl" id="userurl" />
<input type="range" min="2000" max="2050" value="2022" />
```

Ces nouveaux champs permettent entre autre une validation automatique du format des données entrées par les utilisateurs. La plupart de ces nouveaux éléments ne fonctionnent aujourd'hui qu'avec Opéra. Ceci étant dit, la plupart se dégradent élégamment dans les autres navigateurs (sous la forme de champs de type texte pour la plupart).

HTML5 permet également l'utilisation de nouveaux attributs pour les champs de formulaires. En voici quelques uns parmi les plus utiles (du moins à mon avis).

Le nouvel attribut placeholder permet de spécifier un texte dans un champ tant que celui-ci n'est pas rempli ni activé. Lorsque l'utilisateur active le champ de formulaire, ce texte disparait. Cet attribut est pour le moment supporté uniquement par Safari 4 et Chrome 3.

```html
<input type="tel" name="gsm" id="gsm" placeholder="+32475335162" />
```

Pour sa part, l'attribut autofocus permet d'activer un champ de formulaire dès la page chargée.

```html
<input type="search" name="search" id="search" autofocus="autofocus" />
```

Intéressant également, l'attribut required permettant de spécifier un champ comme obligatoire dans le cadre d'un formulaire HTML5.

```html
<input type="text" name="name" id="name" required="required" />
```

Pour ceux qui veulent en savoir plus, [un excellent article introductif est disponible sur 24 Ways](http://24ways.org/2009/have-a-field-day-with-html5-forms/) et une [démonstration a été mise en ligne par Opéra](http://devfiles.myopera.com/articles/67/example.html). Les [quelques pages de Mark Pilgrim sur le sujet](http://diveintohtml5.info/) sont également intéressantes, même si [la spécification HTML5 reste évidemment la source faisant autorité](http://dev.w3.org/html5/markup/Overview.html).

*Exercice: créer un formulaire en HTML5*

#### L'élément Canvas

HTML5 permet également d'utiliser l'élément `<canvas>` pour réaliser des dessins en 2D à l'aide de javascript. Il est possible de réaliser des graphiques en temps réel, des compositions à base d'images et de sons, des transformations, des animations, etc. Une petite introduction par les gens d'Opera Software peut être ?

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

Lors de ce cours, nous utiliserons principalement CSS 2.1 et quelques éléments de CSS3. A partir de CSS3, la spécification CSS est passée d’une spécification monolithique à une spécification modulaire, plus flexible. Une plus grande modularité permet aux navigateurs d’implémenter l’un ou l’autre module, sans pour autant devoir implémenter la spécification dans son ensemble.

### Lier une feuille de style à un document HTML

Les déclarations CSS peuvent être liées de 4 façons à un document HTML afin d’en gérer l’affichage :

#### CSS liées

C'est la méthode la plus utilisée dans la mesure où elle permet de séparer vos styles (CSS) de votre structure et de votre contenu de document (HTML). C'est 
égalmement la méthode la plus performante, [comme le précise Steve Souders](http://www.stevesouders.com/blog/2009/04/09/dont-use-import/).

```html
<link rel="stylesheet" href="css/main.css" />
```

#### CSS importées

```html
<style>@import url(css/main.css);</style>
```

#### CSS en ligne

```html
<style>body {background:#fff;}</style>
```

#### CSS dans l’attribut style des balises

```html
<p style="color:blue;">
```

### CSS et types de media

Les types de media permettent d’appliquer les feuilles de style en fonction du media avec lequel les documents HTML sont lus. La mise en page du document sera gérée différemment selon qu’il est imprimé sur papier, affiché à l’écran ou encore lu par un navigateur vocal.

Les divers types de media disponibles sont les suivants :

- braille
- embossed
- handheld
- print
- projection
- screen
- speech
- tty
- tv

Le support de ces divers types de media est encore partiel et présente de nombreux problèmes. Les types de media screen et print sont les plus largement et les mieux supportés.

Certaines propriétés CSS sont destinées à un seul type de media (voice-family par exemple), alors que d’autres peuvent être utilisées avec plusieurs types de media (font).

Il est possible d’utiliser les types de media avec plusieurs des façons de lier une CSS à un document (X)HTML

CSS liées

```html
<link rel="stylesheet" href="css/main.css" media="screen" />
```

CSS importées

```html
<style media="print">@import url(css/print.css)</style>
```

CSS en ligne

```html
<style media="screen">
	body {background:#fff;}
</style>
```

*Exercice: lier une feuille de style à un document HTML5 et tester l'attribut media*

### Anatomie d’une déclaration CSS

```html
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

Ressources: [une explication ludique basée sur Star Wars et proposée par Andy Clarke](http://www.stuffandnonsense.co.uk/archives/css_specificity_wars.html).

#### Exemples

	p = 0,0,1
	p.last = 0,1,1
	#content p.last = 1,1,1

	!important et sélecteur universel
	l’ajout de !important à une déclaration CSS permet de passer outre ce calcul de spécificité.
	Le sélecteur universel (*) possède une spécificité de 0,0,0

### Les sélecteurs CSS

Nous verrons ici les sélecteurs présents en CSS 2.1 pour commencer. Notez simplement que CSS3 comporte un module de sélecteurs plus étendu que nous verrons en détail l’année prochaine.

Certains de ces sélecteurs CSS utilisent les relations entre les éléments au sein de l’arbre structurant un document HTML.

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="utf-8" />
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
	color:red ;
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
p em:first-child 
{
	font-weight:bold;
}
```

##### Lang

```css
li:lang(fr) {color:red ;}
```

Les pseudo-classes appliquées aux liens fonctionnent bien dans l’ensemble des navigateurs modernes. IE 5, 5.5 et 6 ne supportent pas les pseudo-classes appliquées à autre chose que les liens et ne supportent pas les pseudo-classes lang et `:first-child`. IE7 supporte les pseudo-classes appliquées a d’autres éléments que les liens et supporte également :fist-child. :lang n’est pas supporté. IE8 supporte l’ensemble des pseudo-classes de CSS 2.1

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

Nous ne développerons pas ici toutes les propriétés CSS existantes et nous contenterons de les voir aux travers des exercices et exemples. Pour une documentation complète, se reporter au document du W3C sur le sujet: Recommandation CSS 2.1.

## Le modèle de mise en forme CSS

CSS utilise un modèle de mise en forme basé sur les boîtes (“box model” en anglais). Chaque élément d’un document existe dans le cadre d’une de ces boîtes.
	
La plupart de ces boîtes se comportent comme des blocs conteneurs pour les boîtes qui en sont les descendantes : on dit que la boîte "établit" le bloc conteneur de ses descendants. L'expression "le bloc conteneur d'une boîte" ("containing block" en anglais) signifie "le bloc conteneur dans lequel se trouve la boîte", et non la propre boîte que celle-ci génère.

Le bloc conteneur est utilisé afin de déterminer la position des boîtes qu’il renferme et, dans certains cas, les dimensions de ces boîtes. Par exemple, si un élément possède une largeur de 50%, celle-ci sera calculée par rapport à la largeur de son bloc conteneur.

Pour tout élément qui n’est pas absolument positionné, le bloc conteneur est la zone de contenu de son ancêtre de type block le plus proche dans l’arbre du document. Si aucun n’existe, la fenêtre du navigateur sert de bloc conteneur. Nous aborderons cela plus en profondeur lorsque nous parlerons des divers types de positionnement.

Les diverses dimensions de ces boîtes sont gérées par les propriétés CSS suivantes: width, height, padding, margin et border.

- La largeur totale d’une boîte se calcule de la façon suivante : largeur du contenu (width) + padding + borders + margin.
- La hauteur totale d’une boîte se calcule de la façon suivante : hauteur du contenu (height) + padding + borders + margin.

La propriété **CSS3** `box-sizing` permet de changer ce comportement de base et est supportée dans tous les navigateurs modernes et dans IE8+.

- `box-sizing: border-box;` modifie le modèle par défaut. La hauteur et la largeur de l’élément sont toujours égales aux valeurs de width / height, les valeurs de padding et de border en sont soustraites.
- `box-sizing: content-box;` correspond au modèle par défaut. La hauteur et la largeur de l’élement se calcule en additionnant width / height et padding, margin et border.

Voir à ce sujet [l'article de Paul Irish](http://www.paulirish.com/2012/box-sizing-border-box-ftw/).

### éléments en blocs et en lignes

Deux types de boîtes principales sont liées par défaut aux divers éléments du HTML : on parle d’éléments de type block (`<p>`,`<div>`, `<blockquote>` et `<h1>` par exemple) et de type inline (`<a>`, `<strong>`, `<em>`, `<span>`, `<img>` par exemple).

- Un élément block génère une boîte de bloc qui prend toujours un maximum d’espace horizontal, sauf si sa largeur est définie ou si la propriété float lui est appliquée. Les éléments block se placent, dans le flux du document, les uns en dessous des autres (par exemple : une suite de paragraphes ou une liste).
- Un élément inline génère une boîte en ligne. Ces éléments inline se placent toujours, dans le flux du document, les uns à côté des autres (par exemple : plusieurs `<span>` ou une partie de texte mise en gras à l’aide de la balise `<strong>`)

### Autres valeurs possibles
Toutes sortes de boites peuvent être générées à l’aide de la propriété CSS display : `none`, `inline`, `block`, `list-item`, `inline-block`, `inline-table`,`table`, `table-caption`, `table-cell`,`table-column.`,`table-column-group`, `table-footer-group`, `table-header-group`, `table-row`, `table-row-group`.

Nous nous contenterons ici d’en détailler quelques unes parmi les plus courantes. Pour une explication plus détaillée, vous pouvez vous référer au document du W3C sur le sujet: Recommendation CSS 2.1.

#### Inline-Block

Nous verons plus loin que cette valeur peut être très utile pour contrôler les padding et les margin sur des éléments inline. Malheureusement, IE7 ne la supporte que si elle est appliquée à des éléments ayant un display par défaut de inline (`<a>`, `<em>`, `<strong>`, etc.). Cette valeur est également utilisée pour générer des grilles en CSS. 

Nous verons l'année prochaine qu'lle peut s'avérer très utile pour le responsive web design. Attention également à bien contrôler le white-space lorsque vous utilisez cette propriété. [Chris Coyier vous détaille les techniques utilisables](http://css-tricks.com/fighting-the-space-between-inline-block-elements/).

#### List-item

Les éléments de liste ne sont ni des balises de type block, ni des balises de type inline. Ils ont un comportement différent. En attribuant à un élément la déclaration CSS `display:list-item`, il pourra supporter les propriétés suivantes : `list-style-type`, `list-style-image`, `list-style-position` et `list-style`.

#### None

Cette valeur fait qu'aucune boîte n'est générée par l'élément dans la structure de formatage (cet élément n'a pas d'influence sur la mise en forme du document). Les éléments auxquels cette propriété est appliquée ne s’affichent pas dans le media concerné. Les éléments qui en descendent ne génèrent pas de boîtes non plus et il n’est plus possible de modifier leur comportement avec la propriété `display`.

Une valeur `none` ne crée pas de boîte invisible, elle ne crée pas de boîte du tout. CSS comprend des mécanismes permettant la génération de boîtes qui influencent la mise en forme mais qui ne sont pas visibles (propriété visibility en CSS).

#### Les valeurs liées aux tableaux

Les valeurs liées aux tableaux : `inline-table`,`table`,`table-caption`,`table-cell`,`table-column.`,`table-column-group`,`table-footer-group`,`table-header-group`,`table-row`,`table-row-group` donnent à un élément le comportement de celui d'une table ou d’un de ses composants.

### La fusion des marges



- Deux paragraphes se suivant et ayant respectivement une marge inférieure de 10px et une marge supérieure de 15px seront séparés par 15px.
- Deux paragraphes se suivant et ayant respectivement une marge inférieure de -10px et une marge supérieure de 30px seront séparés par 20px.
 -Deux paragraphes se suivant et ayant respectivement une marge inférieure de -10px et une marge supérieure de -15px seront séparés par -15px.

#### Parent et premier/dernier enfant

Les marges entre un parent et son premier/dernier enfant ne fusionnent pas si le parrent possède une `border`, un `padding`, une `height` ou une `min-height`. spécifiée.

Les marges entre un parent et ses enfants ne fusionnent pas si le parent possède une propriété overflow avec une valeur autre que visible. 

*Exercice sur la fusion des marges*

## Mises en page CSS

















```

La génération de contenu à l’aide des CSS permet également de forcer un élément parent à contenir ses éléments enfants en mode float. Cette technique est expliquée en détail [par Big John et Holly Bergevin sur leur site "Position Is Everything"](http://www.positioniseverything.net/easyclearing.html) [Une variante plus moderne reposant sur les pseudo-éléments :before et :after a été développée par Nicolas Gallagher](http://nicolasgallagher.com/micro-clearfix-hack/). Ces solutions genèrent un élement à l'aide de CSS et lui applquent un `clear:both;`, émulant ainsi la solutin vue plus haut.


*Exercice: expériementer avec float et clearing*



```html
	<div class="primary">
		<h1>Demo</h1>
		<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quam, amet tenetur obcaecati similique ea quas quaerat modi nam quos nobis soluta odit nemo voluptate enim alias facere harum itaque! Ut!</p>
		<p>Quasi itaque veritatis excepturi at adipisci libero nesciunt. Natus, voluptatibus, autem, id placeat facilis incidunt laudantium eos asperiores aperiam molestias quas architecto unde dolorem necessitatibus eius. Placeat facere quae voluptate.</p>
		<p>Eligendi, commodi, similique nobis quae natus non repellendus tempora voluptate dignissimos eos eaque explicabo atque ipsam et rem fugit animi fugiat. Adipisci, nihil, ratione totam sed blanditiis cumque tempora odit!</p>
		<div class="sitefooter">
			<p>Footer</p>
		</div>
	</div>
	<div class="secondary">
		<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Repellendus, aut, optio, nisi, tenetur possimus vero hic enim quibusdam in voluptas ab voluptatum sequi corrupti maxime dolorum perspiciatis nihil soluta odio.</p>
	</div>
</div>
```

CSS

```css
.wrapper
{
	margin:0 auto;
	width:960px;
	position:relative; /*positioning context*/
	background:green;
}

.primary
{
	margin-left:340px;
	padding:20px;
	background:yellow;
}

.secondary
{
	position:absolute;
	top:0;
	left:0;
	width:260px;
	padding:20px;
	background:red;
}

.sitefooter
{
	padding:20px;
	background:#ccc;
}
```

*Exercice: réaliser une mise en page fixe avec positionnement absolu / fixe et marges (2 et 3 colonnes)*

```html
	<div class="siteheader">
		<p>Header</p>
	</div>
	<div class="content-primary">
		<h1>Demo</h1>
		<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quam, amet tenetur obcaecati similique ea quas quaerat modi nam quos nobis soluta odit nemo voluptate enim alias facere harum itaque! Ut!</p>
		<p>Quasi itaque veritatis excepturi at adipisci libero nesciunt. Natus, voluptatibus, autem, id placeat facilis incidunt laudantium eos asperiores aperiam molestias quas architecto unde dolorem necessitatibus eius. Placeat facere quae voluptate.</p>
		<p>Eligendi, commodi, similique nobis quae natus non repellendus tempora voluptate dignissimos eos eaque explicabo atque ipsam et rem fugit animi fugiat. Adipisci, nihil, ratione totam sed blanditiis cumque tempora odit!</p>
	</div>
	<div class="content-secondary">
		<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Repellendus, aut, optio, nisi, tenetur possimus vero hic enim quibusdam in voluptas ab voluptatum sequi corrupti maxime dolorum perspiciatis nihil soluta odio.</p>
	</div>
	<div class="sitefooter">
		<p>Footer</p>
	</div>
</div>
```

CSS

```css
.wrapper
{
	width:960px;
	margin:0 auto;
	overflow:hidden; /*float containment*/
}

.content-main
{
	float:right;
	width:620px;
	background:yellow;
}

.content-secondary
{
	float:left;
	width:300px;
	background:green;
}

.footer
{
	clear:both;
	background:red;
}


propriétés CSS permettent de contrôler efficacement les longueurs de lignes.
<div class="wrapper">
	<div class="primary">
		<h1>Demo</h1>
		<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quam, amet tenetur obcaecati similique ea quas quaerat modi nam quos nobis soluta odit nemo voluptate enim alias facere harum itaque! Ut!</p>
		<p>Quasi itaque veritatis excepturi at adipisci libero nesciunt. Natus, voluptatibus, autem, id placeat facilis incidunt laudantium eos asperiores aperiam molestias quas architecto unde dolorem necessitatibus eius. Placeat facere quae voluptate.</p>
		<p>Eligendi, commodi, similique nobis quae natus non repellendus tempora voluptate dignissimos eos eaque explicabo atque ipsam et rem fugit animi fugiat. Adipisci, nihil, ratione totam sed blanditiis cumque tempora odit!</p>
		<div class="sitefooter">
			<p>Footer</p>
		</div>
	</div>
	<div class="secondary">
		<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Repellendus, aut, optio, nisi, tenetur possimus vero hic enim quibusdam in voluptas ab voluptatum sequi corrupti maxime dolorum perspiciatis nihil soluta odio.</p>
	</div>
</div>


.wrapper
{
	margin:0 auto;
	width:80%;
	min-width:600px;
	max-width:1140px;
	position:relative; /*positioning context*/
	background:green;
}

.primary
{
	margin-left:35%;
	padding:2%;
	background:yellow;
}

.secondary
{
	position:absolute;
	top:0;
	left:0;
	width:26%;
	padding:2%;
	background:red;
}

.sitefooter
{
	padding:2%;
	background:#ccc;
}


HTML

```html
<div class="wrapper">
	<div class="siteheader">
		<p>Header</p>
	</div>
	<div class="content-primary">
		<h1>Demo</h1>
		<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quam, amet tenetur obcaecati similique ea quas quaerat modi nam quos nobis soluta odit nemo voluptate enim alias facere harum itaque! Ut!</p>
		<p>Quasi itaque veritatis excepturi at adipisci libero nesciunt. Natus, voluptatibus, autem, id placeat facilis incidunt laudantium eos asperiores aperiam molestias quas architecto unde dolorem necessitatibus eius. Placeat facere quae voluptate.</p>
		<p>Eligendi, commodi, similique nobis quae natus non repellendus tempora voluptate dignissimos eos eaque explicabo atque ipsam et rem fugit animi fugiat. Adipisci, nihil, ratione totam sed blanditiis cumque tempora odit!</p>
	</div>
	<div class="content-secondary">
		<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Repellendus, aut, optio, nisi, tenetur possimus vero hic enim quibusdam in voluptas ab voluptatum sequi corrupti maxime dolorum perspiciatis nihil soluta odio.</p>
	</div>
	<div class="sitefooter">
		<p>Footer</p>
	</div>
</div>
``

CSS

.wrapper
{
	margin:0 auto;
	width:80%;
	min-width:600px;
	max-width:1140px;
	background:green;
}

.siteheader
{
	padding:2%;
	background:#ccc;
}

.content-primary
{
	float:left;
	padding:2%;
	width:61%;
	background:yellow;
}

.content-secondary
{
	float:right;
	padding:2%;
	width:26%;
	background:red;
}

.sitefooter
{
	clear:both;
	padding:2%;
	background:#ccc;
}


```html
	<div class="siteheader">
		<p>Header</p>
	</div>
	<div class="content-primary">
		<div class="content-primary-inner">
			<h1>Demo</h1>
			<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quam, amet tenetur obcaecati similique ea quas quaerat modi nam quos nobis soluta odit nemo voluptate enim alias facere harum itaque! Ut!</p>
			<p>Quasi itaque veritatis excepturi at adipisci libero nesciunt. Natus, voluptatibus, autem, id placeat facilis incidunt laudantium eos asperiores aperiam molestias quas architecto unde dolorem necessitatibus eius. Placeat facere quae voluptate.</p>
			<p>Eligendi, commodi, similique nobis quae natus non repellendus tempora voluptate dignissimos eos eaque explicabo atque ipsam et rem fugit animi fugiat. Adipisci, nihil, ratione totam sed blanditiis cumque tempora odit!</p>
		</div>
	</div>
	<div class="content-secondary">
		<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Repellendus, aut, optio, nisi, tenetur possimus vero hic enim quibusdam in voluptas ab voluptatum sequi corrupti maxime dolorum perspiciatis nihil soluta odio.</p>
	</div>
	<div class="sitefooter">
		<p>Footer</p>
	</div>
</div>
```

CSS

```css
.wrapper
{
	margin:0 auto;
	width:80%;
	min-width:600px;
	max-width:1140px;
	background:green;
}

.siteheader
{
	padding:2%;
	background:#ccc;
}

.content-primary
{
	float:left;
	width:100%;
	margin-right:-300px;
	background:yellow;
}

.content-primary-inner
{
	margin-right:340px;
	padding:2%;
	background:teal;
}

.content-secondary
{
	float:right;
	width:260px;
	padding:20px;
	background:red;
}

.sitefooter
{
	clear:both;
	padding:2%;
	background:#ccc;
}
```








	list-style:none;
	margin:0;
	padding:0;
}
{
	display:block;
	padding:.5em 1em;
	background:#ccc;
	color:#000;
}

.nav-v a:hover
{
	background:#000;
	color:#fff;
}
```

	list-style:none;
	margin:0;
	padding:0;
	background:#ccc;
	overflow:hidden; /*float containment: clearfix can also be used*/
}
{
	float:left;
	padding:.5em 1em;
	background:#ccc;
	color:#000;
}

.nav-v a:hover
{
	background:#000;
	color:#fff;
}
```

*Exercice: réaliser des interfaces de navigation à partir de listes*
```


```css
```
centrer un élément de type block quel que soit le navigateur utilisé.
```


```css
	
	
```css
	position:absolute; 
	overflow:hidden; 
	clip:rect(0 0 0 0); 
	height:1px; width: 1px; 
	margin:-1px;
	padding:0;
	border:0; 
}
```
```

*Exercice: expérimenter avec faux columns*

```





```


```




lien hypertexte.


```css




```css
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

## Debugging

### Dans le doute … validez





```










## Ressources Complémentaires

- [A beginner's guide to HTML & CSS](http://learn.shayhowe.com/html-css/) par Shay Howe: un bon résumé des bases en HTML et CSS
- [Highly Maintainable, Efficient, and Optimized CSS](http://zomigi.com/blog/maintainable-efficient-css/) par Zoe Mickley Gillenwater: quelques bonnes informations sur les "best practises" en matière de CSS.
- [caniuse.com](http://caniuse.com): tables de support navigateurs pour HTML5 et CSS3
- [html5please](http://html5please.com): conseils d’utilisation pour HTML5 et CSS3. Polyfill javascript renseignés.
- [Mozilla Developer Network](https://developer.mozilla.org/): une bonne référence exhausitive sur les technologies du web (HTML/CSS/JS) [disponible en Français également](https://developer.mozilla.org/fr/).
- [Webplatform.org](https://developer.mozilla.org/): un site de ressource exhaustif maintenu par le W3C et la communauté. 
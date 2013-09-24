# HTML & CSS: Introduction

IAD 2013-2014 - Jérôme Coupé

## Introduction

Avec CSS3, HTML5 représente une petite révolution dans le monde du développement front-end. HTML4 et ses successeurs sont parmi nous depuis 10 ans déjà et une évolution était nécessaire.

Depuis [l'annonce par le W3C de la fin des travaux sur XHTML2 en 2009](http://www.w3.org/News/2009#entry-6601), HTML5 reste le seul candidat en lice pour une refonte du langage structurant du web. Le travail sur la spécification HTML5 a commencé en 2004 et est un effort conjoint du W3C et du WHATWG Group. Même si cette spécification n'est pas encore terminée à l'heure actuelle, elle est néanmoins utilisable dès aujourd'hui.

HTML5 est à la fois un enrichissement du "vocabulaire" du HTML, mais aussi une tentative de faire du HTML un langage du web d'aujourd'hui: sémantique, applicatif (à travers les divers API) et réellement intégrateur de divers médias (sons, vidéos, élément CANVAS, etc.).

Ce cours est une introduction, nous ne verrons ici que les nouveaux éléments sémantiques introduits par HTML5. Les tags `video` et `audio`, ainsi que les nouveaux champs de formulaires seront également évoqués. L'élément `canvas` et les API de drag and drop, de géolocalisation et de stockage offline ne seront pas traitées dans le cadre de ce cours. 

Outre la [spécification HTML5](http://www.w3.org/TR/html5/), de nombreuses ressources telles que [webplateform.org](http://www.webplatform.org/), [HTML5 Rocks](http://www.html5rocks.com) et [Mozilla Developer Network (MDN)](https://developer.mozilla.org/) sont disponibles si ces sujets vous intéressent. Nous nous pencherons sur certains de ces sujet lors du cours de l'année prochaine.

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

#### L'attribut `name` est remplacé par l'attribut `id` pour créer des ancres

L'attribut `name`, utilisé en HTML pour nommer les ancres est remplacé dans ce rôle par l'attribut `id` en XHTML. Le principe de nommer un objet revenant à l'identifier de manière unique, le recours à l'attribut `id` permet de s'assurer que la communication par le DOM avec un objet identifié ne visera qu'un seul objet.

L'attribut `name` reste utilisé dans d'autres contextes que les ancres, comme par exemple pour nommer les champs de formulaires.

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

Cette forme d’arbre et d’emboîtement hiérarchisé est parfaitement visible dans des outils tels que [Firebug](https://addons.mozilla.org/en-US/firefox/addon/firebug/) ou [la barre d’outils développeurs de firefox](https://addons.mozilla.org/en-US/firefox/addon/web-developer/) ou encore dans les developer tools disponibles dans tous les navigateurs modernes (Chrome, Safari, Firefox, Opera)

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

Ce JS ne fait que créer ces nouveaux éléments dans le DOM à l'intention de IE, il suffit donc de le servir via l'utilisation de conditional comments et le tour est joué (du moins pour les utilisateur de IE disposant du JavaScript activé). [Une version compacte de ce script de Remy Sharp est disponible en ligne](http://code.google.com/p/html5shiv/). Vous pouvez le télécharger ou lier vers une version hébergée sur google code.

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

Ce HTML5 shiv est également inclus dans [Modernizr](http://www.modernizr.com). Attention cependant, [la version du shiv incluse dans Modernizr 3.6.2 ne générère pas l’élément `<main>`](http://drublic.de/blog/add-main-element-modernizr/). [La version 3 de Modernizr incluera la dernière version du shiv](https://github.com/Modernizr/Modernizr/pull/837) et permettra également de gérer `<main>` dans les versions de IE < 9. 

Il est important de noter que ces scripts créent de facto une dépendance à Javascript pour les utilisateurs de Internat Explorer < 9.

*Exercice: créer un starter kit en HTML5*

### HTML5: Une sémantique améliorée

L’une des pricipale nouveauté de HTML5, c’est l’introduction de nouveaux éléments sémantiques permettant une qualification plus précise des divers éléments de votre document. Certains comme Luke Stevens [arguent que l'utilisation de de ces éléments est problématique pour diverses raisons](http://www.truthabouthtml5.com/). A vous de voir.

Nous ne présenterons pas l’ensemble de ces nouveaux éléments dans le cadre de ce cours mais nous vous présenterons les principaux. L'ensemble de ces nouveaux éléments et des renseignements sur leurs usages sont disponibles sur le site du W3C ou dans [le glossaire rédigé pour vous par l'équipe de HTML5 Doctor](http://html5doctor.com/element-index/).

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
<p>posted on <time datetime="2009-04-12">12 April 2009</time> by Jérôme Coupé</p>
```

##### `<figure>` et `<figcaption>`

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
<audio controls="controls">	<source src="elvis.ogg" />	<source src="elvis.mp3" />	<p><strong>Your browser does not support the HTML5 audio tag but you can download the file either in <a href="elvis.ogg">OGG format</a> or in <a href="elvis.mp3">MP3 format</a></strong></p></audio>```

##### Figure et figcaption

Les élément figure et figcaption servent à grouper images et légendes dans vos documents HTML5.

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
p em:last-child 
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
Cette expression "Collapsing Margins" signifie que les marges adjacentes de plusieurs boîtes peuvent se combiner afin de ne plus en former qu’une seule.Les marges verticales de deux boîtes (ou plus) d'éléments de type bloc, placés dans un flux normal fusionnent. La largeur de la marge finale devient la valeur la plus grande parmi celles des marges adjacentes.
Dans le cas de marges négatives, on soustrait la plus grande des valeurs des marges négatives adjacentes (en valeur absolue) de la plus grande des marges positives adjacentes. S'il n'y pas de marges positives, on déduit de zéro la plus grande (en valeur absolue) des marges négatives.

- Deux paragraphes se suivant et ayant respectivement une marge inférieure de 10px et une marge supérieure de 15px seront séparés par 15px.
- Deux paragraphes se suivant et ayant respectivement une marge inférieure de -10px et une marge supérieure de 30px seront séparés par 20px.
 -Deux paragraphes se suivant et ayant respectivement une marge inférieure de -10px et une marge supérieure de -15px seront séparés par -15px.#### Elements adjascentsLes marges des blocs flottants et de tout autre bloc ne fusionnent jamais, comme les marges entre des blocs absolument et relativement positionnés;Les marges entre des boîtes ne fusionnent pas si l'une des boite est en display:inline-block;La marge supérieure d'un élément auquel la propriété `clear` est appliquée et placé après un ou plusieurs élément floatés ne sera pas visible sauf si elle excède la hauteur du/des blocs floatés.

#### Parent et premier/dernier enfant

Les marges entre un parent et son premier/dernier enfant ne fusionnent pas si le parrent possède une `border`, un `padding`, une `height` ou une `min-height`. spécifiée.

Les marges entre un parent et ses enfants ne fusionnent pas si le parent possède une propriété overflow avec une valeur autre que visible. Pour en savoir plus concernant la fusion des marges, lire les excellents articles de [Andy Budd](http://www.andybudd.com/archives/2003/11/no_margin_for_error/) et [Eric Meyer](http://www.complexspiral.com/publications/uncollapsing-margins/).

*Exercice sur la fusion des marges*

## Mises en page CSSCes diverses boîtes dont nous avons parlées sont utilisées dans le cadre de différents schémas de positionnement qui sont autant d’outils permettant de créer une mise en page à l’aide de CSS.
### Schémas de positionnement CSSIl existe trois modes ou schémas de positionnement en CSS 2 .1: static (relative), absolute (fixed ) et float. Les modes de positionnement relatif et fixe sont des cas particuliers des modes statique et absolu. Chacun de ces modes obéit à ses règles propres.
Les modes de positionnement sont gérés en CS 2.1 via les propriétés position et float.#### Flux normal: positionnement statique et positionnement relatif##### Flux du document et positionnement statiqueLe flux normal du document est le mode par défaut utilisé pour le positionnement. C’est celui qui s’applique à tous les éléments lorsque ceux-ci ne sont pas ni en mode float ni positionnés de façon absolue. Il s’agit alors d’un positionnement en mode statique.Dans le flux normal du document, les éléments de type block sont positionnés les uns sous les autres et leurs marges verticales fusionnent, tandis que les éléments de type inline se suivent sur la même ligne et passent à une nouvelle ligne lorsque la place manque.##### Positionnement relatifLorsqu’un élément est positionné relativement, il est initialement positionné d’après le flux du document. Les boîtes des autres éléments sont positionnées et ENSUITE, l’élément positionné relativement est déplacé selon les valeurs spécifiées par les propriétés top bottom left et right.La place originale de l’élément est préservée dans le flux du document et il existe de grandes chances que cet élément en recouvre d’autres. La propriété z-index peut être utilisée pour déterminer quel élément sera placé devant l’autre sur l’axe de profondeur. Le bloc ayant la propriété z-index la plus élevée sera affiché devant l’autre.Si l’élément positionné est un élément de type block, il crée un nouveau bloc conteneur pour les éléments qui en dépendent dans l’arbre du document. Ces éléments utiliseront maintenant le positionnement modifié de l’élément comme bloc conteneur.Si les propriétés top ou bottom sont contradictoires, la propriété top l’emporte. Si les propriétés left ou right sont contradictoires, la propriété left l’emporte dans les langages se lisant de gauche à droite et right l’emporte dans les langages se lisant de droite à gauche.*Exercice: positionnement relatif*#### Positionnement absolu et fixe##### Positionnement absolu
Ce mode de positionnement est appliqué à tous les éléments dont la propriété position est définie comme absolute ou fixed. Si un tel élément n’existe pas, c’est l’élément racine (html) du document qui fait office de bloc conteneur.Les boîtes utilisant ce mode de positionnement sont extraites du flux du document et n’influencent plus les autres boîtes qui agissent comme si les boîtes positionnées absolument ou de manière fixe n’existaient pas. De plus, les éléments positionnés absolument se comportent toujours comme des éléments de type block.*Exercice: positionnement absolu et fixe*
Exemple de layout: [Lost World Fair](http://lostworldsfairs.com/moon/)Ces éléments utilisent comme contexte de positionnement l’élément parent (de type block ou inline) le plus proche ayant lui-même un positionnement spécifié comme absolu, relatif ou fixe.1. Un élément positionné absolument l’est par rapport aux bordures de son bloc conteneur (le padding n’est pas pris en compte et l’élément est positionné par rapport au bord intérieur de la bordure éventuelle du bloc conteneur).2. Un élément absolument positionné devient un bloc conteneur pour les éléments qu’il contient et ceux-ci suivent les règles de positionnement normal à l’intérieur de l’élément positionné absolument.3. Les éléments absolument positionnés peuvent contenir d’autres éléments positionnés absolument, qui sont à leur tour hors du flux normal du document, ce qui a pour conséquence qu’ils peuvent apparaître hors des limites de leur parent.
###### z-index et positionnement en couchesLes éléments positionnés absolument, comme ils sont hors du flux normal du document, peuvent recouvrir d’autres éléments (absolument positionnés ou non).
Chaque élément positionné génère une couche et, au sein d’une même couche, la profondeur de chaque élément est gérée par la propriété CSS `z-index`. Au sein d’une même couche, les éléments ayant une valeur `z-index` élevée sont placés devant ceux ayant une valeur `z-index` moindre.*Exercice: propriété z-index*##### Positionnement fixePour ce cas particulier du positionnement absolu, le bloc conteneur est toujours la fenêtre du navigateur.Les éléments positionnés de façon fixe ne bougent pas lorsque l’utilisateur descend dans la page. A l’impression, un élément positionné de manière fixe doit s’imprimer sur chaque page.Internet Explorer ne supporte le positionnement fixe qu’à partir de la version 7.
*Exercice: positionnement fixe*
Exemples de layouts: [Web Designer Wall](http://webdesignerwall.com/), [Lost World's Fair: Atlantis](http://lostworldsfairs.com/atlantis/),[Bonzai Sky CSS Zen Garden Design by Mike Davidson](http://www.csszengarden.com/?cssfile=069/069.css)
#### FloatsUn élément est positionné en mode float lorsque sa propriété float est spécifiée à l’aide des valeurs left ou right.
L’élément est alors positionné verticalement comme dans le flux normal du document : le côté supérieur de l’élément est aligné sur le dessus de la zone de contenu de son élément parent. Horizontalement par contre, l’élément est placé le plus à gauche ou le plus à droite possible par rapport à la zone de contenu de l’élément parent. Le contenu de l’élément parent contourne alors l’élément en mode float par le côté opposé.Quelques règles de base :
1. Les éléments positionnés en mode float sont toujours gérés comme des éléments de type block.2. D’après les spécifications, un élément en mode float doit toujours avoir une dimension, implicite ou explicite (nous verrons plus loin que cela n’est pas toujours vrai dans la pratique, mais c’est un bon principe de base).3. Les marges verticales d’un élément en mode float ne sont pas fusionnées avec celles des éléments placés avant ou après dans le flux du document.4. Des éléments en mode float seront placés les uns à côté des autres si la place disponible est suffisante. Si tel n’est pas le cas, le dernier élément sera placé sous les autres.
En fonction de la quantité de contenu des divers éléments, un élément en mode float peut affecter les éléments situés après lui dans le flux du document.
*Exercice: expériementer avec float*
##### Contrôler le flux des floats: propriété `clear`et float containment
La propriété CSS clear peut être utilisée pour contrôler la manière dont les éléments de type block interagissent avec les éléments en mode float. La propriété clear ne s’applique qu’aux éléments de type block. Cette propriété peut prendre les valeurs `left`, `right` et `both`.- `clear:left;`: l’élément visé ne peut se situer sur la gauche d’un élément en mode float.- `clear:right;`: l’élément visé ne peut se situer sur la droite d’un élément en mode float.- `clear:both;`: l’élément visé ne peut se situer ni sur la gauche ni sur la droite d’un élément en mode float.Par défaut, étant donné que les éléments en mode float sont hors du flux du document, leur éléments parent ne les contiennent pas. Il est possible de contraindre l’élément parent d’un élément en mode float à contenir l’ensemble de celui-ci, indépendamment du contenu de chacun d’entre eux. Eric Meyer a écrit [un article de référence décrivant précisément cet aspect des éléments en mode float](http://www.complexspiral.com/publications/containing-floats/).Cela peut être accompli à l’aide d’autres éléments situés à l’intérieur de l’élément parent de l’élément en mode float ou à l’aide de CSS lorsque le code HTML ne contient pas d’élément utilisable.###### Utilisation d’un élément du code et de la propriété `clear`Comme vu plus haut, en utilisant la propriété CSS `clear`, il est possible de forcer un élément à ne pas être côté à côte avec un élément en mode float. 
Nous verrons par exemple qu’un pied de page peut s’avérer bien pratique pour forcer un conteneur à contenir deux colonnes en mode float (deux `<div>` par exemple).###### A l’aide des CSS uniquementIl est également possible d’utiliser uniquement les CSS afin de forcer son élément parent à contenir un élément en mode float. La solution la plus simple consiste à placer l’élément parent en mode float lui aussi, sans oublier de lui donner une dimension (width:100%; dans la plupart des cas). En effet, la spécification CSS précise qu’un élement en mode float contient toujours ses enfant floatés.**Overflow**[La propriété `overflow` peut également être utilisée pour obtenir cet effet](http://annevankesteren.nl/2005/03/clearing-floats) mais peut poser des problèmes dans certaines situations.
```htmldiv{	overflow:hidden;}
```

La génération de contenu à l’aide des CSS permet également de forcer un élément parent à contenir ses éléments enfants en mode float. Cette technique est expliquée en détail [par Big John et Holly Bergevin sur leur site "Position Is Everything"](http://www.positioniseverything.net/easyclearing.html) [Une variante plus moderne reposant sur les pseudo-éléments :before et :after a été développée par Nicolas Gallagher](http://nicolasgallagher.com/micro-clearfix-hack/). Ces solutions genèrent un élement à l'aide de CSS et lui applquent un `clear:both;`, émulant ainsi la solutin vue plus haut.Il suffit de créer une classe CSS spécifique et d’y copier le code renseigné par ces auteurs pour pouvoir utiliser cette possibilité aussi souvent que nécessaire. Le code spécifique à IE6 et IE7 peut être servi uniquement à ces navigateurs à l’aide de [conditional comments](http://www.quirksmode.org/css/condcom.html) ou d’une [approche mixte crée par Paul Irish](http://paulirish.com/2008/conditional-stylesheets-vs-css-hacks-answer-neither/). Ils sont nécessaire en raison de la problématique de "has layout" dans IE. [A lire sur ce sujet: l’excellent article d’Ingo Chao](http://www.satzansatz.de/cssd/onhavinglayout.html).**Clearfix**HTML```html<!--[if lt IE 7]> <html lang="fr" class="no-js lt-ie9 lt-ie8 lt-ie7"> <![endif]--><!--[if IE 7]> <html lang="fr" class="no-js lt-ie9 lt-ie8"> <![endif]--><!--[if IE 8]> <html lang="fr" class="no-js lt-ie9"> <![endif]--><!--[if gt IE 8]><!--> <html lang="fr" class="no-js"> <!--<![endif]-->```
CSS```css.group:before, .group:after{	content: "";	display: table;}.group:after
{	clear: both;}.lt-ie7 .group { height: 1%; } /*IE6*/.lt-ie8 .group { min-height: 1px; } /*IE7*/```
*Exercice: expériementer avec float et clearing*
## CSS comme outil de mise en pageLes CSS peuvent être utilisées comme outils de mise en page, au travers des divers schémas de positionnement. [De nombreuses techniques existent et sont disponibles en ligne](http://css-discuss.incutio.com/?page=CssLayouts). Nous en détaillerons seulement quelques-unes unes dans la suite.### Mises en page fixesEtant donné la facilité de calcul des dimensions qu’elles offrent pour les divers éléments composant ces dernières, les mises en pages fixes sont (encore) très utilisées.Elles offrent l’avantage de ne pas modifier les longueurs de lignes, ce qui permet un meilleur confort de lecture.Les modes de positionnement flottés et absolus sont tous deux utilisables. Les deux systèmes ont des avantages et des inconvénients qu’il convient de connaître avant de les utiliser.#### Positionnement absolu et marges.Ce type de mise en page offre une grande facilité d’exécution.
La principale limitation de ce type de mise en page est l’impossibilité pour les éléments en mode statique d’influer sur le comportement des éléments absolument positionnés. Il est par exemple impossible de placer un pied de page couvrant le même espace horizontal que la somme des diverses colonnes si les longueurs ces dernières ne sont pas connues.HTML

```html<div class="wrapper">
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

*Exercice: réaliser une mise en page fixe avec positionnement absolu / fixe et marges (2 et 3 colonnes)*#### Positionnement en mode floatCe type de mise en page est très populaire, car il permet de réaliser facilement une mise en page très courante: deux ou trois colonnes entourées d’une bannière et d’un pied de page.HTML

```html<div class="wrapper">
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
}```
*Exercice: réaliser une mise en page fixe avec floats (2 et 3 colonnes)*
### Mises en page fluidesLes mises en pages fluides sont moins communes mais offrent l’avantage de s’adapter à toutes les résolutions.Le support par les prochaines versions d’Internet Explorer des propriétés max-width, min-width et max-height min-height vont sans doute les rendre plus populaires, puisque ces 
propriétés CSS permettent de contrôler efficacement les longueurs de lignes.Les modes de positionnement flottés et absolus sont tous deux utilisables. Les deux systèmes ont des avantages et des inconvénients qu’il convient de connaître avant de les utiliser.#### Positionnement absolu et marges.Cette mise en page n’est qu’une variation sur la mise en page deux colonnes que nous avons vue précédemment. Le seul changement consiste en une spécification des dimensions des éléments à l’aide d’une unité relative (ici en %). Certaines valeurs pour margin et padding sont également spécifiées en %.HTML```html
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
</div>```
CSS
```css
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
}```
*Exercice: réaliser une mise en page fluide avec positionnement absolu et marges (2 et 3 colonnes)*#### Positionnement en mode floatCette mise en page n’est qu’une variation sur la mise en page deux colonnes que nous avons vue précédemment. Le seul changement consiste en une spécification des dimensions des éléments à l’aide d’une unité relative (ici en %).

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
}```
*Exercice: réaliser une mise en page fluide avec floats (2 et 3 colonnes)*### Mises en page mixtes: marges négatives et floatsLes mises en pages mixtes sont des mises en page dans lesquelles un élément est de taille fixe, tandis que certains autres sont de tailles variable.Une mise en page souvent utilisée est celle reposant sur la propriété float et sur des marges négatives. Elle permet de disposer d’une colonne de largeur variable, alors que les autres sont de tailles fixes.HTML

```html<div class="wrapper">
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
```Il est également possible de [réaliser des mises en pages 3 colonnes à laide de cette technique](http://www.alistapart.com/articles/negativemargins/).
*Exercice: réaliser une mise en page mixte avec floats (2 et 3 colonnes)*
### Nouveaux outils de layout en CSS
Les propriétés `float` et 'clear' (ou de `inline-block`) ne sont pas des outils prévus pour réaliser des mises en page complexes. Ces solutions ont été utilisées parce que c'est tout ce que nous avions sous la main.
Récemment, de nouveaux outils de layouts sont créés en CSS: flexbox, grid, css regions, etc. Les changements dans les spécification et le manque de support dans les navigateurs n'en font pas encore des solutions utilisables en production pour le moment.
Nous aborderons ces outils l'année prochaine avec plus de détail. Si vous voulez un avant goût, jetez un oeil à [cette vidéo de Eric Meyer: "The Era of Intentional CSS Layout"](http://www.youtube.com/watch?v=XKpiP60HXwM) à lire également, [le compte rendu de Chris Coyier](http://css-tricks.com/w3conf-eric-meyer-the-era-of-intentional-layout/).## Quelques Techniques CSS utiles
Nous avons déjà examiné quelques astuces et hacks CSS permettant de contourner les défauts de certains navigateurs. Nous allons maintenant passer en revue quelques autres techniques bien utiles.### Listes et interfaces de navigation
Avec l’émergence des standards du W3C et des sites construits à l’aide de HTML et CSS, la tendance est à utiliser un code sémantiquement correct. Le choix des éléments utilisés pour coder divers éléments obéit à une certaine logique : on utilise d’avantage les listes de définition, les titres et intertitres sont codés comme tels, … Logiquement parlant, la plupart des interfaces de navigation que nous rencontrons sont des listes de liens (imbriquées ou non), il est donc logique de les coder comme tels. 
C’est devenu à ce point une habitude que certains en ont fait le sujet [d’articles](http://www.alistapart.com/articles/taminglists/) et de [tutoriaux](http://css.maxdesign.com.au/listutorial/index.htm) désormais célèbres.De simples listes non ordonnées ul peuvent facilement être mises en forme à l’aide d’un code CSS simple.#### Listes verticalesQuelques règles CSS peuvent transformer une simple liste non ordonnée en barre de navigation verticale.Pour ce qui est des puces décoratives, il est préférable de ne pas utiliser les puces des listes mais d’utiliser plutôt des images de fond sur les balises de lien.```css.nav-v{
	list-style:none;
	margin:0;
	padding:0;
}.nav-v a
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
```#### Listes horizontales (Floated left, Floated right)
Quelques règles CSS peuvent transformer une simple liste non ordonnée en barre de navigation horizontale, flottée à droite ou à gauche. [Une technique développée par Douglas Bowman et connue sous le nom de "sliding doors"](http://www.alistapart.com/articles/slidingdoors/) permet d’utiliser quelques images afin de créer des effets intéressants.```css.nav-h{
	list-style:none;
	margin:0;
	padding:0;
	background:#ccc;
	overflow:hidden; /*float containment: clearfix can also be used*/
}.nav-v a
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

*Exercice: réaliser des interfaces de navigation à partir de listes*### Une taille de texte constante à l’aide de valeurs relativesLes guidelines d’accessibilité du W3C nous demandent d’utiliser en CSS des valeurs relatives afin de spécifier la taille des polices. Cela provient du fait qu’Internet Explorer ne permet pas à l’utilisateur de modifier la taille des polices si celle-ci est spécifiée à l’aide d’unités absolues (en pixels par exemple).Consultez [les pages dédiées à cette question sur css-dicsuss](http://css-discuss.incutio.com/?page=FontSize) si vous souhaitez en savoir plus. Personnellement, ma méthode de prédilection consiste à spécifier la taille des polices en pourcentages au niveau du `body` et puis de poursuivre en spécifiant les tailles pour les éléments enfant en `em`.```cssbody{	font :normal 75%/1.5 arial, sans-serif ; /*10px comme taille de base*/}
```
ou

```cssbody{	font :normal 100%/1.5 arial, sans-serif ; /*16px comme taille de base*/}
```	### Centrer un bloc horizontalementBien que d’autres techniques existent également, voici une technique éprouvée pour 
centrer un élément de type block quel que soit le navigateur utilisé.```css.centered-block{	width:750px;	margin:0 auto;}
```	Autre méthode```css.centered-block{	position:relative;	width:750px;	left:50%;	margin-left:-375px;}```
### Faire disparaître des éléments visuellement sans les cacher aux navigateurs vocauxLa déclaration display:none; a été utilisée pour cacher des éléments en mode visuel (souvent dans le cadre de remplacement par images1). Le problème c’est qu’[elle rend les éléments auxquels elle est appliquée invisibles aux navigateurs vocaux également](http://css-discuss.incutio.com/?page=ScreenreaderVisibility).Elle peut souvent être avantageusement remplacée par la déclaration suivante :

```css.offleft{	position:absolute;	top:0;	left:-2000px	width:100px;	overflow:hidden;}```
	Autre option
	
```css.visuallyhidden{ 
	position:absolute; 
	overflow:hidden; 
	clip:rect(0 0 0 0); 
	height:1px; width: 1px; 
	margin:-1px;
	padding:0;
	border:0; 
}
```### Faux columnsComme nous l’avons vu dans le cadre des exemples de mises en page, il existe une astuce efficace pour donner visuellement l’impression que le fond des diverses colonnes s’étend jusqu’en bas quelle que soit la longueur des diverses colonnes.Cette astuce développée par Dan Cederholm et baptisée « faux columns » est utilisable avec des [mises en page à largeur fixes](http://www.alistapart.com/articles/fauxcolumns/) ou [variables](http://www.communitymx.com/content/article.cfm?page=1&cid=AFC58) et consiste à utiliser intelligemment une image de fond sur l’élément parent des diverses colonnes.```css.wrapper{	background:url(images/bkg_faucolumns.gif) top left repeat-y;}
```

*Exercice: expérimenter avec faux columns*### Solutions de remplacement par images[De nombreuses solutions ont été développées pour remplacer du texte par des images](http://css-discuss.incutio.com/?page=ImageReplacement), en partie parce que les développeurs se sentent limités par le nombre restreint de polices disponibles.Généralement, utilisera des méthodes qui cachent le texte en le plaçant sous l’image de remplacement. Ces méthodes nécessitent l’ajout d’un élément non sémantique dans le code HTML (dans ce cas-ci un <span>). L’autre problème de ces méthodes est l’impossibilité d’utiliser des images transparentes. HTML```css<h3 class="replace"><span></span>Revised Image Replacement</h3>```CSS
```css.replace{	width: 329px; /*largeur image*/	height: 25px; /*hauteur image*/	position: relative; /*établi un contexte de positionnement pour le <span>*/	overflow :hidden ; /*cache le texte si il déborde*/}	.replace span{	background: url(image_opaque.gif) no-repeat;	position: absolute;	width: 100%;	height: 100%;}
```
S’il faut utiliser des images transparentes, on utilisera alors une autre méthode qui cache le texte hors écran avant d’appliquer l’image.#### Phark Image Replacement
Cette technique utilise simplement un text indent négatif pour cacher le texte de l'élément hors page.```css.imgreplace{	text-indent:-9999px;}```
#### Scott Kellum Image Replacement
La méthode créée par Phark oblige le navigateur à créer d'énormes "boites" pour les éléments cachés hors écran, cela pose certains problèmes de performance, entre autre sur iOS. Une autre solution a donc vu le jour.HTML
```html<h3 class="imgreplace">Texte remplacé</h3>```CSS```css.imgreplace{	/* ne fonctionne que si l’élément est de type block / inline-block */	text-indent: 100%;	white-space: nowrap;	overflow: hidden;}
```
Ces technique, utilisée pour des éléments importants des pages, peuvent poser des problèmes d’accessibilité dans le cas où l’utilisateur dispose du support CSS mais pas de celui des images (CSS ON / IMAGES OFF). Dans ce cas, l’utilisateur ne voit rien.Il est possible de développer des interfaces de navigation très graphiques en utilisant ces techniques. Nous pouvons par exemple reconstituer l’interface de navigation principal du site d’Apple.
*Exercice: réaliser une barre de navigation graphique inspirée de celle de Appleen utilisant le spriting*### @font-face: Utilisation de polices non standardsAvec l’avènement de CSS3, il est désormais possible, sans faire appel à d’autre technologies, d’utiliser des polices spécifiques dans le cadre de projets Internet. [@font-face jouit d’un bon support dans la plupart des versions récentes des navigateurs](http://caniuse.com/fontface) et se dégrade élégamment dans les navigateurs plus anciens. Cette propriété permet de spécifier les polices à utiliser pour le rendu des textes et permet à l’utilisateur de les télécharger si il n’en dispose pas.CSS```css@font-face{	font-family: 'MyFontFamily';	src:url('myfont-webfont.eot?#iefix') format('embedded-opentype'), 		url('myfont-webfont.woff') format('woff'), 		url('myfont-webfont.ttf')  format('truetype'),		url('myfont-webfont.svg#svgFontName') format('svg');}
```
HTML```htmlh1{	font:normal 2em/1.1 MyFontFamily, Helvetica, Arcial, sans-serf;}```
Les principaux problèmes liées à l’utilisation de @font-face sont de nature légale. La licence de certaines polices ne permet pas de les utiliser de cette façon car, étant disponibles sur le serveur, elles peuvent y être téléchargées par quelqu’un qui ne les a pas forcément achetées. De nombreuses polices offrent explicitement la possibilité d’une utilisation à l’aide de @font-face dans le cadre de leur licence.
L’autre difficulté, de nature technique celle-là, est l’existence de [divers formats](http://snook.ca/archives/html_and_css/becoming-a-font-embedding-master) pour les fichiers de polices, supportés de façon diverses par les différents navigateurs. Il existe cependant des [outils de conversion](http://www.fontsquirrel.com/fontface/generator) et une [syntaxe éprouvée](http://paulirish.com/2009/bulletproof-font-face-implementation-syntax/) puis [améliorée](http://www.fontspring.com/blog/the-new-bulletproof-font-face-syntax) permettant de résoudre ces questions techniques. A signaler également, les [temps de chargement](http://www.stevesouders.com/blog/2009/10/13/font-face-and-performance/) qui, sur les sites très fréquentés, peuvent poser certains problèmes de performance.Cette technique est dores et déjà bien supportée par les divers navigateurs et constitue à ce jour notre meilleure option.Divers services tels que [Google Fonts](http://www.google.com/fonts), [Typekit](https://typekit.com/) et [Fontdeck](http://fontdeck.com/) se sont développés pour simplifier l’aspect technique et résoudre les questions légales tout en proposant un très large choix de polices. Certains de ces services sont payants, d'autres sont gratuits.
*Exercice: expérimenter avec des fontes*### Boutons en CSS3 avec Inline-block, border radius, text-shadow & box-shadowGrâce à quelques propriétés CSS3, il est facile de créer des boutons à l’aide d’un simple 
lien hypertexte.HTML```html<p><a href=”fake.html” class=”btn”>Text of my button</a></p>```
CSS

```css.btn{	display:inline-block;	background:#7AA020;	color:#fff;	border-radius:.2em;	padding:.75em 1em;	font:bold 1em/1 helvetica,arial,sans-serif;	text-decoration:none;	text-shadow:1px 1px 0 rgba(0,0,0,.5);	box-shadow:inset 0 -3px 0 rgba(0,0,0,.5);}
.btn:hover{	background:#5C7917;}```
### Coins arrondis avec la propriété CSS3 border-radius
Avant CSS3, créer des boites avec des coins arrondis impliquait d'utiliser des structures HTML complexes et des images. Aujourd'hui, la propriété border-radius permet de le faire en une seule ligne de code.

```css.box-rounded
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

### Dans le doute … validezLorsque vous “débuguez”, vous pouvez éviter bien des problèmes en validant tout d’abord votre code. Du code HTML ou CSS incorrect peut créer des problèmes de mise en page.Élaborez et testez vos CSS dans les navigateurs les plus avancés avant des les tester dans d’autres, mais pas après.Si vous développez un site dans un navigateur approximatif, votre code repose sur l’approximation de ce navigateur. Vous seriez alors frustré en le testant dans un navigateur plus proche des standards, le rendu affiché apparaissant « incorrect ».Commencez plutôt par produire un code répondant à vos attentes avec un navigateur dont le rendu est conforme aux standards et ajustez pour les navigateurs moins capables. Le travail d’ajustement sera moindre, plus logique et vous serez certain que votre site se comportera bien dans les futurs navigateurs. Aujourd’hui cela signifie, développer pour Mozilla, Safari ou Opera et corriger pour Internet Explorer.### Votre mise en page repose sur des “floats” ? Assurez vous que leur flux soit contrôlé efficacement par la propriété clear.
Les floats sont facétieux, et ne font pas toujours ce que vous en attendez. Si vous êtes dans une situation ou un float sort de son contenant ou ne semble pas se comporter comme bon vous semble, assurez-vous que ce que vous souhaitez est correct.
Passez voir [l’article d’Eric Meyer](http://www.complexspiral.com/publications/containing-floats/) à ce sujet. Si des comportements étranges persistent, poursuivez votre recherche avec [les ressources mises à votre disposition par John Gallant et Holly Bergevin](http://www.positioniseverything.net/).
### Vos marges fusionnent ?(“Margins collapse”); utilisez les propriétés padding ou border pour éviter cela.Vous pouvez vous retrouver avec des espaces là où vous n'en vouliez aucun ou aucun espace là où vous en souhaitiez. Si vous utilisez la propriété margin pour espacer vos éléments, le phénomène de fusion des marges (“margin collapsing”) est probablement le coupable. [Andy Budd vous explique tout ce qu’il faut savoir au sujet de la fusion des marges dans son article "no margin for error"](http://andybudd.com/archives/2003/11/no_margin_for_error/).
### En cas de doute, diminuez vos dimensions.Parfois, des erreurs d’arrondis dans certains navigateurs font que 50% + 50% donne plus que 100%, ce qui peut mener à des erreurs de rendu. Essayez de transformer 50% en 49% ou même 49.9%.
Assurez-vous que les navigateurs ciblés supportent les propriétés utiliséesLorsque vous rencontrez des problèmes dans l’un ou l’autre navigateurs, assurez-vous que ce dernier supporte les propriétés utilisées. Il existe de nombreuses ressources en ligne, comme [les tables de Peter Paul Kosh sur quirksmode.org](http://www.quirksmode.org/compatibility.html) ou encore le site [caniuse.com](http://caniuse.com/).### Utilisez les commentaires pour activer ou désactiver de larges parties de vos codes CSS ou HTML afin d’isoler un problème.Ce conseil est particulièrement utile lorsque vous travaillez sur des fichiers CSS et HTML de taille importante et avec lesquels vous n’êtes pas familier. Plus un problème est bien circonscrit, plus il devient facile à décrire et à résoudre.```css/* Ceci est un commentaire CSS */``````html<!-- Ceci est un commentaires HTML -->
```
### Attention à l’ordre des pseudo-classes appliquées aux liens.
Pour spécifier vos pseudo-classes de liens (:hover, etc.), utilisez l’ordre suivant: link, visited, hover, active (L’expression mnémotechnique «LoVe Hate» vous permettra de vous souvenir de cet ordre). Aucun autre ordre ne fonctionnera correctement. Si vous souhaitez aussi utiliser :focus, il vous faut modifier l’ordre ainsi: LVHFA.
### Spécifiez vos valeurs dans l’ordre top right bottom left lorsque vous utilisez des propriétés raccourcies vous évitera bien des TRouBLes
Les valeurs des propriétés raccourcies border, `margin` et `padding` internes doivent être spécifiées dans l’ordre des aiguilles d’une montre : top, right, bottom, left. Ainsi margin: 0 1px 3px 5px; donne pour résultat, pas de marge en haut, 1 pixel pour la marge droite, 3 pixels pour la marge du bas et 5 pixels pour la marge de gauche.
### Spécifiez une unité pour toutes les valeurs différentes de ZEROLes CSS requièrent que des unités de mesure (px, em, %, …) soient spécifiées pour toutes les valeurs différentes de zéro des propriétés CSS. La seule exception est `line-height` qui ne demande pas qu’une unité de mesure soit spécifiée. Cette propriété est toujours relative à l’unité utilisée pour spécifier vos tailles de polices.N’oubliez pas de spécifier une unité pour les valeurs différentes de 0. Les CSS requièrent que soit spécifiée une unité pour chaque mesure, comme les polices, les marges, et les dimensions. Pour le reste, 0=0 qu’il soit question de px, de em ou de n’importe quoi d’autre.Dans le cadre de ces propriétés raccourcies, si une ou plusieurs valeurs sont omises, elles sont déduites des valeurs fournies. Les valeurs gauche et droite fonctionnent ensemble, ainsi que les valeur dessus et dessous.```cssmargin:10px; est équivalent à margin :10px 10px 10px 10px;margin:10px 15px; est équivalent à margin :10px 15px 10px 15px;margin:10px 15px 8px; est équivalent à margin :10px 15px 8px 15px;```
### Testez différentes tailles de policesLes navigateurs évolués comme Mozilla et Opera permettent de redimensionner le texte quelle que soit l’unité utilisée. Certains utilisateurs peuvent faire usage d’une police par défaut plus grande que la vôtre; essayez de correspondre à la gamme la plus large possible.Idéalement, votre contenu et votre navigation devraient rester utilisables quelle que soit la taille des polices affichées par votre navigateur.
### Vérifiez que vos fichiers CSS et HTML correspondent au niveau des noms de classes et d’id.Une faute de frappe est vite commise et les navigateurs les plus stricts sont aussi sensibles aux fautes de frappes (underscores et tirets, majuscules et minuscules, etc.).### Utilisez les outils de debugging mis à disposition par votre navigateur afin de détecter les problèmes éventuels de vos mises en pages CSSUtilisez Firebug, les outils de développement de chrome ou de Firefox, combinés avec l’extension développeur de Firefox afin de visualiser les choses plus aisément et de détecter certains problèmes dans vos mises en page.### N’oubliez pas de créer une CSS print.Les pages web sont parfois imprimées, assurez vous que le contenu de votre site est formaté pour cela.### Organisez et commentez vos fichiers CSSCommentez vos fichiers CSS afin que d’autres et vous-même puissent s’y retrouver facilement. Regroupez les éléments semblables et adoptez des conventions pour vos commentaires et les noms de classes ou d’id utilisés.Jonathan Snook a écrit un bon ouvrage à ce sujet: [SMACSS](http://smacss.com/). Ce petit livre est disponible en ligne gratuitement. et détaille une bonne méthodologie d'organisation pour les fichiers CSS. Voir aussi les excellents articles de [Harry Robert](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) et de [Nicolas Gallager](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/).Nommez vos classes et ID d’après leurs fonctions plutôt que d’après leurs formesSi vous créez une classe nommée .textbleusmall et que, en cours de développement, le texte auquel est appliqué cette classe devient rouge, il sera plus difficile de s’y retrouver. Utilisez plutôt des classes et ID descriptives telles que `.footer` et `.list--compact`.
### N’utilisez filtres et hacks qu’en dernier recours.[Modernizr](http://modernizr.com/) et [la solution de conditionnal comments de Paul Irish](http://www.paulirish.com/2008/conditional-stylesheets-vs-css-hacks-answer-neither/) vous permettent d’éviter de recourir à des hacks CSS.
### Optimisez vos CSSPour en savoir plus sur le sujet, consultez [la page de ressources mise à votre disposition par Zoe Gillenwater](http://zomigi.com/blog/maintainable-efficient-css/).### Attention à l’accessibilité lorsque vous utilisez des techniques de remplacement d’images via CSS.Beaucoup de ces techniques peuvent poser des problèmes aux utilisateurs de navigateurs vocaux ou aux navigateurs dans lesquels le support des images est désactivé. Pour un test d’accessibilité en 10 secondes : visualisez vos pages avec un support CSS, un support images et un support Javascript désactivé. Testez différentes combinaisons.

## Ressources Complémentaires

- [A beginner's guide to HTML & CSS](http://learn.shayhowe.com/html-css/) par Shay Howe: un bon résumé des bases en HTML et CSS
- [Highly Maintainable, Efficient, and Optimized CSS](http://zomigi.com/blog/maintainable-efficient-css/) par Zoe Mickley Gillenwater: quelques bonnes informations sur les "best practises" en matière de CSS.
- [caniuse.com](http://caniuse.com): tables de support navigateurs pour HTML5 et CSS3
- [html5please](http://html5please.com): conseils d’utilisation pour HTML5 et CSS3. Polyfill javascript renseignés.
- [Mozilla Developer Network](https://developer.mozilla.org/): une bonne référence exhausitive sur les technologies du web (HTML/CSS/JS) [disponible en Français également](https://developer.mozilla.org/fr/).
- [Webplatform.org](https://developer.mozilla.org/): un site de ressource exhaustif maintenu par le W3C et la communauté. 
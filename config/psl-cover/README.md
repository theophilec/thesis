Couverture LaTeX de thèse PSL
=============================

Par [Pierre Guillou](https://pierre.guillou.net)

Version 1.2 (20 juillet 2019)

****

![Logo PSL](logo-psl.jpg)

Grâce à cette feuille de style, vous pourrez directement compiler
votre thèse LaTeX avec la couverture !

Cette page concerne le modèle 2018 des couvertures de thèse. Pour le
modèle 2016, se reporter à [cette adresse](../2016).

Pour plus de renseignements, se reporter à l'[espace ressources
PSL](https://collegedoctoral.psl.eu/doctorat-psl/espace-ressources/)

Fonctionnalités
---------------

* Facile (?) à utiliser : une feuille de style LaTeX et des commandes
  pour compléter les informations
* Directement utilisable dans un projet LaTeX préexistant (pas besoin
  de compiler un PDF séparément, et de l’insérer avec
  [`pdfpages`](https://ctan.org/pkg/pdfpages))
* Un fichier d’exemple fourni (qui compile, mais pas avec PDFLaTeX…)
* Peu de dépendances (voir plus bas) : meilleure portabilité
* Code lisible (bon, ça reste du LaTeX) et documenté (un peu…) :
  possibilité d’éditer le template selon ses besoins
* Aucun caractère UTF-8 ou autre, uniquement des caractères ASCII,
  pour une meilleure compatibilité avec des encodages exotiques
* Fallback possible avec le .docx pour celles et ceux ayant accès à
  Word
* License GPL

Fichiers du projet
------------------

Ce projet contient les fichiers suivants :

* [psl-cover.sty](psl-cover.sty) : le fichier principal, la feuille de
  style, le cœur du template, à importer dans votre projet de thèse
  LaTeX
* [logo-institute.jpg](logo-institute.jpg) : le logo de
  l’établissement PSL (ici celui de l’école des mines, accolé au logo PSL)
* [front-bg.jpg](front-bg.jpg) et [back-bg.png](back-bg.png), deux
  fichiers image servant de fond à la couverture
* [sample.tex](sample.tex) : un fichier d’exemple d’utilisation
* [sample.pdf](sample.pdf) : le résultat après compilation
* [README.md](README.md) : à l’origine de la présente page

L’ensemble de ces fichiers peut se récupérer directement au format
[archive tar](psl-cover.tar) ou au format
[compressé zip](psl-cover.zip).

Prérequis
---------

Ce fichier de style LaTeX a été testé sous Ubuntu 14.04, Ubuntu 16.04,
ArchLinux et Windows 10 (MikTeX 2.9).

Une distribution LaTeX de type Texlive (de préférence à jour) est bien
évidemment nécessaire.

La police Arial devra être installée si vous utilisez le compilateur
LuaLaTeX (packages msttfcorefonts sous Ubuntu et Debian, ttf-ms-fonts
sous ArchLinux, sans doute incluse sous Windows). Par défaut,
PDFLaTeX se rabat élégamment sur la police Helvetica, proche d’Arial
et normalement inclue dans votre distribution LaTeX.

Utilisation basique
-------------------

Seuls les images de fond, le logo et le fichier psl-cover.sty sont
nécessaires pour générer la couverture. Il suffit de les placer à la
racine de votre projet LaTeX (ou dans un sous-dossier, c.f. la macro
`\pslassetspath`) et d’importer le fichier de style dans le préambule
de votre document principal.

Ceci fait, l’exemple minimal qui fonctionne est le suivant :

```latex
\documentclass[a4paper]{book} %% ou report ou memoir…

\usepackage[T1]{fontenc}
\usepackage[utf8]{inputenc}
\usepackage{psl-cover}

\title{titre de la thèse}

\begin{document}

\maketitle{}

\end{document}
```

Les quatre pages de couverture doivent se générer automatiquement si
un appel à la méthode `\maketitle` est présent dans le corps du
document.

Les informations manquantes du template sont fournies au travers des
commandes :

```latex
%% commande à remplir obligatoirement
%% (sinon la compilation plante)
\title{titre de la thèse}

%% commandes avec des valeurs par défaut non nulles
\institute{nom de l’organisme d’accueil PSL}
\doctoralschool{nom de l’école doctorale}{numéro}
\specialty{spécialité de votre thèse dans l’école doctorale}

%% commandes avec des valeurs par défaut nulles (vides)
\author{nom du futur docteur}
\date{date de la soutenance}
\jurymember{numéro}{nom du juré}{titre et établissement}{rôle}
\frabstract{
  Le résumé en français…

  …sur un ou plusieurs paragraphes
}
\enabstract{
  The thesis abstract in english…

  …which can be spread over several paragraphs

}
\frkeywords{Une liste de mots-clés}
\enkeywords{A list of keywords}

%% uniquement si les fichiers du template sont placés dans un
%% sous-dossier de votre projet LaTeX
%% (c’est pour que les \includegraphics puissent trouver les images)
\pslassetspath{chemin/relatif/vers/le/dossier/contenant/le/template}
```

(ou directement éditées à la bonne place dans la feuille de style).

### Nouveautés par rapport à la version 2016

* Moins de figures TikZ, remplacées par des images (front-bg.jpg, back-bg.png)
* Changement de nom pour la macro `\logopath` -> `\pslassetspath` :
  avant, on n’avait que des logos, maintenant, il y a également les
  images de fond
* Évolution de la macro `\jury`, qui prenait avant un bloc de texte
  sur plusieurs paragraphes, vers `\jurymember`, qui permet de passer
  au template des informations structurées, pour les rentrer dans un
  tableau pré-formaté. Par contre, il y a au maximum 12 entrées. En
  rajouter des supplémentaires ne devrait pas être trop compliqué (par
  exemple, chercher les mentions de `\@jiname` dans le template). Ne
  pas oublier de déplacer le champ texte vers le haut (augmenter la
  valeur de `yshift` ligne 240).Par contre, le public de votre
  soutenance risque de moins apprécier les questions supplémentaires…
* Une option pour les cotutelles (avec des commandes dédiées)
* Des tests (PDFLaTeX, LuaLaTeX, XeLaTeX)
* Une meilleure documentation

Questions/remarques fréquentes
------------------------------

### Compilation du fichier d’exemple

Le fichier sample.tex fournit un exemple basique d’utilisation basé
sur ce modèle. Attention, ce fichier se compile par défaut avec
LuaLaTeX et non avec PDFLaTeX. Pour retrouver la compatibilité avec
PDFLaTeX, remplacer

```latex
\usepackage{fontspec}
```

par le classique diptyque

```latex
\usepackage[T1]{fontenc}
\usepackage[utf8]{inputenc}
```

### Récupérer des données passées au template

J’ai aussi ajouté les commandes `\thefrabstract`, `\theenabstract`,
`\thefrkeywords` et `\theenkeywords` qui permettent de réutiliser les
résumés et les mots clés dans une autre partie de votre thèse.

Exemple d’utilisation (tiré de ma propre thèse) :

```latex
\chapter{Résumé}
\thefrabstract{}
\vfill
\textbf{Mots clés :} \thefrkeywords{}

\chapter{Abstract}
\theenabstract{}
\vfill
\textbf{Keywords:} \theenkeywords{}
```

### Adaptation à d’autres établissements PSL

Le présent template, bien que spécifique à l’école des mines,
peut facilement (enfin, je l’espère…) être adaptée à d’autres
établissements de l’Université de recherche Paris Sciences et Lettres.

Pour ce faire, la feuille de style fournit, d’une part, la méthode

```latex
\institute{nom d’établissement}
```

(par défaut réglée à « MINES ParisTech »).

Il s’agit, ensuite, de remplacer le fichier
[logo-institute.jpg](logo-institute.jpg), qui contient actuellement le
logo de (l’école des mines | PSL), par celui de l’établissement adéquat.

Si la mise à l’échelle du logo sur la couverture rend mal, il est
possible de modifier sa taille directement dans la feuille de style (à
la ligne 268 ou pas loin).

### Options de la feuille de style

#### Avoir une page de titre (en plus de la couverture)

La feuille de style surcharge la méthode `\maketitle` et génère deux
feuilles de couvertures au début et à la fin, avec à chaque fois une
page blanche intercalaire.

Si, néanmoins, vous souhaitez conserver l’usage de `\maketitle`, par
exemple pour générer une page de titre hors couverture, l’option
`nomaketitle`, à passer au package, désactive cette surcharge.

Dans ce cas, une méthode alternative `\pslcover` peut être utilisée
pour générer la couverture. Attention, il faut utiliser cette commande
**avant** `\maketitle`, afin de s’assurer que la page de couverture est
bien au début du document :

```latex
\usepackage[nomaketitle]{psl-cover}
%% [...]
\begin{document}
%% [...]
\pslcover{} %% **avant** \maketitle
\maketitle{}
%% [...]
\end{document}
```

#### Pour les cotutelles

Une version modifiée du template existe en cas de cotutelle avec un
organisme extérieur à PSL. Cette version affiche notamment :

* une mention « Dans le cadre d’une cotutelle avec… » placée en
  dessous de « Préparée à… » ;
* un titre en anglais placé sous le titre en français (qui lui est
  légèrement translaté vers le haut) et
* un logo de l’organisme d’accueil hors-PSL en haut à droite.

Cette version alternative est accessible au travers de l’option
`cotutelle` passée à l’import de la feuille de style. Si c’est le cas,
les commandes suivantes doivent être renseignées :

```latex
\entitle{English Thesis Title}
\otherinstitute{Nom de l’institut partenaire}
\logootherinstitute{chemin/vers/le/logo/de/l’institut/partenaire}
```

En voici un exemple basique d’utilisation :

```latex
\documentclass[a4paper]{book}

\usepackage[T1]{fontenc}
\usepackage[utf8]{inputenc}
\usepackage[cotutelle]{psl-cover}

\title{titre de la thèse}

\entitle{English Thesis Title}
\otherinstitute{Nom de l’institut partenaire}
\logootherinstitute{chemin/vers/le/logo/de/l’institut/partenaire}

\begin{document}

\maketitle{}

\end{document}
```

### Dépendances

J’ai utilisé les paquets suivants pour me faciliter la vie :

* `iftex` (<https://ctan.org/pkg/iftex>) pour <del>les gens qui
  n'utilisent pas LuaLaTeX</del> sélectionner la police Arial (ou
  Helvetica) selon la variante de LaTeX utilisée ;
* `tikz` (<https://www.ctan.org/pkg/pgf>) pour le placement de chaque
  champ texte sur les pages, ainsi que pour quelques dessins simples ;
* `etoolbox` (<https://ctan.org/pkg/etoolbox>) pour les commandes
  `\AfterPreamble` (faire en sorte que la première de couverture
  s’affiche bien en première page) et `\ifdefempty` (pour le tableau
  des membres du jury) et
* `tabularx` (<https://ctan.org/pkg/tabularx>) pour le formatage du
  tableau des membres du jury (colonnes à taille fixe).

Informations pratiques
----------------------

Les félicitations, louanges, commentaires, remarques, critiques,
insultes ou rapports de bugs peuvent être adressées à l’auteur de ce
document via l’email `pierre dot guillou at mines-paris dot org`. Ce
dernier se réservera le droit de répondre selon son emploi du temps de
doctorant de 3<sup>e</sup> année, de post-doctorant, ou de tout autre
poste qu’il occupera par la suite.

Remerciements
-------------

Ce projet LaTeX n’aurait pas été rendu possible sans les essais des
doctorants et doctorantes des centres de recherche en informatique et
en morphologie mathématique de l’école des mines, qui m’ont permis de
tester et d’améliorer la portabilité des premières versions de mon
code.

Plus tard, les retours et questionnements des utilisateurs ont,
notamment, permis d’affiner la documentation du projet, qui, je
l’espère, saura se montrer compréhensible et exhaustive.

Que toutes et tous en soient remerciés.


# Le DOM (Document Object Model)

  

La capacité de changer de façon dynamique une page Web par le JavaScript, est rendue possible par le Document Object Model, en abrégé le DOM.

  

Le Modèle Objet de Document (DOM) peut se définir comme une interface de programmation d’applications pour des documents Html. En clair, il définit la structure logique des objets d’un document, la manière d’y accéder et de les manipuler.

  

Avec le DOM, les programmeurs peuvent construire des documents, naviguer dans leur structure ainsi qu’ajouter, modifier ou effacer des éléments et leur contenu. Tout ce qui se trouve dans un document Html peut être touché, modifié, effacé ou ajouté en utilisant le Modèle Objet du Document.

  

Le DOM fournit aussi une interface de gestion des événements, pour capturer les actions du navigateur ou de son utilisateur, et y réagir.

  

Exemples d'instructions DOM :

  

- document.getElementById(id)

- document.getElementsByTagName(name)

- document.createElement(name)

- element.innerHTML

- element.style

  

---------------------------

  

### La fonction getElementById()

  

getElementById est une des principales fonctions pour manipuler un élément du DOM, elle permet tout simplement d’accéder à l’élément de votre page qui est identifié par son attribut id, à condition de l’avoir mentionné, car il n’est pas obligatoire :

  

```javascript

// An highlighted block

<div  id="mondiv">Exemple de texte</div>

```

  

Ainsi, getElementById vous permet d’accéder à cet élément via son id (mondiv). Cet élément est en fait un objet sur lequel on peut agir pour changer le contenu du texte, ses propriétés de style (couleur, font…) comme ceci :

  

```javascript

<script>

document.getElementById('mondiv').style.color = 'blue';

</script>

```

  

Gardez bien en tête qu’un élément du DOM identifié par un id doit être unique. Dans le cas contraire, vous risquez d’obtenir des comportements inattendus.

  

---

### La fonction getElementByClassName()

  

Contrairement aux identifiants uniques repérés par l’attribut id, il est parfois nécessaire d’accéder à plusieurs éléments à la fois dans la page HTML. Pour cela, on utilise l’attribut class.

  

La différence avec un id réside dans le fait qu’on peut l’utiliser plusieurs fois la page. Dans ce cas, tous les éléments du DOM ayant la même class seront traités à la fois.

  

La fonction getElementByClassName vous permet d’identifier chaque élément du DOM qui a la classe passée en paramètre.

  

Contrairement à la fonction getElementById(), getElementByClassName() peut retourner plusieurs éléments, donc on obtient en retour de fonction un tableau.

  

On peut alors utiliser cette fonction comme ceci :

  

```javascript

var  tableau_maclass = document.getElementsByClassName('maclass')

```

  

Voyez l'exemple suivi :

  

```javascript

<body>

<div  id="mondiv">Exemple de texte</div>

<br>

<div  class="maclass">Un div avec maclass</div>

<p  class="maclass">Un paragraphe avec maclass</p>

<script>

document.getElementById('mondiv').style.color = 'blue';

//on recupère tous les éléments dont la class est maclass

var tableau_maclass = document.getElementsByClassName('maclass');

//on traite les éléments de maclass

for (i = 0 ; i <  tableau_maclass.length  ;  i++)  {

tableau_maclass[i].style.textDecoration = 'underline';

}

</script>

</body>

```

  

On a utilisé une simple boucle for pour parcourir tous les éléments du tableau, puis sur chacun d’eux on modifie le style et on les souligne (propriété underline).

  

Notez que l’on a utilisé dans l’exemple précédent un tableau intermédiaire pour stocker toutes les références à **maclass** (tableau_maclass), vous pouvez néanmoins accéder à l’ensemble des éléments directement, vous obtiendrez le même résultat avec le code ci-dessous :

  

```javascript

<script>

document.getElementById('mondiv').style.color = 'blue';

//on traite les éléments de maclass

for (i = 0 ; i <

document.getElementsByClassName('maclass').length ; i++) {

document.getElementsByClassName('maclass')[i].style.

textDecoration = 'underline overline';

}

</script>

```

La propriété textDecoration utilisée dans l’exemple précédent représente une propriété CSS qui est normalement orthographiée comme ceci dans un fichier CSS : text-decoration. Mais JavaScript réserve le caractère tiret (-) pour l’utiliser comme opérateur mathématique. En fait, chaque fois que vous devez accéder à une propriété CSS comportant un tiret, vous devez omettre celui-ci et mettre en majuscule le caractère immédiatement après le tiret. Ainsi, text-decoration en CSS deviendra textDecoration en JavaScript, font-size deviendra fontSize. Toutefois, il existe une alternative à ceci en utilisant la fonction setAttribute, que l’on va voir dans le paragraphe suivant.

---

### La fonction setAttribute()

L’utilisation de cette fonction est simple et permet d’accéder à un attribut sur l’élément du DOM, cela peut être le style, une classe, name, id, etc. Pour ce qui est des attributs de style, vous devrez indiquer le nom de la propriété CSS telle qu’elle est indiquée dans un fichier CSS, comme par exemple :

```javascript
document.getElementById('mondiv').setAttribute('style', 
'text-decoration : underline'); 
document.getElementById('mondiv').setAttribute('class','maclass'); 
document.getElementById("monInput").setAttribute("type",  
"button"); //change un champ input en bouton
```

Un cas concret : vous désirez ajouter un lien sur un texte à l’écran repéré par un  \<a id='monLien'>, il suffira alors d’ajouter un attribut  href  sur cet élément, voyez plutôt :

Un exemple de code avant l’utilisation de JavaScript :

```javascript
<a id="monLien">lien vers google</a>
```

À l’aide de JavaScript, on ajoute facilement l’attribut  href  sur cet élément, ainsi le lien devient effectif :

```javascript
<script> 
    document.getElementById("monLien").setAttribute("href", 
"https://www.google.be");  
</script>
```

---

### La fonction hasAttribute()

Il est parfois utile de vérifier si un attribut existe ou non avant de l’ajouter ou de le modifier. La fonction  hasAttribute()  permet d’effectuer cette vérification sur l’élément du DOM que vous désirez contrôler.

L’exemple suivant vérifie simplement que l’élément  \<a>  possède une cible (attribut target), et si oui, on lui affecte la propriété  _blank  pour que le lien s’ouvre dans un nouvel onglet (ou fenêtre) :

```javascript
<script> 
    var item_a = document.getElementById("monItemA"); 
 
    //vérifie si l’élément <a> possède un attribut target 
    //si oui, on lui assigne la valeur _blank 
    if (item_a.hasAttribute("target")) { 
           item_a.setAttribute("target" , "_blank"); 
    } 
</script>
```

---

### La fonction removeAttribute()

Vous avez vu que l’on peut facilement ajouter un attribut à un élément du DOM, il est également très simple de le supprimer, pour cela vous utilisez la fonction  removeAttribute()  comme ceci, par exemple pour supprimer un lien sur un élément  \<a> :

```javascript
document.getElementById("monItemA").removeAttribute("href");
```

---

### Exemple de mise en forme d’un élément du DOM

Voici un exemple d’utilisation de JavaScript pour mettre en forme une balise  \<div> :

```javascript
<body>     
    <div id='mondiv'>Bonjour</div> 
 
    <script>   
           document.getElementById('mondiv').style.border     = 
'solid 1px red'  
           document.getElementById('mondiv').style.width      = 
'100px'       
           document.getElementById('mondiv').style.height     = 
'50px'  
           document.getElementById('mondiv').style.background = 
'#eee' 
           document.getElementById('mondiv').style.color      = 
'blue' 
           document.getElementById('mondiv').style.fontSize   = 
'15pt'
           document.getElementById('mondiv').style.fontFamily = 
'Helvetica'  
           document.getElementById('mondiv').style.fontStyle  = 
'italic' 
           document.getElementById('mondiv').style.textAlign  = 
'center' 
    </script>  
</body>
```

Vous pouvez vraiment accéder à toutes les propriétés CSS d’un élément, l’exemple ci-dessus ne présente qu’un petit échantillon.

Bien entendu, cet exemple ne sert strictement à rien, car il vaut mieux créer un fichier CSS distinct pour gérer les propriétés d’un élément. Mais cet exemple démontre comment accéder aux propriétés, et c’est l’interaction avec l’utilisateur qui devient intéressante, vous le verrez dans les pages suivantes.

---

### Accéder aux propriétés de la fenêtre

JavaScript ouvre également l’accès à un très large éventail d’autres propriétés, telles que la fenêtre même du navigateur, sa largeur et sa hauteur, des informations pratiques telles que la fenêtre parente (s’il y en a une), l’historique des URL visitées, etc.

Toutes ces propriétés sont accessibles à partir de l’objet  window, le tableau suivant les répertorie toutes, avec une description de chacune d’entre elles :

Propriétés | Assigne ou retourne
-------- | -----
closed | Retourne une valeur booléenne indiquant si une fenêtre a été fermée ou non.
defaultStatus | Définit ou retourne le texte par défaut dans la barre d’état d’une fenêtre (navigateur).
document | Renvoie l’objet document dans la fenêtre.
frames | Retourne un tableau de toutes les frames et iframes dans la fenêtre.
history | Retourne l’objet history dans la fenêtre qui permet de recenser toutes les URL visitées.
innerHeight | Définit ou retourne la hauteur interne de la zone de contenu d’une fenêtre.
innerWidth | Définit ou retourne la largeur interne de la zone de contenu d’une fenêtre.
length | Retourne le nombre de cadres et d’iframes dans une fenêtre.
location | Retourne l’objet  location  dans la fenêtre.
name | Définit ou retourne le nom d’une fenêtre.
navigator | Objet regroupant les propriétés décrivant le navigateur : nom, version, langue, système d’exploitation, acceptation des cookies, etc.
opener | Retourne l’objet de type  window  qui a créé la fenêtre à vl’aide de la méthode  open().
outerHeight | Définit ou retourne la hauteur d’une fenêtre, en tenant compte des barres d’outils et de défilement.
outerWidth | Définit ou retourne la largeur d’une fenêtre, en tenant compte des barres d’outils et de défilement.
pageXOffset | Retourne le déplacement horizontal de la fenêtre courante en nombre de pixels depuis la gauche de la fenêtre.
pageYOffset | Retourne le déplacement vertical de la fenêtre courante en nombre de pixels depuis le haut de la fenêtre.
parent | Retourne la fenêtre parente d’une fenêtre.
screen | Retourne l’objet  screen  de la fenêtre.
screenLeft | Retourne la coordonnée X de la fenêtre par rapport à l’écran (sauf Mozilla Firefox où il faudra utiliser  screenX).
screenTop | Retourne la coordonnée Y de la fenêtre par rapport à l’écran (sauf Mozilla Firefox où il faudra utiliser  screenY).
screenX | Retourne la coordonnée X de la fenêtre par rapport à l’écran.
screenY | Retourne la coordonnée Y de la fenêtre par rapport à l’écran.
self | Retourne la fenêtre courante.
status | Définit ou retourne le texte de la barre de statut.
top | Pointe sur la fenêtre la plus haute dans la hiérarchie du tableau de frames (iframes).

La plupart de ces propriétés sont précieuses lorsque vous ciblez des téléphones mobiles et des tablettes, car elles vous indiquent exactement l’espace d’écran avec lequel vous devez travailler, le type de navigateur utilisé, et bien plus encore.

Exemple d'utilisation : 

```javascript
<script>

var tailleEcran = window.innerHeight;

alert(tailleEcran)

</script>
```

---

### Ajouter un élément au DOM

JavaScript ne sert pas uniquement à manipuler les éléments du DOM, il permet également d’en créer de nouveaux.

Pour cela, vous pouvez utiliser les fonctions  createElement()  et  appendChild(), voici un exemple qui ajoute une nouvelle balise  \<div>  dans le  \<body>  de la page HTML :

```javascript
<body>

Cette page contient uniquement ce texte.<br><br>

  

<script>

alert('Cliquez sur OK pour ajouter une nouvelle balise <div> dans la page')

var  newdiv = document.createElement('div')

newdiv.id = 'NewDiv'

document.body.appendChild(newdiv)

newdiv.innerHTML = "Et voila le nouvel element du DOM, et on le colore en rouge!"

document.getElementById(newdiv.id).setAttribute('style',

'color : red')

</script>

</body>
```

La fonction document.createElement(’div’) permet simplement de créer un nouvel élément et il est stocké dans la variable newdiv. À partir de là, on peut invoquer la fonction appendChild(), qui permet d’insérer le nouvel élément où l’on veut dans le DOM, dans l’exemple on l’a ajouté dans le body.

La fonction  newdiv.innerHTML  permet d’indiquer du contenu à la nouvelle balise  \<div>.

Aussi, si vous consultez le code source dans l’onglet  Elements de Chrome, vous pouvez constater que le nouvel élément inséré a bien un id équivalent à NewDiv.

---

### Supprimer un élément du DOM

Bien évidemment, s’il est possible d’ajouter des éléments, il est aussi possible d’en supprimer.

Il faut dans un premier temps accéder au nœud parent pour pouvoir ensuite supprimer l’élément du DOM. Dans l’exemple de la section précédente, vous avez créé un élément  newdiv  (avec l’identifiant "NewDiv"). Pour supprimer cet élément, il va donc falloir procéder ainsi :

```javascript
<script> 
	var  noeud_parent = newdiv.parentNode
	noeud_parent.removeChild(newdiv)
	tmp = pnode.offsetTop  //optionnel 
</script>
```

Un élément du DOM doit être rattaché à un nœud parent (body dans l’exemple ci-dessus, en effet, la fonction  parentNode  retournera  [object HTMLBodyElement]). Ensuite, il suffit de supprimer l’élément à l’aide de l’instruction  removeChild().

La dernière instruction (tmp = pnode.offsetTop) ne sert qu’à rafraîchir le navigateur pour que l’élément ne soit plus visible à l’écran, ce qui peut être nécessaire sur certaines anciennes versions de navigateur.

---

### Alternative à la création et à la suppression d’un élément

On a vu qu’il est possible de créer des nouveaux éléments dans le DOM, ce n’est pas forcément facile à maîtriser et cela demande un peu de réflexion avant de se lancer dans ce concept. Bien entendu, cela dépend de ce que vous avez à faire, du projet à mettre en œuvre.

Il existe toutefois une alternative qui est très simple à concevoir, dans la mesure où votre projet ne consiste en fin de compte qu’à masquer certains éléments, et à les montrer en fonction de certaines actions de l’utilisateur. Pour cela, il y a des propriétés CSS qui permettent de rendre visibles ou invisibles les éléments désirés.

Constituez votre page dans son ensemble, y compris les éléments qui ne doivent pas nécessairement être affichés au départ. Vous attribuerez à ces éléments la propriété de style display  à  none, ou la propriété  visibility  à  hidden.

La différence entre ces deux méthodes est la suivante : la propriété  display  libère la place si elle est à  none, c’est-à-dire que les autres éléments de la page situés en dessous remonteront à l’emplacement de l’élément caché. A contrario, la propriété  visibility  rend l’élément invisible, mais l’emplacement est conservé, les autres éléments du DOM ne bougeront pas.

Voici comment utiliser ces propriétés :

```javascript
<script>

document.getElementById('mondiv').setAttribute('style',

'display : none') //cache l’élément mondiv et libère l’emplacement

document.getElementById('mondiv').setAttribute('style',

'display : block') //affiche l’élément mondiv

document.getElementById('mondiv').setAttribute('visibility',

'hidden') //cache l’élément mondiv

document.getElementById('mondiv').setAttribute('visibility',

'visible') //affiche l’élément mondiv

</script>
```

---

### Les événements JavaScript 

Tout le code JavaScript que nous avons vu dans les chapitres précédents ne s’exécute qu’une seule fois, au chargement de la page. C’est donc une utilisation extrêmement limitée, il n’y a aucune interaction avec l’utilisateur de la page. Un des objectifs du JavaScript est de dynamiser la page, de proposer des interactions avec les utilisateurs.

Or, comment interagir avec ces utilisateurs  ? Eh bien, par l’intermédiaire d’événements. Les événements se produisent à tout moment dans une page, par exemple lorsque le pointeur de la souris se déplace sur la page, quand il passe au-dessus d’un élément et quand il en sort, quand l’utilisateur clique sur un bouton. Mais vous avez aussi des événements qui sont déclenchés avec le clavier, comme appuyer sur une touche ou relâcher cette touche du clavier. Donc, il y a en permanence des événements qui se produisent dans une page web.

Aussi, pour nous, la seule question qu’il faut se poser est : à quels événements nous devons réagir et de quelle manière ? Pour réagir à un événement, il faudra être à son écoute, il faudra gérer un écouteur spécifique à cet événement.

---

#### Réagir au clic sur un bouton

Dans cet exemple très simple, nous allons réagir au clic de l’utilisateur sur un bouton de la page.

Voici la structure de la page et celle du bouton :

```javascript
<body> 
     <p>Integer posuere erat a ante venenatis...</p> 
     <button id="monBouton">Cliquez-moi</button> 
</body>
```
Le bouton possède l’identifiant  id="monBouton".

Voilà le code JavaScript utilisé dans cette page :

```javascript
<script> 
       var leBouton = document.getElementById("monBouton") ;
       leBouton.onclick = function(){ 
           alert(’Vous avez cliqué sur le bouton.’); 
       }; 
</script>
```

Détaillons ce script simple :

-   Dans la variable  leBouton, nous identifions le bouton.
    
-   Ensuite, nous associons à ce bouton l’événement  onclick. Cela permet de savoir si l’utilisateur clique sur ce bouton.
    
-   Si l’utilisateur clique sur le bouton, nous exécutons une fonction anonyme :  function(){...}. Cette fonction est dite anonyme, car elle ne possède pas de nom. Ce n’est pas nécessaire, car cette fonction n’est appelée qu’une seule fois, qu’à un seul moment, lorsque l’utilisateur clique sur le bouton. Cette fonction n’a pas besoin d’être appelée ailleurs.
    
-   Cette fonction affiche un simple message dans un  alert().

---
    
#### Utiliser un écouteur d’événement

Dans ce deuxième exemple, nous allons utiliser la fonction JavaScript écouteur d’événements : addEventListener()

Nous allons utiliser le même code HTML que dans l’exemple précédent.

```javascript
<script> 
    var leBouton = document.getElementById("monBouton") ; 
    leBouton.addEventListener("click",monAlerte,false) ; 
    function monAlerte(){ 
        alert(’Vous avez cliqué sur le bouton.’) ; 
    } ; 
</script>
```

Analysons ce code :

-   Nous retrouvons la même variable pour identifier le bouton.
    
-   Sur ce bouton, nous utilisons la méthode  addEventListener().
    
-   Le premier argument est l’événement que nous souhaitons écouter. Cet argument est une chaîne de caractères, il est donc placé entre guillemets. C’est l’événement  "click", c’est le fait que l’utilisateur clique sur un élément identifié. Voici l’URL des événements que nous pouvons écouter :  [https://developer.mozilla.org/fr/docs/Web/Events](https://developer.mozilla.org/fr/docs/Web/Events)
    

-   Le deuxième argument est le nom de la fonction qui doit être appelée lorsque cet événement est déclenché :  monAlerte.
    
-   Le troisième argument concerne des options, nous n’en avons pas besoin, donc nous indiquons  false.
    
-   Ensuite, nous avons la définition de la fonction  monAlerte()  qui doit être exécutée.
    

Les affichages sont strictement identiques aux précédents.

Cette deuxième solution est nettement plus propre et plus technique. Elle distingue bien tous les paramètres liés à l’écoute d’un événement.

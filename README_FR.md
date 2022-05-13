# Bonnes Pratiques : 

Les **bonnes pratiques** sont une sorte de liste de choses à faire, qui, lorsqu'appliquée, peut fortement aider le développement, la maintenance, la modification, l'optimisation et la compréhension du code en général.
 
 
*Voici une liste non exhaustive de bonnes pratiques que vous pouvez-suivre pour vos projets :*

## Sommaire

 - [Bonnes pratiques générales](https://github.com/TheHerbin/DevOps-GoodPractises/blob/main/README_FR.md#bonnes-pratiques-g%C3%A9n%C3%A9rales)
 - [Node JS](https://github.com/TheHerbin/DevOps-GoodPractises/blob/main/README_FR.md#bonne-pratiques-nodejs)
 - [React JS](https://github.com/TheHerbin/DevOps-GoodPractises/blob/main/README_FR.md#bonne-pratique-reactjs)
 - [Définition Of Done](https://github.com/TheHerbin/DevOps-GoodPractises/edit/main/README_FR.md#d%C3%A9finition-of-done)

## Bonnes pratiques générales

### `indent`

 - *Avoir une bonne indentation rendra votre code bien plus facile à comprendre..*.
   
   
     ```javascript
    function anExampleFunction() {
        let x;
        if(true){
            x = true;
        }else{
            x = false;
        }
        return x;
    }

    ```
### `Respect des convention de syntaxe `   


 - *Respecter les conventions comme camelCase ou SnakeCase peut être 
   bénéfique pour un projet en les rendant les fonctions, variables et
   objets plus faciles à lire.*
   

### `Commentez votre code ` 


 - *Aussi simple que cela puisse paraître,commenter son code peut être utile
   et peut avoir plusieures utilisations : cela peut être utilisé pour décrire 
   ce que fait une fonction, les paramètres qu'elle reçoit ou retourne,
   ou encore de partager ses doutes.*

### `Faites des sauvegardes ` 


 - *Faire des sauvegarde fréquentes, quelles soit locales ou en ligne
   vous permet de retrouver des morceaux de code en cas d'erreur 
    ou de retourner dans un état antérieur de votre projet.*

### `Gardez un code simple ` 


 - *Un code simple et concis facilite la lecture du code 
   et optimise indirectement votre projet*
   
### `Portabilité ` 


 - *N'utilisez pas trop de code ou de texte en dûr*

### `Evolubilité du code` 


 - *Ne verrouillez pas votre code et pensez à comment améliorer votre projet*
   

### `Modules, APIs et réutilisabilité du code` 


 - *Vous pouvez créer des modules et des fonctions destinées à être réutilisées. 
   Ainsi, votre code sera plus optimisé et moins lourd
   N'hésitez pas à utiliser l'api d'autres personnes.*

### `Réalisez des tests quotidiens et périodiques ` 


 - *Si vous voulez un code propre et carré, réalisez des tests de votre code quotidiennement et
   hebdomadairement. Cela peut réellement vous faire gagner du temps et réduit les chances d'erreurs
   et vous fera gagner du temps au final.*


# Bonne pratiques Node.js

(https://github.com/goldbergyoni/nodebestpractices/blob/master/README.french.md#1-structure-de-projet) 
(https://github.com/airbnb/javascript#comments)

## Table des matières

1. [Structure de projet](#1-structure-du-projet)
2. [Style du code](#2-style-du-code)


<br/><br/>
## `1. Structure du projet`
### 1.1 Organisez votre projet en composants

Le pire obstacle des énormes applications est la maintenance d'une base de code immense contenant des centaines de dépendances - un tel monolithe ralentit les développeurs tentant d'ajouter de nouvelles fonctionnalités. Pour éviter cela, répartissez votre code en composants, chacun dans son dossier avec son code dédié, et assurez vous que chaque unité soit courte et simple. Visitez le lien « Plus d'infos » plus bas pour voir des exemples de structure de projet correcte.

**Autrement :** Lorsque les développeurs qui codent de nouvelles fonctionnalités ont du mal à réaliser l'impact de leur changement et craignent de casser d'autres composants dépendants - les déploiements deviennent plus lents et plus risqués. Il est aussi considéré plus difficile d'élargir un modèle d'application quand les unités opérationnelles ne sont pas séparées.

<br/><br/>
### 1.2 Organisez vos composants en strates, gardez la couche web à l'intérieur de son périmètre

Chaque composant devrait contenir des « strates » - un objet dédié pour le web, un pour la logique et un pour le code d'accès aux données. Cela permet non seulement de séparer clairement les responsabilités mais permet aussi de simuler et de tester le système de manière plus simple. Bien qu'il s'agisse d'un modèle très courant, les développeurs d'API ont tendance à mélanger les strates en passant l'objet dédié au web (Par exemple Express req, res) à la logique opérationnelle et aux strates de données - cela rend l'application dépendante et accessible seulement par les frameworks web spécifiques.

**Autrement :** Les tests, les jobs CRON, les déclencheurs des files d'attente de messages et etc ne peuvent pas accéder à une application qui mélange les objets web avec les autres strates.

<br/><br/>

### 1.3 Séparez Express 'app' et 'server'

Evitez la sale habitude de définir l'appli [Express](https://expressjs.com/) toute entière dans un seul fichier immense - séparez la définition de votre 'Express' en au moins deux fichiers : la déclaration de l'API (app.js) et les responsabilités de gestion de réseau (WWW). Pour une structure encore plus poussée, localisez la déclaration de l'API dans les composants.

**Autrement :** Votre API sera seulement accessible aux tests par le biais d'appels HTTP (plus lent et plus difficile de générer des rapports de couverture). Cela ne sera pas un réel plaisir de maintenir des centaines de lignes de code dans un fichier unique.


<br/><br/>

### 1.4 Utilisez une configuration respectueuse de l'environnement, sécurisée et hiérarchique

La mise en place d'une configuration parfaite et sans faille doit garantir que (a) les clés peuvent être lues depuis un fichier ET à partir de la variable d'environnement (b) les secrets sont conservés hors du code source (c) la configuration est hiérarchique pour une recherche plus simple. Certains paquets peuvent gérer la plupart de ces points comme [rc](https://www.npmjs.com/package/rc), [nconf](https://www.npmjs.com/package/nconf), [config](https://www.npmjs.com/package/config) et [convict](https://www.npmjs.com/package/convict).

**Autrement :** Ne pas se soucier de ces exigences de configuration ne fera que ralentir l'équipe de développement ou l'équipe de DevOps. Probablement les deux.


<br/><br/><br/>



## `2. Style du code` 
### 2.1. Commentaire

  <a name="comments--multiline"></a><a name="2.1.1"></a>
  - [2.1.1](#comments--multiline) Utiliser `/** ... */` pour les commentaires mutilignes.

    ```javascript
    // bad
    // make() returns a new element
    // based on the passed in tag name
    //
    // @param {String} tag
    // @return {Element} element
    function make(tag) {

      // ...

      return element;
    }

    // good
    /**
     * make() returns a new element
     * based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }
    ```
     <a name="comments--singleline"></a><a name="1.2"></a>
  - [2.1.2](#comments--singleline) Utiliser `//` pour les commentaires sur une ligne.

    ```javascript
    // bad
    const active = true;  // is current tab

    // good
    // is current tab
    const active = true;

    // bad
    function getType() {
      console.log('fetching type...');
      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }

    // good
    function getType() {
      console.log('fetching type...');

      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }

    // also good
    function getType() {
      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }
    ```
    
    <a name="comments--spaces"></a>
  - [2.1.3](#comments--spaces) Commencez tous les commentaires par un espace pour faciliter la lecture. 

    ```javascript
    // bad
    //is current tab
    const active = true;

    // good
    // is current tab
    const active = true;

    // bad
    /**
     *make() returns a new element
     *based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }

    // good
    /**
     * make() returns a new element
     * based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }
    ```
<a name="comments--actionitems"></a><a name="1.4"></a>
  - [2.1.4](#comments--actionitems) Préfixer vos commentaires avec FIXMEou TODO aide les autres développeurs à comprendre rapidement si vous signalez un problème qui doit être réexaminé, ou si vous suggérez une solution au problème qui doit être implémentée. Ceux-ci sont différents des commentaires réguliers car ils sont exploitables..

  <a name="comments--fixme"></a><a name="1.5"></a>
  - [2.1.5](#comments--fixme) Utiliser `// FIXME:` pour annoter les problèmes.

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // FIXME: shouldn’t use a global here
        total = 0;
      }
    }
    ```

  <a name="comments--todo"></a><a name="1.6"></a>
  - [2.1.6](#comments--todo) Utiliser `// TODO:` pour annoter les solutions au problèmes.

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // TODO: total should be configurable by an options param
        this.total = 0;
      }
    }
    ```
    
### 2.2 Espace Blanc

<a name="whitespace--spaces"></a><a name="2.1"></a>
  - [2.2.1](#whitespace--spaces) Utilisez des tabulations logicielles (caractère d'espacement) définies sur 2 espaces.

    ```javascript
    // bad
    function foo() {
    ∙∙∙∙let name;
    }

    // bad
    function bar() {
    ∙let name;
    }

    // good
    function baz() {
    ∙∙let name;
    }
    ```

<a name="whitespace--before-blocks"></a><a name="2.2"></a>
  - [2.2.2](#whitespace--before-blocks) Placez 1 espace avant l'accolade principale.

    ```javascript
    // bad
    function test(){
      console.log('test');
    }

    // good
    function test() {
      console.log('test');
    }
    ```
<a name="whitespace--infix-ops"></a><a name="2.3"></a>
  - [2.2.3](#whitespace--infix-ops) Démarrez les opérateurs avec des espaces.

    ```javascript
    // bad
    const x=y+5;

    // good
    const x = y + 5;
    ```
    
<a name="whitespace--after-blocks"></a><a name="2.4"></a>
  - [2.2.4](#whitespace--after-blocks) Laissez une ligne vide après les blocs et avant l'instruction suivante..

    ```javascript
    // bad
    if (foo) {
      return bar;
    }
    return baz;

    // good
    if (foo) {
      return bar;
    }

    return baz;
    ```
  <a name="whitespace--in-parens"></a><a name="2.5"></a>
  - [2.2.5](#whitespace--in-parens) N'ajoutez pas d'espaces entre parenthèses. 

    ```javascript
    // bad
    function bar( foo ) {
      return foo;
    }

    // good
    function bar(foo) {
      return foo;
    }
    ```
 <a name="whitespace--in-braces"></a><a name="2.6"></a>
  - [2.2.6](#whitespace--in-braces) Ajoutez des espaces à l'intérieur des accolades.

    ```javascript
    // bad
    const foo = {clark: 'kent'};

    // good
    const foo = { clark: 'kent' };
    ```
<a name="whitespace--comma-spacing"></a>
  - [2.2.7](#whitespace--comma-spacing) Évitez les espaces avant les virgules et exigez un espace après les virgules.

    ```javascript
    // bad
    var foo = 1,bar = 2;
    var arr = [1 , 2];

    // good
    var foo = 1, bar = 2;
    var arr = [1, 2];
    ```
  <a name="whitespace--func-call-spacing"></a>
  - [2.2.8](#whitespace--func-call-spacing) Évitez les espaces entre les fonctions et leurs invocations.

    ```javascript
    // bad
    func ();

    func
    ();

    // good
    func();
    ```
### 2.3 Points-virgules

 <a name="semicolons--required"></a><a name="3.1"></a>
  - [2.3.1](#semicolons--required) Sensible

    > Lorsque JavaScript rencontre un saut de ligne sans point-virgule, il utilise un ensemble de règles appelé Insertion automatique de point-virgule (https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion) pour déterminer s'il doit considérer ce saut de ligne comme la fin d'une instruction et (comme son nom l'indique) placer un point-virgule dans votre code avant le saut de ligne. ASI contient cependant quelques comportements excentriques et votre code se cassera si JavaScript interprète mal votre saut de ligne.

    ```javascript
    // bad - raises exception
    const luke = {}
    const leia = {}
    [luke, leia].forEach((jedi) => jedi.father = 'vader')

    // bad - raises exception
    const reaction = "No! That’s impossible!"
    (async function meanwhileOnTheFalcon() {
      // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
      // ...
    }())

    // bad - returns `undefined` instead of the value on the next line - always happens when `return` is on a line by itself because of ASI!
    function foo() {
      return
        'search your feelings, you know it to be foo'
    }

    // good
    const luke = {};
    const leia = {};
    [luke, leia].forEach((jedi) => {
      jedi.father = 'vader';
    });

    // good
    const reaction = "No! That’s impossible!";
    (async function meanwhileOnTheFalcon() {
      // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
      // ...
    }());

    // good
    function foo() {
      return 'search your feelings, you know it to be foo';
    }
    ```

 ### 2.4. Conventions de nommage

  <a name="naming--descriptive"></a><a name="4.1"></a>
  - [2.4.1](#naming--descriptive) Évitez les noms à une seule lettre. Soyez descriptif avec votre nom.

    ```javascript
    // bad
    function q() {
      // ...
    }

    // good
    function query() {
      // ...
    }
    ```

  <a name="naming--camelCase"></a><a name="4.2"></a>
  - [2.4.2](#naming--camelCase) Utilisez camelCase pour nommer des objets, des fonctions et des instances.

    ```javascript
    // bad
    const OBJEcttsssss = {};
    const this_is_my_object = {};
    function c() {}

    // good
    const thisIsMyObject = {};
    function thisIsMyFunction() {}
    ```

  <a name="naming--PascalCase"></a><a name="4.3"></a>
  - [2.4.3](#naming--PascalCase) Utilisez PascalCase uniquement lorsque vous nommez des constructeurs ou des classes.

    ```javascript
    // bad
    function user(options) {
      this.name = options.name;
    }

    const bad = new user({
      name: 'nope',
    });

    // good
    class User {
      constructor(options) {
        this.name = options.name;
      }
    }

    const good = new User({
      name: 'yup',
    });
    ```

  <a name="naming--leading-underscore"></a><a name="4.4"></a>
  - [2.4.4](#naming--leading-underscore) N'utilisez pas de traits de soulignement à la fin ou au début.

    > Pourquoi? JavaScript n'a pas le concept de confidentialité en termes de propriétés ou de méthodes. Bien qu'un trait de soulignement en tête soit une convention courante pour signifier "privé", en fait, ces propriétés sont entièrement publiques et, en tant que telles, font partie de votre contrat d'API publique. Cette convention peut amener les développeurs à penser à tort qu'un changement ne sera pas considéré comme une rupture ou que les tests ne sont pas nécessaires.

    ```javascript
    // bad
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';
    this._firstName = 'Panda';

    // good
    this.firstName = 'Panda';

    // good, in environments where WeakMaps are available
    // see https://kangax.github.io/compat-table/es6/#test-WeakMap
    const firstNames = new WeakMap();
    firstNames.set(this, 'Panda');
    ```
    <br/>
 ### 2.5 Utilisez ESLint

[ESLint](https://eslint.org) est la norme de facto pour vérifier d'éventuelles erreurs de code et pour corriger le style du code, ce n'est pas uniquement pour identifier les problèmes d'espacement mais aussi pour détecter les antipatterns préoccupants du code comme par exemple les développeurs levant des erreurs sans classification. Bien qu'ESLint puisse corriger automatiquement les styles du code, d'autres outils comme [prettier](https://www.npmjs.com/package/prettier) et [beautify](https://www.npmjs.com/package/js-beautify) sont plus puissants dans le formatage de la correction et fonctionnent en collaboration avec ESLint.

**Autrement :** Les développeurs se concentreront sur les problèmes fastidieux d'espacement et de largeur de ligne, ce qui pourrait faire perdre du temps à trop réfléchir sur le style de code du projet.

<br/>

### 2.6 Commencez les accolades d'un bloc de code sur la même ligne

Les accolades ouvrantes d'un bloc de code doivent être sur la même ligne que l'instruction d'ouverture.

```javascript
// bad
function someFunction
{
  // bloc de code
}

// good
function someFunction() {
  // bloc de code
}
```

**Autrement :** Le non-respect de cette bonne pratique peut conduire à des résultats inattendus.

<br/><br/>


# Bonne pratique React.js

(https://www.codeinwp.com/blog/react-best-practices/)

Pour assurer la maintenabilité, la fiabilité et l'evolution du code voici 10 conseils des meilleurs pratiques de codage React.

<br/>

### `🐛 Conseil n°1 : Gardez les composant petits et spécifiques à la fonction`
Avec React, il est possible d'avoir d'énormes composants qui exécutent un certain nombre de tâches. Mais une meilleure façon de concevoir des composants est de les garder petits, de sorte qu'un composant corresponde à une fonction. Idéalement, un seul composant devrait rendre une partie spécifique de votre page ou modifier un comportement particulier. 

### `♻️ Conseil n°2 : La réutilisabilité des composants est importante`
En respectant la règle une fonction = un composant, vous pouvez améliorer la réutilisabilité des composants. Cela signifie que vous devez éviter d'essayer de créer un nouveau composant pour une fonction s'il existe déjà un composant pour cette fonction.
En réutilisant des composants dans votre projet ou dans n'importe quel nombre de projets, non seulement vous atteindrez la cohérence, mais vous contribuerez également à la communauté.

### ` 🤝 Conseil n°3 : Consolidez le code en double`
Une règle commune à tout code est de le garder aussi bref et concis que possible.

Ce n'est pas différent ici aussi, puisque les meilleures pratiques de React vous demandent également de garder un code bref et précis. Une façon d'y parvenir est d'éviter les doubles emplois – Ne vous répétez pas (DRY).

Vous pouvez y parvenir en examinant le code à la recherche de modèles et de similitudes. Si vous en trouvez, il est possible que vous répétiez du code et qu'il soit possible d'éliminer les doublons. Très probablement, un peu de réécriture peut le rendre plus concis.


### `🎨 Conseil n°4 : Mettez CSS dans JavaScript`
Lorsque vous commencez à travailler sur un projet, il est courant de conserver tous les styles CSS dans un seul fichier SCSS. L'utilisation d'un préfixe global empêche toute collision potentielle de noms. Cependant, lorsque votre projet évolue, cette solution peut ne pas être réalisable.

Il existe de nombreuses bibliothèques qui vous permettent d'écrire du CSS en JS. EmotionJS et Glamorous sont les deux CSS les plus populaires dans les bibliothèques JS.

### `📝 Conseil n°5 : Ne commentez que si nécessaire`
Joignez des commentaires au code uniquement lorsque cela est nécessaire. Ce n'est pas seulement conforme aux meilleures pratiques de React, cela sert également deux objectifs en même temps :

1. Cela gardera le code visuellement sans encombrement.
2. Vous éviterez un conflit potentiel entre le commentaire et le code, s'il vous arrive de modifier le code ultérieurement.

### `🦒 Conseil n°6 : Utilisez des majuscules pour les noms de composants`
Si,vous utilisez JSX (une extension JavaScript), les noms des composants que vous créez doivent commencer par des lettres majuscules. Par exemple, vous nommerez les composants au SelectButtonlieu de selectbutton, ou Menuau lieu de menu. Nous faisons cela pour que JSX puisse les identifier différemment des balises HTML par défaut.

Les versions antérieures de React maintenaient une liste de tous les noms intégrés pour les différencier des noms personnalisés. Mais comme la liste nécessitait une mise à jour constante, elle a été supprimée et les majuscules sont devenues la norme.

Si JSX n'est pas la langue de votre choix, vous pouvez utiliser des lettres minuscules. Cependant, cela peut réduire la réutilisation des composants au-delà de votre projet.

### `🚀 Conseil n°7 : Le code doit s'exécuter comme prévu et être testable`
Le code que vous écrivez doit se comporter comme prévu et pouvoir être testé facilement et rapidement. C'est une bonne pratique de nommer vos fichiers de test identiques aux fichiers source avec un .testsuffixe. Il sera alors facile de trouver les fichiers de test.

Vous pouvez utiliser JEST pour tester votre code React.

### `📁 Conseil n°8 : Tous les fichiers liés à un composant doivent être dans un seul dossier`
Conservez tous les fichiers relatifs à un composant dans un seul dossier, y compris les fichiers de style.

S'il existe un petit composant utilisé uniquement par un composant particulier, il est logique de conserver ces petits composants tous ensemble dans ce dossier de composants. La hiérarchie sera alors facile à comprendre - les gros composants ont leur propre dossier et toutes leurs petites parties sont divisées en sous-dossiers. De cette façon, vous pouvez facilement extraire du code vers n'importe quel autre projet ou même modifier le code quand vous le souhaitez.

### `🧰 Conseil n°9 : Utilisez des outils comme Bit`
L'une des meilleures pratiques React qui aide à organiser tous vos composants React est l'utilisation d'outils comme [Bit](https://bit.dev/).

Ces outils aident à maintenir et à réutiliser le code. Au-delà de cela, cela aide le code à devenir détectable et favorise la collaboration d'équipe dans la construction de composants. De plus, le code peut être synchronisé entre les projets.

### `✍️ Conseil n°10 : Ecrire des tests pour tout le code`
Dans n'importe quel langage de programmation, des tests adéquats garantissent que tout nouveau code ajouté à votre projet s'intègre bien au code existant et ne perturbe pas les fonctionnalités existantes. C'est une bonne idée d'écrire des tests pour tout nouveau composant que vous créez. En tant que bonne pratique, vous devez créer un __Test__répertoire dans le répertoire de votre composant pour héberger tous les tests pertinents.


# Définition Of Done

## C'est quoi ? 
La definition of done peut être élaborée en atelier par l’équipe technique, le product owner, scrum master et l’équipe QA agile.
L’exercice consiste à se mettre d’accord sur les critères qui semblent essentiels pour atteindre le niveau d’exigence souhaité pour le produit et assurer des livraisons de qualité.

Exemple de critères présents dans la DoD :
- Revue du code effectuée
- Les critères d’acceptation de la User Story sont tous validés
- Les différents tests ont été finalisés et acceptés par les acteurs de la qualité du produit (QA, PO, développeurs)
- La documentation a été mise à jour
- Les maquettes graphiques sont respectées
- Livré sur un environnement stable

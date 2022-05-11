Bonnes pratiques ?  

Les bonnes pratiques sont un ensemble de normes qui, lorsqu’elles sont respectées peuvent fortement aider le développement, la maintenance, la modification, pour l’optimisation et la compréhension du code en général. 



Voici une liste (non exhaustive) de bonnes pratiques à respecter lors du développement d’un projet en équipe ou seul : 



Bonnes Pratiques Générales :  

Indentation : 

Avoir une bonne indentation facilitera fortement la compréhension de votre code par les autres développeurs... 

Respect des conventions de syntaxe (ex : camelCase, SnakeCase) 

Le respect de telles conventions peut être très bénéfique un projet, cela permet de distinguer les fonctions des classes et des variables plus aisément et donc facilite la lecture du code. 

Commenter son code 

Aussi simple que cela puisse paraître, commenter son code peut être très utile et peut avoir plusieurs utilisations : cela peut être utilisé pour décrire ce que fait une fonction, les paramètres qu’elle reçoit ou retourne ou encore pour partager à d’autres développeurs ses doutes ou ajouter différentes indications comme ce qu’il faut ajouter à cet emplacement. 

Faire des sauvegardes  

Réaliser des sauvegardes fréquentes , que ce soit en local ou en ligne (git / github) 		permet de récupérer des morceaux de code que l’on peut avoir perdu ou encore de 		retourner à un état antérieur du projet. 

Garder un code simple 

Un code simple et concis facilite la lecture du code et permet d’avoir un 			programme moins lourd. 

Portabilité (pas de données entrées en Dur) 

Évolutivité du code  

Réutilisation de code et modules  

Réaliser des “tests” quotidiens et hebdomadaires 

Créer des classes de tests unitaires, fonctionnels, d’intégration... 

Utilisation d’API 



Bonne pratique REACT JS 

Architecture 

Afin de comprendre le déroulement du projet et à ajouter d’autres fonctionnalités à l’application, il est conseillé par REACT JS (https://fr.reactjs.org/docs/faq-structure.html) 

Groupé des dossiers par fonctionnalité ou par route 

Ex : placer le CSS, le JS et les tests ensemble dans des dossiers groupés par fonctionnalité ou par route. 

Groupé par type de fichier 

Ex : Une autre manière répandue de structurer les projets consiste à grouper les fichiers similaires ensemble 

Se limiter à maximum trois ou quatre imbrications de dossier dans un même projet car il devient plus difficile d’écrire des importations relatives entre eux ou de mettre à jours ces importations lorsque les fichiers sont déplacés. 

Bonne pratique NodeJS 

Architecture 

Organisez votre projet en composants 

Organisez vos composants en strates, gardez la couche web à l'intérieur de son périmètre 

Externalisez les utilitaires communs en paquets NPM 

Séparez Express 'app' et 'server' 

Utilisez une configuration respectueuse de l'environnement, sécurisée et hiérarchique 



Style de code  

(https://github.com/goldbergyoni/nodebestpractices/blob/master/README.french.md#1-structure-de-projet) 

ESLint:  est la norme de facto pour vérifier d'éventuelles erreurs de code et pour corriger le style du code, ce n'est pas uniquement pour identifier les problèmes d'espacement mais aussi pour détecter les antipatterns préoccupants du code comme par exemple les développeurs levant des erreurs sans classification. 



Commencez les accolades d'un bloc de code sur la même ligne.  

Le non-respect de cette bonne pratique peut conduire à des résultats inattendus.  





Bonne pratiques REACT JS 

Architecture 

Afin de comprendre le déroulement du projet et à ajouter d’autres fonctionnalités à l’application, il est conseillé par REACT JS (https://fr.reactjs.org/docs/faq-structure.html) 

Groupé des dossiers par fonctionnalité ou par route 

Ex : placer le CSS, le JS et les tests ensemble dans des dossiers groupés par fonctionnalité ou par route. 

Groupé par type de fichier 

Ex : Une autre manière répandue de structurer les projets consiste à grouper les fichiers similaires ensemble 

Se limiter à maximum trois ou quatre imbrications de dossier dans un même projet car il devient plus difficile d’écrire des importations relatives entre eux ou de mettre à jours ces importations lorsque les fichiers sont déplacés. 



# Bonne pratique Node.js

## Table des matières

1. [Structure de projet](#1-structure-du-projet)
2. [Style du code](#2-style-du-code)


<br/><br/>
## `1. Structure du projet`
### 1.1 Organisez votre projet en composants

**TL;PL :** Le pire obstacle des énormes applications est la maintenance d'une base de code immense contenant des centaines de dépendances - un tel monolithe ralentit les développeurs tentant d'ajouter de nouvelles fonctionnalités. Pour éviter cela, répartissez votre code en composants, chacun dans son dossier avec son code dédié, et assurez vous que chaque unité soit courte et simple. Visitez le lien « Plus d'infos » plus bas pour voir des exemples de structure de projet correcte.

**Autrement :** Lorsque les développeurs qui codent de nouvelles fonctionnalités ont du mal à réaliser l'impact de leur changement et craignent de casser d'autres composants dépendants - les déploiements deviennent plus lents et plus risqués. Il est aussi considéré plus difficile d'élargir un modèle d'application quand les unités opérationnelles ne sont pas séparées.

<br/><br/>
### 1.2 Organisez vos composants en strates, gardez la couche web à l'intérieur de son périmètre

**TL;PL :** Chaque composant devrait contenir des « strates » - un objet dédié pour le web, un pour la logique et un pour le code d'accès aux données. Cela permet non seulement de séparer clairement les responsabilités mais permet aussi de simuler et de tester le système de manière plus simple. Bien qu'il s'agisse d'un modèle très courant, les développeurs d'API ont tendance à mélanger les strates en passant l'objet dédié au web (Par exemple Express req, res) à la logique opérationnelle et aux strates de données - cela rend l'application dépendante et accessible seulement par les frameworks web spécifiques.

**Autrement :** Les tests, les jobs CRON, les déclencheurs des files d'attente de messages et etc ne peuvent pas accéder à une application qui mélange les objets web avec les autres strates.

<br/><br/>

### 1.3 Séparez Express 'app' et 'server'

**TL;PL :** Evitez la sale habitude de définir l'appli [Express](https://expressjs.com/) toute entière dans un seul fichier immense - séparez la définition de votre 'Express' en au moins deux fichiers : la déclaration de l'API (app.js) et les responsabilités de gestion de réseau (WWW). Pour une structure encore plus poussée, localisez la déclaration de l'API dans les composants.

**Autrement :** Votre API sera seulement accessible aux tests par le biais d'appels HTTP (plus lent et plus difficile de générer des rapports de couverture). Cela ne sera pas un réel plaisir de maintenir des centaines de lignes de code dans un fichier unique.


<br/><br/>

### 1.4 Utilisez une configuration respectueuse de l'environnement, sécurisée et hiérarchique

**TL;PL :** La mise en place d'une configuration parfaite et sans faille doit garantir que (a) les clés peuvent être lues depuis un fichier ET à partir de la variable d'environnement (b) les secrets sont conservés hors du code source (c) la configuration est hiérarchique pour une recherche plus simple. Certains paquets peuvent gérer la plupart de ces points comme [rc](https://www.npmjs.com/package/rc), [nconf](https://www.npmjs.com/package/nconf), [config](https://www.npmjs.com/package/config) et [convict](https://www.npmjs.com/package/convict).

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



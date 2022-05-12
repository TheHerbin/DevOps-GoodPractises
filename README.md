# Good Practices : 

The **good practises** are a set of standards which, when adhered to, can greatly help the development, maintenance, modification, optimization and understanding of code in general.
 
 
*Here is a list of good practices that you can follow when developing a project in a team or alone:*

## Summary 

 - [General Good Practices](https://github.com/TheHerbin/DevOps-GoodPractises#general-good-practices)
 - [Node JS](https://github.com/TheHerbin/DevOps-GoodPractises#best-practices-nodejs)
 - [React JS](https://github.com/TheHerbin/DevOps-GoodPractises#best-practices-reactjs)

## General Good Practices

### `indent`

 - *Having good indentation will make it much easier for other developers
   to understand your code..*.
   
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
### `Respect of syntax conventions `   


 - *Respecting conventions such as camelCase or SnakeCase can be very
   beneficial to a project, it makes it easier to distinguish functions
   from classes and variables and therefore makes it easier to read the
   code.*

### `Comment your code ` 


 - *As simple as it may seem, commenting on your code can be very useful
   and can have several uses: it can be used to describe what a function
   does, the parameters it receives or returns, or to share its doubts
   or add different indications like what to add to this location.*

### `Make backups ` 


 - *Performing frequent backups, whether locally or online (git / github)
   allows you to recover pieces of code that you may have lost or to
   return to a previous state of the project.*

### `Keep code simple ` 


 - *A simple and concise code facilitates the reading of the code and
   makes it possible to have a less cumbersome program.*
   
### `Portability ` 


 - *Do not use too much of hardcoded text, data or code*

### `Code scalability` 


 - *Do not lock your code and always think of how to upgrade or improve
   your code...*

### `Modules, API's and code re-usability` 


 - *You can create modules and functions that can be re-used later. This
   way, your code will be optimised because you will have less code
   locally. You can even use the APi's and modules of other people.*

### `Carry out daily and weekly “tests” ` 


 - *If you want a clean and squared code, dont forget to do daily and
   weekly tests of your application / Software. It can really make you
   gain some time and prevent you from creating bugs and other troubles
   at the end.*

# Best practices Node.js

(https://github.com/goldbergyoni/nodebestpractices/blob/master/README.french.md#1-structure-de-projet) 
(https://github.com/airbnb/javascript#comments)

## Table of contents

1. [Project structure](#1-project-structure)
2. [Style of code](#2-style-of-code)


<br/><br/>
## `1. Project structure`
### 1.1 Organize your project into components

The worst obstacle of huge applications is maintaining a huge code base with hundreds of dependencies - such a monolith slows down developers trying to add new features. To avoid this, break your code into components, each in its own folder with its own dedicated code, and keep each unit short and simple. Visit the "More Info" link below to see examples of proper project structure.

Otherwise: When developers coding new features have trouble realizing the impact of their change and fear breaking other dependent components - deployments become slower and riskier. It is also considered more difficult to extend an application model when business units are not separated.

<br/><br/>
### 1.2 Organize your components in layers, keep the web layer inside its perimeter
Each component should contain 'layers' - a dedicated object for the web, one for the logic and one for the data access code. This not only provides a clear separation of responsibilities but also allows for simpler simulation and testing of the system. Although this is a very common model, API developers tend to mix the layers by passing the web-dedicated object (e.g. Express req, res) to the business logic and data layers - this makes the application dependent on and accessible only by specific web frameworks.

Otherwise: Tests, CRON jobs, message queue triggers and etc cannot access an application that mixes web objects with other strata.


**Autrement :** Les tests, les jobs CRON, les déclencheurs des files d'attente de messages et etc ne peuvent pas accéder à une application qui mélange les objets web avec les autres strates.

<br/><br/>

### 1.3 Separate Express 'app' and 'server

Avoid the nasty habit of defining the entire [Express](https://expressjs.com/) app in one huge file - separate your 'Express' definition into at least two files: the API declaration (app.js) and the network management responsibilities (WWW). For even more structure, locate the API declaration in the components.

**Otherwise:** Your API will only be accessible to tests via HTTP calls (slower and harder to generate coverage reports). It won't be much fun to maintain hundreds of lines of code in a single file.


<br/><br/>

### 1.4 Use an environmentally friendly, secure and hierarchical configuration

Setting up a perfect and flawless configuration must ensure that (a) keys can be read from a file AND from the environment variable (b) secrets are kept out of the source code (c) the configuration is hierarchical for easier searching. Some packages can handle most of these points like [rc](https://www.npmjs.com/package/rc), [nconf](https://www.npmjs.com/package/nconf), [config](https://www.npmjs.com/package/config) and [convict](https://www.npmjs.com/package/convict).

**Otherwise:** Not caring about these configuration requirements will only slow down the development team or the DevOps team. Probably both.


<br/><br/><br/>



## `2. Style of code`
### 2.1. Comments

  <a name="comments--multiline"></a><a name="2.1.1"></a>
  - [2.1.1](#comments--multiline) Use `/** ... */` for multiline comments.

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
  - [2.1.2](#comments--singleline) Use `//` for single line comments.

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
  - [2.1.3](#comments--spaces) Start all comments with a space to make it easier to read.  

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
  - [2.1.4](#comments--actionitems) Prefixing your comments with FIXME or TODO helps other developers quickly understand if you’re pointing out a problem that needs to be revisited, or if you’re suggesting a solution to the problem that needs to be implemented. These are different than regular comments because they are actionable..

  <a name="comments--fixme"></a><a name="1.5"></a>
  - [2.1.5](#comments--fixme) Use `// FIXME:` to annotate problems.

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
  - [2.1.6](#comments--todo) Use `// TODO:` to annotate solutions to problems.

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // TODO: total should be configurable by an options param
        this.total = 0;
      }
    }
    ```
    
### 2.2 Whitespace

<a name="whitespace--spaces"></a><a name="2.1"></a>
  - [2.2.1](#whitespace--spaces) Use soft tabs (space character) set to 2 spaces.

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
  - [2.2.2](#whitespace--before-blocks) Place 1 space before the leading brace.

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
  - [2.2.3](#whitespace--infix-ops) Set off operators with spaces.

    ```javascript
    // bad
    const x=y+5;

    // good
    const x = y + 5;
    ```
    
<a name="whitespace--after-blocks"></a><a name="2.4"></a>
  - [2.2.4](#whitespace--after-blocks) Leave a blank line after blocks and before the next statement.

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
  - [2.2.5](#whitespace--in-parens) Do not add spaces inside parentheses.

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
  - [2.2.6](#whitespace--in-braces) Add spaces inside curly braces.

    ```javascript
    // bad
    const foo = {clark: 'kent'};

    // good
    const foo = { clark: 'kent' };
    ```
<a name="whitespace--comma-spacing"></a>
  - [2.2.7](#whitespace--comma-spacing) Avoid spaces before commas and require a space after commas.

    ```javascript
    // bad
    var foo = 1,bar = 2;
    var arr = [1 , 2];

    // good
    var foo = 1, bar = 2;
    var arr = [1, 2];
    ```
  <a name="whitespace--func-call-spacing"></a>
  - [2.2.8](#whitespace--func-call-spacing) Avoid spaces between functions and their invocations.

    ```javascript
    // bad
    func ();

    func
    ();

    // good
    func();
    ```
### 2.3 Semicolons

 <a name="semicolons--required"></a><a name="3.1"></a>
  - [2.3.1](#semicolons--required) Sensitive

    > When JavaScript encounters a line break without a semicolon, it uses a set of rules called (https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion) to determine whether it should regard that line break as the end of a statement, and (as the name implies) place a semicolon into your code before the line break if it thinks so. ASI contains a few eccentric behaviors, though, and your code will break if JavaScript misinterprets your line break. 

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

 ### 2.4. Naming Conventions

  <a name="naming--descriptive"></a><a name="4.1"></a>
  - [2.4.1](#naming--descriptive) Avoid single letter names. Be descriptive with your naming.

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
  - [2.4.2](#naming--camelCase) Use camelCase when naming objects, functions, and instances.

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
  - [2.4.3](#naming--PascalCase) Use PascalCase only when naming constructors or classes.

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
  - [2.4.4](#naming--leading-underscore) Do not use trailing or leading underscores. 

    > Why? JavaScript does not have the concept of privacy in terms of properties or methods. Although a leading underscore is a common convention to mean “private”, in fact, these properties are fully public, and as such, are part of your public API contract. This convention might lead developers to wrongly think that a change won’t count as breaking, or that tests aren’t needed.

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
 ### 2.5 Use ESLint

[ESLint](https://eslint.org) is the de facto standard for code error checking and code style correction, not only for identifying spacing problems but also for detecting worrisome anti-patterns in the code, such as developers lifting errors without classification.  Although ESLint can automatically correct code styles, other tools such as [prettier](https://www.npmjs.com/package/prettier) and [beautify](https://www.npmjs.com/package/js-beautify) are more powerful in formatting the correction and work in conjunction with ESLint.

**Otherwise**: Developers will focus on tedious spacing and line-width issues, which may waste time overthinking the project's code style.

<br/>

### 2.6 Start the braces of a code block on the same line

The opening braces of a code block must be on the same line as the opening statement.

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

**Otherwise:** Failure to follow this good practice may lead to unexpected results.

<br/><br/>


# Best practices React.js

(https://www.codeinwp.com/blog/react-best-practices/)

To ensure code maintainability, reliability, and evolution, here are 10 React coding best practices tips.

<br/>

### `🐛 Advice n°1 : Keep components small and function-specific`
With React, it’s possible to have huge components that execute a number of tasks. But a better way to design components is to keep them small, so that one component corresponds to one function. Ideally, a single component should render a specific bit of your page or modify a particular behavior.

### `♻️ Advice n°2 : Reusability of components is important`
By sticking to the rule of one function = one component, you can improve the reusability of components. What this means is that you should skip trying to build a new component for a function if there already exists a component for that function.
By reusing components across your project or across any number of projects, not only will you achieve consistency, you’ll also be contributing to the community.

### ` 🤝 Advice n°3 : Consolidate duplicate code`
A common rule for all code is to keep it as brief and concise as possible.

It’s no different here too, since React best practices also instruct you to keep code brief and precise. One way to do this is to avoid duplication – Don’t Repeat Yourself (DRY).

You can achieve this by scrutinizing the code for patterns and similarities. If you find any, it’s possible you’re repeating code and there’s scope to eliminate duplication. Most likely, a bit of rewriting can make it more concise.


### `🎨 Advice n°4 : Put CSS in JavaScript`
When you start working on a project, it is a common practice to keep all the CSS styles in a single SCSS file. The use of a global prefix prevents any potential name collisions. However, when your project scales up, this solution may not be feasible.

There are many libraries that enable you to write CSS in JS. EmotionJS and Glamorous are the two most popular CSS in JS libraries.

### `📝 Advice n°5 : Comment only where necessary`
Attach comments to code only where necessary. This is not only in keeping with React best practices, it also serves two purposes at the same time:

1. It’ll keep code visually clutter free.
2. You’ll avoid a potential conflict between comment and code, if you happen to alter the code at some later point in time.

### `🦒 Advice n°6 : Use capitals for component names`
If, like most folks, you’re using JSX (a JavaScript extension), the names of the components you create need to begin with uppercase letters. For instance, you’ll name components as SelectButton instead of selectbutton, or Menu instead of menu. We do this so that JSX can identify them differently from default HTML tags.

Earlier React versions maintained a list of all built-in names to differentiate them from custom names. But as the list needed constant updating, that was scrapped and capitals became the norm.

In case JSX is not your language of choice, you can use lowercase letters. However, this may reduce the reusability of components beyond your project.

### `🚀 Advice n°7 : Code should execute as expected and be testable`
Really, this rule needs no explanation. The code you write should behave as expected, and be testable easily and quickly. It’s a good practice to name your test files identical to the source files with a .test suffix. It’ll then be easy to find the test files.

You can use JEST to test your React code.

### `📁 Advice n°8 : All files related to any one component should be in a single folder`
Keep all files relating to any one component in a single folder, including styling files.

If there’s any small component used by a particular component only, it makes sense to keep these smaller components all together within that component folder. The hierarchy will then be easy to understand – large components have their own folder and all their smaller parts are split into sub-folders. This way, you can easily extract code to any other project or even modify the code whenever you want.

### `🧰 Advice n°9 : Use tools like Bit`
One of React best practices that helps to organize all your React components is the use of tools like [Bit](https://bit.dev/).

These tools help to maintain and reuse code. Beyond that, it helps code to become discoverable, and promotes team collaboration in building components. Also, code can be synced across projects.

### `✍️ Advice n°10 : Write tests for all code`
In any programming language, adequate testing ensures that any new code added to your project integrates well with existing code and does not break existing functionality. It is a good idea to write tests for any new component that you create. As a good practice, you should create a __Test__ directory within your component’s directory to house all relevant tests.

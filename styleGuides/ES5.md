# Stroll JavaScript ES5 Style Guide () {
*A somewhat reasonable-ish approach to JavaScript*
*Praying to move to ES6 once we don't have to support IE8*

## Table of Contents

1. [Types](#types)
2. [Objects](#objects)
3. [Arrays](#arrays)
4. [Strings](#strings)
5. [Functions](#functions)
6. [Properties](#properties)
7. [Variables](#variables)
8. [Hoisting](#hoisting)
9. [Comparison Operators & Equality](#comparison-operators--equality)
10. [Blocks](#blocks)
11. [Comments](#comments)
12. [Whitespace](#whitespace)
13. [Commas](#commas)
14. [Semicolons](#semicolons)
15. [Type Casting & Coercion](#type-casting--coercion)
16. [Naming Conventions](#naming-conventions)
17. [Accessors](#accessors)
18. [Constructors](#constructors)
19. [Events](#events)
20. [Modules](#modules)
21. [jQuery](#jQuery)
22. [ECMA Script 5 Compatability](#ecmascript-5-compatability)
23. [Testing](#testing)
24. [Performance](#performance)
25. [Resources](#resources)
26. [Additional Notes](#additional-notes)
27. [License](#license)

## Types

  - **Primatives**: When you acces a primative type you work directly on its value.

    + `string`
    + `number`
    + `boolean`
    + `null`
    + `undefined`

    ```javascript
    var foo = [1, 2];
    var bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9;
    ```

**[⬆ back to top](#table-of-contents)**

## Objects

  - Use the literal syntax for object creation. [Why?](http://stackoverflow.com/questions/4597926/what-is-the-difference-between-new-object-and-object-literal-notation)

    ```javascript
    // bad
    var item = new Object();

    // good
    var item = {};
    ```

  - Don't use [reserved words](http://es5.github.io/#x7.6.1) as keys. It won't work in IE8 [More info](https://github.com/airbnb/javascript/issues/61).

    ```javascript
    // bad
    var superman = {
      default: { clark: 'kent' },
      private: true
    };

    // good
    var superman = {
      defaults: { clark: 'kent' },
      hidden: true
    };
    ```

  - Use readable synonyms in place of reserved words.

    ```javascript
    // bad
    var superman = {
      class: 'alien'
    };

    // bad
    var superman = {
      klass: 'alien'
    };

    // good
    var superman = {
      type: 'alien'
    };
    ```

**[⬆ back to top](#table-of-contents)**

## Arrays

  - Use the literal syntax for array. [Why?](http://stackoverflow.com/questions/931872/what-s-the-difference-between-array-and-while-declaring-a-javascript-ar)

    ```javascript
    // bad
    var items = new Array();

    // good
    var items = [];
    ```

  - Use Array#push instead of direct assignment to add items to an array.

    ```javascript
    var someStack = [];

    // bad
    someStack[someStack.length] = 'aabbcc';

    // good
    someStack.push('aabbcc');
    ```

  - When you need to copy an array use Array#slice. [jsPerf](http://jsperf.com/converting-arguments-to-an-array/7)

    ```javascript
    var len = items.length;
    var itemsCopy = [];
    var i;

    // bad
    for (var i = 0; i < len.length; i++) {
      itemsCopy[i] = len[i];
    }

    // good
    itemsCopy = items.slice();
    ```

  - To convert an array-like object to an array, use Array#slice.

    ```javascript
    function trigger() {
      var args = Array.prototype.slice.call(arguments);
      // alternatively:
      var args = [].slice.call(arguments)
      ...
    };
    ```

**[⬆ back to top](#table-of-contents)**

## Strings

  - Strings longer than 100 characters should be written across multiple lines using string concatenation.
  - Note: If overused, long strings with concatenation could impact performance. [jsPerf](http://jsperf.com/ya-string-concat) & [Discussion](https://github.com/airbnb/javascript/issues/40).

    ```javascript
    // bad
    var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

    // bad
    var errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // good
    var errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';
    ```

    - When programatically building up a string, use Array#join instead of string concatenation. Mostly due to our friend IE: [jsPerf](http://jsperf.com/string-vs-array-concat/2).

    ```javascript
    var items;
    var messages;
    var length;
    var i;

    messages = [{
      state: 'success',
      message: 'This one worked.'
    }, {
      state: 'success',
      message: 'This one worked as well.'
    }, {
      state: 'error',
      message: 'This one did not work.'
    }];

    length = messages.length;

    // bad
    function inbox(messages) {
      items = '<ul>';

      for (i = 0; i < length; i++) {
        items += '<li>' + messages[i].message + '</li>';
      }

      return items + '</ul>';
    }

    // good
    function inbox(messages) {
      items = [];

      for (i = 0; i < length; i++) {
        // use direct assignment in this case because we're micro-optimizing.
        items[i] = '<li>' + messages[i].message + '</li>';
      }

      return '<ul>' + items.join('') + '</ul>';
    }
    ```

**[⬆ back to top](#table-of-contents)**

## Functions

  - Function expressions:

    ```javascript
    // anonymous function expression
    var anonymous = function () {
      return true;
    };

    // named function expression
    var named = function named () {
      return true;
    };

    // immediately-invoked function expression (IIFE)
    (function () {
      console.log('Welcome to the Internet. Please follow me.');
    })();
    ```

  - Never declare a function in a non-function block (if, while, etc).  Assign the function to a variable instead.  Browsers will allow you to do it, but they all interpret it differently.
  ![alt text](http://i.imgur.com/BY3Jlhj.png "Bad News Bears")

  - **Note:** ECMA-262 defines a `block` as a list of statements. A function declaration is not a statement. [Read ECMA-262's note on this issue](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf#page=97).

    ```javascript
    // bad
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    // good
    var test;
    if (currentUser) {
      test = function test() {
        console.log('Yup.');
      };
    }
    ```

  - Never name a parameter `arguments`. This will take precedence over the `arguments` object that is given to every function scope.

    ```javascript
    // bad
    function nope(name, options, arguments) {
      // ...stuff...
    }

    // good
    function yup(name, options, args) {
      // ...stuff...
    }
    ```

**[⬆ back to top](#table-of-contents)**

## Properties

  - Use dot notation when accessing properties.

    ```javascript
    var luke = {
      jedi: true
      age: 28
    };

    // bad
    var isJedi = luke['jedi'];

    // good
    var isJedi = luke.jedi;
    ```

  - Use subscript notation `[]` when accessing properties with a variable, for instance when meta-programming (very useful when making reusable components).

    ```javascript
    var luke = {
      jedi = true,
      age: 28
    };

    function getProp(prop) {
      return luke[prop];
    };

    var isJedi = getProp('jedi');
    ```

**[⬆ back to top](#table-of-contents)**

## Variables

  - Always use `var` to declare variables (we can't use const due to IE not supporting it).  Not doing so will result in global variables.  We want to avoid poluting the global namespace.  Remember what Captain Planet warned us about.

    ```javascript
    // bad
    superPower = new SuperPower();

    // good
    var superPower = new SuperPower();
    ```

  - Use one `var` declaration per variable.
    It's easier to add new variable declarations this way, and you never have to worry about swapping out a `;` for a `,` or introducing punctuation only diffs.

      ```javascript
      // bad
      var items = getItems(),
          goSportsTeam = true,
          dragonball = 'z';

      // bad
      // (compare to above, and try to spot the mistake)
      var items = getItems(),
          goSportsTeam = true;
          dragonball = 'z';

      // good
      var items = getItems();
      var goSportsTeam = true;
      var dragonball = 'z';
      ```

    - Declare unassigned variables last.  This is helpful when later on you might need to assign a variable depending on one of the previous assigned variables.

      ```javascript
      // bad
      var i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

      // bad
      var i;
      var items = getItems();
      var dragonball;
      var goSportsTeam = true;
      var len;

      // good
      var items = getItems();
      var goSportsTeam = true;
      var dragonball = 'z';
      var length;
      var i;
      ```

    - Assign variables at the top of their scope. This helps avoid issues with variable declaration and assignment hoisting related issues.

      ```javascript
      // bad
      function () {
        test();
        console.log('doing stuff..');

        //..other stuff..

        var name = getName();

        if (name === 'test') {
          return false;
        }

        return name;
      }

      // good
      function () {
        var name = getName();

        test();
        console.log('doing stuff..');

        //..other stuff..

        if (name === 'test') {
          return false;
        }

        return name;
      }

      // bad - unnecessary function call
      function () {
        var name = getName();

        if (!arguments.length) {
          return false;
        }

        this.setFirstName(name);

        return true;
      }

      // good
      function () {
        var name;

        if (!arguments.length) {
          return false;
        }

        name = getName();
        this.setFirstName(name);

        return true;
      }
      ```

**[⬆ back to top](#table-of-contents)**

## Hoisting

  - Variable declarations get hoisted to the top of their scope, but their assignment does not.

    ```javascript
    // we know this wouldn't work (assuming there
    // is no notDefined global variable)
    function example () {
      console.log(notDefined); // => throws a ReferenceError
    };

    /* creating a variable declaration after you
    *  reference the variable will work due to
    *  variable hoisting.  Note: the assignment
    *  value of `true` is not hoisted.
    */
    function example () {
      console.log(declaredButNotAssigned); // => undefined
      var declaredButNotAssigned = true;
    };

    /* The interpreter is hoisting the variable
    *  declaration to the top of the scope,
    *  which means our example could be rewritten as:
    */
    function example () {
      var declaredButNotAssigned;
      console.log(declaredButNotAssigned); // => undefined
      declaredButNotAssigned = true;
    };
    ```
  - Anonymous function expressions hoist their variable name, but not the function assignment.

    ```javascript
    function example () {
      console.log(anonymous); // => undefined

      anonymous(); // => TypeError anonymous is not a function

      var anonymous = function () {
        console.log('anonymous function expression')
      };
    };
    ```

  - Named function expressions hoist the variable name, not the function name or the function body.

    ```javascript
    function example () {
      console.log(named); // => undefined

      named(); // TypeError named is not a function

      superPower(); // => ReferenceError superPower is not defined

      var named = function superPower () {
        console.log('Flying');
      };
    };

    // the same is true when the function name
    // is the same as the variable name.
    function example () {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      var named = function named () {
        console.log('named');
      };
    };
    ```

  - Function declarations hoist their name and function body.

    ```javascript
    function example () {
      superPower(); // => Flying

      function superPower () {
        console.log('Flying');
      };
    };
    ```

  - For more information refer to [JavaScript Scoping & Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting) by [Ben Cherry](http://www.adequatelygood.com/).

**[⬆ back to top](#table-of-contents)**

# };

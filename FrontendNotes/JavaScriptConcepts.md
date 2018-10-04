# JavaScript
- Prototypical inheritance
- Closures
- Async

## Overview
- **Interpreted**
- **Prototype-based**: style of OOP, classes not explicitly defined, instead objects are reused
- **Multi-paradigm**
  - **Imperative/procedural programming** (explicit statements that change program state), **OOP**, **functional programming** (functions to avoid global state)
- **Weakly typed**:

## Asynchronous
- **Asynchronous**: engine runs in an event loop --> single program thread can handle concurrent operations

## Function Expression vs. Declaration
- **Function declaration**: defines a named function variable wo assignment, like sibling of variable declaration (function instead of const)
  ```js
  function bar() {
    return 3;
  }
  ```
- **Function expression**: preferred, defines named or anonymous function as part of a larger expression syntax (variable assignment)
  ```js
  // anonymous
  var a = function() {
    return 3;
  }
  ```
- Difference: expression not visible outside its scope
  - Hoisting
    ```js
    // function declaration alw hoisted
    function foo(){
      function bar() {
        return 3;
      }
      return bar();
      function bar() {
        return 8;
      }
    }
    alert(foo()); //8
    ```
    ```js
    // variable declarations are hoisted, but assignment expressions don't
    function foo(){
        var bar = function() {
            return 3;
        };
        return bar();
        // when bar below is hoisted, its var bar = undefined
        var bar = function() {
            return 8;
        };
    }
    alert(foo());
    ```


## Strict Mode
ES5, intentionally has diff semantics from normal code
- ```'use strict';``` to invoke in entire script or single func (recommended, bc it will concat non-strict with strict scripts)
  ```js
  function strict() {
    // function-level strict mode syntax
    'use strict';
    function nested() { return 'And so am I!'; }
    return "Hi!  I'm a strict mode function!  " + nested();
  }
  function notStrict() { return "I'm not strict."; }
  ```

Changes:
2 major: silent errors to throw errors, can sometimes run faster (bc fixes mistakes that make it difficult for JS engines to optimize)

- Silent errors to throw errors
    1. Global variables --> ReferenceError thrown
    2. Assignments that would normally silently fail --> TypeError thrown
      - Assignment to non-writable global (var undefined = 5; var Infinity = 5;)
      - Assignment to non-writable property, getter-only property, or new property on a non-extensible obj
    3. Attempts to delete undeletable properties --> TypeError thrown
    4. Function params names not unique --> syntax error
    5. Octal syntax --> syntax error
    6. Set properties on primitives --> TypeError thrown
      - Ex.: ```(14).sailing = 'home'```, ```false.true = ''```, ```'with'.you = 'far away'```

- Simplifies variable uses
  1. ```with``` --> syntax error
  2. ```eval``` --> doesn't introduce new variables into scope
  3. Delete plain names --> syntax error
    ```js
      var x;
      delete x; // error
    ```

- Makes ```eval``` and ```arguments``` simpler

## Immediately-Invoked Function Expression (IIFE, 'iffy')
- IIFE: variables declared inside IIFE not visible outside
- Several stylistic variations
  1. ```!```, ```+```, ```-```, ```~```, or ```void``` signals treatment of code afterward as an expression
    - If no need to reuse the function's return value
    ```js
    !function() {
        alert("Hello from IIFE!");
    }();
    // Shows the alert "Hello from IIFE!"
    ```
  2. Turn into expression in another way and invoke
    ```js
    // Variation 1
    (function() {
        alert("I am an IIFE!");
    }());

    // Variation 2
    (function() {
        alert("I am an IIFE, too!");
    })();
    ```
- Uses
  1. Prevent polluting global environment: make variable block scope, if you can't use let and const (not ES5 supported)
  2. Avoid variable hoisting wi blocks
  3. Allow public access to methods while retaining privacy for variables in that func
  4. Aliasing variables: resolve two global naming conflicts
    ```js
    window.$ = function somethingElse() {
        // ...
    };

    (function($) {
        // ...
    })(jQuery);
    ```
  5. Capturing global object

## ECMAScript Versions
ES5
- Strict mode
- Methods
  - String.trim()
  - Array.isArray()
  - Array.forEach(), Array.map(), Array.filter(), Array.reduce()
  - Array.every(), Array.some()
  - Array.indexOf(), Array.lastIndexOf()
  - JSON.parse() receives data from server, JSON.stringify() sends data
  - Date.now()
- Trailing commas in array and objects

## Sources:
Strict mode: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode
IIFE's: https://medium.com/@vvkchandra/essential-javascript-mastering-immediately-invoked-function-expressions-67791338ddc6, https://blog.mariusschulz.com/2016/01/19/use-cases-for-javascripts-iifes, https://en.wikipedia.org/wiki/Immediately-invoked_function_expression

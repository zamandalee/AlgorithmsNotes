<p align="center>JavaScript</p>
- Closures
- Async

<p align="center">
  <a href="#overview">Overview</a> •
  <a href="#asynchronous">Asynchronous</a> •
  <a href="#promise">Promise</a> •
  <a href="#prototypal-inheritance">Prototypal Inheritance</a> •
  <a href="#closures">Closures</a> •
  <a href="#function-expression-vs-declaration">Func Expression vs Declaration</a> •
  <a href="#pure-functions">Pure Functions</a> •
  <a href="#iife">IIFE</a> •
  <a href="#strict-mode">Strict Mode</a> •
  <a href="#ecmascript-versions">ECMAScript Versions</a>
  <a href="#jquery">jQuery</a>
  <a href="#context">Context</a>
  <a href="#attribute-vs-property">Attribute vs Property</a> •
  <a href="#equals">Equals</a>
  <a href="#currying">Currying</a>
</p>

## Overview
- **Interpreted**: language --> ready to run --> virtual machine interprets --> machine code
- **Prototype-based**: style of OOP, classes not explicitly defined, instead objects are reused
- **Multi-paradigm**
  - **Imperative/procedural programming** (explicit statements that change program state), **OOP**, **functional programming** (functions to avoid global state)
- **Dynamically typed**: a type is associated with each value, rather than just with each expression. In fact, JavaScript supports various ways to test the type of an object, including duck typing
- **Lexical scope**: scope is defined by author-time decisions of where functions are declared
  - **Lexing phase**: during compilation, know the where and how of declarations, able to predict how they'll be looked up during execution


## Asynchronous
- **Asynchronous**: engine runs in an event loop --> single program thread can handle concurrent operations
- Scope challenges w asynchronous
  ```js
  // outputs 4 sec, 4 sec, 4 sec
  for (var i = 1; i <= 3; i++) {
    setTimeout(function() {
      console.log(i + " sec");
    }, i * 1000);
  }

  // fix: let creates new scope for i in each interaction
  for (let i = 1; i <= 3; i++) {
    setTimeout(function() {
      console.log(i + " second(s) elapsed");
    }, i * 1000);
  }

  // another fix: wrap in a closure --> creates new scope with different i each iteration
  for (var i = 1; i <= 3; i++) {
    (function(i) {
      setTimeout(function() {
        console.log(i + " second(s) elapsed");
      }, i * 1000);
    })(i);
  }
  ```

## Promise
- **Promise**: POJO that represents the eventual completion or failure of an sync func
- Possible states:
  - Settled: can't transition into any other state, alw has value (can be undefined)
    - Fulfilled: promise's action succeeded
    - Rejected: promise's action failed
  - Pending
- Creation: 1 arg is a cb w ```resolve``` and ```reject``` params
  ```js
  const promise = new Promise( (resolve, reject) => {
    // do a thing, possibly async, then…
    if (/* everything turned out fine */) {
      resolve("Stuff worked!");
    }
    else {
      reject(Error("It broke"));
    }
  } );
  ```
- Chaining: alw return results, so subsequent cbs can catch it
  - .then(): 2 args, cbs for success and failure cases
    ```js
    promise.then( (result) => {
      console.log(result); // "Stuff worked!"
    }, (err) => {
      console.log(err); // Error: "It broke"
    });
    ```
  - ```.catch( (err) => failureCallback )```: short for ```.then( (null, failureCallback) => {...} )```

## Prototypal Inheritance
- Object has private property w link to **prototype** (another obj)
- When accessing property of an obj, obj itself is looked at, then its prototype, all the way up **prototype chain**, until null or property found
  - Use ```obj.hasOwnProperty('toString')``` to return boolean to check only that obj
  - ``` let f = function() { this.a = 1; this.b = 2 }```
  - ```f.prototype.b = 3``` good, ```f.prototype = {b:3,c:4}``` will break the prototype chai
  - ```f```'s prototype is Object.prototype, Object's is null
- Changes can be seen by all objects through chain
- JS ```class TodoListItem extends React.Component``` is syntactic sugar that builds on prototypal inheritance
- Better than class inheritance, bc class inheritance has more flaws:
  - Tight coupling
  - Fragile base class: widespread use of base class --> difficult to fix
  - Duplication by necessity: inflexible hierarchies often force duplication
  - Gorilla/banana problem: wanted a banana, but got a banana held by a gorilla in the entire jungle

## Closures
- Closure: inner func that has access to outer func's variables, globals, while maintaining own scope
  - Outer func's variables stored as references

## Function Expression vs Declaration
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
    // variable declarations are hoisted, but assignment expressions aren't
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
    alert(foo()); //3
    ```

## Pure Functions
- **Pure function**: same input produces same output, no side effects
  - Independent of outside state --> foundation of functional programming, easy to reorganize and refactor
  - Uses: good for parallel processing across CPUs and distributed computing clusters
  - Same I/O ex.: ```double()```, but NOT ```Math.random()```
  - No side effects --> don't mutate external state --> ex.: Redux reducers ```Object.assign()```

## IIFE
- Immediately-Invoked Function Expression: 'iffy,' variables declared inside IIFE not visible outside
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

## ECMAScript Versions
ES5
- Strict mode
- Methods
  - ```String.trim()```
  - ```Array.isArray()```
  - ```Array.forEach()```, ```Array.map()```, ```Array.filter()```, ```Array.reduce()```
  - ```Array.every()```, ```Array.some()```
  - ```Array.indexOf()```, ```Array.lastIndexOf()```
  - ```JSON.parse()``` receives data from server, ```JSON.stringify()``` sends data
  - ```Date.now()```
- Trailing commas in array and objects

ES6
- ```let```, ```const```: block scoped, can't be re-declared in same scope, hoisted but not initialized (```ReferenceError``` if variable tried to use before declaration)
  - ```let```: can be updated
  - ```const```: can't be updated, must be initialized during declaration
  - Old pre-ES6 ```var```: globally/function scoped (defined outside func, globally), can be updated and re-declared, hoisted and initialized as ```undefined```,

- Arrow function syntax: () => ..., retains external ```this``` inside block
  - Doesn't have own ```this```, ```arguments```, ```super```, or ```new.target```

- Promises: library for async,
  ```js
  function timeout(duration = 0) {
    return new Promise((resolve, reject) => {
        setTimeout(resolve, duration);
    })
  }

  const p = timeout(1000)
    .then( res => console.log(res); )
    .catch( err => throw new Error(err); )
  ```

- Classes: ```class ListItem extends React.Component {...}```

- Template strings/string interpolation: ````${variable here}````

- Parameter values
  - Default: ```function foo(x, y = 12)```
  - Rest operator: ```function foo(...args)```, turns individual args to an array
  - Spread operator: ```function foo(x, y, z) {...} foo(...[x, y, z])```, turns arr to individual

- Unicode
- Modules
- Map, Set, WeakMap, WeakSet
- Symbols
- ```Array.find()```, ```Array.findIndex()``` take callbacks

## jQuery
- jQuery: fast, lightweight JS library to simplify DOM manipulation (can do the same thing, but with more code, in vanilla JS)

## Context
- ```theFunc.apply(valueForThis, arrayOfArgs)```
- ```theFunc.call(valueForThis, arg1, arg2, ...)```
- ```theFunc.bind(valueForThis)(arg1, arg2, ...)``` --> returns func with modified ```this```

## Attribute vs Property
- **Attribute**: defined by HTML
- **Property**: defined by DOM, on JS DOM objects
  - jQuery: ```$('#someEl').prop('className')```
  - Interact w this instead of attributes when possible

## Equals
- ```==```: tries to convert one side to same type as other
- ```===```: no conversions

## Currying
```js
function(numArgs) {
  const arr = [];
  const _myCurry = num => {
    arr.push(num);
    if (arr.length === numArgs) {
      return this(...arr); // do function's operations here
      // like for (let i = 0; ...) { sum += arr[i] } for curry sum
    }
    return _myCurry;
  }
  return _myCurry;
}
```
```js
add(2, 5); // 7
add(2)(5); // 7
let add = function(x, ...xArgs) {
  let total = x;
  if (xArgs.length > 0) {
    xArgs.forEach((el) => {
      total += el;
    });
    return total;
  } else {
    return function(y) {
      return total += y;
    };
  }
};
```

## module.exports
- ```module```: POJO w exports property
- ```exports```: variable

## typeof vs instanceof
- ```typeof```: returns str
  - Ex.: ```typeof(null)``` => ```Object```
- ```instanceof```: works on level of prototype, doesn't work on primitives, returns boolean
  - Ex.: ```'xyz' instanceof String``` => ```true```

## Object
- Object.values, Object.prototype(obj), Object.freeze(func) to prevent changes, Object.seal(func) to prevent new property addition or deletion but allows modification

## Sources:
Promises: https://developers.google.com/web/fundamentals/primers/promises
Lexical scope: https://github.com/getify/You-Dont-Know-JS/blob/master/scope%20&%20closures/README.md#you-dont-know-js-scope--closures
Strict mode: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode
IIFE's: https://medium.com/@vvkchandra/essential-javascript-mastering-immediately-invoked-function-expressions-67791338ddc6, https://blog.mariusschulz.com/2016/01/19/use-cases-for-javascripts-iifes, https://en.wikipedia.org/wiki/Immediately-invoked_function_expression
ES5: https://www.w3schools.com/js/js_es5.asp
ES6: https://github.com/lukehoban/es6features
Angular: https://github.com/rlee0525/TechnicalConceptsForInterviews/blob/master/AngularVReact.md

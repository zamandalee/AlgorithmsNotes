# JavaScript
- Strict mode
- Difference between a function expression and a function declaration
- Utility of IIFEs
- Prototypical inheritance
- Closures
- Async

### Overview
- **Interpreted**
- **Prototype-based**: style of OOP, classes not explicitly defined, instead objects are reused
- **Multi-paradigm**
  - **Imperative/procedural programming** (explicit statements that change program state), **OOP**, **functional programming** (functions to avoid global state)

### Asynchronous
- **Asynchronous**: engine runs in an event loop --> single program thread can handle concurrent operations

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

### Sources:
Strict mode: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode

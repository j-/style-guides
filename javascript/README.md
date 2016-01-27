# JavaScript Style Guide

## Contents

1.  [Whitespace](#1-whitespace)
2.  [Variables](#2-variables)
3.  [Naming](#3-naming)
4.  [Comments](#4-comments)
5.  [Types](#5-types)
6.  [Strings](#6-strings)
7.  [Numbers](#7-numbers)
8.  [Booleans](#8-booleans)
9.  [Equality operators](#9-equality-operators)
10. [Inequality operators](#10-inequality-operators)
11. [Arrays](#11-arrays)
12. [Objects](#12-objects)
13. [Commas](#13-commas)
14. [Semicolons](#14-semicolons)
15. [Functions](#15-functions)
16. [Arrow functions](#16-arrow-functions)
17. [Method chaining](#17-method-chaining)
18. [Blocks](#18-blocks)
19. [If statement](#19-if-statement)
20. [For loops](#20-for-loops)
21. [While loops](#21-while-loops)
22. [Switch statement](#22-switch-statement)
23. [With statement](#23-with-statement)
24. [Promises](#24-promises)

## 1. Whitespace

  * <a name="1.1" href="#1.1">1.1</a>.
    Use tabs, not spaces.

    ```js
    function bad () {
    ····return 'four spaces';
    }

    function good () {
    ————return 'single tab';
    }
    ```

    **Note**: Enable invisible characters in your text editor or IDE to avoid introducing mixed indentation.

  * <a name="1.2" href="#1.2">1.2</a>.
    Avoid introducing whitespace at the end of a line.

    ```js
    // Bad
    const problem = 'extra spaces';····↵

    // Good
    const noProblem = 'spaces gone';↵
    ```

    **Note**: Enabling invisible characters will help here, too. Your text editor or IDE may also be able to remove whitespace at the end of lines automatically.

  * <a name="1.3" href="#1.3">1.3</a>.
    Use spaces between operators.

    ```js
    // Bad
    const squashed=Math.PI*r*r;

    // Good
    const roomy = Math.PI * r * r;
    ```

  * <a name="1.4" href="#1.4">1.4</a>.
    Prefix, postfix and unary operators do not need to be spaced.

    ```js
    // Bad
    console.log(- x);
    console.log(y ++);
    console.log(-- z);

    // Good
    console.log(-x);
    console.log(y++);
    console.log(--z);
    ```

  * <a name="1.5" href="#1.5">1.5</a>.
    Do not add spaces inside parentheses.

    ```js
    // Bad
    console.log( 'Hello world' );

    // Good
    console.log('Hello world');
    ```

  * <a name="1.6" href="#1.6">1.6</a>.
    Do not add spaces inside square brackets.

    ```js
    // Bad
    [ 'Foo' ];

    // Good
    ['Bar'];
    ```

  * <a name="1.7" href="#1.7">1.7</a>.
    Add spaces inside braces and after colons.

    ```js
    // Bad
    {foo:'bar'};

    // Good
    { foo: 'bar' }
    ```

  * <a name="1.8" href="#1.8">1.8</a>.
    Add spaces after commas.

    ```js
    // Bad
    fn([1,2,3],'a','b','c');

    // Good
    fn([1, 2, 3], 'a', 'b', 'c');
    ```

  * <a name="1.9" href="#1.9">1.9</a>.
    Use spaces around keywords, argument lists and conditions.

    ```js
    // Bad
    function squashed(x){
        if(x){
            return typeof(x);
        }
    }

    // Good
    function roomy (x) {
        if (x) {
            return typeof x;
        }
    }
    ```

  * <a name="1.10" href="#1.10">1.10</a>.
    Do not use tabs for alignment. Tabs can vary in width depending on user/application configuration. Instead, use spaces. They will always appear the same in any editor.

    ```js
    // Bad (tab width: 4)
    const foods = [
        { name: 'Enchiladas',———rating: 60 },
        { name: 'Burritos',—————rating: 50 },
        { name: 'Tacos',————————rating: 30 },
    ];

    // Bad (tab width: 2)
    const foods = [
      { name: 'Enchiladas',—rating: 60 },
      { name: 'Burritos',———rating: 50 },
      { name: 'Tacos',————rating: 30 },
    ];

    // Good (tab width: 4)
    const foods = [
        { name: 'Enchiladas',···rating: 60 },
        { name: 'Burritos',·····rating: 50 },
        { name: 'Tacos',········rating: 30 },
    ];

    // Good (tab width: 2)
    const foods = [
      { name: 'Enchiladas',···rating: 60 },
      { name: 'Burritos',·····rating: 50 },
      { name: 'Tacos',········rating: 30 },
    ];
    ```

## 2. Variables

  * <a name="2.1" href="#2.1">2.1</a>.
    Declare each variable separately and on their own lines. The exception is undefined variables, which may be declared in the same statement.

    ```js
    // Bad
    var foo, bar = 123,
        baz = true, qux;

    // Good
    var bar = 123;
    var baz = true;
    var foo, qux;
    ```

  * <a name="2.2" href="#2.2">2.2</a>.
    Prefer `let` and `const` over `var` where possible.

    ```js
    // OK
    var ITERATIONS = 100;
    var current = 0;
    var remaining = ITERATIONS - current;

    // Better
    const iterations = 100;
    let current = 0;
    let remaining = iterations - current;
    ```

    [`let` on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let). [`const` on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const). [`var` on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var).

  * <a name="2.3" href="#2.3">2.3</a>.
    Avoid saving references to `this`. These can almost always be replaced with an arrow function.

    ```js
    // Bad
    function foo () {
        const self = this;
        return new Promise(function (resolve) {
            setTimeout(function () {
                resolve(self.foo);
            }, 1000);
        });
    }

    // Good
    function bar () {
        return new Promise((resolve) => {
            setTimeout(() => {
                resolve(this.bar);
            }, 1000);
        });
    }
    ```

  * <a name="2.4" href="#2.4">2.4</a>.
    Avoid introducing ["magic numbers"](https://en.wikipedia.org/wiki/Magic_number_\(programming\)#Unnamed_numerical_constants) and assign them to clearly named variables instead.

    ```js
    // Bad, significance of 52 unclear
    for (let i = 0; i < 52; i++) {
        let j = i + Math.floor(Math.random() * (52 - i));
        [arr[i], arr[j]] = [arr[j], arr[i]];
    }

    // Good
    const deckSize = 52;
    for (let i = 0; i < deckSize; i++) {
        let j = i + Math.floor(Math.random() * (deckSize - i));
        [arr[i], arr[j]] = [arr[j], arr[i]];
    }
    ```

## 3. Naming

  * <a name="3.1" href="#3.1">3.1</a>.
    Give variables clear names.

    ```js
    // Bad
    const c = 100;
    const s = String(c);
    const l = s.length;

    // Good
    const count = 100;
    const countString = String(count);
    const length = countString.length;
    ```

    **Note**: Single letter variable names are not forbidden. Notable examples are `i` (and to a lesser extent, `j`) in `for` loops, as well as common variable names like `x` and `y` (as long as their meaning is clear in context).

    ```js
    // Fine
    let x, y;
    for (let i = 0; i < arr.length; i++) {
        x = arr[i][0];
        y = arr[i][1];
        console.log('Data point at (%i, %i)', x, y);
    }
    ```

  * <a name="3.2" href="#3.2">3.2</a>.
    Use camelCase for variable names.

    ```js
    // Bad
    const Namespace = {};
    const price_aud = 1.61;
    const inputvalue = 'foobar';

    // Good
    const namespace = {};
    const priceAUD = 1.61;
    const inputValue = 'foobar';
    ```

  * <a name="3.3" href="#3.3">3.3</a>.
    Use PascalCase for constructors and class names.

    ```js
    // Bad
    function controller () {}
    class applicationView extends view {}

    // Good
    function Controller () {}
    class ApplicationView extends View {}
    ```

  * <a name="3.4" href="#3.4">3.4</a>.
    Use UPPER_CASE for global constants.

    ```js
    const API_ORIGIN = 'http://example.com';

    function fetchProfile (userID) {
        const endpoint = `${API_ORIGIN}/user/${userID}`;
        return $.ajax(endpoint);
    }
    ```

  * <a name="3.5" href="#3.5">3.5</a>.
    Keep variable names professional.

    ```js
    // Bad
    const potato = 3;
    const ohhai = 'lol';
    const pants = ohhai.repeat(potato);

    // Good
    const iterations = 3;
    const string = 'hello';
    const result = string.repeat(iterations);
    ```

## 4. Comments

  * <a name="4.1" href="#4.1">4.1</a>.
    Try and use sentence case in comments.

    ```js
    // bad: it can be difficult to tell if two line comments are a
    // continuation or distinct comments when they are all lower case
    const foo = 'foo';

    // Good: Using uppercase at the beginning of the line comment (and,
    // where necessary, punctuation at the end) makes comments clear
    const bar = 'bar';
    ```

  * <a name="4.2" href="#4.2">4.2</a>.
    Keep comments professional.

    ```js
    // Bad
    // IE is shitty and doesn't support $FEATURE
    const isIE = detectIE();

    // Good
    // $FEATURE is not supported on IE
    const isIE = detectIE();
    ```

  * <a name="4.3" href="#4.3">4.3</a>.
    Use doc blocks. They should allow the reader to understand the purpose and behavior of a chunk of code (like a function, class, property etc.) before they have actually read the code. Doc blocks are multiline comments beginning with `/**` (two asterisks).

    ```js
    // Bad
    function easeInOutQuad (t, b, c, d) {
        t /= d / 2;
        if (t < 1) {
            return c / 2 * t * t + b;
        }
        t--;
        return -c / 2 * (t * (t - 2) - 1) + b;
    }

    // Bad, single asterisk
    /*
     * Quadratic in/out easing algorithm.
     * @param {Number} t Current time (value between 0 and d)
     * @param {Number} b Start value at t=0
     * @param {Number} c Change in value at t=d
     * @param {Number} d Duration
     * @return {Number} Value at current time
     */
    function easeInOutQuad (t, b, c, d) {
        t /= d / 2;
        if (t < 1) {
            return c / 2 * t * t + b;
        }
        t--;
        return -c / 2 * (t * (t - 2) - 1) + b;
    }

    // Good
    /**
     * Quadratic in/out easing algorithm.
     * @param {Number} t Current time (value between 0 and d)
     * @param {Number} b Start value at t=0
     * @param {Number} c Change in value at t=d
     * @param {Number} d Duration
     * @return {Number} Value at current time
     */
    function easeInOutQuad (t, b, c, d) {
        t /= d / 2;
        if (t < 1) {
            return c / 2 * t * t + b;
        }
        t--;
        return -c / 2 * (t * (t - 2) - 1) + b;
    }
    ```

    **Note**: If you use documentation generators, make sure you are familiar with the syntax they expect:
    * [JSDoc](http://usejsdoc.org/)
    * [YUIDoc](http://yui.github.io/yuidoc/syntax/)
    * [ESDoc](https://esdoc.org/tags.html)

## 5. Types

  * <a name="5.1" href="#5.1">5.1</a>.
    Use `typeof` to check the type of primitives.

    ```js
    const value = 'hello world';

    // Bad
    value instanceof String; // => false

    // Good
    typeof value === 'string'; // => true
    ```

  * <a name="5.2" href="#5.2">5.2</a>.
    Use `instanceof` to check the type of objects.

    ```js
    class Base {}
    class Foo extends Base {}
    class Bar extends Base {}
    const foo = new Foo();
    const bar = new Bar();

    // Bad, does not check superclasses
    foo.constructor === Foo; // => true
    foo.constructor === Base; // => false

    // Good, checks superclasses
    foo instanceof Foo; // => true
    foo instanceof Base; // => true
    ```

## 6. Strings

  * <a name="6.1" href="#6.1">6.1</a>.
    Use `String()` to coerce values into strings.

    ```js
    const maybeString = 123;

    // Bad
    const avoid = maybeString + '';

    // Good
    const prefer = String(maybeString);
    ```

  * <a name="6.2" href="#6.2">6.2</a>.
    Avoid using `#toString()` if possible.

    ```js
    const input = null;

    // Bad
    input.toString() // TypeError: Cannot read property 'toString' of null

    // Good
    String(input); // => null
    ```

    **Note**: `String()` invokes `#toString()` if it is available.

    ```js
    class Example {
        toString () {
            return 'Hello world';
        }
    }

    String(new Example()); // => 'Hello world'
    ```

  * <a name="6.3" href="#6.3">6.3</a>.
    Do not use the `new` keyword when initializing a string.

    ```js
    const response = 123;
    let result;

    // Bad
    result = new String(response);
    typeof result; // => 'object'

    // Good
    result = String(response);
    typeof result; // => 'string'
    ```

  * <a name="6.4" href="#6.4">6.4</a>.
    Use single quotes for strings. Escape single quotes inside the string with a backslash.

    ```js
    // Bad
    const avoid = "What's your name?";

    // Good
    const prefer = 'My name\'s Superman';
    ```

  * <a name="6.5" href="#6.5">6.5</a>.
    Try and use template strings to concatenate values.

    ```js
    const foo = 'foo';
    const bar = 'bar';
    let result;

    // Bad
    result = [foo, ' - ', bar].join('');

    // OK
    result = foo + ' - ' + bar;

    // Good
    result = `${foo} - ${bar}`;
    ```

    ['Template strings' on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings).

  * <a name="6.6" href="#6.6">6.6</a>.
    Use only references in template strings. Avoid using complex statements.

    ```js
    // Bad
    const ugly = `HELLO ${this.get('name').toUpperCase()}`;

    // Good
    const name = this.get('name').toUpperCase();
    const pretty = `HELLO ${name}`;

    // OK
    const result = 'HELLO ${this.name}';
    ```

  * <a name="6.7" href="#6.7">6.7</a>.
    Avoid using template strings where not necessary.

    ```js
    // Unnecessary
    const foo = `Foo`;

    // Better
    const bar = 'Bar';
    ```

## 7. Numbers

  * <a name="7.1" href="#7.1">7.1</a>.
    Use `Number()` to coerce values into numbers where possible. This pattern is preferred for numeric values generated by other systems (e.g. via APIs).

    ```js
    const response = '123';
    let result;

    // Bad
    result = response + 0;

    // Bad
    result = +response;

    // Bad
    result = response >> 0;

    // Better
    result = parseInt(response);

    // Best
    result = Number(response);
    ```

  * <a name="7.2" href="#7.2">7.2</a>.
    Do not use the `new` keyword when initializing a number.

    ```js
    const response = '123';
    let result;

    // Bad
    result = new Number(response);
    typeof result; // => 'object'

    // Good
    result = Number(response);
    typeof result; // => 'number'
    ```

  * <a name="7.3" href="#7.3">7.3</a>.
    Use `Number()` if you _expect_ a value to be a number.

    ```js
    const input = '100x';

    // Bad
    parseInt(input, 10); // => 100

    // Good
    Number(input); // => NaN
    ```

  * <a name="7.4" href="#7.4">7.4</a>.
    Try and use `parseInt()` to coerce user input to numbers. Always use a radix to specify the base you expect the number to be in.

    ```js
    const input = '0x10';
    let result;

    // Bad, implicit radix
    result = Number(input); // => 16

    // Bad, implicit radix
    result = parseInt(input); // => 16

    // Good, explicit radix
    result = parseInt(input, 10); // => 0

    // Good, explicit radix
    result = parseInt(input, 16); // => 16
    ```

  * <a name="7.5" href="#7.5">7.5</a>.
    Use `parseFloat()` only for floating point input in base 10.

    ```js
    const input = '3.14159';
    let result;

    // Bad, loss of precision
    result = parseInt(input, 10); // => 3

    // Bad, unnecessary radix
    result = parseFloat(input, 10); // => 3.14159

    // Bad, ignored radix
    result = parseFloat(input, 16); // => 3.14159

    // Good
    result = parseFloat(input); // => 3.14159
    ```

  * <a name="7.6" href="#7.6">7.6</a>.
    Declare numbers in their original base if appropriate.

    ```js
    // Bad
    const whiteDec = 16777215;

    // Good
    const whiteHex = 0xffffff;

    // Examples
    const dec = 16;
    const hex = 0x10;
    const oct = 0o20; // Introduced in ES6
    const bin = 0b10000; // Introduced in ES6
    ```

  * <a name="7.8" href="#7.8">7.8</a>.
    Do not use the leading-zero pattern of declaring octal numbers. It is unclear and inconsistent with binary and hexadecimal numbers.

    ```js
    // Bad
    const unclear = 010; // => 8

    // Good
    const clear = 0o10; // => 8
    ```

  * <a name="7.9" href="#7.9">7.9</a>.
    Avoid using bitshift operators where possible. Bitshift operators return 32 bit integers instead of an eight byte IEEE 754 floating point number. They will only return whole number values between -2,147,483,648 and 2,147,483,647.

    ```js
    2147483647 >> 0; // => 2147483647
    2147483648 >> 0; // => -2147483648
    2147483649 >> 0; // => -2147483647
    ```

    **Note**: You may be able to use other operators to achieve the intended result:

    ```js
    const x = 10; // 0b1010

    // Bitshift left 5 places
    x << 5;              // 0b100000
    x * Math.pow(2, 5);  // 0b100000

    // Bitshift left 32 places
    x << 32;             // 0b000000000000000000000000000000001 (Bad)
    x * Math.pow(2, 32); // 0b100000000000000000000000000000000 (Good)
    ```

## 8. Booleans

  * <a name="8.1" href="#8.1">8.1</a>.
    Use `Boolean()` to coerce values into booleans. Try and return actual boolean values from any method that declares its return type as boolean.

    ```js
    /**
     * Returns true if `x` and `y` are both truthy, false otherwise.
     * @param {*} x
     * @param {*} y
     * @return {Boolean}
     */
    function and (x, y) {
        let result;

        // Bad
        result = x && y; // and(1, 2) => 2

        // Bad
        result = x && y && true; // and(1, 2) => true

        // Bad
        result = !!(x && y); // and(1, 2) => true

        // Worse
        result = x && y ? true : false;

        // Terrible
        result = x && y === true ? true : false;

        // Good
        result = Boolean(x && y); // and(1, 2) => true

        return result;
    }
    ```

  * <a name="8.2" href="#8.2">8.2</a>.
    Do not use the `new` keyword when initializing a boolean.

    ```js
    const falsy = 0;
    let result;

    // Bad
    result = new Boolean(falsy);
    typeof result; // => 'object'

    // Really bad
    result ? 'actual' : 'expected'; // => 'actual'

    // Good
    result = Boolean(falsy);
    typeof result; // => 'boolean'
    ```

## 9. Equality operators

  * <a name="9.1" href="#9.1">9.1</a>.
    Always use strict equality operators.

    ```js
    // Bad
    '1' == 1; // => true

    // Bad
    '1' != 1; // => false

    // Good
    '1' === 1; // => false

    // Good
    '1' !== 1; // => true
    ```

  * <a name="9.2" href="#9.2">9.2</a>.
    Coerce values before comparing them where appropriate.

    ```js
    const x = '1';

    // Bad
    x === 1 || x === '1';

    // Good
    Number(x) === 1; // => true
    ```

  * <a name="9.3" href="#9.3">9.3</a>.
    Be careful when comparing two floating point numbers.

    ```js
    const a = 0.1;
    const b = 0.2;
    const expected = 0.3;
    const actual = a + b; // => 0.30000000000000004
    let eq;

    // Bad
    eq = actual === expected; // => false

    // Good
    eq = Math.abs(actual - expected) < Number.EPSILON; // => true
    ```

    [`Number.EPSILON` on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/EPSILON). Introduced in ES6.

  * <a name="9.4" href="#9.4">9.4</a>.
    Use `isNaN` to compare with `NaN`

    ```js
    const val = 0 / 0; // => NaN

    // Bad
    val === NaN; // => false

    // Good
    isNaN(val); // => true
    ```

    [`isNaN()` on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/isNaN).

  * <a name="9.5" href="#9.5">9.5</a>.
    Keep in mind that comparing object references will not compare their state or value.

    ```js
    [] === []; // => false
    ({} === {}); // => false

    class Example {
        valueOf () {
            return 1;
        }
    }

    new Example() === new Example(); // => false
    ```

## 10. Inequality operators

  * <a name="10.1" href="#10.1">10.1</a>.
    Be careful when comparing with a value that may be `null`.

    ```js
    const a = 5;
    const b = null;

    a >= 0; // => true
    b >= 0; // => true
    ```

  * <a name="10.2" href="#10.2">10.2</a>.
    Keep in mind that comparing object references will compare the objects' values.

    ```js
    class Example {
        constructor (value) {
            this.value = value;
        }
        valueOf () {
            return this.value;
        }
    }

    const foo = new Example(5);
    const bar = new Example(10);
    const baz = new Example(10);

    foo > bar; // => false
    foo < bar; // => true
    foo > 3; // => true
    bar >= baz && bar <= baz; // => true
    ```

  * <a name="10.3" href="#10.3">10.3</a>.
    Note that comparing strings may result in numeric coercion.

    ```js
    '3' > 4; // => false
    '4' > 3; // => true
    ```

## 11. Arrays

  * <a name="11.1" href="#11.1">11.1</a>.
    Use the array literal syntax to create arrays.

    ```js
    // Bad
    const arr = new Array();

    // Good
    const arr = [];
    ```

  * <a name="11.2" href="#11.2">11.2</a>.
    Use the rest and spread operators where possible.

    ```js
    const items = document.querySelectorAll('.foo');

    // Bad
    Array.prototype.map.call(items, (item) => item.textContent);

    // Good
    [...items].map((item) => item.textContent);
    ```

  * <a name="11.3" href="#11.3">11.3</a>.
    Be careful when using `Array#sort()`. Note that if a comparator function is not supplied, the default algorithm uses a _case-sensitive string sort_.

    ```js
    // Bad
    ['a', 'b', 'C'].sort(); // => ['C', 'a', 'b']
    [5, 10, 15, 20].sort(); // => [10, 15, 20, 5]

    // Good
    function strCompCI (a, b) {
        a = String(a).toUpperCase();
        b = String(b).toUpperCase();
        if (a < b) {
            return -1;
        }
        if (a > b) {
            return 1;
        }
        return 0;
    }
    ['a', 'b', 'C'].sort(strCompCI); // => ['a', 'b', 'C'];
    [5, 10, 15, 20].sort((a, b) => a - b); // => [5, 10, 15, 20];
    ```

    [`Array.prototype.sort()` on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort).

## 12. Objects

  * <a name="12.1" href="#12.1">12.1</a>.
    Use the object literal syntax to create objects.

    ```js
    // Bad
    const obj = new Object();

    // Good
    const obj = {};
    ```

  * <a name="12.2" href="#12.2">12.2</a>.
    Use dot notation when accessing properties where possible.

    ```js
    const foo = { bar: 'baz' };

    // Bad
    console.log(foo['bar']);

    // Good
    console.log(foo.bar);
    ```

  * <a name="12.3" href="#12.3">12.3</a>.
    Avoid using complex property names.

    ```js
    // Bad
    const attrs = {
        'data-foo': 'foo',
        'data-bar': 'bar',
    };

    // Good
    const attrs = {
        dataFoo: 'foo',
        dataBar: 'bar',
    };
    ```

  * <a name="12.4" href="#12.4">12.4</a>.
    Avoid using reserved words as property names.

    ```js
    // Bad
    const attrs = {
        default: getDefaultValues(),
        switch: 'test-flag',
        export: 'main',
    };

    // Good
    const attrs = {
        defaults: getDefaultValues(),
        switches: 'test-flag',
        exports: 'main',
    };
    ```

  * <a name="12.5" href="#12.5">12.5</a>.
    Use computed property names where possible. Like [6.6](#6.6), avoid using complex statements in a computed property name.

    ```js
    // Bad
    function bad () {
        const key = getKeyName();
        const result = {
            foo: 'bar',
        };
        result[key] = getValue();
        return result;
    }

    // Bad
    function good () {
        return {
            foo: 'bar',
            [getKeyName()]: getValue(),
        };
    }

    // Good
    function good () {
        const key = getKeyName();
        return {
            foo: 'bar',
            [key]: getValue(),
        };
    }
    ```

## 13. Commas

  * <a name="13.1" href="#13.1">13.1</a>.
    Use trailing commas when list items are on their own lines. [See this gist](https://gist.github.com/j-/2c12c64b48d703aa9112) for an example of why trailing commas are a good thing.

    ```js
    // Bad
    const arr = [
        'foo',
        'bar',
        'baz'
    ];
    const obj = {
        foo: 'foo',
        bar: 'bar',
        baz: 'baz'
    };

    // Good
    const arr = [
        'foo',
        'bar',
        'baz',
    ];
    const obj = {
        foo: 'foo',
        bar: 'bar',
        baz: 'baz',
    };
    ```

  * <a name="13.2" href="#13.2">13.2</a>.
    Do not use trailing commas when list items are on the same line.

    ```js
    // Bad
    const args = ['foo', 'bar', 'baz',];
    const options = { foo: 'foo', bar: 'bar', baz: 'baz', };

    // Good
    const args = ['foo', 'bar', 'baz'];
    const options = { foo: 'foo', bar: 'bar', baz: 'baz' };
    ```

## 14. Semicolons

  * <a name="13.2" href="#13.2">13.2</a>.
    Use semicolons. Do not rely on ASI.

    ```js
    // Bad
    const foo
    const bar = baz()

    // Good
    const foo;
    const bar = baz();
    ```

## 15. Functions

  * <a name="15.1" href="#15.1">15.1</a>.
    Use function declarations over function expressions where possible.

    ```js
    // Bad
    var add = function () { };

    // Good
    function add () { }
    ```

    **Note**: Function declarations are not statements and as such are not followed by a semicolon.

  * <a name="15.2" href="#15.2">15.2</a>.
    Avoid re-declaring functions.

    ```js
    // Bad, unnecessary re-declaration
    for (let i = 0; i < 10; i++) {
        function square (i) {
            return i * i;
        }
        console.log(square(i));
    }

    // Good, only declared once
    function square (i) {
        return i * i;
    }
    for (let i = 0; i < 10; i++) {
        console.log(square(i));
    }
    ```

  * <a name="15.3" href="#15.3">15.3</a>.
    Document functions where possible. Generally, named functions should all have proper documentation blocks. See [4.3](#4.3).

  * <a name="15.4" href="#15.4">15.4</a>.
    Give functions descriptive, [imperative](https://en.wikipedia.org/wiki/Imperative_mood) names.

    ```js
    // Bad, name not descriptive
    function fn () {
        return Math.random() < 0.5;
    }

    // Bad, functionality unclear
    function value () {
        // ...
    }

    // Good, name descriptive
    function getRandomBoolean () {
        return Math.random() < 0.5;
    }

    // Good, functionality clear
    function getValue () {
        // ...
    }
    ```

  * <a name="15.5" href="#15.5">15.5</a>.
    Avoid declaring methods which do not depend on `this`. A method is a function declared as a member of an object. If a method does not use `this`, it can probably be defined as a function instead.

    ```js
    class Example {
        constructor () {
            this.foo = 'foo';
        }

        // Unnecessary, does not reference `this`
        logBaz () {
            console.log('baz');
        }

        // Good, references `this`
        logFoo () {
            console.log(this.foo);
        }

        // Good, declared as function
        static logBar () {
            console.log('bar');
        }
    }

    const ex = new Example();
    ex.logFoo(); // => 'foo'
    Example.logBar(); // => 'bar'
    ```

    Notable exceptions are abstract and virtual methods. These may be intentionally stubbed if anticipating child classes to implement those methods.

  * <a name="15.6" href="#15.6">15.6</a>.
    Treat object references as immutable unless your function is a mutator.

    ```js
    const numbers = [3, 1, 4, 1, 5, 9];

    // Bad, mutates input
    function largest (arr) {
        return arr.sort((a, b) => a - b).pop();
    }
    console.log('Largest: %i', largest(numbers)); // => 9
    console.log('Numbers: %o', numbers); // => [1, 1, 3, 4, 5]

    // Good, accesses input
    function largest (arr) {
        return [...arr].sort((a, b) => a - b).pop();
    }
    console.log('Largest: %i', largest(numbers)); // => 9
    console.log('Numbers: %o', numbers); // => [3, 1, 4, 1, 5, 9]
    ```

    ```js
    const DEFAULT_ENDPOINT = '/api';
    const options = { data: 'foobar' };

    // Bad, mutates input
    function fetchData (options) {
        options.url = options.url || DEFAULT_ENDPOINT;
        return $.ajax(options);
    }
    fetchData(options);
    console.log(options); // => { data: 'foobar', url: '/api' }

    // Good, accesses input
    function fetchData (options) {
        options = Object.assign({
            url: DEFAULT_ENDPOINT,
        }, options);
        return $.ajax(options);
    }
    fetchData(options);
    console.log(options); // => { data: 'foobar' }
    ```

  * <a name="15.7" href="#15.7">15.7</a>.
    Do not access the `arguments` object directly. Instead use the rest operator.

    ```js
    // Bad
    function addNumbers () {
        return [...arguments].reduce((total, num) => total + num, 0);
    }
    addNumbers(1, 2, 3, 4); // => 10

    // Good
    function addNumbers (...nums) {
        return nums.reduce((total, num) => total + num, 0);
    }
    addNumbers(1, 2, 3, 4); // => 10
    ```

    ['Rest parameters' on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters).

## 16. Arrow functions

  * <a name="16.1" href="#16.1">16.1</a>.
    Prefer arrow functions over function declarations where possible. Arrow functions are cleaner and do not introduce their own scope.

    ```js
    const input = [1, 2, 3];
    let squared;

    // Bad
    squared = input.map(function (num) {
        return num * num;
    });

    // Better
    squared = input.map((num) => {
        return num * num;
    });

    // Best
    squared = input.map((num) => num * num);
    ```

  * <a name="16.2" href="#16.2">16.2</a>.
    Use parentheses around arguments list even when there is a single argument.

    ```js
    const input = [1, 2, 3];

    // Bad
    input.forEach(x => console.log(x));

    // Good
    input.forEach((x) => console.log(x));
    ```

## 17. Method chaining

  * <a name="17.1" href="#17.1">17.1</a>.
    Split method chains with newlines. This makes functionality clearer, diffs simpler, and [blames](https://git-scm.com/docs/git-blame) easier.

    ```js
    // Bad
    $('.foo').filter('ul').find('li').text((i) => `Item ${i + 1}`);

    // Good
    $('.foo')
        .filter('ul')
        .find('li')
        .text((i) => `Item ${i + 1}`);
    ```

  * <a name="17.2" href="#17.2">17.2</a>.
    Use a leading dot when chaining. Indent chained methods.

    ```js
    // Bad
    Promise.resolve().then(() => {
        const data = getUserInput();
        return asyncFunction1(data);
    }).then(() => asyncFunction2())
    .catch((err) => displayError(err));

    // Good
    Promise.resolve()
        .then(() => {
            const data = getUserInput();
            return asyncFunction1(data);
        })
        .then(() => asyncFunction2())
        .catch((err) => displayError(err));
    ```

  * <a name="17.3" href="#17.3">17.3</a>.
    Limit chain length where possible. It may be clearer to assign intermediary results to a variable.

    ```js
    // Bad
    $('#items')
        .find('.selected')
            .highlight()
            .end()
        .find('.open')
            .updateCount();

    // Good
    const $items = $('#items');
    const $selected = $items.find('.selected');
    const $open = $items.find('.open');
    $selected.highlight();
    $open.updateCount();
    ```

## 18. Blocks

  * <a name="18.1" href="#18.1">18.1</a>.
    Always use braces around blocks.

    ```js
    // Bad
    if (condition) action();

    // Worse
    if (condition)
        action();

    // Terrible
    if (condition)
        for (let key in obj)
            if (Object.hasOwnProperty.call(obj, key)) {
                console.log(key, obj[key]);
                delete obj[key];
            }

    // Good
    if (condition) {
        action();
    }
    ```

## 19. If statement

  * <a name="19.1" href="#19.1">19.1</a>.
    Assign complicated conditions to an intermediate variable (similar idea to [2.4](#2.4)).

    ```js
    // Bad
    if (foo === 'bar' && baz > qux) {
        console.log('mystery condition passed');
    }

    // Good
    const condition = foo === 'bar' && baz > qux;
    if (condition) {
        console.log('condition passed');
    }
    ```

  * <a name="19.2" href="#19.2">19.2</a>.
    You may put `else` and `else if` on the same line as a closing brace if you like. I prefer closing braces on their own line -- just because you can add a comment for the whole `else` block that does not reside in the previous `if` block. Really either way is fine.

    ```js
    // Check if user input is valid
    if (valueEntered && userInput.length > 0) {
        saveValue(userInput);
    // Otherwise reset the value
    } else {
        userInput = null;
        valueEntered = false;
    }

    // Check if user input is valid
    if (valueEntered && userInput.length > 0) {
        saveValue(userInput);
    }
    // Otherwise reset the value
    else {
        userInput = null;
        valueEntered = false;
    }
    ```

  * <a name="19.3" href="#19.3">19.3</a>.
    Do not use an `if` statement where a ternary statement would suffice.

    ```js
    // Bad
    function getFoo () {
        if (foo) {
            return 'foo';
        }
        else {
            return 'bar';
        }
    }

    // Good
    function getFoo () {
        return foo ? 'foo' : 'bar';
    }
    ```

  * <a name="19.4" href="#19.4">19.4</a>.
    Do not use an `if` statement where a boolean would suffice.

    ```js
    // Bad
    function getFoo () {
        if (foo) {
            return true;
        }
        return false;
    }

    // Bad
    function getFoo () {
        if (foo) {
            return true;
        }
        else {
            return false;
        }
    }

    // Good
    function getFoo () {
        return foo;
    }
    ```

## 20. For loops

## 21. While loops

## 22. Switch statement

## 23. With statement

  * <a name="23.1" href="#23.1">23.1</a>.
    No.

## 24. Promises

  * <a name="24.1" href="#24.1">24.1</a>.
    Use `Promise#catch(fn)` instead of `Promise#then(null, fn)`. `catch` is clearer and can be more concise.

    ```js
    // Bad, unclear behavior
    Promise.resolve()
        .then(() => {
            throw new Error('Not implemented');
        }, (err) => {
            // Does not handle the above error
            console.error(err);
        });

    // Bad, verbose
    Promise.resolve()
        .then(() => {
            throw new Error('Not implemented');
        })
        .then(null, (err) => {
            // Handles the above error
            console.error(err);
        });

    // Good, clear and concise
    Promise.resolve()
        .then(() => {
            throw new Error('Not implemented');
        })
        // Handles the above error
        .catch((err) => console.error(err));
    ```

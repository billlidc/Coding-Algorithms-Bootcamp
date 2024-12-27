# Lecture 19 - JavaScript Syntax

## Table of Contents
- [History](#history)
- [Differences Between Java and JavaScript](#differences-between-java-and-javascript)
- [Similarities Between Java and JavaScript](#similarities-between-java-and-javascript)
- [Object Models](#object-models)
- [JavaScript Usage Paradigms](#javascript-usage-paradigms)
- [Document Object Model (DOM)](#document-object-model-dom)
- [Variable Typing](#variable-typing)
- [Native Primitive Types](#native-primitive-types)
- [Native Class/Object Types](#native-classobject-types)
- [Primitive vs. Object Types in JavaScript](#primitive-vs-object-types-in-javascript)
- [Special Pointers](#special-pointers)
- [Strong vs. Weak Typing](#strong-vs-weak-typing)
- [Block Scoping](#block-scoping)
- [Variable Declarations and Scoping](#variable-declarations-and-scoping)
- [Determining the Type of a Variable](#determining-the-type-of-a-variable)
- [Library Import](#library-import)
- [Equality Tests](#equality-tests)
- [Function Declaration](#function-declaration)
- [Class Declaration](#class-declaration)
- [Accessing Class Members](#accessing-class-members)
- [Exception Handling](#exception-handling)
- [Flow Control](#flow-control)
- [Python-Like Features](#python-like-features)
- [Strings in JavaScript](#strings-in-javascript)
- [Type Conversions](#type-conversions)
- [Implicit Type Conversion – To Boolean](#implicit-type-conversion--to-boolean)
- [JavaScript Arithmetic Operators](#javascript-arithmetic-operators)
- [JavaScript Mutation Operators](#javascript-mutation-operators)
- [JavaScript Bitwise Operators](#javascript-bitwise-operators)
- [JavaScript Comparison Operators](#javascript-comparison-operators)
- [JavaScript Boolean Operators](#javascript-boolean-operators)
- [Defining Functions](#defining-functions)


## History
- Originally designed for the Netscape browser.
- *JavaScript* is marginally related to *Java*:
    - Created when Sun Microsystems (developer of Java) collaborated with Netscape.
    - Originally called "*Mocha*", later renamed *JavaScript* as a **marketing strategy** to leverage *Java*'s popularity.
- **Standardized version** of *JavaScript* is called *ECMAScript*:
    - Named by the European Computer Manufacturer's Association (ECMA).

## Differences Between Java and JavaScript

| Feature                        | Java                                | JavaScript                          |
|--------------------------------|-------------------------------------|-------------------------------------|
| **Execution**                  | Compiled                           | Interpreted                         |
| **Typing**                     | Static typing                      | Dynamic typing                      |
| **Variable Typing**            | Strong                             | Weak                                |
| **Hash Tables**                | Provided by libraries              | Native type                         |
| **Object Model**               | Class-based                        | Prototype-based                     |
| **Verbosity**                  | More verbose                       | Less verbose: <br> - No need for class declarations <br> - No need for separate files |

## Similarities Between Java and JavaScript

- Cross-platform support
- (Almost) everything is an object
- Garbage-collected automatic memory management
- Use of braces `{ }` to delimit blocks of code
- Use of semicolons `;` to terminate statements

## Object Models

* **Java - Class-Based:** 
    - Static typing
    - Type safety
    - Class inheritance

* **JavaScript - Prototype-Based:** 
    - Dynamic typing
    - Enables inheritance from any other object

## JavaScript Usage Paradigms

- **Server-side**: Node.js applications

- **Client-side**:
    - Web browsers
    - Mobile apps

## Document Object Model (DOM)

- API for HTML and XML documents
- Represents the page as a tree-like structure
- Enables and simplifies dynamic content in web pages and other mobile contents

## Variable Typing

```java
boolean x = true;
int x = 1;
float x = 2.5;
String x = new String(“s”); List x;
Hashtable x;
Complex x;
```

```js
var x = True;
var x = 1;
var x = 2.5;
var x = 's';
var x = [1, '2', [3.5, 4], 5];
var x = {};
// not available natively
```

## Native Primitive Types

| Feature                | Java                                      | JavaScript                              |
|------------------------|-------------------------------------------|-----------------------------------------|
| **Boolean**            | `boolean` (true, false)                   | `boolean` (true, false)                 |
| **Integers**           | `short`, `int`, `long` (+ unsigned types) | Not available (all numbers are floating-point) |
| **Floating-Point**     | `float`, `double`                         | Equivalent to `double`                  |
| **Characters/Strings** | `char`, `char[]`                          | Strings are equivalent to `char[]`      |



## Native Class/Object Types

| Feature                  | Java                                             | JavaScript                                     |
|--------------------------|--------------------------------------------------|-----------------------------------------------|
| **Class System**         | Uses actual classes with a strict hierarchy      | No actual classes, uses constructor functions |
| **Base of Hierarchy**    | `Object`                                         | `Object`                                      |
| **Native Classes/Types** | `Integer`, `Float`, `String`, `Array`, `List`, `Map` | `Object`, `Array`, `Date`                     |

## Primitive vs. Object Types in JavaScript

**Primitive**

- **Copy Semantics**:
    - Passing primitive values creates a copy of the actual value.
- **Auto-Boxing**:
    - Can be used anywhere an object is required.
    - The interpreter creates a temporary object and fills it with the value of the primitive type when needed.
    - Example: `(3.14).toString();` works because of auto-boxing.

**Object**

- **Reference-Copy Semantics**:
  - Passing objects creates a copy of the reference to the object (not the actual object itself).
- **Object-Declaration Syntax**:
    - `var o = new Object();`
    - `var o = {};` (Object Literal Syntax: `{ key: val, ... }`)

## Special Pointers

| Pointer Type | Java | JavaScript |
|---|---|---|
| Invalid/ "Null" Pointer | `null` | `null` |
| Object Non-existence | `null` (typically used) | `undefined` |
| Current Object | `this` | `this` <br> *(The value of `this` depends on how a function is called.)* |
| | `this.value = null;` | `this.value = null;` |

## Strong vs. Weak Typing

```js
var x = 5;
if (x == '5')
    console.log('True');
//==> True
```

## Block Scoping

```js
if (x < y) { ... } else { ... }
if (y == z) {
   conditional1();
   conditional2();
}
common();
```

## Variable Declarations and Scoping

* **`var`** applies to an entire function
    - The variable can be accessed even before declaration with value `undefined`
    
        ```js
        y = 1;
        
        if (x) {
            var y;
        }
        
        console.log(y);
        ```

        //==> Console outputs 1

* **`let`** is limited in scope to the current block like Java variables
    - `if (x) { let y = 1; } console.log(y);` //==> ReferenceError: y is not defined

* **`const`** does not allow any further assignments
    - `const x = 1; x = 2;` //==> TypeError: Assignment to constant variable

## Determining the Type of a Variable

**`typeof`** operator returns a string indicating the type

```js
console.log(typeof "Ralf");         // "string"
console.log(typeof 3.14);           // "number"
console.log(typeof false);          // "boolean"
console.log(typeof [1, 2]);         // "object"
console.log(typeof new Date());     // "object"
console.log(typeof null);           // "object" (backward compat with old JS)
console.log(typeof function() {});  // "function"
console.log(typeof undefined);      // "undefined"
```

## Library Import

Java

```java
// import a single library
import library;

// import multiple libraries
import library.*;
```

JavaScript

```js
// insert all of a module's exports into namespace name
import * as name from 'mod';

// insert specified export into current scope
import { exp } from 'mod';

// insert an export under an alias
import { exp as alias } from 'mod';
```

## Equality Tests

| Equality Test | Java | JavaScript |
|---|---|---|
| Object (Strict) Identity | `==` | `===` (no type coercion) |
| Value Equality | `.equals()` (method-based) | `==` (with type coercion if needed) |

## Function Declaration

```js
function funcname (argname, ...) {
  var result = X;
  // body
  return result;
}
```

## Class Declaration

Java

```java
class cl extends X {
    type data = defvalue;
    type func(type N) { 
        return N * data;
    }
}
```

JavaScript

```js
function MyClass() {
  this.__proto__ = X;
  this.data = defvalue;
  this.func = function(N) {
    return N * this.data;
  };
}
```

```js
class Car {
  constructor(make, model, year) {
    this.make = make;
    this.model = model;
    this.year = year;
  }

  start() {
    console.log("The car is starting.");
  }

  stop() {
    console.log("The car is stopping.");
  }
}

// Create an instance of the Car class
const myCar = new Car("Toyota", "Camry", 2023);

// Access properties
console.log(myCar.make); // Output: "Toyota"
console.log(myCar.model); // Output: "Camry"
console.log(myCar.year); // Output: 2023

// Call methods
myCar.start(); // Output: "The car is starting."
myCar.stop(); // Output: "The car is stopping."
```

## Accessing Class Members

```js
var foo = new MyClass();

var d1 = foo.data;
var d2 = foo.func(X);
var v = foo.fact(5);
```

## Exception Handling

```js
function E() { ... }

function foo() {
  throw new E();
}

function bar() {
  try {
    foo();
  } catch (exc_var) {
    console.log("Err");
  } finally {
    console.log("Always");
  }
  return;
}
```


## Flow Control


```js
// Conditional statements
if (COND1) {
  block1;
} else if (COND2) {
  block2;
} else if (COND3) {
  block3;
} else {
  block4;
}

// While loops
while (COND) {
  block;
}

do {
  block;
} while (COND);

// For loops
for (INIT; COND; UPDATE) {
  block;
}

for (var V of ARRAY) {
  // ...
}

for (var PROP in OBJ) {
  // ...
}

// Switch statements
switch (EXPR) {
  case X:
    // ...
  default:
    // ...
}

// Within-loop control
break; // end loop
continue; // skip to next iteration
```

## Python-Like Features

Python

```py
# multiple assignment
a, b = x, y
```

```js
// "destructuring" assignment
var [a, b] = [x, y];

var { a, b } = { a: 1, b: 2 };

// with renaming
var { a: foo, b: bar } = { a: 1, b: 2 };
console.log(foo); //==> 1

// with defaults
var { a = 10, b = 5 } = { a: 3 };
console.log(a); //==> 3
console.log(b); //==> 5

// separate from declaration
({ a, b } = {});
```

## Strings in JavaScript

- JavaScript strings are sequences of UTF-16 code points

- Non-printable characters can be specified using backslash escapes as in C or Java:
    - `\0`, `\n`, `\xXX` (Latin-1 in hex), `\uXXXX` (Unicode in hex)

- String literals can be enclosed in single or double quotes

- Strings (including literals) have attributes and methods:
    - `"hello".length` → `5`
    - `'hello'.charAt(0)` → `'h'`

- **Comparison**: `<` and `>` can be used to compare strings based on Unicode code points

## Type Conversions

* **From string to number:**
    - `x = Number(string)`
    - `x = +string` (Unary plus can only operate on numbers, so it will implicitly convert its arg)

* **From number to string:**
    - `x = String(number)`
    - `x = (1).toString()`

* **Automatically:**
    - string + number becomes string + string: "2" + "3" == "23"
    - string - number becomes number - number: "8" - 3 == 5
    - string * string becomes number * number: "2" * "3" == 6

## Implicit Type Conversion – To Boolean

| Value | Boolean Conversion |
|---|---|
| **numbers** |  |
| 0 | false |
| Nonzero number | true |
| NaN | false |
| Infinity | true |
| **strings** |  |
| "" (Empty string) | false |
| Non-empty string | true |
| **Objects** |  |
| null | false |
| undefined | false |
| All other objects | true |

## JavaScript Arithmetic Operators

| Op | Description |
|---|---|
| `a + b` | addition |
| `a - b` | subtraction |
| `a * b` | multiplication |
| `a / b` | division |
| `a % b` | modulus: remainder of a/b |
| `-a` | negation |
| `+a` | (unary plus) a unchanged |

## JavaScript Mutation Operators

| Op | Description |
|---|---|
| `a += b` | add b to a (equivalent to `a = a + b`) |
| `a -= b` | subtract b from a (equivalent to `a = a - b`) |
| `a *= b` | multiply a by b (equivalent to `a = a * b`) |
| `a /= b` | divide a by b (equivalent to `a = a / b`) |
| `a %= b` | modulus: remainder of a/b (equivalent to `a = a % b`) |

## JavaScript Bitwise Operators

| Op | Description |
|---|---|
| `a & b` | bitwise AND |
| `a \| b` | bitwise OR |
| `a ^ b` | bitwise XOR |
| `~a` | bitwise NOT |
| `a << b` | left shift |
| `a >> b` | arithmetic right shift |

* The operators treat the args as 32-bit integers.
* Shifts are modulo 32, meaning the result of the shift operation is wrapped around if it exceeds 32 bits.

## JavaScript Comparison Operators

| Op | Description |
|---|---|
| `a == b` | equals (with type conversion) |
| `a === b` | equals (without type conversion) |
| `a != b` | does not equal |
| `a !== b` | not equal (without type conversion) |
| `a < b` | less than |
| `a > b` | greater than |
| `a <= b` | less than or equal |
| `a >= b` | greater than or equal |

## JavaScript Boolean Operators

| Op | Description |
|---|---|
| `a && b` | both a and b are true |
| `a \|\| b` | at least one of a, b is true |
| `!a` | a is false |

- `&&` and `||` exhibit **short-circuit evaluation**: stop evaluating as soon as the result is determined. 
    - For `&&`, if the first operand is false, the result is false, and the second operand is not evaluated.
    - For `||`, if the first operand is true, the result is true, and the second operand is not evaluated.

## Defining Functions

```js
function fib(N) {
  var L = new Array();
  var a = 0, b = 1, c = 0;

  while (c < N) {
    var tmp = b;
    b = a + b;
    a = tmp;
    L[c++] = a;
  }

  return L;
}

fib(5); // ==> [1, 1, 2, 3, 5]
```

```js
function fib(N, a=0, b=1) {
  var L = new Array();
  var c = 0;
  while (c < N) {
    var tmp = b;
    b = a + b;
    a = tmp;
    L[c++] = a;
  }
  return L;
}

fib(5); // ==> [1, 1, 2, 3, 5]
fib(5, 0, 2); // ==> [2, 2, 4, 6, 10]
fib(5, 3, 1); // ==> [3, 4, 7, 11, 18]
```

Functions can be called with **more** args than declared

```js
function foo(a) {
  console.log(a, arguments);
}

foo(1, 2, 3); // ==> 1 [1, 2, 3]
```

Collect optional args into an array with the **rest** (`...`) operator

```js
function bar(a, ...b) {
  console.log(a, b);
}

bar(1, 2, 3); // ==> 1 [2, 3]
```

Functions can be called with **fewer** args than declared

```js
function foo(a, b, c) {
  console.log(a, b, c);
}

foo(1); // ==> 1 undefined undefined
```

Turn array into separate args with the **spread** (`...`) operator

```js
a = [2, 3];
foo(1, ...a); // ==> 1 2 3
```

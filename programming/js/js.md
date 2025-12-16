# Table of Contents
- [Table of Contents](#table-of-contents)
  - [Basics](#basics)
    - [What are primitive data types?](#what-are-primitive-data-types)
    - [What is the purpose of the let keyword?](#what-is-the-purpose-of-the-let-keyword)
    - [What is the difference between let and var?](#what-is-the-difference-between-let-and-var)
    - [What is scope in javascript?](#what-is-scope-in-javascript)
    - [What is the Temporal Dead Zone?](#what-is-the-temporal-dead-zone)
    - [What is the difference between == and === operators?](#what-is-the-difference-between--and--operators)
    - [How do you redeclare variables in a switch block without an error?](#how-do-you-redeclare-variables-in-a-switch-block-without-an-error)
    - [What is JSON and its common operations?](#what-is-json-and-its-common-operations)
    - [What is the difference between Call, Apply and Bind?](#what-is-the-difference-between-call-apply-and-bind)
    - [How do you decode or encode a URL in JavaScript?](#how-do-you-decode-or-encode-a-url-in-javascript)
    - [What is a strict mode in javascript?](#what-is-a-strict-mode-in-javascript)
    - [Why do you need strict mode?](#why-do-you-need-strict-mode)
    - [How do you declare strict mode?](#how-do-you-declare-strict-mode)
    - [What is the purpose of double exclamation?](#what-is-the-purpose-of-double-exclamation)
    - [What is the purpose of the delete operator?](#what-is-the-purpose-of-the-delete-operator)
    - [What is typeof operator?](#what-is-typeof-operator)
    - [What is undefined property?](#what-is-undefined-property)
    - [What is null value?](#what-is-null-value)
    - [What is the difference between null and undefined?](#what-is-the-difference-between-null-and-undefined)
    - [What is eval?](#what-is-eval)
    - [What is isNaN?](#what-is-isnan)
    - [What are the differences between undeclared and undefined variables?](#what-are-the-differences-between-undeclared-and-undefined-variables)
    - [What are global variables?](#what-are-global-variables)
    - [What are the problems with global variables?](#what-are-the-problems-with-global-variables)
    - [What is NaN property?](#what-is-nan-property)
    - [What is the purpose of isFinite function?](#what-is-the-purpose-of-isfinite-function)
    - [How do you check whether a string contains a substring?](#how-do-you-check-whether-a-string-contains-a-substring)
    - [How do you check if a key exists in an object?](#how-do-you-check-if-a-key-exists-in-an-object)
    - [How do you loop through or enumerate javascript object?](#how-do-you-loop-through-or-enumerate-javascript-object)
    - [How do you assign default values to variables?](#how-do-you-assign-default-values-to-variables)
    - [What are js labels?](#what-are-js-labels)
    - [How do you search a string for a pattern?](#how-do-you-search-a-string-for-a-pattern)
    - [What is the purpose of exec method?](#what-is-the-purpose-of-exec-method)
    - [What is a debugger statement?](#what-is-a-debugger-statement)
    - [What is a conditional operator in javascript?](#what-is-a-conditional-operator-in-javascript)
    - [What is the purpose of uneval?](#what-is-the-purpose-of-uneval)
    - [What is the difference between uneval and eval?](#what-is-the-difference-between-uneval-and-eval)
    - [What is the precedence order between local and global variables?](#what-is-the-precedence-order-between-local-and-global-variables)
    - [What are javascript accessors?](#what-are-javascript-accessors)
    - [What is nodejs?](#what-is-nodejs)
    - [What is typescript?](#what-is-typescript)
    - [What are the differences between javascript and typescript?](#what-are-the-differences-between-javascript-and-typescript)
    - [What are the advantages of typescript over javascript?](#what-are-the-advantages-of-typescript-over-javascript)
    - [What Is Obfuscation in javascript?](#what-is-obfuscation-in-javascript)
    - [Why do you need Obfuscation?](#why-do-you-need-obfuscation)
    - [What is Minification?](#what-is-minification)
    - [What are the advantages of minification?](#what-are-the-advantages-of-minification)
    - [Is enums feature available in javascript?](#is-enums-feature-available-in-javascript)
    - [What is an enum?](#what-is-an-enum)
    - [Does JavaScript supports namespace?](#does-javascript-supports-namespace)
    - [How do you declare namespace?](#how-do-you-declare-namespace)
    - [What is V8 JavaScript engine?](#what-is-v8-javascript-engine)
    - [Why do you need to avoid with statement?](#why-do-you-need-to-avoid-with-statement)
    - [List down some of the features of ES6](#list-down-some-of-the-features-of-es6)
    - [What are template literals?](#what-are-template-literals)
    - [What is destructuring assignment?](#what-is-destructuring-assignment)
    - [What are the differences between for...of and for...in statements?](#what-are-the-differences-between-forof-and-forin-statements)
    - [What is nullish coalescing operator (??)?](#what-is-nullish-coalescing-operator-)
  - [Functions](#functions)
    - [What is an IIFE (Immediately Invoked Function Expression)?](#what-is-an-iife-immediately-invoked-function-expression)
    - [What is Hoisting?](#what-is-hoisting)
    - [What are lambda expressions or arrow functions?](#what-are-lambda-expressions-or-arrow-functions)
    - [What is an anonymous function?](#what-is-an-anonymous-function)
    - [What is a first class function?](#what-is-a-first-class-function)
    - [What is a first order function?](#what-is-a-first-order-function)
    - [What is a higher order function?](#what-is-a-higher-order-function)
    - [What is a unary function?](#what-is-a-unary-function)
    - [What is the currying function?](#what-is-the-currying-function)
    - [What is a pure function?](#what-is-a-pure-function)
    - [What are closures?](#what-are-closures)
    - [What is memoization?](#what-is-memoization)
    - [What is a callback function?](#what-is-a-callback-function)
    - [Why do we need callbacks?](#why-do-we-need-callbacks)
    - [What is a callback hell?](#what-is-a-callback-hell)
    - [What is callback in callback?](#what-is-callback-in-callback)
    - [Can we define properties for functions?](#can-we-define-properties-for-functions)
    - [What is a polyfill?](#what-is-a-polyfill)
    - [What is a rest parameter?](#what-is-a-rest-parameter)
    - [What is a spread operator?](#what-is-a-spread-operator)
    - [What is a decorator?](#what-is-a-decorator)
    - [What are the different kinds of generators?](#what-are-the-different-kinds-of-generators)
  - [Objects and Prototypes](#objects-and-prototypes)
    - [What is a constructor method?](#what-is-a-constructor-method)
    - [How do you call the constructor of a parent class?](#how-do-you-call-the-constructor-of-a-parent-class)
    - [What are the possible ways to create objects in JavaScript?](#what-are-the-possible-ways-to-create-objects-in-javascript)
    - [What is a prototype chain?](#what-is-a-prototype-chain)
    - [How do you compare Object and Map?](#how-do-you-compare-object-and-map)
    - [What is the difference between native, host and user objects?](#what-is-the-difference-between-native-host-and-user-objects)
    - [How do you test for an empty object?](#how-do-you-test-for-an-empty-object)
    - [What is an arguments object?](#what-is-an-arguments-object)
    - [What is the difference between proto and prototype?](#what-is-the-difference-between-proto-and-prototype)
    - [What is a freeze method?](#what-is-a-freeze-method)
    - [What is the purpose of freeze method?](#what-is-the-purpose-of-freeze-method)
    - [How do you determine two values same or not using object?](#how-do-you-determine-two-values-same-or-not-using-object)
    - [How do you copy properties from one object to other](#how-do-you-copy-properties-from-one-object-to-other)
    - [What are the applications of assign method?](#what-are-the-applications-of-assign-method)
    - [What is a proxy object](#what-is-a-proxy-object)
    - [What is the purpose of seal method?](#what-is-the-purpose-of-seal-method)
    - [What are the applications of seal method?](#what-are-the-applications-of-seal-method)
    - [How do you get enumerable key and value pairs?](#how-do-you-get-enumerable-key-and-value-pairs)
    - [What is the main difference between Object.values and Object.entries method?](#what-is-the-main-difference-between-objectvalues-and-objectentries-method)
    - [How can you get the list of keys of any object?](#how-can-you-get-the-list-of-keys-of-any-object)
    - [How do you create an object with prototype?](#how-do-you-create-an-object-with-prototype)
    - [How do you define property on Object constructor?](#how-do-you-define-property-on-object-constructor)
    - [What is the difference between get and defineProperty?](#what-is-the-difference-between-get-and-defineproperty)
    - [What are the advantages of Getters and Setters?](#what-are-the-advantages-of-getters-and-setters)
    - [Can I add getters and setters using defineProperty method?](#can-i-add-getters-and-setters-using-defineproperty-method)
    - [What are the different ways to access object properties?](#what-are-the-different-ways-to-access-object-properties)
    - [What is an error object?](#what-is-an-error-object)
    - [What are the different error names from error object?](#what-are-the-different-error-names-from-error-object)
    - [How do you get property descriptors of an object](#how-do-you-get-property-descriptors-of-an-object)
    - [How do you extend classes?](#how-do-you-extend-classes)
    - [Does javascript uses mixins?](#does-javascript-uses-mixins)
    - [How do you define instance and non-instance properties?](#how-do-you-define-instance-and-non-instance-properties)
  - [Collections](#collections)
    - [What is the purpose of the array slice method?](#what-is-the-purpose-of-the-array-slice-method)
    - [What is the purpose of the array splice method?](#what-is-the-purpose-of-the-array-splice-method)
    - [What is the difference between slice and splice?](#what-is-the-difference-between-slice-and-splice)
    - [What is a WeakSet?](#what-is-a-weakset)
    - [What are the differences between WeakSet and Set?](#what-are-the-differences-between-weakset-and-set)
    - [What is a WeakMap?](#what-is-a-weakmap)
    - [What are the differences between WeakMap and Map?](#what-are-the-differences-between-weakmap-and-map)
    - [How do you compare scalar arrays?](#how-do-you-compare-scalar-arrays)
    - [What is the difference between dense and sparse arrays?](#what-is-the-difference-between-dense-and-sparse-arrays)
    - [What are the different ways to create sparse arrays?](#what-are-the-different-ways-to-create-sparse-arrays)
  - [Asynchronous JavaScript](#asynchronous-javascript)
    - [What is a promise?](#what-is-a-promise)
    - [Why do you need a promise?](#why-do-you-need-a-promise)
    - [What are the three states of promise?](#what-are-the-three-states-of-promise)
    - [What are the main rules of promise?](#what-are-the-main-rules-of-promise)
    - [What is promise chaining?](#what-is-promise-chaining)
    - [What is promise.all?](#what-is-promiseall)
    - [What is the purpose of the race method in promise?](#what-is-the-purpose-of-the-race-method-in-promise)
    - [What are the pros and cons of promises over callbacks?](#what-are-the-pros-and-cons-of-promises-over-callbacks)
    - [What is the use of setTimeout?](#what-is-the-use-of-settimeout)
    - [What is the use of setInterval?](#what-is-the-use-of-setinterval)
    - [What is the purpose of clearTimeout method?](#what-is-the-purpose-of-cleartimeout-method)
    - [What is the purpose of clearInterval method?](#what-is-the-purpose-of-clearinterval-method)
    - [What is an async function?](#what-is-an-async-function)
    - [What is the event loop in JavaScript runtimes?](#what-is-the-event-loop-in-javascript-runtimes)
  - [References](#references)


## Basics

### What are primitive data types?
A primitive data type is data that has a primitive value (which has no properties or methods). There are 7 types of primitive data types.

- string
- number
- boolean
- null
- undefined
- bigint
- symbol

---

### What is the purpose of the let keyword?


The `let` statement declares a **block scope local variable**. Hence the variables defined with let keyword are limited in scope to the block, statement, or expression on which it is used. Whereas variables declared with the `var` keyword used to define a variable globally, or locally to an entire function regardless of block scope.

Let's take an example to demonstrate the usage,

```js
let counter = 30;
if (counter === 30) {
  let counter = 31;
  console.log(counter); // 31
}
console.log(counter); // 30 (because the variable in if block won't exist here)
```

---

### What is the difference between let and var?

You can list out the differences in a tabular format

| var                                                            | let                                           |
| -------------------------------------------------------------- | --------------------------------------------- |
| It has been available from the beginning of JavaScript         | Introduced as part of ES6                     |
| It has function scope                                          | It has block scope                            |
| Variable declaration will be hoisted, initialized as undefined | Hoisted but not initialized                   |
| It is possible to re-declare the variable in the same scope    | It is not possible to re-declare the variable |

Let's take an example to see the difference,
```js
function userDetails(username) {
  if (username) {
    console.log(salary); // undefined due to hoisting
    console.log(age); // ReferenceError: Cannot access 'age' before initialization
    let age = 30;
    var salary = 10000;
  }
  console.log(salary); //10000 (accessible due to function scope)
  console.log(age); //error: age is not defined(due to block scope)
}
userDetails("John");
```
---

### What is scope in javascript?
Scope is the accessibility of variables, functions, and objects in some particular part of your code during runtime. In other words, scope determines the visibility of variables and other resources in areas of your code.

---


### What is the Temporal Dead Zone?

The Temporal Dead Zone(TDZ) is a specific period or area of a block where a variable is inaccessible until it has been initialized with a value. This behavior in JavaScript that occurs when declaring a variable with the let and const keywords, but not with var. In ECMAScript 6, accessing a let or const variable before its declaration (within its scope) causes a ReferenceError.

Let's see this behavior with an example,

```js
function somemethod() {
  console.log(counter1); // undefined
  console.log(counter2); // ReferenceError
  var counter1 = 1;
  let counter2 = 2;
}
```

---


### What is the difference between == and === operators?

JavaScript provides both strict(===, !==) and type-converting(==, !=) equality comparison. The strict operators take type of variable in consideration, while non-strict operators make type correction/conversion based upon values of variables. The strict operators follow the below conditions for different types,

1. Two strings are strictly equal when they have the same sequence of characters, same length, and same characters in corresponding positions.
2. Two numbers are strictly equal when they are numerically equal, i.e., having the same number value. There are two special cases in this,
     1. NaN is not equal to anything, including NaN.
     2. Positive and negative zeros are equal to one another.
3. Two Boolean operands are strictly equal if both are true or both are false.
4. Two objects are strictly equal if they refer to the same Object.
5. Null and Undefined types are not equal with ===, but equal with == . i.e, `null===undefined --> false`, but `null==undefined --> true`

Some of the example which covers the above cases:
```js
0 == false   // true
0 === false  // false
1 == "1"     // true
1 === "1"    // false
null == undefined // true
null === undefined // false
'0' == false // true
'0' === false // false
NaN == NaN or NaN === NaN // false
[]==[] or []===[] //false, refer different objects in memory
{}=={} or {}==={} //false, refer different objects in memory
```

---


### How do you redeclare variables in a switch block without an error?

If you try to redeclare variables in a `switch block` then it will cause errors because there is only one block. For example, the below code block throws a syntax error as below,

```js
let counter = 1;
switch (x) {
  case 0:
    let name;
    break;

  case 1:
    let name; // SyntaxError for redeclaration.
    break;
}
```

To avoid this error, you can create a nested block inside a case clause and create a new block scoped lexical environment.

```js
let counter = 1;
switch (x) {
  case 0: {
    let name;
    break;
  }
  case 1: {
    let name; // No SyntaxError for redeclaration.
    break;
  }
}
```

---


### What is JSON and its common operations?

**JSON** is a text-based data format following JavaScript object syntax, which was popularized by `Douglas Crockford`. It is useful when you want to transmit data across a network. It is basically just a text file with an extension of .json, and a MIME type of application/json

**Parsing**: Converting a string to a native object
```js
JSON.parse(text);
```

**Stringification**: Converting a native object to a string so that it can be transmitted across the network
```js
JSON.stringify(object);
```

---

### What is the difference between Call, Apply and Bind?

The difference between Call, Apply and Bind can be explained with below examples:

**Call**: The call() method invokes a function with a given `this` value and arguments provided one by one

```js
var employee1 = { firstName: "John", lastName: "Rodson" };
var employee2 = { firstName: "Jimmy", lastName: "Baily" };

function invite(greeting1, greeting2) {
  console.log(
    greeting1 + " " + this.firstName + " " + this.lastName + ", " + greeting2
  );
}

invite.call(employee1, "Hello", "How are you?"); // Hello John Rodson, How are you?
invite.call(employee2, "Hello", "How are you?"); // Hello Jimmy Baily, How are you?
```

**Apply**: Invokes the function with a given `this` value and allows you to pass in arguments as an array
```js
var employee1 = { firstName: "John", lastName: "Rodson" };
var employee2 = { firstName: "Jimmy", lastName: "Baily" };

function invite(greeting1, greeting2) {
  console.log(
    greeting1 + " " + this.firstName + " " + this.lastName + ", " + greeting2
  );
}

invite.apply(employee1, ["Hello", "How are you?"]); // Hello John Rodson, How are you?
invite.apply(employee2, ["Hello", "How are you?"]); // Hello Jimmy Baily, How are you?
```

**Bind**: returns a new function, allowing you to pass any number of arguments
```js
var employee1 = { firstName: "John", lastName: "Rodson" };
var employee2 = { firstName: "Jimmy", lastName: "Baily" };

function invite(greeting1, greeting2) {
  console.log(
    greeting1 + " " + this.firstName + " " + this.lastName + ", " + greeting2
  );
}

var inviteEmployee1 = invite.bind(employee1);
var inviteEmployee2 = invite.bind(employee2);
inviteEmployee1("Hello", "How are you?"); // Hello John Rodson, How are you?
inviteEmployee2("Hello", "How are you?"); // Hello Jimmy Baily, How are you?
```

Call and Apply are pretty much interchangeable. Both execute the current function immediately. You need to decide whether it’s easier to send in an array or a comma separated list of arguments. You can remember by treating Call is for **comma** (separated list) and Apply is for **Array**.  

Bind creates a new function that will have this set to the first parameter passed to bind().

---


### How do you decode or encode a URL in JavaScript?
`encodeURI()` function is used to encode an URL. This function requires a URL string as a parameter and return that encoded string. `decodeURI()` function is used to decode an URL. This function requires an encoded URL string as parameter and return that decoded string.

**Note**: If you want to encode characters such as `/ ? : @ & = + $ #` then you need to use `encodeURIComponent()`.

```js
let uri = "employeeDetails?name=john&occupation=manager";
let encoded_uri = encodeURI(uri);
let decoded_uri = decodeURI(encoded_uri);
```

---


### What is a strict mode in javascript?
Strict Mode is a new feature in ECMAScript 5 that allows you to place a program, or a function, in a “strict” operating context. This way it prevents certain actions from being taken and throws more exceptions. The literal expression `"use strict";` instructs the browser to use the javascript code in the Strict mode. This also enables block-scoped variables.

---

### Why do you need strict mode?

Strict mode is useful to write "secure" JavaScript by notifying "bad syntax" into real errors. For example, it eliminates accidentally creating a global variable by throwing an error and also throws an error for assignment to a non-writable property, a getter-only property, a non-existing property, a non-existing variable, or a non-existing object.

---

### How do you declare strict mode?

The strict mode is declared by adding "use strict"; to the beginning of a script or a function. If declared at the beginning of a script, it has global scope.

```js
"use strict";
x = 3.14; // This will cause an error because x is not declared
```
 
 and if you declare inside a function, it has local scope

```js
x = 3.14; // This will not cause an error.
myFunction();

function myFunction() {
  "use strict";
  y = 3.14; // This will cause an error
}
```

---

### What is the purpose of double exclamation?
The double exclamation or negation(!!) ensures the resulting type is a boolean. If it was falsey (e.g. 0, null, undefined, etc.), it will be false, otherwise, it will be true. For example, you can test IE version using this expression as below,

```js
let isIE8 = false;
isIE8 = !!navigator.userAgent.match(/MSIE 8.0/);
console.log(isIE8); // returns true or false
```
If you don't use this expression then it returns the original value.

```js
console.log(navigator.userAgent.match(/MSIE 8.0/)); // returns either an Array or null
```

**Note**: The expression !! is not an operator, but it is just twice of ! operator.

---

### What is the purpose of the delete operator?
The delete operator is used to delete the property as well as its value.

```js
var user = { firstName: "John", lastName:"Doe", age: 20 };
delete user.age;

console.log(user); // {firstName: "John", lastName:"Doe"}
```

### What is typeof operator?
You can use the JavaScript typeof operator to find the type of a JavaScript variable. It returns the type of a variable or an expression.

```js
typeof "John Abraham"; // Returns "string"
typeof (1 + 2); // Returns "number"
typeof [1, 2, 3]; // Returns "object" because all arrays are also objects
```

---

### What is undefined property?
The undefined property indicates that a variable has not been assigned a value, or declared but not initialized at all. The type of undefined value is undefined too.

```js
var user; // Value is undefined, type is undefined
console.log(typeof user); //undefined
```

Any variable can be emptied by setting the value to undefined.

```js
user = undefined;
```

---

### What is null value?
The value null represents the intentional absence of any object value. It is one of JavaScript's primitive values. The type of null value is object. You can empty the variable by setting the value to null.

```js
var user = null;
console.log(typeof user); //object
```

---

### What is the difference between null and undefined?
Below are the main differences between null and undefined,

| Null                                                                                            | Undefined                                                                                               |
| ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| It is an assignment value which indicates that variable points to no object.                    | It is not an assignment value where a variable has been declared but has not yet been assigned a value. |
| Type of null is object                                                                          | Type of undefined is undefined                                                                          |
| The null value is a primitive value that represents the null, empty, or non-existent reference. | The undefined value is a primitive value used when a variable has not been assigned a value.            |
| Indicates the absence of a value for a variable                                                 | Indicates absence of variable itself                                                                    |
| Converted to zero (0) while performing primitive operations                                     | Converted to NaN while performing primitive operations                                                  |

---

### What is eval?
The eval() function evaluates JavaScript code represented as a string. The string can be a JavaScript expression, variable, statement, or sequence of statements.

```js
console.log(eval("1 + 2")); //  3
```

---

### What is isNaN?
The isNaN() function is used to determine whether a value is an illegal number (Not-a-Number) or not. i.e, This function returns true if the value equates to NaN. Otherwise it returns false.

```js
isNaN("Hello"); //true
isNaN("100"); //false
```

---

### What are the differences between undeclared and undefined variables?
Below are the major differences between undeclared(not defined) and undefined variables,

  | undeclared                                                                                  | undefined                                                                              |
  | ------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
  | These variables do not exist in a program and are not declared                              | These variables declared in the program but have not assigned any value                |
  | If you try to read the value of an undeclared variable, then a runtime error is encountered | If you try to read the value of an undefined variable, an undefined value is returned. |

```js
var a; a; // yields undefined

b; // Throws runtime error like "Uncaught ReferenceError: b is not defined"
```
This can be confusing, because it says „not defined“ instead of „not declared“ (Chrome)

---

### What are global variables?
Global variables are those that are available throughout the length of the code without any scope. The var keyword is used to declare a local variable but if you omit it then it will become global variable

```js
msg = "Hello"; // var is missing, it becomes global variable
```

---

### What are the problems with global variables?

The problem with global variables is the conflict of variable names of local and global scope. It is also difficult to debug and test the code that relies on global variables. 

---

### What is NaN property?

The NaN property is a global property that represents "Not-a-Number" value. i.e, It indicates that a value is not a legal number. It is very rare to use NaN in a program but it can be used as return value for few cases 

```js
Math.sqrt(-1);
parseInt("Hello");
```

---

### What is the purpose of isFinite function?

The isFinite() function is used to determine whether a number is a finite, legal number. It returns false if the value is +infinity, -infinity, or NaN (Not-a-Number), otherwise it returns true.

```js
isFinite(Infinity); // false
isFinite(NaN); // false
isFinite(-Infinity); // false

isFinite(100); // true
```

---

### How do you check whether a string contains a substring?
There are 3 possible ways to check whether a string contains a substring or not,

1. Using **includes**: ES6 provided `String.prototype.includes` method to test a string contains a substring

```js
var mainString = "hello",
  subString = "hell";
mainString.includes(subString);
```

2. Using **indexOf**: In an ES5 or older environment, you can use String.prototype.indexOf which returns the index of a substring. If the index value is not equal to -1 then it means the substring exists in the main string.

```js
var mainString = "hello",
  subString = "hell";
mainString.indexOf(subString) !== -1;
```

3. Using **RegEx**: The advanced solution is using Regular expression's test method(RegExp.test), which allows for testing for against regular expressions

```js
var mainString = "hello",
  regex = /hell/;
regex.test(mainString);
```

---

### How do you check if a key exists in an object?
You can check whether a key exists in an object or not using three approaches,

1. Using **in** operator: You can use the in operator whether a key exists in an object or not 

```js
"key" in obj;
```

and If you want to check if a key doesn't exist, remember to use parenthesis,

```js
!("key" in obj);
```

2. Using **hasOwnProperty** method: You can use `hasOwnProperty` to particularly test for properties of the object instance (and not inherited properties)

```js
obj.hasOwnProperty("key"); // true
```

3. Using **undefined** comparison: If you access a non-existing property from an object, the result is undefined. Let’s compare the properties against undefined to determine the existence of the property.

```js
const user = {
  name: "John",
};

console.log(user.name !== undefined); // true
console.log(user.nickName !== undefined); // false
```

---

### How do you loop through or enumerate javascript object?
You can use the `for-in` loop to loop through javascript object. You can also make sure that the key you get is an actual property of an object, and doesn't come from the prototype using `hasOwnProperty` method.

```js
var object = {
  k1: "value1",
  k2: "value2",
  k3: "value3",
};

for (var key in object) {
  if (object.hasOwnProperty(key)) {
    console.log(key + " -> " + object[key]); // k1 -> value1 ...
  }
}
```

---

### How do you assign default values to variables?
You can use the logical or operator || in an assignment expression to provide a default value. The syntax looks like as below,

```js
var a = b || c;
```
As per the above expression, variable 'a 'will get the value of 'c' only if 'b' is falsy (if is null, false, undefined, 0, empty string, or NaN), otherwise 'a' will get the value of 'b'.

---

### What are js labels?
The label statement allows us to name loops and blocks in JavaScript. We can then use these labels to refer back to the code later. For example, the below code with labels avoids printing the numbers when they are same,

```js
var i, j;

loop1: for (i = 0; i < 3; i++) {
  loop2: for (j = 0; j < 3; j++) {
    if (i === j) {
      continue loop1;
    }
    console.log("i = " + i + ", j = " + j);
  }
}

// Output is:
//   "i = 1, j = 0"
//   "i = 2, j = 0"
//   "i = 2, j = 1"
```

---


### How do you search a string for a pattern?
You can use the test() method of regular expression in order to search a string for a pattern, and return true or false depending on the result.

```js
var pattern = /you/;
console.log(pattern.test("How are you?")); //true
```

---

### What is the purpose of exec method?
The purpose of exec method is similar to test method but it executes a search for a match in a specified string and returns a result array, or null instead of returning true/false.

```js
var pattern = /you/;
console.log(pattern.exec("How are you?")); //["you", index: 8, input: "How are you?", groups: undefined]
```

---

### What is a debugger statement?
The debugger statement invokes any available debugging functionality, such as setting a breakpoint. If no debugging functionality is available, this statement has no effect. For example, in the below function a debugger statement has been inserted. So execution is paused at the debugger statement just like a breakpoint in the script source.

```js
function getProfile() {
  // code goes here
  debugger;
  // code goes here
}
```

---

### What is a conditional operator in javascript?
The conditional (ternary) operator is the only JavaScript operator that takes three operands which acts as a shortcut for if statements.

```js
var isAuthenticated = false;
console.log(
  isAuthenticated ? "Hello, welcome" : "Sorry, you are not authenticated"
); //Sorry, you are not authenticated
```

---


### What is the purpose of uneval?
The uneval() is an inbuilt function which is used to create a string representation of the source code of an Object. It is a top-level function and is not associated with any object. Let's see the below example to know more about it's functionality,

```js
var a = 1;
uneval(a); // returns a String containing 1
uneval(function user() {}); // returns "(function user(){})"
```

The `uneval()` function has been deprecated. It is recommended to use `toString()` for functions and `JSON.toStringify()` for other cases.

```js
function user() {}
console.log(user.toString()); // returns "(function user(){})"
```

---

### What is the difference between uneval and eval?
The uneval function returns the source of a given object; whereas the eval function does the opposite, by evaluating that source code in a different memory area. Let's see an example to clarify the difference,

```js
var msg = uneval(function greeting() {
  return "Hello, Good morning";
});
var greeting = eval(msg);
greeting(); // returns "Hello, Good morning"
```

---

### What is the precedence order between local and global variables?
A local variable takes precedence over a global variable with the same name. Let's see this behavior in an example.

```js
var msg = "Good morning";
function greeting() {
  msg = "Good Evening";
  console.log(msg); // Good Evening
}
greeting();
```

---

### What are javascript accessors?
ECMAScript 5 introduced javascript object accessors or computed properties through getters and setters. Getters uses the get keyword whereas Setters uses the set keyword.

```js
var user = {
  firstName: "John",
  lastName: "Abraham",
  language: "en",
  get lang() {
    return this.language;
  },
  set lang(lang) {
    this.language = lang;
  },
};
console.log(user.lang); // getter access lang as en
user.lang = "fr";
console.log(user.lang); // setter used to set lang as fr
```

---

### What is nodejs?
Node.js is a server-side platform built on Chrome's JavaScript runtime for easily building fast and scalable network applications. It is an event-based, non-blocking, asynchronous I/O runtime that uses Google's V8 JavaScript engine and libuv library.

---


### What is typescript?
TypeScript is a typed superset of JavaScript created by Microsoft that adds optional types, classes, async/await, and many other features, and compiles to plain JavaScript. Angular is built entirely in TypeScript and is used as the primary language. You can install it globally as

```bash
npm install -g typescript
```
Let's see a simple example of TypeScript usage,

```js
function greeting(name: string): string {
  return "Hello, " + name;
}

let user = "Sudheer";

console.log(greeting(user));
```
The greeting method allows only string type as argument.

---


### What are the differences between javascript and typescript?

Below are the list of differences between javascript and typescript,

| feature             | typescript                            | javascript                                      |
| ------------------- | ------------------------------------- | ----------------------------------------------- |
| Language paradigm   | Object oriented programming language  | Scripting language                              |
| Typing support      | Supports static typing                | It has dynamic typing                           |
| Modules             | Supported                             | Not supported                                   |
| Interface           | It has interfaces concept             | Doesn't support interfaces                      |
| Optional parameters | Functions support optional parameters | No support of optional parameters for functions |


### What are the advantages of typescript over javascript?
Below are some of the advantages of typescript over javascript,

- TypeScript is able to find compile time errors at the development time only and it makes sures less runtime errors. Whereas javascript is an interpreted language.
- TypeScript is strongly-typed or supports static typing which allows for checking type correctness at compile time. This is not available in javascript.
- TypeScript compiler can compile the .ts files into ES3,ES4 and ES5 unlike ES6 features of javascript which may not be supported in some browsers.

---

### What Is Obfuscation in javascript?
Obfuscation is the deliberate act of creating obfuscated javascript code(i.e, source or machine code) that is difficult for humans to understand. It is something similar to encryption, but a machine can understand the code and execute it. Let's see the below function before Obfuscation,

```js
function greeting() {
  console.log("Hello, welcome to JS world");
}
```
And after the code Obfuscation, it would be appeared as below,

```js
eval(
  (function (p, a, c, k, e, d) {
    e = function (c) {
      return c;
    };
    if (!"".replace(/^/, String)) {
      while (c--) {
        d[c] = k[c] || c;
      }
      k = [
        function (e) {
          return d[e];
        },
      ];
      e = function () {
        return "\\w+";
      };
      c = 1;
    }
    while (c--) {
      if (k[c]) {
        p = p.replace(new RegExp("\\b" + e(c) + "\\b", "g"), k[c]);
      }
    }
    return p;
  })(
    "2 1(){0.3('4, 7 6 5 8')}",
    9,
    9,
    "console|greeting|function|log|Hello|JS|to|welcome|world".split("|"),
    0,
    {}
  )
);
```
---

### Why do you need Obfuscation?
Below are the few reasons for Obfuscation,

- The Code size will be reduced. So data transfers between server and client will be fast.
- It hides the business logic from outside world and protects the code from others
- Reverse engineering is highly difficult
- The download time will be reduced

---

### What is Minification?

Minification is the process of removing all unnecessary characters(empty spaces are removed) and variables will be renamed without changing it's functionality. It is also a type of obfuscation .

---

### What are the advantages of minification?

Normally it is recommended to use minification for heavy traffic and intensive requirements of resources. It reduces file sizes with below benefits,

- Decreases loading times of a web page
- Saves bandwidth usages

---

### Is enums feature available in javascript?
No, javascript does not natively support enums. But there are different kinds of solutions to simulate them even though they may not provide exact equivalents. For example, you can use freeze or seal on object,

```js
var DaysEnum = Object.freeze({"monday":1, "tuesday":2, "wednesday":3, ...})
```

---

### What is an enum?
An enum is a type restricting variables to one value from a predefined set of constants. JavaScript has no enums but typescript provides built-in enum support.

```js
enum Color {
 RED, GREEN, BLUE
}
```
---

### Does JavaScript supports namespace?
JavaScript doesn’t support namespace by default. So if you create any element(function, method, object, variable) then it becomes global and pollutes the global namespace. Let's take an example of defining two functions without any namespace,

```js
function func1() {
  console.log("This is a first definition");
}
function func1() {
  console.log("This is a second definition");
}
func1(); // This is a second definition
```
It always calls the second function definition. In this case, namespace will solve the name collision problem.

---

### How do you declare namespace?
Even though JavaScript lacks namespaces, we can use Objects , IIFE to create namespaces.

1. Using **Object Literal Notation**: Let's wrap variables and functions inside an Object literal which acts as a namespace. After that you can access them using object notation

```js
var namespaceOne = {
    function func1() {
        console.log("This is a first definition");
    }
}
var namespaceTwo = {
      function func1() {
          console.log("This is a second definition");
      }
  }
namespaceOne.func1(); // This is a first definition
namespaceTwo.func1(); // This is a second definition
```

2. Using **IIFE** (Immediately invoked function expression): The outer pair of parentheses of IIFE creates a local scope for all the code inside of it and makes the anonymous function a function expression. Due to that, you can create the same function in two different function expressions to act as a namespace.

```js
(function () {
  function fun1() {
    console.log("This is a first definition");
  }
  fun1();
})();

(function () {
  function fun1() {
    console.log("This is a second definition");
  }
  fun1();
})();
```
3. Using a block and a let/const declaration: In ECMAScript 6, you can simply use a block and a let declaration to restrict the scope of a variable to a block.

```js
{
  let myFunction = function fun1() {
    console.log("This is a first definition");
  };
  myFunction();
}
//myFunction(): ReferenceError: myFunction is not defined.

{
  let myFunction = function fun1() {
    console.log("This is a second definition");
  };
  myFunction();
}
//myFunction(): ReferenceError: myFunction is not defined.
```

---

### What is V8 JavaScript engine?
V8 is an open source high-performance JavaScript engine used by the Google Chrome browser, written in C++. It is also being used in the node.js project. It implements ECMAScript and WebAssembly, and runs on Windows 7 or later, macOS 10.12+, and Linux systems that use x64, IA-32, ARM, or MIPS processors. Note: It can run standalone, or can be embedded into any C++ application. 

---

### Why do you need to avoid with statement?
JavaScript's with statement was intended to provide a shorthand for writing recurring accesses to objects. So it can help reduce file size by reducing the need to repeat a lengthy object reference without performance penalty. Let's take an example where it is used to avoid redundancy when accessing an object several times.

```js
a.b.c.greeting = "welcome";
a.b.c.age = 32;
```

Using with it turns this into:

```js
with (a.b.c) {
  greeting = "welcome";
  age = 32;
}
```
But this with statement creates performance problems since one cannot predict whether an argument will refer to a real variable or to a property inside the with argument.

---

### List down some of the features of ES6
Below are the list of some new features of ES6,

- Support for constants or immutable variables
- Block-scope support for variables, constants and functions
- Arrow functions
- Default parameters
- Rest and Spread Parameters
- Template Literals
- Multi-line Strings
- Destructuring Assignment
- Enhanced Object Literals
- Promises
- Classes
- Modules

---

### What are template literals?
Template literals or template strings are string literals allowing embedded expressions. These are enclosed by the back-tick (`) character instead of double or single quotes. In ES6, this feature enables using dynamic expressions as below,

```js
var greeting = `Welcome to JS World, Mr. ${firstName} ${lastName}.`;
```
In ES5, you need break string like below,

```js
var greeting = 'Welcome to JS World, Mr. ' + firstName + ' ' + lastName.`
```
**Note**: You can use multi-line strings and string interpolation features with template literals.


---

### What is destructuring assignment?
The destructuring assignment is a JavaScript expression that makes it possible to unpack values from arrays or properties from objects into distinct variables. Let's get the month values from an array using destructuring assignment

```js
var [one, two, three] = ["JAN", "FEB", "MARCH"];

console.log(one); // "JAN"
console.log(two); // "FEB"
console.log(three); // "MARCH"
```

and you can get user properties of an object using destructuring assignment,

```js
var { name, age } = { name: "John", age: 32 };

console.log(name); // John
console.log(age); // 32
```

---


### What are the differences between for...of and for...in statements?
Both for...in and for...of statements iterate over js data structures. The only difference is over what they iterate:

- for..in iterates over all enumerable property keys of an object
- for..of iterates over the values of an iterable object.  

Let's explain this difference with an example,

```js
let arr = ["a", "b", "c"];

arr.newProp = "newVlue";

// key are the property keys
for (let key in arr) {
  console.log(key); // 0, 1, 2 & newProp
}

// value are the property values
for (let value of arr) {
  console.log(value); // a, b, c
}
```
Since for..in loop iterates over the keys of the object, the first loop logs 0, 1, 2 and newProp while iterating over the array object. The for..of loop iterates over the values of a arr data structure and logs a, b, c in the console.

---


### What is nullish coalescing operator (??)?

It is a logical operator that returns its right-hand side operand when its left-hand side operand is null or undefined, and otherwise returns its left-hand side operand. This can be contrasted with the logical OR (||) operator, which returns the right-hand side operand if the left operand is any falsy value, not only null or undefined.

```js
console.log(null ?? true); // true
console.log(false ?? true); // false
console.log(undefined ?? true); // true 
```
---

## Functions

### What is an IIFE (Immediately Invoked Function Expression)?

IIFE (Immediately Invoked Function Expression) is a JavaScript function that runs as soon as it is defined. The signature of it would be as below,

```js
(function () {
  // logic here
})();
```

The primary reason to use an IIFE is to obtain data privacy because any variables declared within the IIFE cannot be accessed by the outside world. i.e, If you try to access variables from the IIFE then it throws an error as below,

```js
(function () {
  var message = "IIFE";
  console.log(message);
})();
console.log(message); //Error: message is not defined
```

---


### What is Hoisting?
Hoisting is a JavaScript mechanism where variables, function declarations and classes are moved to the top of their scope before code execution. Remember that JavaScript only hoists declarations, not initialisation. Let's take a simple example of variable hoisting,

```js
console.log(message); //output : undefined
var message = "The variable Has been hoisted";
```

The above code looks like as below to the interpreter,
```js
var message;
console.log(message);
message = "The variable Has been hoisted";
```

In the same fashion, function declarations are hoisted too
```js
message("Good morning"); //Good morning

function message(name) {
  console.log(name);
}
```
This hoisting makes functions to be safely used in code before they are declared.

---


### What are lambda expressions or arrow functions?

An arrow function is a shorter/concise syntax for a function expression and does not have its own **this, arguments, super, or new.target**. These functions are best suited for non-method functions, and they cannot be used as constructors.

Some of the examples of arrow functions are listed as below,
```js
const arrowFunc1 = (a, b) => a + b; // Multiple parameters
const arrowFunc2 = a => a * 10; // Single parameter
const arrowFunc3 = () => {} // no parameters
```

---

### What is an anonymous function?
An anonymous function is a function without a name! Anonymous functions are commonly assigned to a variable name or used as a callback function. The syntax would be as below,

```js
function (optionalParameters) {
  //do something
}

const myFunction = function(){ //Anonymous function assigned to a variable
  //do something
};

[1, 2, 3].map(function(element){ //Anonymous function used as a callback function
  //do something
});
```
Let's see the above anonymous function in an example,

```js
var x = function (a, b) {
  return a * b;
};
var z = x(5, 10);
console.log(z); // 50
```

---


### What is a first class function?

In Javascript, functions are first class objects. First-class functions means when functions in that language are treated like any other variable.

For example, in such a language, a function can be passed as an argument to other functions, can be returned by another function and can be assigned as a value to a variable. For example, in the below example, handler functions assigned to a listener

```js
const handler = () => console.log("This is a click handler function");
document.addEventListener("click", handler);
```

---

### What is a first order function?

A first-order function is a function that doesn’t accept another function as an argument and doesn’t return a function as its return value.

```js
const firstOrder = () => console.log("I am a first order function!");
```

---

### What is a higher order function?

A higher-order function is a function that accepts another function as an argument or returns a function as a return value or both. The syntactic structure of higher order function will be as follows,

```js
const firstOrderFunc = () => console.log("Hello, I am a First order function");
const higherOrder = (ReturnFirstOrderFunc) => ReturnFirstOrderFunc();
higherOrder(firstOrderFunc);
```
You can also call the function which you are passing to higher order function as callback function.

The higher order function is helpful to write the modular and reusable code.

---

### What is a unary function?

A unary function (i.e. monadic) is a function that accepts exactly one argument. It stands for a single argument accepted by a function.

Let us take an example of unary function,

```js
const unaryFunction = (a) => console.log(a + 10); // Add 10 to the given argument and display the value
```

---

### What is the currying function?

Currying is the process of taking a function with multiple arguments and turning it into a sequence of functions each with only a single argument. Currying is named after a mathematician **Haskell Curry**. By applying currying, an n-ary function turns into a unary function.

Let's take an example of n-ary function and how it turns into a currying function,

```js
const multiArgFunction = (a, b, c) => a + b + c;
console.log(multiArgFunction(1, 2, 3)); // 6

const curryUnaryFunction = (a) => (b) => (c) => a + b + c;
curryUnaryFunction(1); // returns a function: b => c =>  1 + b + c
curryUnaryFunction(1)(2); // returns a function: c => 3 + c
curryUnaryFunction(1)(2)(3); // returns the number 6
```

Curried functions are great to improve **code reusability** and **functional composition**.

---

### What is a pure function?

A **Pure function** is a function where the return value is only determined by its arguments without any side effects. i.e, If you call a function with the same arguments 'n' number of times and 'n' number of places in the application then it will always return the same value.

Let's take an example to see the difference between pure and impure functions,

```js
//Impure
let numberArray = [];
const impureAddNumber = (number) => numberArray.push(number);
//Pure
const pureAddNumber = (number) => (argNumberArray) =>
  argNumberArray.concat([number]);

//Display the results
console.log(impureAddNumber(6)); // returns 1
console.log(numberArray); // returns [6]
console.log(pureAddNumber(7)(numberArray)); // returns [6, 7]
console.log(numberArray); // returns [6]
```

As per the above code snippets, the **Push** function is impure itself by altering the array and returning a push number index independent of the parameter value, whereas **Concat** on the other hand takes the array and concatenates it with the other array producing a whole new array without side effects. Also, the return value is a concatenation of the previous array.

Remember that Pure functions are important as they simplify unit testing without any side effects and no need for dependency injection. They also avoid tight coupling and make it harder to break your application by not having any side effects. These principles are coming together with the **Immutability** concept of ES6: giving preference to **const** over **let** usage.

---


### What are closures?

A closure is the combination of a function bundled(enclosed) together with its lexical environment within which that function was declared. i.e, It is an inner function that has access to the outer or enclosing function’s variables, functions and other data even after the outer function has finished its execution. The closure has three scope chains.

1. Own scope where variables defined between its curly brackets
2. Outer function's variables
3. Global variables
Let's take an example of closure concept,

```js
function Welcome(name) {
  var greetingInfo = function (message) {
    console.log(message + " " + name);
  };
  return greetingInfo;
}
var myFunction = Welcome("John");
myFunction("Welcome "); //Output: Welcome John
myFunction("Hello Mr."); //output: Hello Mr. John
```

As per the above code, the inner function(i.e, greetingInfo) has access to the variables in the outer function scope(i.e, Welcome) even after the outer function has returned.

---


### What is memoization?

Memoization is a functional programming technique which attempts to increase a function’s performance by caching its previously computed results. Each time a memoized function is called, its parameters are used to index the cache. If the data is present, then it can be returned, without executing the entire function. Otherwise the function is executed and then the result is added to the cache. Let's take an example of adding function with memoization,

```js
const memoizeAddition = () => {
  let cache = {};
  return (value) => {
    if (value in cache) {
      console.log("Fetching from cache");
      return cache[value]; // Here, cache.value cannot be used as property name starts with the number which is not a valid JavaScript  identifier. Hence, can only be accessed using the square bracket notation.
    } else {
      console.log("Calculating result");
      let result = value + 20;
      cache[value] = result;
      return result;
    }
  };
};
// returned function from memoizeAddition
const addition = memoizeAddition();
console.log(addition(20)); //output: 40 calculated
console.log(addition(20)); //output: 40 cached
```

---

### What is a callback function?

A callback function is a function passed into another function as an argument. This function is invoked inside the outer function to complete an action. Let's take a simple example of how to use callback function

```js
function callbackFunction(name) {
  console.log("Hello " + name);
}

function outerFunction(callback) {
  let name = prompt("Please enter your name.");
  callback(name);
}

outerFunction(callbackFunction);
```

---

### Why do we need callbacks?

The callbacks are needed because javascript is an event driven language. That means instead of waiting for a response, javascript will keep executing while listening for other events. Let's take an example with the first function invoking an API call(simulated by setTimeout) and the next function which logs the message.

```js
function firstFunction() {
  // Simulate a code delay
  setTimeout(function () {
    console.log("First function called");
  }, 1000);
}
function secondFunction() {
  console.log("Second function called");
}
firstFunction();
secondFunction();

// Output:
// Second function called
// First function called
```

---

### What is a callback hell?

Callback Hell is an anti-pattern with multiple nested callbacks which makes code hard to read and debug when dealing with asynchronous logic. The callback hell looks like below,

```js
async1(function(){
    async2(function(){
        async3(function(){
            async4(function(){
                ....
            });
        });
    });
});
```

---

### What is callback in callback?

You can nest one callback inside in another callback to execute the actions sequentially one by one. This is known as callbacks in callbacks. Beware, too many levels of nesting lead to Callback hell

```js
loadScript("/script1.js", function (script) {
  console.log("first script is loaded");

  loadScript("/script2.js", function (script) {
    console.log("second script is loaded");

    loadScript("/script3.js", function (script) {
      console.log("third script is loaded");
      // after all scripts are loaded
    });
  });
});
```

---

### Can we define properties for functions?
Yes, we can define properties for functions because functions are also objects.

```js
fn = function (x) {
  //Function code goes here
};

fn.name = "John";

fn.profile = function (y) {
  //Profile code goes here
};
```

---

### What is a polyfill?
A polyfill is a piece of JS code used to provide modern functionality on older browsers that do not natively support it. For example, Silverlight plugin polyfill can be used to mimic the functionality of an HTML Canvas element on Microsoft Internet Explorer 7.

There are two main polyfill libraries available,

- Core.js: It is a modular javascript library used for cutting-edge ECMAScript features.
- Polyfill.io: It provides polyfills that are required for browser needs.

---

### What is a rest parameter?
Rest parameter is an improved way to handle function parameters which allows us to represent an indefinite number of arguments as an array. The syntax would be as below,

```js
function f(a, b, ...theArgs) {
  // ...
}
```

For example, let's take a sum example to calculate on dynamic number of parameters,

```js
function sum(...args) {
  let total = 0;
  for (const i of args) {
    total += i;
  }
  return total;
}

console.log(sum(1, 2)); //3
console.log(sum(1, 2, 3)); //6
console.log(sum(1, 2, 3, 4)); //10
console.log(sum(1, 2, 3, 4, 5)); //15
```

**Note**: Rest parameter is added in ES2015 or ES6

---

### What is a spread operator?

Spread operator allows iterables( arrays / objects / strings ) to be expanded into single arguments/elements. Let's take an example to see this behavior,

```js
function calculateSum(x, y, z) {
  return x + y + z;
}

const numbers = [1, 2, 3];

console.log(calculateSum(...numbers)); // 6
```

---

### What is a decorator?
A decorator is an expression that evaluates to a function and that takes the target, name, and decorator descriptor as arguments. Also, it optionally returns a decorator descriptor to install on the target object. Let's define admin decorator for user class at design time,

```js
function admin(isAdmin) {
   return function(target) {
       target.isAdmin = isAdmin;
   }
}

@admin(true)
class User() {
}
console.log(User.isAdmin); //true

 @admin(false)
 class User() {
 }
 console.log(User.isAdmin); //false
```

---


### What are the different kinds of generators?
There are five kinds of generators,

1. Generator function declaration:

```js
function* myGenFunc() {
  yield 1;
  yield 2;
  yield 3;
}
const genObj = myGenFunc();
```
2. Generator function expressions:

```js
const myGenFunc = function* () {
  yield 1;
  yield 2;
  yield 3;
};
const genObj = myGenFunc();
```
3. Generator method definitions in object literals:

```js
const myObj = {
  *myGeneratorMethod() {
    yield 1;
    yield 2;
    yield 3;
  },
};
const genObj = myObj.myGeneratorMethod();
```

4. Generator method definitions in class:

```js
class MyClass {
  *myGeneratorMethod() {
    yield 1;
    yield 2;
    yield 3;
  }
}
const myObject = new MyClass();
const genObj = myObject.myGeneratorMethod();
```

5. Generator as a computed property:

```js
const SomeObj = {
  *[Symbol.iterator]() {
    yield 1;
    yield 2;
    yield 3;
  },
};

console.log(Array.from(SomeObj)); // [ 1, 2, 3 ]
```

---

## Objects and Prototypes

### What is a constructor method?
The constructor method is a special method for creating and initializing an object created within a class. If you do not specify a constructor method, a default constructor is used. The example usage of constructor would be as below,

```js
class Employee {
  constructor() {
    this.name = "John";
  }
}

var employeeObject = new Employee();

console.log(employeeObject.name); // John
```

---


### How do you call the constructor of a parent class?
You can use the super keyword to call the constructor of a parent class. Remember that super() must be called before using 'this' reference. Otherwise it will cause a reference error. Let's the usage of it,

```js
class Square extends Rectangle {
  constructor(length) {
    super(length, length);
    this.name = "Square";
  }

  get area() {
    return this.width * this.height;
  }

  set area(value) {
    this.area = value;
  }
}
```
---


### What are the possible ways to create objects in JavaScript?

There are many ways to create objects in javascript as mentioned below:

1. **Object literal syntax**:  

The object literal syntax (or object initializer), is a comma-separated set of name-value pairs wrapped in curly braces.

```js
var object = {
     name: "John",
     age: 33
};
```  
Object literal property values can be of any data type, including array, function, and nested object.

2. **Object constructor**:  

The simplest way to create an empty object is using the `Object` constructor.
```js
var object = new Object();
```
The `Object()` is a built-in constructor function so "new" keyword is not required. The above code snippet can be re-written as:
```js
var object = Object();
```

3. **Object's create method**:  

The `create` method of Object is used to create a new object by passing the specified prototype object and properties  
as arguments, i.e., this pattern is helpful to create new objects based on existing objects. The second argument is  
optional and it is used to create properties on a newly created object.  

The following code creates a new empty object whose prototype is null.
```js
var object = Object.create(null);
```

The following example creates an object along with additional new properties.
```js
let vehicle = {
  wheels: '4',
  fuelType: 'Gasoline',
  color: 'Green'
}
let carProps = {
  type: {
    value: 'Volkswagen'
  },
  model: {
    value: 'Golf'
  }
}

var car = Object.create(vehicle, carProps);
console.log(car);
```

4. **Function constructor**:  

In this approach, create any function and apply the new operator to create object instances.

```js
function Person(name) {
  this.name = name;
  this.age = 21;
}
var object = new Person("John");
```

5. **Function constructor with prototype**:  

This is similar to function constructor but it uses prototype for their properties and methods,
```js
function Person() {}
Person.prototype.name = "John";
var object = new Person();
```

This is equivalent to creating an instance with Object.create method with a function prototype and then calling  
that function with an instance and parameters as arguments.

```js
function func() {}

new func(x, y, z);
```

OR

```js
// Create a new instance using function prototype.
var newInstance = Object.create(func.prototype)

// Call the function
var result = func.call(newInstance, x, y, z),

// If the result is a non-null object then use it otherwise just use the new instance.
console.log(result && typeof result === 'object' ? result : newInstance);
```

6. **Object's assign method**:

The `Object.assign` method is used to copy all the properties from one or more source objects and stores them  
into a target object.

The following code creates a new staff object by copying properties of his working company and the car he owns.

```js
const orgObject = { company: 'XYZ Corp'};
const carObject = { name: 'Toyota'};
const staff = Object.assign({}, orgObject, carObject);
```

7. **ES6 Class syntax**:  

ES6 introduces class feature to create objects.

```js
class Person {
  constructor(name) {
    this.name = name;
  }
}

var object = new Person("John");
```

8. **Singleton pattern**":

A Singleton is an object which can only be instantiated one time. Repeated calls to its constructor return  
the same instance. This way one can ensure that they don't accidentally create multiple instances.

```js
var object = new (function () {
  this.name = "John";
})();
```

---


### What is a prototype chain?

**Prototype chaining** is used to build new types of objects based on existing ones. It is similar to inheritance in  
a class based language. i.e, When you create an object using a constructor function or a class, the created   
object inherits properties from a prototype object.

The prototype on object instance is available through **Object.getPrototypeOf(object)** or `__proto__` property  
whereas prototype on constructor function is available through **Object.prototype**.

![prototype-chain](images/prototype_chain.png)

---

### How do you compare Object and Map?

**Objects** are similar to **Maps** in that both let you set keys to values, retrieve those values, delete keys, and detect whether something is stored at a key. Due to this reason, Objects have been used as Maps historically. But there are important differences that make using a Map preferable in certain cases:

1. The keys of an Object can be Strings and Symbols, whereas they can be any value for a Map, including functions, objects, and any primitive type.

2. The keys in a Map are ordered while keys added to Object are not. Thus, when iterating over it, a Map object returns keys in the order of insertion.

3. You can get the size of a Map easily with the size property, while the number of properties in an Object must be determined manually.

4. A Map is an iterable and can thus be directly iterated, whereas iterating over an Object requires obtaining its keys in some fashion and iterating over them.

5. An Object has a prototype, so there are default keys in an object that could collide with your keys if you're not careful. As of ES5 this can be bypassed by creating an object(which can be called a map) using `Object.create(null)`, but this practice is seldom done.

6. A Map may perform better in scenarios involving frequent addition and removal of key pairs.

---


### What is the difference between native, host and user objects? 

`Native objects` are objects that are part of the JavaScript language defined by the ECMAScript specification. For example, String, Math, RegExp, Object, Function etc core objects defined in the ECMAScript spec. `Host objects` are objects provided by the browser or runtime environment (Node).

For example, window, XmlHttpRequest, DOM nodes etc are considered as host objects. `User objects` are objects defined in the javascript code. For example, User objects created for profile information.

---

### How do you test for an empty object?
There are different solutions based on ECMAScript versions

1. Using **Object entries**(ECMA 7+): You can use object entries length along with constructor type.

```js
Object.entries(obj).length === 0 && obj.constructor === Object; // Since date object length is 0, you need to check constructor check as well
```

2. Using **Object keys**(ECMA 5+): You can use object keys length along with constructor type.
```js
Object.keys(obj).length === 0 && obj.constructor === Object; // Since date object length is 0, you need to check constructor check as well
```
3. Using **for-in with hasOwnProperty**(Pre-ECMA 5): You can use a for-in loop along with hasOwnProperty.
```js
function isEmpty(obj) {
  for (var prop in obj) {
    if (obj.hasOwnProperty(prop)) {
      return false;
    }
  }

  return JSON.stringify(obj) === JSON.stringify({});
}
```

---

### What is an arguments object?
The arguments object is an Array-like object accessible inside functions that contains the values of the arguments passed to that function. For example, let's see how to use arguments object inside sum function,
```js
function sum() {
  var total = 0;
  for (var i = 0, len = arguments.length; i < len; ++i) {
    total += arguments[i];
  }
  return total;
}

sum(1, 2, 3); // returns 6
```
**Note**: You can't apply array methods on arguments object. But you can convert into a regular array as below.

```js
var argsArray = Array.prototype.slice.call(arguments);
```

---

### What is the difference between proto and prototype?

The `__proto__` object is the actual object that is used in the lookup chain to resolve methods, etc. Whereas `prototype` is the object that is used to build `__proto__` when you create an object with new.

```js
new Employee().__proto__ === Employee.prototype;
new Employee().prototype === undefined;
```

There are few more differences,

| feature    | Prototype                                                    | proto                                                      |
| ---------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| Access     | All the function constructors have prototype properties.     | All the objects have \_\_proto\_\_ property                |
| Purpose    | Used to reduce memory wastage with a single copy of function | Used in lookup chain to resolve methods, constructors etc. |
| ECMAScript | Introduced in ES6                                            | Introduced in ES5                                          |
| Usage      | Frequently used                                              | Rarely used                                                |

---

### What is a freeze method?
The `freeze()` method is used to freeze an object. Freezing an object does not allow adding new properties to an object, prevents removing, and prevents changing the enumerability, configurability, or writability of existing properties. i.e. It returns the passed object and does not create a frozen copy.

```js
const obj = {
  prop: 100,
};

Object.freeze(obj);
obj.prop = 200; // Throws an error in strict mode

console.log(obj.prop); //100
```

Remember freezing is only applied to the top-level properties in objects but not for nested objects. For example, let's try to freeze user object which has employment details as nested object and observe that details have been changed.

```js
const user = {
  name: "John",
  employment: {
    department: "IT",
  },
};

Object.freeze(user);
user.employment.department = "HR";
```
**Note**: It causes a TypeError if the argument passed is not an object.

---

### What is the purpose of freeze method?
Below are the main benefits of using freeze method,

- It is used for freezing objects and arrays.
- It is used to make an object immutable.

---

### How do you determine two values same or not using object?
The Object.is() method determines whether two values are the same value. For example, the usage with different types of values would be,

```js
Object.is("hello", "hello"); // true
Object.is(window, window); // true
Object.is([], []); // false
```

Two values are the same if one of the following holds:

- both undefined
- both null
- both true or both false
- both strings of the same length with the same characters in the same order
- both the same object (means both object have same reference)
- both numbers and both +0 both -0 both NaN both non-zero and both not NaN and both have the same value.

---

### How do you copy properties from one object to other
You can use the Object.assign() method which is used to copy the values and properties from one or more source objects to a target object. It returns the target object which has properties and values copied from the source objects. The syntax would be as below,

```js
Object.assign(target, ...sources);
```
Let's take example with one source and one target object,

```js
const target = { a: 1, b: 2 };
const source = { b: 3, c: 4 };

const returnedTarget = Object.assign(target, source);

console.log(target); // { a: 1, b: 3, c: 4 }

console.log(returnedTarget); // { a: 1, b: 3, c: 4 }
```

As observed in the above code, there is a common property(b) from source to target so it's value has been overwritten.

---

### What are the applications of assign method?
Below are the some of main applications of Object.assign() method,

- It is used for cloning an object.
- It is used to merge objects with the same properties.

---

### What is a proxy object
The Proxy object is used to define custom behavior for fundamental operations such as property lookup, assignment, enumeration, function invocation, etc.

A proxy is created with two parameters: a target object which you want to proxy and a handler object which contains methods to intercept fundamental operations. The syntax would be as follows,

```js
var p = new Proxy(target, handler);
```

Let's take a look at below examples of proxy object and how the get method which customize the lookup behavior,

```js
 //Example1:

   const person = {
     name: 'Sudheer Jonna',
     age: 35
   };

 const handler = {
   get(target, prop) {
     if (prop === 'name') {
       return 'Mr. ' + target[prop];
     }
     return target[prop];
   }
 };

 const proxy = new Proxy(person, handler);

 //Example2: 

 var handler1 = {
   get: function (obj, prop) {
     return prop in obj ? obj[prop] : 100;
   },
 };

 var p = new Proxy({}, handler1);
 p.a = 10;
 p.b = null;

 console.log(p.a, p.b); // 10, null
 console.log("c" in p, p.c); // false, 100
```

In the above code, it uses `get` handler which define the behavior of the proxy when an operation is performed on it. These proxies are mainly used for some of the below cross-cutting concerns.

- Logging
- Authentication or Authorization
- Data binding and observables
- Function parameter validation

**Note**: This is a new feature in ES6.

---

### What is the purpose of seal method?
The `Object.seal()` method is used to seal an object, by preventing new properties from being added to it and marking all existing properties as non-configurable. But values of present properties can still be changed as long as they are writable. The next level of immutability would be the `Object.freeze()` method. Let's see the below example to understand more about seal() method

```js
const object = {
  property: "Welcome JS world",
};
Object.seal(object);
object.property = "Welcome to object world";
console.log(Object.isSealed(object)); // true
delete object.property; // You cannot delete when sealed
console.log(object.property); //Welcome to object world
```

---

### What are the applications of seal method?
Below are the main applications of Object.seal() method,

- It is used for sealing objects and arrays.
- It is used to make properties of an object non-configurable.

---

### How do you get enumerable key and value pairs?
The Object.entries() method is used to return an array of a given object's own enumerable string-keyed property [key, value] pairs, in the same order as that provided by a for...in loop. Let's see the functionality of object.entries() method in an example,

```js
const object = {
  a: "Good morning",
  b: 100,
};

for (let [key, value] of Object.entries(object)) {
  console.log(`${key}: ${value}`); // a: 'Good morning'
  // b: 100
}
```

---

### What is the main difference between Object.values and Object.entries method?
The Object.values() method's behavior is similar to Object.entries() method but it returns an array of values instead [key,value] pairs.

```js
const object = {
  a: "Good morning",
  b: 100,
};

for (let value of Object.values(object)) {
  console.log(`${value}`); // 'Good morning \n100'
}
```

---

### How can you get the list of keys of any object?
You can use the Object.keys() method which is used to return an array of a given object's own property names, in the same order as we get with a normal loop. For example, you can get the keys of a user object,

```js
const user = {
  name: "John",
  gender: "male",
  age: 40,
};

console.log(Object.keys(user)); //['name', 'gender', 'age']
```

---

### How do you create an object with prototype?
The Object.create() method is used to create a new object with the specified prototype object and properties. i.e, It uses an existing object as the prototype of the newly created object. It returns a new object with the specified prototype object and properties.

```js
const user = {
  name: "John",
  printInfo: function () {
    console.log(`My name is ${this.name}.`);
  },
};

const admin = Object.create(user);

admin.name = "Nick"; // Remember that "name" is a property set on "admin" but not on "user" object

admin.printInfo(); // My name is Nick
```

---

### How do you define property on Object constructor?
The Object.defineProperty() static method is used to define a new property directly on an object, or modify an existing property on an object, and returns the object. Let's see an example to know how to define property,

```js
const newObject = {};

Object.defineProperty(newObject, "newProperty", {
  value: 100,
  writable: false,
});

console.log(newObject.newProperty); // 100

newObject.newProperty = 200; // It throws an error in strict mode due to writable setting

```

---

### What is the difference between get and defineProperty?
Both have similar results unless you use classes. If you use `get` the property will be defined on the prototype of the object whereas using `Object.defineProperty()` the property will be defined on the instance it is applied to.

---

### What are the advantages of Getters and Setters?
Below are the list of benefits of Getters and Setters,

- They provide simpler syntax
- They are used for defining computed properties, or accessors in JS.
- Useful to provide equivalence relation between properties and methods
- They can provide better data quality
- Useful for doing things behind the scenes with the encapsulated logic.

---

### Can I add getters and setters using defineProperty method?
Yes, You can use the `Object.defineProperty()` method to add Getters and Setters. For example, the below counter object uses increment, decrement, add and subtract properties,

```js
var obj = { counter: 0 };

// Define getters
Object.defineProperty(obj, "increment", {
  get: function () {
    this.counter++;
    return this.counter;
  },
});
Object.defineProperty(obj, "decrement", {
  get: function () {
    this.counter--;
    return this.counter;
  },
});

// Define setters
Object.defineProperty(obj, "add", {
  set: function (value) {
    this.counter += value;
  },
});
Object.defineProperty(obj, "subtract", {
  set: function (value) {
    this.counter -= value;
  },
});

obj.add = 10;
obj.subtract = 5;
console.log(obj.increment); //6
console.log(obj.decrement); //5
```

---

### What are the different ways to access object properties?
There are 3 possible ways for accessing the property of an object.

1. Dot notation: It uses dot for accessing the properties
```js
objectName.property;
```
2. Square brackets notation: It uses square brackets for property access
```js
objectName["property"];
```
3. Expression notation: It uses expression in the square brackets
```js
objectName[expression];
```
---

### What is an error object?
An error object is a built in error object that provides error information when an error occurs. It has two properties: name and message. For example, the below function logs error details,

```js
try {
  greeting("Welcome");
} catch (err) {
  console.log(err.name + "<br>" + err.message);
} 
```
---

### What are the different error names from error object?

There are 7 different types of error names returned from error object,
| Error Name     | Description                                        |
| -------------- | -------------------------------------------------- |
| AggregateError | An error indicating that multiple errors occurred  |
| EvalError      | An error has occurred in the eval() function       |
| RangeError     | An error has occurred with a number "out of range" |
| ReferenceError | An error due to an illegal reference               |
| SyntaxError    | An error due to a syntax error                     |
| TypeError      | An error due to a type error                       |
| URIError       | An error due to encodeURI()                        |

---

### How do you get property descriptors of an object
You can use the `Object.getOwnPropertyDescriptors()` method which returns all own property descriptors of a given object. The example usage of this method is below,

```js
const newObject = {
  a: 1,
  b: 2,
  c: 3,
};
const descriptorsObject = Object.getOwnPropertyDescriptors(newObject);
console.log(descriptorsObject.a.writable); //true
console.log(descriptorsObject.a.configurable); //true
console.log(descriptorsObject.a.enumerable); //true
console.log(descriptorsObject.a.value); // 1
```

---

### How do you extend classes?
The extends keyword is used in class declarations/expressions to create a class which is a child of another class. It can be used to subclass custom classes as well as built-in objects. The syntax would be as below,

```js
class ChildClass extends ParentClass { ... }
```
Let's take an example of Square subclass from Polygon parent class,

```js
class Square extends Rectangle {
  constructor(length) {
    super(length, length);
    this.name = "Square";
  }

  get area() {
    return this.width * this.height;
  }

  set area(value) {
    this.area = value;
  }
}

```
---


### Does javascript uses mixins?
Mixin is a generic object-oriented programming term - is a class containing methods that can be used by other classes without a need to inherit from it. In JavaScript we can only inherit from a single object. ie. There can be only one `[[prototype]]` for an object.

But sometimes we require to extend more than one, to overcome this we can use Mixin which helps to copy methods to the prototype of another class.

Say for instance, we've two classes `User` and `CleanRoom`. Suppose we need to add `CleanRoom` functionality to `User`, so that user can clean the room at demand. Here's where concept called mixins comes into picture.

```js
// mixin
let cleanRoomMixin = {
  cleanRoom() {
    alert(`Hello ${this.name}, your room is clean now`);
  },
  sayBye() {
    alert(`Bye ${this.name}`);
  },
};

// usage:
class User {
  constructor(name) {
    this.name = name;
  }
}

// copy the methods
Object.assign(User.prototype, cleanRoomMixin);

// now User can clean the room
new User("Dude").cleanRoom(); // Hello Dude, your room is clean now!

```

---

### How do you define instance and non-instance properties?
The Instance properties must be defined inside of class methods. For example, name and age properties defined inside constructor as below,

```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}
```
But Static(class) and prototype data properties must be defined outside of the ClassBody declaration. Let's assign the age value for Person class as below,


```js
Person.staticAge = 30;
Person.prototype.prototypeAge = 40;
```

---


## Collections

### What is the purpose of the array slice method?

The **slice()** method returns the selected elements in an array as a new array object. It selects the elements starting at the given start argument, and ends at the given optional end argument without including the last element. If you omit the second argument then it selects till the end of the array. This method can also accept negative index which counts back from the end of the array.

Some of the examples of this method are,
```js
let arrayIntegers = [1, 2, 3, 4, 5];
let arrayIntegers1 = arrayIntegers.slice(0, 2); // returns [1,2]
let arrayIntegers2 = arrayIntegers.slice(2, 3); // returns [3]
let arrayIntegers3 = arrayIntegers.slice(4); //returns [5]
let arrayIntegers4 = arrayIntegers.slice(-3, -1); //returns [3, 4]
```

**Note**: Slice method doesn't mutate the original array but it returns the subset as a new array.

---




### What is the purpose of the array splice method?

The **splice()** method adds/removes items to/from an array, and then returns the removed item. The first argument specifies the array position/index for insertion or deletion whereas the optional second argument indicates the number of elements to be deleted. Each additional argument is added to the array.

Some of the examples of this method are:

```js
let arrayIntegersOriginal1 = [1, 2, 3, 4, 5];
let arrayIntegersOriginal2 = [1, 2, 3, 4, 5];
let arrayIntegersOriginal3 = [1, 2, 3, 4, 5];

let arrayIntegers1 = arrayIntegersOriginal1.splice(0, 2); // returns [1, 2]; original array: [3, 4, 5]
let arrayIntegers2 = arrayIntegersOriginal2.splice(3); // returns [4, 5]; original array: [1, 2, 3]
let arrayIntegers3 = arrayIntegersOriginal3.splice(3, 1, "a", "b", "c"); //returns [4]; original array: [1, 2, 3, "a", "b", "c", 5]
```
**Note:** Splice method modifies the original array and returns the deleted array.

---

### What is the difference between slice and splice?

Some of the major differences in a tabular form:
| Slice                                        | Splice                                       |
| -------------------------------------------- | -------------------------------------------- |
| Doesn't modify the original array(immutable) | Modifies the original array(mutable)         |
| Returns the subset of original array         | Returns the deleted elements as array        |
| Used to pick the elements from array         | Used to insert/delete elements to/from array |

---

### What is a WeakSet?
WeakSet is used to store a collection of weakly(weak references) held objects. The syntax would be as follows,

```js
new WeakSet([iterable]);
```

Let's see the below example to explain it's behavior,

```js
var ws = new WeakSet();
var user = {};
ws.add(user);
ws.has(user); // true
ws.delete(user); // removes user from the set
ws.has(user); // false, user has been removed
```

---

### What are the differences between WeakSet and Set?
The main difference is that references to objects in Set are strong while references to objects in WeakSet are weak. i.e, An object in WeakSet can be garbage collected if there is no other reference to it. Other differences are,

- Sets can store any value Whereas WeakSets can store only collections of objects
- WeakSet does not have size property unlike Set
- WeakSet does not have methods such as clear, keys, values, entries, forEach.
- WeakSet is not iterable.

---

### What is a WeakMap?
The WeakMap object is a collection of key/value pairs in which the keys are weakly referenced. In this case, keys must be objects and the values can be arbitrary values. The syntax looks like the following:

```js
new WeakMap([iterable]);
```
Let's see the below example to explain it's behavior,

```js
var ws = new WeakMap();
var user = {};
ws.set(user);
ws.has(user); // true
ws.delete(user); // removes user from the map
ws.has(user); // false, user has been removed
```

---

### What are the differences between WeakMap and Map?
The main difference is that references to key objects in Map are strong while references to key objects in WeakMap are weak. i.e, A key object in WeakMap can be garbage collected if there is no other reference to it. Other differences are,

- Maps can store any key type Whereas WeakMaps can store only collections of key objects
- WeakMap does not have size property unlike Map
- WeakMap does not have methods such as clear, keys, values, entries, forEach.
- WeakMap is not iterable. 

---

### How do you compare scalar arrays?
You can use length and every method of arrays to compare two scalar(compared directly using ===) arrays. The combination of these expressions can give the expected result,

```js
const arrayFirst = [1, 2, 3, 4, 5];
const arraySecond = [1, 2, 3, 4, 5];
console.log(
  arrayFirst.length === arraySecond.length &&
    arrayFirst.every((value, index) => value === arraySecond[index])
); // true
```
If you would like to compare arrays irrespective of order then you should sort them before,

```js
const arrayFirst = [2, 3, 1, 4, 5];
const arraySecond = [1, 2, 3, 4, 5];
console.log(
  arrayFirst.length === arraySecond.length &&
    arrayFirst.sort().every((value, index) => value === arraySecond[index])
); //true
```

---

### What is the difference between dense and sparse arrays?
An array contains items at each index starting from first(0) to last(array.length - 1) is called as Dense array. Whereas if at least one item is missing at any index, the array is called as sparse.

Let's see the below two kind of arrays,

```js
const avengers = ["Ironman", "Hulk", "CaptainAmerica"];
console.log(avengers[0]); // 'Ironman'
console.log(avengers[1]); // 'Hulk'
console.log(avengers[2]); // 'CaptainAmerica'
console.log(avengers.length); // 3

const justiceLeague = ["Superman", "Aquaman", , "Batman"];
console.log(justiceLeague[0]); // 'Superman'
console.log(justiceLeague[1]); // 'Aquaman'
console.log(justiceLeague[2]); // undefined
console.log(justiceLeague[3]); // 'Batman'
console.log(justiceLeague.length); // 4 
```

---

### What are the different ways to create sparse arrays?
There are 4 different ways to create sparse arrays in JavaScript

1. **Array literal**: Omit a value when using the array literal
```js
const justiceLeague = ["Superman", "Aquaman", , "Batman"];
console.log(justiceLeague); // ['Superman', 'Aquaman', empty ,'Batman']
```
2. **Array() constructor**: Invoking Array(length) or new Array(length)
```js
const array = Array(3);
console.log(array); // [empty, empty ,empty]
```
3. **Delete operator**: Using delete array[index] operator on the array
```js
const justiceLeague = ["Superman", "Aquaman", "Batman"];
delete justiceLeague[1];
console.log(justiceLeague); // ['Superman', empty, ,'Batman']
```
4. **Increase length property**: Increasing length property of an array
```js
const justiceLeague = ["Superman", "Aquaman", "Batman"];
justiceLeague.length = 5;
console.log(justiceLeague); // ['Superman', 'Aquaman', 'Batman', empty, empty]
```

---

## Asynchronous JavaScript

### What is a promise?
A promise is an object that may produce a single value some time in the future with either a resolved value or a reason that it’s not resolved (i.e. rejected, that means for example, due to a network error). It will be in one of the 3 possible states: fulfilled, rejected, or pending.

The syntax of Promise creation looks like below,
```js
const promise = new Promise(function (resolve, reject) {
  // promise description
});
```
The usage of a promise would be as below,
```js
const promise = new Promise(
  (resolve) => {
    setTimeout(() => {
      resolve("I'm a Promise!");
    }, 5000);
  },
  (reject) => {}
);

promise.then((value) => console.log(value));
```
The action flow of a promise will be as below,
![Promises](images/promises.png)

---

### Why do you need a promise?
Promises are used to handle asynchronous operations. They provide an alternative approach for callbacks by reducing the callback hell and writing the cleaner code.

---

### What are the three states of promise?

Promises have three states:

- Pending: This is an initial state of the Promise before an operation begins
- Fulfilled: This state indicates that the specified operation was completed.
- Rejected: This state indicates that the operation did not complete. In this case an error value will be thrown.

---

### What are the main rules of promise?
A promise must follow a specific set of rules:

- A promise is an object that supplies a standard-compliant .then() method
- A pending promise may transition into either fulfilled or rejected state
- A fulfilled or rejected promise is settled and it must not transition into any other state.
Once a promise is settled, the value must not change.

---

### What is promise chaining?

The process of executing a sequence of asynchronous tasks one after another using promises is known as Promise chaining. Let's take an example of promise chaining for calculating the final result,

```js
new Promise(function (resolve, reject) {
  setTimeout(() => resolve(1), 1000);
})
  .then(function (result) {
    console.log(result); // 1
    return result * 2;
  })
  .then(function (result) {
    console.log(result); // 2
    return result * 3;
  })
  .then(function (result) {
    console.log(result); // 6
    return result * 4;
  });
```

In the above handlers, the result is passed to the chain of `.then()` handlers with the below work flow,

- The initial promise resolves in 1 second,
- After that `.then` handler is called by logging the result(1) and then return a promise with the value of result * 2.
- After that the value passed to the next `.then` handler by logging the result(2) and return a promise with result * 3.
- Finally the value passed to the last `.then` handler by logging the result(6) and return a promise with result * 4.

---


### What is promise.all?

Promise.all is a promise that takes an array of promises as an input (an iterable), and it gets resolved when all the promises get resolved or any one of them gets rejected. For example, the syntax of promise.all method is below,

```js
Promise.all([Promise1, Promise2, Promise3]) .then(result) => {   console.log(result) }) .catch(error => console.log(`Error in promises ${error}`))
```

**Note**: Remember that the order of the promises(output the result) is maintained as per input order.

---

### What is the purpose of the race method in promise?

Promise.race() method will return the promise instance which is firstly resolved or rejected. Let's take an example of race() method where promise2 is resolved first

```js
var promise1 = new Promise(function (resolve, reject) {
  setTimeout(resolve, 500, "one");
});
var promise2 = new Promise(function (resolve, reject) {
  setTimeout(resolve, 100, "two");
});

Promise.race([promise1, promise2]).then(function (value) {
  console.log(value); // "two" // Both promises will resolve, but promise2 is faster
});
```

---

### What are the pros and cons of promises over callbacks?
Below are the list of pros and cons of promises over callbacks,

**Pros**:

- It avoids callback hell which is unreadable
- Easy to write sequential asynchronous code with .then()
- Easy to write parallel asynchronous code with Promise.all()
- Solves some of the common problems of callbacks(call the callback too late, too early, many times and swallow errors/exceptions)

**Cons**:

- It makes little complex code
- You need to load a polyfill if ES6 is not supported 


---

### What is the use of setTimeout?
The setTimeout() method is used to call a function or evaluate an expression after a specified number of milliseconds. For example, let's log a message after 2 seconds using setTimeout method,

```js
setTimeout(function () {
  console.log("Good morning");
}, 2000);
```

---

### What is the use of setInterval?
The setInterval() method is used to call a function or evaluate an expression at specified intervals (in milliseconds). For example, let's log a message after 2 seconds using setInterval method,

```js
setInterval(function () {
  console.log("Good morning");
}, 2000);
```

---

### What is the purpose of clearTimeout method?
The clearTimeout() function is used in javascript to clear the timeout which has been set by setTimeout()function before that. i.e, The return value of setTimeout() function is stored in a variable and it’s passed into the clearTimeout() function to clear the timer.

For example, the below setTimeout method is used to display the message after 3 seconds. This timeout can be cleared by the clearTimeout() method.

```js
var msg;
function greeting() {
  alert('Good morning');
}
function start() {
  msg =setTimeout(greeting, 3000);

}

function stop() {
    clearTimeout(msg);
}
```

---

### What is the purpose of clearInterval method?
The clearInterval() function is used in javascript to clear the interval which has been set by setInterval() function. i.e, The return value returned by setInterval() function is stored in a variable and it’s passed into the clearInterval() function to clear the interval.

For example, the below setInterval method is used to display the message for every 3 seconds. This interval can be cleared by the clearInterval() method.

```js
var msg;
function greeting() {
  alert('Good morning');
}
function start() {
  msg = setInterval(greeting, 3000);

}

function stop() {
    clearInterval(msg);
}
```

---

### What is an async function?
An async function is a function declared with the async keyword which enables asynchronous, promise-based behavior to be written in a cleaner style by avoiding promise chains. These functions can contain zero or more await expressions.

Let's take a below async function example,

```js
async function logger() {
  let data = await fetch("http://someapi.com/users"); // pause until fetch returns
  console.log(data);
}
logger();
```
It is basically syntax sugar over ES2015 promises and generators. 

---

### What is the event loop in JavaScript runtimes?

<!-- Update here: /questions/what-is-event-loop-what-is-the-difference-between-call-stack-and-task-queue/en-US.mdx -->

The event loop is concept within the JavaScript runtime environment regarding how asynchronous operations are executed within JavaScript engines. It works as such:

1. The JavaScript engine starts executing scripts, placing synchronous operations on the call stack.
2. When an asynchronous operation is encountered (e.g., `setTimeout()`, HTTP request), it is offloaded to the respective Web API or Node.js API to handle the operation in the background.
3. Once the asynchronous operation completes, its callback function is placed in the respective queues – task queues (also known as macrotask queues / callback queues) or microtask queues. We will refer to "task queue" as "macrotask queue" from here on to better differentiate from the microtask queue.
4. The event loop continuously monitors the call stack and executes items on the call stack. If/when the call stack is empty:
   1. Microtask queue is processed. Microtasks include promise callbacks (`then`, `catch`, `finally`), `MutationObserver` callbacks, and calls to `queueMicrotask()`. The event loop takes the first callback from the microtask queue and pushes it to the call stack for execution. This repeats until the microtask queue is empty.
   2. Macrotask queue is processed. Macrotasks include web APIs like `setTimeout()`, HTTP requests, user interface event handlers like clicks, scrolls, etc. The event loop dequeues the first callback from the macrotask queue and pushes it onto the call stack for execution. However, after a macrotask queue callback is processed, the event loop does not proceed with the next macrotask yet! The event loop first checks the microtask queue. Checking the microtask queue is necessary as microtasks have higher priority than macrotask queue callbacks. The macrotask queue callback that was just executed could have added more microtasks!
      1. If the microtask queue is non-empty, process them as per the previous step.
      2. If the microtask queue is empty, the next macrotask queue callback is processed. This repeats until the macrotask queue is empty.
5. This process continues indefinitely, allowing the JavaScript engine to handle both synchronous and asynchronous operations efficiently without blocking the call stack.

The unfortunate truth is that it is extremely hard to explain the event loop well using only text. We recommend checking out one of the following excellent videos explaining the event loop:

- [JavaScript Visualized - Event Loop, Web APIs, (Micro)task Queue](https://www.youtube.com/watch?v=eiC58R16hb8) (2024): Lydia Hallie is a popular educator on JavaScript and this is the best recent videos explaining the event loop. There's also an [accompanying blog post](https://www.lydiahallie.com/blog/event-loop) for those who prefer detailed text-based explanations.
- [In the Loop](https://www.youtube.com/watch?v=cCOL7MC4Pl0) (2018): Jake Archibald previously from the Chrome team provides a visual demonstration of the event loop during JSConf 2018, accounting for different types of tasks.
- [What the heck is the event loop anyway?](https://www.youtube.com/watch?v=8aGhZQkoFbQ) (2014): Philip Robert's gave this epic talk at JSConf 2014 and it is one of the most viewed JavaScript videos on YouTube.

## References
   - https://github.com/sudheerj/javascript-interview-questions
   - https://github.com/yangshun/top-javascript-interview-questions
    
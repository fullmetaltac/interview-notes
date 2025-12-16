# Table of Contents
- [Table of Contents](#table-of-contents)
  - [Basics](#basics)
    - [What is TypeScript, and how does it differ from JavaScript?](#what-is-typescript-and-how-does-it-differ-from-javascript)
    - [What are data types available in TypeScript?](#what-are-data-types-available-in-typescript)
    - [What are the differences between var, let, and const?](#what-are-the-differences-between-var-let-and-const)
    - [What is any type?](#what-is-any-type)
    - [What are differences between unknown and any?](#what-are-differences-between-unknown-and-any)
    - [What are modules?](#what-are-modules)
    - [What is a decorator?](#what-is-a-decorator)
    - [What are property decorators?](#what-are-property-decorators)
    - [What are strict null checks?](#what-are-strict-null-checks)
    - [What are union types?](#what-are-union-types)
  - [OOP](#oop)
    - [What are classes in TypeScript?](#what-are-classes-in-typescript)
    - [How to call base class constructor?](#how-to-call-base-class-constructor)
    - [What are getters and setters?](#what-are-getters-and-setters)
    - [What are class constants?](#what-are-class-constants)
    - [What are interfaces in TypeScript?](#what-are-interfaces-in-typescript)
    - [What is the implements clause?](#what-is-the-implements-clause)
    - [What are generics?](#what-are-generics)
    - [What are enums?](#what-are-enums)
    - [What are access modifiers?](#what-are-access-modifiers)
    - [What is a namespace?](#what-is-a-namespace)
    - [What is optional chaining?](#what-is-optional-chaining)
    - [What is type compatibility?](#what-is-type-compatibility)
    - [What is the difference between type and interface?](#what-is-the-difference-between-type-and-interface)
    - [What is a discriminated union?](#what-is-a-discriminated-union)
    - [What are mapped types?](#what-are-mapped-types)
    - [What are conditional types?](#what-are-conditional-types)
    - [What are rest parameters and spread operators?](#what-are-rest-parameters-and-spread-operators)
    - [What is the keyof keyword?](#what-is-the-keyof-keyword)
    - [What are utility types like Partial, Readonly, and Record?](#what-are-utility-types-like-partial-readonly-and-record)
    - [What is never type?](#what-is-never-type)
  - [Setup](#setup)
    - [Basic setup](#basic-setup)
  - [References](#references)

## Basics

###  What is TypeScript, and how does it differ from JavaScript?
TypeScript is a **statically typed superset of JavaScript** that compiles down to plain JavaScript.

Key differences between TypeScript and JavaScript include:

- **Static Typing**: While JavaScript is dynamically typed, TypeScript uses static typing, which means that types are evaluated at compile-time instead of run-time. This can help catch potential bugs before the code is run
- **Interfaces and Classes**: TypeScript supports the latest JavaScript features, such as classes and interfaces, which are not available in some older JavaScript versions
- **Compile-time Errors**: The TypeScript compiler provides errors at compile-time, whereas JavaScript gives you an error at runtime. Early error-catching helps reduce the chance of running faulty code and speeds up bug-fixing
- **Tooling**: TypeScript has powerful tools for navigating code and automatic refactoring, which improves developer experience

---

### What are data types available in TypeScript?

TypeScript supports all JavaScript data types, plus its own static types for better safety and clarity.

**Basic Data Types:**  
 
| Type        | Description                        | Example                          |
| ----------- | ---------------------------------- | -------------------------------- |
| `number`    | All numbers (int, float, etc.)     | `let x: number = 42;`            |
| `string`    | Text                               | `let name: string = "Alice";`    |
| `boolean`   | True/false                         | `let isOn: boolean = true;`      |
| `null`      | Null value                         | `let n: null = null;`            |
| `undefined` | Undefined value                    | `let u: undefined = undefined;`  |
| `any`       | Any value (disables type checking) | `let val: any = 5;`              |
| `unknown`   | Unknown type (safer than `any`)    | `let data: unknown = "test";`    |
| `never`     | Never returns/occurs               | `function fail(): never { ... }` |
| `void`      | No return value                    | `function log(): void { ... }`   |


**Advanced/Custom Types:**

| Type                 | Description                              | Example                                  |
| -------------------- | ---------------------------------------- | ---------------------------------------- |
| `array`              | List of elements of same type            | `let nums: number[] = [1, 2, 3];`        |
| `tuple`              | Fixed-size, ordered array of types       | `let pair: [string, number] = ["A", 1];` |
| `enum`               | Named set of numeric or string constants | `enum Color { Red, Green }`              |
| `object`             | Non-primitive types                      | `let obj: object = { x: 10 };`           |
| `union`              | One of several types                     | `let id: string \| number;`              |
| `literal`            | Specific fixed value                     | `let status: "success" \| "error";`      |
| `type` / `interface` | Custom structured types                  | `type Person = { name: string }`         |
| `function`           | Functions with typed params/return       | `let fn: () => void;`                    |


---

### What are the differences between var, let, and const?

| Feature       | `var`                            | `let`                     | `const`                        |
| ------------- | -------------------------------- | ------------------------- | ------------------------------ |
| Scope         | Function-scoped                  | Block-scoped              | Block-scoped                   |
| Hoisting      | Yes (initialized as `undefined`) | Yes (but not initialized) | Yes (but not initialized)      |
| Reassignment  | ✅ Yes                            | ✅ Yes                     | ❌ No                           |
| Redeclaration | ✅ Yes                            | ❌ No                      | ❌ No                           |
| Use Case      | Legacy code                      | Variables that may change | Constants / immutable bindings |


---

### What is any type?

In TypeScript, the `any` type disables type checking for a variable — it can hold any value (string, number, object, etc.).

```ts
let data: any = "hello";
data = 42;
data = { key: "value" };
```
**Key Points**:  
- Use when the type is unknown or dynamic.
- Avoid overusing — it defeats TypeScript’s type safety.
- Prefer `unknown` if safety is needed.

---

### What are differences between unknown and any?

| Feature           | `any`                  | `unknown`                                  |
| ----------------- | ---------------------- | ------------------------------------------ |
| Type Safety       | ❌ No (unsafe)          | ✅ Yes (safe)                               |
| Assign Any Type   | ✅ Yes                  | ✅ Yes                                      |
| Use Without Check | ✅ Allowed              | ❌ Not allowed without check                |
| Best For          | Legacy or dynamic code | Values of unknown type needing type checks |

```ts
let valueAny: any = "hello";
valueAny.toFixed(); // No error (but runtime error!)

let valueUnknown: unknown = "hello";
// valueUnknown.toFixed(); Error: Object is of type 'unknown'

// Safe usage after type check:
if (typeof valueUnknown === "string") {
    console.log(valueUnknown.toUpperCase());
}
```

---

### What are modules?
In TypeScript, **modules** are files that **export** and import code (like variables, functions, classes) to organize and reuse it across files.

**Key Features**  
- Each file is its own module.
- Helps in code **modularity** and **maintainability**.
- Uses `export` and import `keywords`.

math.ts (module file):
```ts
export function add(a: number, b: number): number {
    return a + b;
}
```

main.ts (importing module):
```ts
import { add } from './math';

console.log(add(2, 3)); // Output: 5
```

Modules must be compiled with a module system like `ESNext`, `CommonJS`, etc., set in `tsconfig.json`.


---

### What is a decorator?

A TypeScript decorator is a special function that can be attached to classes, methods, properties, or parameters to modify their behavior at runtime.

```ts
function Logger(constructor: Function) {
  console.log("Class created:", constructor.name);
}

@Logger
class Person {
  name = "Alice";
}
```

---

### What are property decorators?

Property decorators in TypeScript are special functions that can be attached to class properties to add metadata or behavior at runtime or during compilation.

They are part of experimental features and require `experimentalDecorators` enabled in `tsconfig.json`.

```ts
function LogProperty(target: any, propertyKey: string) {
  console.log(`Property decorated: ${propertyKey}`);
}

class Person {
  @LogProperty
  name: string;
}
```

---

### What are strict null checks?

Strict null checks is a TypeScript feature that prevents assigning `null` or `undefined` to variables unless explicitly allowed.

```ts
//  Without strict null checks
let name: string = null; // Allowed
//  With strict null checks
let name: string = null; // Error
let name: string | null = null; // Allowed
```

---

### What are union types?

In TypeScript, **Union Types** allow a variable to hold more than one type.

```ts
let value: string | number;

value = "hello"; // Allowed
value = 42;      // Allowed
// value = true; // Error

```

---

## OOP

### What are classes in TypeScript?

In TypeScript, classes are blueprints for creating objects with properties and methods. They support OOP features like inheritance, access modifiers, and constructors.

```ts
class Person {
    constructor(public name: string, private age: number) { }

    greet() {
        console.log(`Hi, I'm ${this.name}`);
    }
}

const user = new Person("Bob", 25);
user.greet(); // Hi, I'm Bob
// user.age => Error: 'age' is private
```

**Key Points**:  
- `public`, `private`, `protected` control access.
- Supports inheritance: `class Student extends Person`.
- Can implement interfaces.

---

### How to call base class constructor?

To call a **base class constructor** in TypeScript, use the `super()` keyword inside the child class constructor. This ensures the parent class is properly initialized.

```ts
class Animal {
  constructor(public name: string) {
    console.log(`Animal created: ${name}`);
  }
}

class Dog extends Animal {
  constructor(name: string, public breed: string) {
    super(name); // Call to base class constructor
    console.log(`Breed: ${breed}`);
  }
}

const dog = new Dog("Buddy", "Labrador");
```

---

### What are getters and setters?

**Getters** and **setters** in TypeScript are special methods that allow you to control access to an object's properties — like computed properties or validation wrappers.

```ts
class Person {
  private _age: number = 0;

  get age(): number {
    return this._age;
  }

  set age(value: number) {
    if (value >= 0) {
      this._age = value;
    }
  }
}

const p = new Person();
p.age = 25;               // setter called
console.log(p.age);       // getter called → 25
```

---

### What are class constants?

In TypeScript, you can implement class constants using the `static` and `readonly` keywords.

```ts
class MathUtils {
  static readonly PI = 3.14159;
}

console.log(MathUtils.PI); // Output: 3.14159
```

---

### What are interfaces in TypeScript?

In TypeScript, interfaces define the shape of an object — what properties and methods it should have. They are used for type-checking.

```ts
interface Person {
    name: string;
    age: number;
    greet(): void;
}

const user: Person = {
    name: "Alice",
    age: 30,
    greet() {
        console.log(`Hello, I'm ${this.name}`);
    }
};

user.greet(); // Output: Hello, I'm Alice
```

---

### What is the implements clause?

The **implements** clause in TypeScript is used when a class agrees to follow the structure of an interface. It ensures the class implements all required properties and methods defined by the interface.

```ts
interface Animal {
  name: string;
  speak(): void;
}

class Dog implements Animal {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} barks.`);
  }
}
```

---

### What are generics?

**Generics** in TypeScript let you write **reusable**, **type-safe** code that works with any **data type**, without losing type information.

```ts
function identity<T>(arg: T): T {
  return arg;
}

let output1 = identity<string>("hello"); // T = string
let output2 = identity<number>(42);      // T = number
```

---


### What are enums?

In TypeScript, enums (short for enumerations) are a way to define a set of named constants — useful for representing a fixed set of values.

```ts
enum Direction {
  Up,
  Down,
  Left,
  Right
}

let move: Direction = Direction.Up;
console.log(move); // Output: 0
```

---

### What are access modifiers?

Access modifiers in TypeScript control the visibility of class members (properties or methods).

| Modifier    | Access Level                                   |
| ----------- | ---------------------------------------------- |
| `public`    | Accessible from **anywhere** (default)         |
| `private`   | Accessible **only within the class**           |
| `protected` | Accessible within the class **and subclasses** |

---

### What is a namespace?

In TypeScript, a namespace is a way to group related code (like functions, interfaces, or classes) under a single name, helping avoid name collisions in large codebases.

```ts
namespace MathUtils {
  export function add(a: number, b: number): number {
    return a + b;
  }
}

console.log(MathUtils.add(2, 3)); // Output: 5
```

---

### What is optional chaining?

Optional chaining `(?.)` is a TypeScript feature that allows you to safely access nested object properties without throwing an error if a value is `null` or `undefined`.

```ts
const user = {
  name: "Alice",
  address: {
    city: "Paris"
  }
};

console.log(user.address?.city);    // "Paris"
console.log(user.profile?.email);   // undefined (no error)
```

---

### What is type compatibility?


Type compatibility in TypeScript is the ability to assign one type to another if their structures are compatible — this is based on structural typing (not nominal typing).

```ts
interface Person {
  name: string;
  age: number;
}

let p1: Person = { name: "Alice", age: 30 };
let p2 = { name: "Bob", age: 25, gender: "male" };

p1 = p2; // Compatible: p2 has all required fields of Person
```

---

### What is the difference between type and interface?


Here’s a quick comparison of type vs interface in TypeScript:

| Feature        | `interface`                       | `type`                                   |
| -------------- | --------------------------------- | ---------------------------------------- |
| Usage          | Defines object structure          | Defines any type (objects, unions, etc.) |
| Extending      | Can extend other interfaces       | Can extend via intersection (`&`)        |
| Merging        | Auto-merges declarations          | Cannot merge                             |
| Flexibility    | Limited to objects                | More flexible (unions, primitives, etc.) |
| Preferred When | Defining object shapes or classes | Defining unions, complex types           |

```ts
interface Person {
  name: string;
  age: number;
}

type Person = {
  name: string;
  age: number;
};
```

---

### What is a discriminated union?

A discriminated union in TypeScript is a type pattern that combines:
- Union types
- A common literal property (the discriminant) to tell types apart

This allows safe and precise type narrowing.

```ts
type Circle = {
  kind: "circle";
  radius: number;
};

type Square = {
  kind: "square";
  side: number;
};

type Shape = Circle | Square;

function area(shape: Shape): number {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.side ** 2;
  }
}
```

---

### What are mapped types?


Mapped types in TypeScript let you create new types by transforming existing ones, using keyof and type operators.

```ts
type NewType = {
  [Key in keyof ExistingType]: TransformedType;
};
```

Example:
```ts
type Person = {
  name: string;
  age: number;
};

type ReadOnlyPerson = {
  readonly [K in keyof Person]: Person[K];
};
// Equivalent to:
// type ReadOnlyPerson = {
//   readonly name: string;
//   readonly age: number;
// }

```

---

### What are conditional types?

Conditional types in TypeScript allow you to define a type based on a condition, using the extends keyword.

```ts
T extends U ? X : Y
```

Example:

```ts
type IsString<T> = T extends string ? "Yes" : "No";

type A = IsString<string>; // "Yes"
type B = IsString<number>; // "No"
```

### What are rest parameters and spread operators?

**Rest Parameters (...args)**  

Used in function definitions to gather multiple arguments into an array.

```ts
function sum(...numbers: number[]) {
  return numbers.reduce((a, b) => a + b, 0);
}

sum(1, 2, 3); // Output: 6
```
**Spread Operator (...obj/arr)**  
Used to expand an array or object into individual elements or properties.
```ts
// For arrays:
const nums = [1, 2, 3];
const moreNums = [...nums, 4, 5]; // [1, 2, 3, 4, 5]

// For objects:
const person = { name: "Alice" };
const updated = { ...person, age: 30 }; // { name: "Alice", age: 30 }

```
---

### What is the keyof keyword?

The `keyof` keyword in TypeScript creates a union of all property names (keys) of a given type.

```ts
type Person = {
  name: string;
  age: number;
};

type PersonKeys = keyof Person; 
// PersonKeys = "name" | "age"

```

---

### What are utility types like Partial, Readonly, and Record?

**Utility types** in TypeScript are built-in helpers that transform existing types to reduce repetition and improve flexibility.


| Utility        | Description                                                 | Example Output                                    |
| -------------- | ----------------------------------------------------------- | ------------------------------------------------- |
| `Partial<T>`   | Makes all properties in `T` optional                        | `{ name?: string; age?: number }`                 |
| `Readonly<T>`  | Makes all properties in `T` readonly                        | `{ readonly name: string; readonly age: number }` |
| `Record<K, T>` | Creates an object type with keys `K` and values of type `T` | `{ key1: T; key2: T; ... }`                       |

```ts
type Person = {
  name: string;
  age: number;
};

const p1: Partial<Person> = { name: "Alice" }; // age is optional

const p2: Readonly<Person> = { name: "Bob", age: 30 };
// p2.age = 31; Error: Cannot assign to 'age'

const roles: Record<"admin" | "user", boolean> = {
  admin: true,
  user: false,
};

```
---

### What is never type?


In TypeScript, the **never** type represents values that never occur — it's used when a function never returns or a value is impossible.

```ts
// Function that never returns:
function throwError(message: string): never {
  throw new Error(message);
}

// Infinite loop:
function infiniteLoop(): never {
  while (true) {}
}

```

## Setup

### Basic setup

- Initialize the Project

```shell
mkdir new-app
cd new-app
npm init -y
```
- Install TypeScript

```shell
npm install typescript @types/node --save-dev
```

- Configure TypeScript

```shell
npx tsc --init
```

Ensure the following settings are included in `tsconfig.json`:

```json
{
  "compilerOptions": {
    "target": "ES6",
    "module": "commonjs",
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true
  }
}
```
-  Create Project Structure

```shell
mkdir src
touch src/index.ts
```

- Write the Code

Open the `src/index.ts` file and add the following code:

```ts
function sayHello(): void {
    console.log("Hello, World!");
}

sayHello();
```

- Compile and run

Add scripts in `package.json`:

```json
"scripts": {
  "build": "tsc",
  "start": "node dist/index.js"
}
```

```shell
npm build && npm start
```

---


## References
  - https://zerotomastery.io/blog/typescript-interview-questions/
  - https://github.com/FAQGURU/FAQGURU/blob/master/topics/en/typeScript.md
    
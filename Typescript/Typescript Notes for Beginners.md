A complete beginner-friendly reference covering all the core TypeScript topics you need to know.

## 📑 Table of Contents

1. [[#1. Introduction to TypeScript|Introduction to TypeScript]]
2. [[#2. Setup and Compilation|Setup and Compilation]]
3. [[#3. Basic Types|Basic Types]]
4. [[#4. Type Inference and Type Annotations|Type Inference and Type Annotations]]
5. [[#5. Arrays and Tuples|Arrays and Tuples]]
6. [[#6. Enums|Enums]]
7. [[#7. Functions|Functions]]
8. [[#8. Interfaces|Interfaces]]
9. [[#9. Type Aliases|Type Aliases]]
10. [[#10. Union and Intersection Types|Union and Intersection Types]]
11. [[#11. Classes and OOP|Classes and OOP]]
12. [[#12. Access Modifiers|Access Modifiers]]
13. [[#13. Generics|Generics]]
14. [[#14. Optional and Readonly Properties|Optional and Read only Properties]]
15. [[#15. Type Assertions|Type Assertions]]
16. [[#16. Any, Unknown, Never, Void|Any, Unknown, Never, Void]]
17. [[#17. Modules (import/export)|Modules (import/export)]]
18. [[#18. Interfaces vs Type Aliases|Interfaces vs Type Aliases]]
19. [[#19. Utility Types|Utility Types]]
20. [[#20. Common Beginner Mistakes to Avoid|Common Beginner Mistakes to Avoid]]
21. [[#21. Quick Practice Ideas|Quick Practice Ideas]]

---

## 1. Introduction to TypeScript

- TypeScript is a **superset of JavaScript** that adds **static typing**.
- Developed and maintained by **Microsoft**.
- Any valid JavaScript code is also valid TypeScript.
- TypeScript code is **compiled (transpiled)** into plain JavaScript before running.
- Helps catch errors **at compile time** instead of runtime.

---

## 2. Setup and Compilation

```bash
npm install -g typescript
tsc --version
```

```bash
tsc app.ts        # compiles app.ts into app.js
tsc app.ts --watch  # auto-recompile on changes
```

- `tsconfig.json` — configuration file for a TypeScript project.

```bash
tsc --init   # generates tsconfig.json
```

---

## 3. Basic Types

```typescript
let id: number = 5;
let username: string = "John";
let isActive: boolean = true;
let notAssigned: undefined = undefined;
let empty: null = null;
```

|Type|Example|
|---|---|
|`number`|`5`, `3.14`|
|`string`|`"hello"`|
|`boolean`|`true` / `false`|
|`undefined`|uninitialized value|
|`null`|intentional empty value|

---

## 4. Type Inference and Type Annotations

```typescript
let age = 25;          // inferred as number automatically
let name: string = "John";  // explicit annotation
```

- TypeScript infers types automatically when possible.
- Use explicit annotations when the type isn't obvious or for function parameters.

---

## 5. Arrays and Tuples

### Arrays

```typescript
let numbers: number[] = [1, 2, 3];
let names: Array<string> = ["Alice", "Bob"];
```

### Tuples (fixed-length, fixed-type arrays)

```typescript
let person: [string, number] = ["John", 25];
```

---

## 6. Enums

Named set of constant values.

```typescript
enum Direction {
  Up,
  Down,
  Left,
  Right
}

let move: Direction = Direction.Up;   // 0
```

```typescript
enum Status {
  Active = "ACTIVE",
  Inactive = "INACTIVE"
}
```

---

## 7. Functions

```typescript
function add(a: number, b: number): number {
  return a + b;
}

// optional parameter
function greet(name: string, greeting?: string): string {
  return `${greeting || "Hello"}, ${name}!`;
}

// default parameter
function multiply(a: number, b: number = 2): number {
  return a * b;
}

// arrow function
const subtract = (a: number, b: number): number => a - b;
```

- `: number` after the parameter list defines the **return type**.

---

## 8. Interfaces

Define the shape/structure of an object.

```typescript
interface Person {
  name: string;
  age: number;
  greet(): void;
}

const user: Person = {
  name: "John",
  age: 25,
  greet() {
    console.log("Hello!");
  }
};
```

---

## 9. Type Aliases

Create a custom name for a type.

```typescript
type ID = number | string;
type Point = { x: number; y: number };

let userId: ID = 101;
let card: Point = { x: 10, y: 20 };
```

---

## 10. Union and Intersection Types

### Union (`|`) — value can be one of several types

```typescript
let value: string | number;
value = "hello";
value = 10;
```

### Intersection (`&`) — combines multiple types into one

```typescript
type Employee = { id: number } & { name: string };
const emp: Employee = { id: 1, name: "John" };
```

---

## 11. Classes and OOP

```typescript
class Animal {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  makeSound(): void {
    console.log("Some sound");
  }
}

class Dog extends Animal {
  makeSound(): void {
    console.log("Bark");
  }
}

const d = new Dog("Rex");
d.makeSound();   // Bark
```

- `extends` — inheritance
- `super()` — calls the parent constructor

---

## 12. Access Modifiers

|Modifier|Description|
|---|---|
|`public`|accessible everywhere (default)|
|`private`|accessible only within the class|
|`protected`|accessible within class and subclasses|
|`readonly`|value cannot be changed after initialization|

```typescript
class Account {
  private balance: number;
  readonly accountNumber: string;

  constructor(balance: number, accountNumber: string) {
    this.balance = balance;
    this.accountNumber = accountNumber;
  }
}
```

---

## 13. Generics

Write reusable code that works with multiple types.

```typescript
function identity<T>(value: T): T {
  return value;
}

identity<string>("hello");
identity<number>(42);

interface Box<T> {
  content: T;
}

const box: Box<number> = { content: 10 };
```

---

## 14. Optional and Readonly Properties

```typescript
interface Product {
  name: string;
  price: number;
  discount?: number;     // optional property
  readonly id: number;    // cannot be reassigned
}
```

---

## 15. Type Assertions

Tell the compiler to treat a value as a specific type.

```typescript
let someValue: unknown = "Hello TypeScript";
let strLength: number = (someValue as string).length;

// alternative syntax
let strLength2: number = (<string>someValue).length;
```

---

## 16. Any, Unknown, Never, Void

|Type|Meaning|
|---|---|
|`any`|disables type checking (avoid overusing)|
|`unknown`|like `any` but safer — must check type before using|
|`never`|represents a value that never occurs (e.g., function that always throws)|
|`void`|represents no return value|

```typescript
function logMessage(message: string): void {
  console.log(message);
}

function throwError(message: string): never {
  throw new Error(message);
}
```

---

## 17. Modules (import/export)

```typescript
// mathUtils.ts
export function add(a: number, b: number): number {
  return a + b;
}
export const PI = 3.14;

// main.ts
import { add, PI } from "./mathUtils";
```

```typescript
// default export
export default function greet() { console.log("Hi"); }
import greet from "./greetModule";
```

---

## 18. Interfaces vs Type Aliases

|Feature|`interface`|`type`|
|---|---|---|
|Extending|`extends` keyword|`&` intersection|
|Reopening|can be re-declared/merged|cannot be re-declared|
|Best for|object shapes, OOP|unions, primitives, complex types|

```typescript
interface A { name: string }
interface A { age: number }  // merges automatically

type B = { name: string };
// type B = { age: number };  // ❌ Error: duplicate identifier
```

---

## 19. Utility Types

Built-in helpers to transform types.

```typescript
interface User {
  id: number;
  name: string;
  email: string;
}

type PartialUser = Partial<User>;    // all properties optional
type ReadonlyUser = Readonly<User>;   // all properties readonly
type UserName = Pick<User, "name">;   // only pick specific properties
type UserWithoutEmail = Omit<User, "email">;  // exclude a property
```

---

## 20. Common Beginner Mistakes to Avoid

- Overusing `any`, which defeats the purpose of TypeScript.
- Forgetting to run `tsc` and expecting `.ts` files to run directly in browsers/Node.
- Confusing `interface` and `type` — both work for objects, but know when to use each.
- Not enabling `strict` mode in `tsconfig.json` (misses many type errors).
- Using type assertions (`as`) to force incorrect types instead of fixing the actual type.
- Forgetting optional chaining (`?.`) when accessing possibly-undefined properties.

---

## 21. Quick Practice Ideas

- Convert a small JavaScript project into TypeScript.
- Create an interface for a `Product` and build a shopping cart function.
- Write a generic function that works with arrays of any type.
- Build a `class` hierarchy using `extends` and access modifiers.
- Use utility types (`Partial`, `Pick`, `Omit`) on a `User` interface.

---

### 📌 Tip

Enable `"strict": true` in your `tsconfig.json` early on — it forces you to write safer code and helps you learn TypeScript's type system faster.
# TypeScript - Complete Topic Guide

A practical reference covering the TypeScript features you'll actually use when building web applications, each with runnable examples.

---

## Table of Contents

1. [[#1. Setup & Basic Types|Setup & Basic Types]]
2. [[#2. Arrays, Tuples & Objects|Arrays, Tuples & Objects]]
3. [[#3. Functions|Functions]]
4. [[#4. Interfaces|Interfaces]]
5. [[#5. Type Aliases|Type Aliases]]
6. [[#6. Union & Intersection Types|Union & Intersection Types]]
7. [[#7. Literal Types & Type Narrowing|Literal Types & Type Narrowing]]
8. [[#8. Enums|Enums]]
9. [[#9. Classes|Classes]]
10. [[#10. Generics|Generics]]
11. [[#11. Utility Types|Utility Types]]
12. [[#12. Type Guards & Custom Guards|Type Guards & Custom Guards]]
13. [[#13. Optional Chaining & Nullish Coalescing|Optional Chaining & Nullish Coalescing]]
14. [[#14. Async/Await & Promises|Async/Await & Promises]]
15. [[#15. Modules & Namespaces|Modules & Namespaces]]
16. [[#16. Working with the DOM|Working with the DOM]]
17. [[#17. Fetch API & Typed HTTP Requests|Fetch API & Typed HTTP Requests]]
18. [[#18. Type Assertions & `as const`|Type Assertions & `as const`]]
19. [[#19. Mapped & Conditional Types|Mapped & Conditional Types]]
20. [[#20. Decorators|Decorators]]
21. [[#21. React + TypeScript|React + TypeScript]]
22. [[#22. Node.js / Express + TypeScript|Node.js / Express + TypeScript]]
23. [[#23. Error Handling Patterns|Error Handling Patterns]]
24. [[#24. `tsconfig.json` Essentials|`tsconfig.json` Essentials]]
25. [[#25. Best Practices for Web Apps|Best Practices for Web Apps]]

---

## 1. Setup & Basic Types

```bash
npm install -D typescript
npx tsc --init
```

```ts
let username: string = "alice";
let age: number = 28;
let isActive: boolean = true;
let notAssigned: undefined = undefined;
let empty: null = null;
let anything: any = "avoid this when possible";
let safer: unknown = fetchDataFromSomewhere(); // must be narrowed before use
let nothingReturned: void = undefined;

function fail(message: string): never {
  throw new Error(message);
}
```

**Why it matters for web apps:** catches typos and wrong data shapes (e.g., passing a `number` where a form expects a `string`) before the code ever reaches the browser.

---

## 2. Arrays, Tuples & Objects

```ts
// Arrays
const tags: string[] = ["news", "tech"];
const scores: Array<number> = [10, 20, 30];

// Tuples — fixed length, fixed types per position
const userEntry: [string, number] = ["alice", 28];
const [name, age] = userEntry;

// Readonly array
const frozenTags: readonly string[] = ["a", "b"];

// Object typing
const user: { id: number; name: string; email?: string } = {
  id: 1,
  name: "Alice",
};
```

---

## 3. Functions

```ts
// Typed parameters and return value
function add(a: number, b: number): number {
  return a + b;
}

// Optional & default parameters
function greet(name: string, greeting: string = "Hello"): string {
  return `${greeting}, ${name}!`;
}

// Rest parameters
function sum(...nums: number[]): number {
  return nums.reduce((total, n) => total + n, 0);
}

// Function type expressions
const multiply: (a: number, b: number) => number = (a, b) => a * b;

// Overloads (useful for API helpers)
function parseInput(value: string): string[];
function parseInput(value: number): number;
function parseInput(value: string | number): string[] | number {
  return typeof value === "string" ? value.split(",") : value;
}
```

---

## 4. Interfaces

Interfaces describe the shape of objects — the backbone of typing API responses, props, and config.

```ts
interface Product {
  id: number;
  title: string;
  price: number;
  inStock?: boolean;         // optional
  readonly sku: string;      // cannot be reassigned after creation
}

const item: Product = {
  id: 1,
  title: "Keyboard",
  price: 49.99,
  sku: "KB-001",
};

// Extending interfaces
interface DiscountedProduct extends Product {
  discountPercent: number;
}

// Interfaces for functions
interface SearchFn {
  (query: string, page: number): Promise<Product[]>;
}
```

---

## 5. Type Aliases

```ts
type ID = string | number;

type Point = {
  x: number;
  y: number;
};

type Callback<T> = (data: T) => void;

// Combining aliases
type UserWithPoint = Point & { user: string };
```

**Interface vs. type alias:** use `interface` for object shapes you expect to extend (e.g., component props), and `type` for unions, tuples, or utility compositions.

---

## 6. Union & Intersection Types

```ts
// Union — value can be one of several types
type Status = "loading" | "success" | "error";

function render(status: Status) {
  if (status === "loading") return "Spinner";
  if (status === "error") return "ErrorBanner";
  return "Content";
}

// Union of object shapes (common for API results)
type ApiResult =
  | { success: true; data: Product[] }
  | { success: false; error: string };

function handleResult(result: ApiResult) {
  if (result.success) {
    console.log(result.data); // TS knows `data` exists here
  } else {
    console.log(result.error); // TS knows `error` exists here
  }
}

// Intersection — combine multiple types into one
type Timestamped = { createdAt: Date };
type Auditable = Timestamped & { updatedAt: Date };
```

---

## 7. Literal Types & Type Narrowing

```ts
type ButtonVariant = "primary" | "secondary" | "danger";

function renderButton(variant: ButtonVariant) {
  // ...
}

renderButton("primary");   // OK
// renderButton("large");  // Error: not assignable

// Narrowing with typeof
function formatValue(value: string | number) {
  if (typeof value === "string") {
    return value.toUpperCase();
  }
  return value.toFixed(2);
}

// Narrowing with `in`
type Admin = { role: "admin"; permissions: string[] };
type Guest = { role: "guest" };

function describe(user: Admin | Guest) {
  if ("permissions" in user) {
    return user.permissions.join(", ");
  }
  return "No permissions";
}
```

---

## 8. Enums

```ts
enum OrderStatus {
  Pending = "PENDING",
  Shipped = "SHIPPED",
  Delivered = "DELIVERED",
}

function trackOrder(status: OrderStatus) {
  if (status === OrderStatus.Delivered) {
    console.log("Order complete");
  }
}

trackOrder(OrderStatus.Shipped);

// Alternative: "as const" object (often preferred, no runtime enum object)
const Role = {
  Admin: "ADMIN",
  User: "USER",
} as const;

type Role = (typeof Role)[keyof typeof Role]; // "ADMIN" | "USER"
```

---

## 9. Classes

```ts
class ApiClient {
  private baseUrl: string;
  protected timeout: number = 5000;
  readonly version = "v1";

  constructor(baseUrl: string) {
    this.baseUrl = baseUrl;
  }

  async get<T>(path: string): Promise<T> {
    const res = await fetch(`${this.baseUrl}/${this.version}/${path}`);
    return res.json() as Promise<T>;
  }
}

// Inheritance
class AuthClient extends ApiClient {
  constructor(baseUrl: string, private token: string) {
    super(baseUrl);
  }

  async getSecure<T>(path: string): Promise<T> {
    // could attach this.token as a header in a real implementation
    return this.get<T>(path);
  }
}

// Implementing an interface
interface Storable {
  save(): void;
}

class Draft implements Storable {
  save() {
    console.log("saved");
  }
}
```

---

## 10. Generics

Generics let you write reusable, type-safe components, hooks, and functions.

```ts
function wrapInArray<T>(value: T): T[] {
  return [value];
}

wrapInArray("hello");  // string[]
wrapInArray(42);        // number[]

// Generic interface — great for API response wrappers
interface ApiResponse<T> {
  data: T;
  status: number;
  message: string;
}

function fetchUser(): ApiResponse<{ id: number; name: string }> {
  return { data: { id: 1, name: "Alice" }, status: 200, message: "OK" };
}

// Generic constraints
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const product = { id: 1, title: "Mouse" };
getProperty(product, "title"); // OK
// getProperty(product, "price"); // Error: not a key of product

// Generic class
class Store<T> {
  private items: T[] = [];
  add(item: T) {
    this.items.push(item);
  }
  getAll(): T[] {
    return this.items;
  }
}

const productStore = new Store<Product>();
```

---

## 11. Utility Types

Built-in types that transform other types — used constantly in real projects.

```ts
interface User {
  id: number;
  name: string;
  email: string;
  password: string;
}

type PublicUser = Omit<User, "password">;         // remove a field
type UserPreview = Pick<User, "id" | "name">;      // keep only some fields
type PartialUser = Partial<User>;                  // all fields optional (great for PATCH requests)
type RequiredUser = Required<PartialUser>;         // all fields required
type ReadonlyUser = Readonly<User>;                // immutable object
type UserMap = Record<string, User>;               // dictionary type

// Extract / Exclude with unions
type Status = "idle" | "loading" | "success" | "error";
type ErrorLikeStatus = Extract<Status, "error" | "idle">;
type NonIdleStatus = Exclude<Status, "idle">;

// ReturnType / Parameters — infer types from existing functions
function createUser(name: string, email: string) {
  return { id: Date.now(), name, email };
}
type NewUser = ReturnType<typeof createUser>;
type CreateUserArgs = Parameters<typeof createUser>;
```

---

## 12. Type Guards & Custom Guards

```ts
interface Cat {
  meow(): void;
}
interface Dog {
  bark(): void;
}

// Custom type guard using "is"
function isCat(animal: Cat | Dog): animal is Cat {
  return (animal as Cat).meow !== undefined;
}

function speak(animal: Cat | Dog) {
  if (isCat(animal)) {
    animal.meow();
  } else {
    animal.bark();
  }
}

// instanceof guard
class NetworkError extends Error {}
class ValidationError extends Error {}

function handleError(err: unknown) {
  if (err instanceof NetworkError) {
    console.log("Retry the request");
  } else if (err instanceof ValidationError) {
    console.log("Show form errors");
  }
}
```

---

## 13. Optional Chaining & Nullish Coalescing

```ts
interface Profile {
  user?: {
    address?: {
      city?: string;
    };
  };
}

function getCity(profile: Profile): string {
  // Optional chaining avoids manual null checks at every level
  return profile.user?.address?.city ?? "Unknown city";
}

// Nullish coalescing assignment
let config: { timeout?: number } = {};
config.timeout ??= 3000;
```

---

## 14. Async/Await & Promises

```ts
interface Post {
  id: number;
  title: string;
}

async function getPost(id: number): Promise<Post> {
  const res = await fetch(`/api/posts/${id}`);
  if (!res.ok) {
    throw new Error(`Failed with status ${res.status}`);
  }
  return res.json() as Promise<Post>;
}

async function getMultiplePosts(ids: number[]): Promise<Post[]> {
  return Promise.all(ids.map((id) => getPost(id)));
}

// Typed try/catch (errors are `unknown` in TS by default)
async function loadPost(id: number) {
  try {
    const post = await getPost(id);
    return post;
  } catch (err) {
    if (err instanceof Error) {
      console.error(err.message);
    }
    return null;
  }
}
```

---

## 15. Modules & Namespaces

```ts
// math.ts
export function square(x: number): number {
  return x * x;
}
export const PI = 3.14159;
export default class Calculator {
  add(a: number, b: number) {
    return a + b;
  }
}

// app.ts
import Calculator, { square, PI } from "./math";

// Re-exporting from an index barrel file
export * from "./math";
export { default as Calculator } from "./math";
```

---

## 16. Working with the DOM

TypeScript ships with built-in DOM types (`lib.dom.d.ts`).

```ts
const button = document.querySelector<HTMLButtonElement>("#submit-btn");

button?.addEventListener("click", (event: MouseEvent) => {
  console.log("Clicked!", event.clientX, event.clientY);
});

const input = document.getElementById("email") as HTMLInputElement;
input.value = "user@example.com";

// Typed custom events
interface CartUpdatedDetail {
  itemCount: number;
}
const event = new CustomEvent<CartUpdatedDetail>("cart-updated", {
  detail: { itemCount: 3 },
});
document.dispatchEvent(event);

document.addEventListener("cart-updated", ((e: CustomEvent<CartUpdatedDetail>) => {
  console.log(e.detail.itemCount);
}) as EventListener);
```

---

## 17. Fetch API & Typed HTTP Requests

```ts
interface Todo {
  id: number;
  title: string;
  completed: boolean;
}

async function fetchTodos(): Promise<Todo[]> {
  const response = await fetch("https://api.example.com/todos");
  if (!response.ok) throw new Error("Network error");
  const data: unknown = await response.json();
  return data as Todo[]; // ideally validate with Zod/io-ts instead of a raw cast
}

async function createTodo(payload: Omit<Todo, "id">): Promise<Todo> {
  const response = await fetch("https://api.example.com/todos", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(payload),
  });
  return response.json();
}
```

> **Tip:** for real production apps, validate untrusted API responses at runtime with a library like `zod` — TypeScript types disappear at runtime, so `as Todo[]` doesn't actually guarantee the shape.

```ts
import { z } from "zod";

const TodoSchema = z.object({
  id: z.number(),
  title: z.string(),
  completed: z.boolean(),
});
type Todo = z.infer<typeof TodoSchema>;

async function fetchTodo(id: number): Promise<Todo> {
  const res = await fetch(`/api/todos/${id}`);
  return TodoSchema.parse(await res.json()); // throws if shape is wrong
}
```

---

## 18. Type Assertions & `as const`

```ts
// Type assertion — tells the compiler "trust me"
const input = document.getElementById("email") as HTMLInputElement;

// as const — locks values as readonly literals instead of widened types
const routes = ["/", "/about", "/contact"] as const;
type Route = (typeof routes)[number]; // "/" | "/about" | "/contact"

const config = {
  env: "production",
  retries: 3,
} as const;
// config.env is type "production", not string
```

---

## 19. Mapped & Conditional Types

```ts
// Mapped type — transform every property of a type
type Nullable<T> = { [K in keyof T]: T[K] | null };

interface Form {
  name: string;
  age: number;
}
type NullableForm = Nullable<Form>; // { name: string | null; age: number | null }

// Conditional types
type IsString<T> = T extends string ? true : false;
type A = IsString<"hi">;   // true
type B = IsString<42>;     // false

// Practical: extract array element type
type ElementType<T> = T extends (infer U)[] ? U : never;
type Item = ElementType<string[]>; // string

// Template literal types — great for typed CSS-in-JS or event names
type EventName = `on${Capitalize<"click" | "hover" | "focus">}`;
// "onClick" | "onHover" | "onFocus"
```

---

## 20. Decorators

Commonly used in Angular apps and backend frameworks like NestJS. Requires `"experimentalDecorators": true` in `tsconfig.json` (or use the newer stage-3 decorators in TS 5+).

```ts
function LogMethod(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
  const original = descriptor.value;
  descriptor.value = function (...args: any[]) {
    console.log(`Calling ${propertyKey} with`, args);
    return original.apply(this, args);
  };
}

class UserService {
  @LogMethod
  getUser(id: number) {
    return { id, name: "Alice" };
  }
}
```

---

## 21. React + TypeScript

```tsx
import { useState, useEffect, ReactNode } from "react";

// Typed props
interface CardProps {
  title: string;
  children: ReactNode;
  onClose?: () => void;
}

function Card({ title, children, onClose }: CardProps) {
  return (
    <div className="card">
      <h2>{title}</h2>
      {children}
      {onClose && <button onClick={onClose}>Close</button>}
    </div>
  );
}

// Typed useState
function Counter() {
  const [count, setCount] = useState<number>(0);
  return <button onClick={() => setCount((c) => c + 1)}>{count}</button>;
}

// Typed useEffect with a fetched resource
interface User {
  id: number;
  name: string;
}

function UserProfile({ userId }: { userId: number }) {
  const [user, setUser] = useState<User | null>(null);

  useEffect(() => {
    let cancelled = false;
    fetch(`/api/users/${userId}`)
      .then((res) => res.json())
      .then((data: User) => {
        if (!cancelled) setUser(data);
      });
    return () => {
      cancelled = true;
    };
  }, [userId]);

  if (!user) return <p>Loading...</p>;
  return <p>{user.name}</p>;
}

// Typed custom hook
function useLocalStorage<T>(key: string, initialValue: T) {
  const [value, setValue] = useState<T>(() => {
    const stored = localStorage.getItem(key);
    return stored ? (JSON.parse(stored) as T) : initialValue;
  });

  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);

  return [value, setValue] as const;
}

// Typed event handlers
function SearchBox() {
  const [query, setQuery] = useState("");
  const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    setQuery(e.target.value);
  };
  const handleSubmit = (e: React.FormEvent<HTMLFormElement>) => {
    e.preventDefault();
    console.log(query);
  };
  return (
    <form onSubmit={handleSubmit}>
      <input value={query} onChange={handleChange} />
    </form>
  );
}
```

---

## 22. Node.js / Express + TypeScript

```ts
import express, { Request, Response, NextFunction } from "express";

const app = express();
app.use(express.json());

interface CreateUserBody {
  name: string;
  email: string;
}

app.post(
  "/users",
  (req: Request<{}, {}, CreateUserBody>, res: Response) => {
    const { name, email } = req.body;
    res.status(201).json({ id: 1, name, email });
  }
);

// Typed middleware
function requireAuth(req: Request, res: Response, next: NextFunction) {
  const token = req.headers.authorization;
  if (!token) {
    return res.status(401).json({ error: "Unauthorized" });
  }
  next();
}

app.get("/profile", requireAuth, (req: Request, res: Response) => {
  res.json({ message: "Welcome" });
});
```

---

## 23. Error Handling Patterns

```ts
// Custom error hierarchy for predictable API/UI handling
class AppError extends Error {
  constructor(message: string, public code: string) {
    super(message);
    this.name = "AppError";
  }
}

class NotFoundError extends AppError {
  constructor(resource: string) {
    super(`${resource} not found`, "NOT_FOUND");
  }
}

// Result type pattern (avoids throwing for expected failures)
type Result<T, E = string> =
  | { ok: true; value: T }
  | { ok: false; error: E };

function parseJson<T>(text: string): Result<T> {
  try {
    return { ok: true, value: JSON.parse(text) as T };
  } catch {
    return { ok: false, error: "Invalid JSON" };
  }
}

const result = parseJson<{ id: number }>('{"id": 1}');
if (result.ok) {
  console.log(result.value.id);
} else {
  console.log(result.error);
}
```

---

## 24. `tsconfig.json` Essentials

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "ESNext",
    "moduleResolution": "Bundler",
    "lib": ["DOM", "ES2020"],
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "jsx": "react-jsx",
    "outDir": "./dist",
    "baseUrl": ".",
    "paths": {
      "@components/*": ["src/components/*"],
      "@utils/*": ["src/utils/*"]
    }
  },
  "include": ["src"]
}
```

**Key flags for web apps:**

- `strict: true` — enables all strict type checks (always turn this on).
- `jsx: "react-jsx"` — needed for React 17+ without importing React in every file.
- `paths` — enables clean absolute imports like `@components/Button`.

---

## 25. Best Practices for Web Apps

- Turn on `strict` mode from day one — retrofitting it later is painful.
- Prefer `unknown` over `any` for values of uncertain shape (like API responses), and narrow before use.
- Validate external data (API responses, form input, `localStorage`) at runtime with `zod` or `io-ts` — types are erased at compile time and don't protect you from bad data.
- Use `interface` for public component/API contracts you expect others to extend; use `type` for unions and utility compositions.
- Model impossible states as impossible — use discriminated unions (`{ success: true, data } | { success: false, error }`) instead of `data?: T; error?: string`.
- Use utility types (`Partial`, `Pick`, `Omit`) instead of duplicating near-identical interfaces.
- Avoid `as` type assertions except when you genuinely know more than the compiler (e.g., DOM queries); prefer type guards.
- Collocate types with the code that uses them; only pull them into shared files once actually reused.

---

_This guide covers the core TypeScript surface used in day-to-day web app development — vanilla DOM apps, React, and Node/Express backends. For deeper dives, see the [official TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)._
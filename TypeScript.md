**What is TypeScript?**

**TypeScript (TS)** is an open-source, strongly typed programming language that builds on **JavaScript**. It's a **syntactical superset of JavaScript**, meaning any valid JavaScript code is also valid TypeScript code. TypeScript adds **optional static typing** and other features to JavaScript, making it easier to write and maintain **large-scale applications**. 

**Problems Solved by TypeScript:**

TypeScript was created to address several limitations of JavaScript, particularly for building large, complex applications.

*   **Dynamic Typing and Runtime Errors:** JavaScript's dynamic typing can lead to unexpected behavior and hard-to-catch runtime errors. TypeScript's **static typing** allows developers to define types at compile time, catching type-related errors **before** the code runs, significantly reducing bugs in production.
*   **Difficulty in Maintaining Large Codebases:**  As projects grow, JavaScript's dynamic typing can make understanding and maintaining large codebases challenging. TypeScript's **explicit type annotations and interfaces** improve code readability and serve as living documentation, clarifying variable and function usage.
*   **Limited Tooling Support:** Without type information, IDEs have limited ability to provide intelligent code completion and refactoring features. TypeScript's static typing enhances tooling support, enabling features like **IntelliSense, autocompletion, and refactoring**, boosting developer productivity.
*   **Complex Object-Oriented Programming:**  While JavaScript has object-oriented features, they can be less intuitive than class-based languages. TypeScript provides robust support for **classes, interfaces, and inheritance**, making it easier to build well-structured and scalable code.

**How TypeScript Works (In-depth):**

1.  **TypeScript Compiler (tsc):** TypeScript code (.ts files) cannot be executed directly by browsers or Node.js. It must be compiled (or transpiled) into plain JavaScript (.js files) using the TypeScript compiler (tsc).
2.  **Compilation Process:** The tsc compiler performs the following steps:
    *   **Parsing:** It reads and parses the TypeScript code into an **Abstract Syntax Tree (AST)**, representing the code's structure and syntax.
    *   **Type Checking:**  It checks the code for type errors based on the defined types and inference rules.
    *   **Transformation:** It removes type annotations and TypeScript-specific features.
    *   **Code Generation:** It generates the equivalent JavaScript code.
3.  **JavaScript Execution:** The generated JavaScript code is then executed in any JavaScript environment.
4.  **Static Typing:** TypeScript uses **static typing** to define types for variables, function parameters, and return values, allowing for early error detection at **compile time**.
5.  **Type Inference:** TypeScript can automatically deduce the type of a variable based on its value or usage, reducing the need for explicit annotations.
6.  **Interfaces:** Interfaces define the **structure or shape** of objects, enforcing consistent design and improving code readability.
7.  **Classes:** TypeScript supports classes and inheritance, providing a more structured approach to object-oriented programming.
8.  **Generics:**  Generics allow for creating **reusable components** that work with various data types while maintaining type safety.

**Key Concepts Explained:**

*   **TypeScript (TS):** A typed superset of JavaScript that compiles to plain JavaScript.
*   **Static Typing:**  Defining types at compile time to catch errors early.
*   **Compile Time:** The phase when the TypeScript code is compiled to JavaScript.
*   **Runtime:** The phase when the JavaScript code is executed.
*   **TypeScript Compiler (tsc):** The tool used to compile TypeScript code into JavaScript.
*   **Transpilation:**  Converting code from one language to another (TypeScript to JavaScript).
*   **Type Inference:**  TypeScript automatically deducing the type of a variable.
*   **Interfaces:**  Defining the structure or shape of objects.
*   **Classes:**  Templates for creating objects.
*   **Generics:**  Creating reusable components that work with multiple data types.

TypeScript provides a robust and type-safe environment for developing large and complex JavaScript applications. It improves code quality, enhances developer productivity, and makes it easier to maintain and scale projects.


**Optional static typing** - A programming language allows you to add type annotations (like string, number, etc.) to your variables and functions, but doesn’t require it — it's optional.

**large-scale applications** - A large-scale application refers to a software system that is: Complex, Feature-rich, and Built to handle a high volume of users, data, and interactions, often across multiple teams, modules, or services.

A large-scale application is not just about size — it’s about how well your app is structured, scalable, and maintainable under heavy use, frequent changes, and real-world demands.

**Scalability** - Scalability means your app can grow without becoming slow, unstable, or difficult to maintain.

---


# Type Declarations in TypeScript

Here are the different ways we can declare types in TypeScript:

---

## 1. Primitive Types
```ts
let age: number = 25;
let name: string = "Manasa";
let isActive: boolean = true;
```

---

## 2. Array Types
```ts
let numbers: number[] = [1, 2, 3];       // square bracket syntax
let numbers2: Array<number> = [1, 2, 3]; // generic syntax
```

---

## 3. Tuple Types
```ts
let person: [string, number] = ["Manasa", 25];
```

---

## 4. Object Types
```ts
let user: { name: string; age: number } = {
  name: "Manasa",
  age: 25
};
```

---

## 5. Any Type
```ts
let data: any = "Hello";
data = 123; // allowed
```

---

## 6. Unknown Type
```ts
let input: unknown = "Hi";
```

---

## 7. Union Types
```ts
let id: string | number;
id = "123";
id = 123;
```

---

## 8. Intersection Types
```ts
type A = { name: string };
type B = { age: number };
type C = A & B;

let user: C = { name: "Manasa", age: 25 };
```

---

## 9. Type Aliases
```ts
type ID = string | number;
let empId: ID = 101;
```

---

## 10. Interfaces
```ts
interface User {
  name: string;
  age: number;
}
let u: User = { name: "Manasa", age: 25 };
```

---

## 11. Enums
```ts
enum Role {
  Admin,
  User,
  Guest
}
let myRole: Role = Role.Admin;
```

---

## 12. Literal Types
```ts
let direction: "up" | "down";
direction = "up"; // ✅
```

---

# Type vs Interface in TypeScript

| Feature / Use Case               | **type**                                                                 | **interface**                                                                 |
|----------------------------------|---------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| **Basic Purpose**                | Create **aliases** for primitives, objects, unions, intersections, etc.  | Define the **shape of objects**, contracts, or class blueprints.              |
| **Objects**                      | Can define object shapes.                                                 | Can define object shapes.                                                     |
| **Primitives**                   | ✅ Can alias primitives (`type ID = number`).                             | ❌ Cannot alias primitives.                                                   |
| **Union / Intersection**         | ✅ Supports unions & intersections (`type X = A | B`).                    | ❌ Does not support unions directly.                                          |
| **Extending**                    | ✅ Extend via intersections (`type X = A & B`).                           | ✅ Extend via `extends` keyword.                                              |
| **Declaration Merging**          | ❌ Not supported.                                                         | ✅ Supported (multiple interfaces with same name merge).                      |
| **Implements (Classes)**         | ✅ Can be used in `implements`.                                           | ✅ Can be used in `implements`.                                               |
| **Mapped/Utility Types**         | ✅ Works well (`Partial<T>`, `Pick<T>`).                                  | ❌ Not designed for this.                                                     |
| **Readability in Large Projects**| Great for **internal helpers** and unions.                                | Great for **public APIs** and extensible models.                              |
| **Performance (TS Compiler)**    | Slightly better optimized for unions & advanced types.                    | Optimized for large object models and declaration merging.                    |
| **When to Use?**                 | - For **flexibility** (unions, intersections).<br>- When aliasing primitives. | - For **contracts, models, public APIs**.<br>- When extensibility is needed. |

---

### 🔑 Quick Takeaway
- Use **`type`** when you need **flexibility** (unions, intersections, aliases, utility types).  
- Use **`interface`** when you want to define **structured object shapes** that may be extended/merged.  

---

## 13. Generics
```ts
function identity<T>(value: T): T {
  return value;
}
let output = identity<number>(100);
```

---

## Generics:

# What are Generics in TypeScript?

Generics are a feature in TypeScript that allows you to create reusable and type-safe components, functions, classes, and interfaces that can work with a variety of data types without sacrificing the benefits of strong typing.

Think of them as placeholder types or type variables that you define when creating a component, and then specify the actual types when you use that component.

---

## Why Use Generics?

Imagine a function that needs to operate on different types of data, but the logic remains the same. Instead of writing separate functions for each data type, generics allow you to write a single function:

```ts
function process<T>(value: T): T {
  return value;
}

process<string>("hello"); // T becomes string
process<number>(123);      // T becomes number
```

### Analogy:
Generics are like cookie cutters — one shape, but can cut different types of dough (data). They act as templates that adapt to the specific data provided.

---

## Problems Solved by Generics

### Code Duplication
**Without Generics:**
```ts
function getFirstString(arr: string[]): string { return arr[0]; }
function getFirstNumber(arr: number[]): number { return arr[0]; }
function getFirstBoolean(arr: boolean[]): boolean { return arr[0]; }
```

**With Generics:**
```ts
function getFirstElement<T>(arr: T[]): T {
  return arr[0];
}

const firstString = getFirstElement<string>(["apple", "banana"]);
const firstNumber = getFirstElement<number>([1, 2, 3]);
const firstBoolean = getFirstElement<boolean>([true, false]);
```

### Loss of Type Safety with `any`
**Problem:** Using `any` disables TypeScript's type checks.
```ts
function identityAny(arg: any): any {
  return arg;
}
const resultAny = identityAny("hello");
resultAny.toFixed(); // Runtime error
```

**Solution with Generics:**
```ts
function identityGeneric<T>(arg: T): T {
  return arg;
}
const resultString = identityGeneric("hello");
const resultNumber = identityGeneric(123);
```

### Reusable Data Structures/API Clients
**Generic Stack:**
```ts
class Stack<T> {
  private elements: T[] = [];
  push(element: T): void { this.elements.push(element); }
  pop(): T | undefined { return this.elements.pop(); }
  peek(): T | undefined { return this.elements[this.elements.length - 1]; }
  isEmpty(): boolean { return this.elements.length === 0; }
}

const numberStack = new Stack<number>();
numberStack.push(10);
numberStack.push(20);

const stringStack = new Stack<string>();
stringStack.push("apple");
stringStack.push("banana");
```

---

## How Generics Work

### Type Parameters
- Usually single uppercase letters: `T`, `K`, `V`, `E`
- Declared using angle brackets: `<T>`

### Inference and Constraints
- TypeScript infers `T` automatically or you can specify it
- You can constrain `T` using `extends`

**Example with Constraint:**
```ts
interface HasLength { length: number; }

function logLength<T extends HasLength>(arg: T): void {
  console.log(arg.length);
}

logLength("hello");       // string
logLength([1, 2, 3]);      // array
// logLength(10);         // Error: number has no .length
```

---

## Examples of Generics

### 1. Generic Functions
```ts
function identity<T>(arg: T): T {
  return arg;
}
let outputString = identity<string>("myString");
let outputNumber = identity(123);
```

**Get Object Property by Key:**
```ts
function getProperty<T, K extends keyof T>(obj: T, key: K) {
  return obj[key];
}

const user = { name: "Alice", age: 30 };
const userName = getProperty(user, "name");
```

### 2. Generic Interfaces
```ts
interface Box<T> {
  value: T;
}

let stringBox: Box<string> = { value: "Hello Generics" };
let numberBox: Box<number> = { value: 123 };
```

**Multiple Type Parameters:**
```ts
interface Pair<K, V> {
  key: K;
  value: V;
}
const userLogin: Pair<string, boolean> = { key: "isActive", value: true };
```

**Function Type Interface:**
```ts
interface GenericFunction<T> {
  (arg: T): T;
}

let myIdentity: GenericFunction<number> = identity;
```

### 3. Generic Classes
```ts
class DataStore<T> {
  private data: T[] = [];

  add(item: T): void {
    this.data.push(item);
  }

  get(index: number): T | undefined {
    return this.data[index];
  }

  getAll(): T[] {
    return this.data;
  }
}

const stringStore = new DataStore<string>();
stringStore.add("apple");

const numberStore = new DataStore<number>();
numberStore.add(100);
```

### 4. Real-World Applications
- **Reusable React components** (tables, dropdowns)
- **Data structures** like stacks or queues
- **Type-safe API clients**
- **Generic utility functions** (`map`, `filter`, etc.)
- **Custom React Hooks**

---

## Summary

- Generics enable you to write **reusable, type-safe** code
- Avoid using `any`; prefer generics for safety and flexibility
- Widely used in **functions, classes, interfaces, and APIs**
- They **reduce code duplication**, increase maintainability, and improve scalability

> **Best practice:** Use generics to maximize the power of TypeScript's type system without sacrificing flexibility



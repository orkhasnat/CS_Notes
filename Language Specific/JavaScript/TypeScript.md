# Basics of TypeScript
(Source: ChatGPT)

### 1. What is TypeScript?
TypeScript is a **superset of JavaScript** that adds optional static types.  
It compiles down to plain JavaScript and can run anywhere JavaScript runs (browser, Node.js, etc.).  
TypeScript helps to catch errors during development by using types, improving code quality, and offering better tooling support (like autocompletion and refactoring).

### 2. Basic Types in TypeScript
TypeScript includes all JavaScript data types and adds its own type annotations.

#### Primitive Types:
- `number`: Represents both integers and floating-point numbers.
```typescript
let num: number = 42;
```
- `string`: Represents text.
```typescript
let name: string = "John";
```
- `boolean`: Represents true or false values.
```typescript
let isActive: boolean = true;
```
- `null` and `undefined`: Both types are also available as their own types.
```typescript
let empty: null = null;
let notAssigned: undefined = undefined;
```
#### Arrays:
You can define an array with a type by using `[]` or `Array<T>`.
```typescript
let numbers: number[] = [1, 2, 3];
let strings: Array<string> = ["apple", "banana"];
```
#### Tuples:
Fixed-size arrays with elements of different types.
```typescript
let tuple: [string, number] = ["John", 30];
```
#### Enums:
Enums allow you to define a set of named constants.
```typescript
enum Direction {
	Up = 1,
	Down,
	Left,
	Right
}
let direction: Direction = Direction.Up;
```
#### Any:
The `any` type disables type checking, allowing any kind of value.
```typescript
let anything: any = 5;
anything = "Now a string";
```
#### Void:
Represents the absence of a type, typically used for functions that don’t return a value.
```typescript
function logMessage(message: string): void {
	console.log(message);
}
```
#### Never:
Represents a value that never occurs, like a function that throws an error or loops forever.
```typescript
function throwError(message: string): never {
	throw new Error(message);
}
```
### 3. Interfaces
Interfaces define the shape of an object, including the types of its properties and methods.
```typescript
interface Person {
  name: string;
  age: number;
  greet(): void;
}

const person: Person = {
  name: "John",
  age: 30,
  greet: () => { console.log("Hello!"); }
};
```

Interface works similar to `[Go] Interface` i.e. they can be implemented by classes. Also using the `extends` keyword, new modified interfaces can be build on top of parent interface.

Example of implementing interfaces:
```typescript
interface Animal {
  name: string;
  makeSound(): void;
}

class Dog implements Animal {
  name: string;
  constructor(name: string) {
    this.name = name;
  }

  makeSound(): void {
    console.log("Woof!");
  }
}
```
### 4. Classes and Object-Oriented Programming
TypeScript supports classes, inheritance, and other object-oriented concepts.
#### Class Declaration:
```typescript
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet(): void {
    console.log(`Hello, my name is ${this.name}.`);
  }
}

const john = new Person("John", 30);
john.greet();

```
#### Inheritance:
```typescript
class Employee extends Person {
  position: string;

  constructor(name: string, age: number, position: string) {
    super(name, age);
    this.position = position;
  }

  getPosition(): void {
    console.log(`${this.name} works as a ${this.position}`);
  }
}

const jane = new Employee("Jane", 28, "Engineer");
jane.getPosition();

```
### 5. Generics
Generics allow you to write flexible, reusable code by defining a type placeholder.
```typescript
function identity<T>(value: T): T {
  return value;
}

let result = identity(5); // inferred as number
let stringResult = identity("hello"); // inferred as string

```
### 6. Type Aliases

You can define custom types with `type`.
```typescript
type Point = {
  x: number;
  y: number;
};

let point: Point = { x: 5, y: 10 };
```

Types are basically like `[C,C++] Struct`. They can not be implemented or extended like interfaces. To extend a type alias we can use intersections(`&`) and unions(`|`).

For example:
```typescript
type Animal = { name: string };
type Age = { age: number };
type Person = Animal & Age;  // Intersection
const person: Person = { name: "John", age: 30 };

type StringOrNumber = string | number;  // Union type
const value: StringOrNumber = "Hello";

```
### 7. Type Assertions
TypeScript allows you to assert the type of a value when you're sure about its type.
```typescript
let someValue: unknown = "Hello World";
let stringLength: number = (someValue as string).length;
```
### 8. Modules
TypeScript supports modules, allowing code to be split across multiple files.
```typescript
// person.ts
export interface Person {
  name: string;
  age: number;
}

// main.ts
import { Person } from './person';
let user: Person = { name: "Alice", age: 25 };
```
### 9. TypeScript Configuration (`tsconfig.json`)

The TypeScript configuration file allows you to customize TypeScript behavior (e.g., module resolution, target version, etc.).

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true,
    "outDir": "./dist"
  }
}
```
### 10. Type Inference
TypeScript can often infer the type of a variable based on its initial value, eliminating the need for explicit type annotations.
```typescript
let greeting = "Hello";  // inferred as string
greeting = 5;  // Error: Type 'number' is not assignable to type 'string'
```
### 11. Advanced Types

#### Union Types:
Allow a value to be one of several types.

```typescript
let value: string | number;
value = "Hello";
value = 42;
```
#### Intersection Types:
Combine multiple types into one.
```typescript
interface A {
  a: string;
}
interface B {
  b: string;
}

type C = A & B;
const obj: C = { a: "Hello", b: "World" };
```
#### Type Guards:
Narrow down types based on conditions.
```typescript
function isString(value: string | number): boolean {
  return typeof value === "string";
}
```
### 12. Decorators (Experimental)
Decorators are an experimental feature in TypeScript, allowing you to add metadata or modify classes and methods.
```typescript
function log(target: any, key: string) {
  console.log(`${key} was called`);
}

class Greeter {
  @log
  greet() {
    console.log("Hello!");
  }
}
```
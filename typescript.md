- [the basics](#the-basics)
  - [TypeScript compiler](#typescript-compiler)
- [types](#types)
  - [type assertions](#type-assertions)
  - [literal types](#literal-types)
  - [`null` and `undefined`](#null-and-undefined)
  - [non-null assertion operator (Postfix `!`)](#non-null-assertion-operator-postfix-)
  - [enums](#enums)
- [narrowing](#narrowing)
  - [`typeof` type guards](#typeof-type-guards)
  - [truthiness narrowing](#truthiness-narrowing)
  - [equality narrowing](#equality-narrowing)
  - [the `in` operator narrowing](#the-in-operator-narrowing)
  - [`instanceof` narrowing](#instanceof-narrowing)
  - [assignments](#assignments)
  - [type predicates](#type-predicates)
  - [discriminated unions](#discriminated-unions)
- [more on functions](#more-on-functions)
  - [function type expressions](#function-type-expressions)
  - [call signatures](#call-signatures)
  - [construct signatures](#construct-signatures)
  - [generic functions](#generic-functions)

# the basics

## TypeScript compiler

- install: `npm install -g typescript`
- build: `tsc hello.ts`
  - ECMAScript version: `tsc --target es2015 hello.ts`
  - if installed on local project: `node_modules/typescript/bin/tsc test.ts`

# types

- the primitives: `string`, `number`, and `boolean`
- arrays: `number[]` or `Array<number>`
- any
- functions
  - parameter type annotations: `function greet(name: string) {...`
  - return type annotations: `function getFavoriteNumber(): number {...`
- object types: `function printCoord(pt: { x: number; y: number }) {...`
  - optional properties: `function printName(obj: { first: string; last?: string }) {...`
    - check for `undefined` before using it
- union types: `function printId(id: number | string) {...`
  - narrowing: TypeScript will only allow an operation if it is valid for every member of the union. (if every member in a union has a property in common, you can use that property without narrowing)
    - TypeScript knows that only a `string` value will have a `typeof` value `string`: `...if (typeof id === "string") {...`
    - another example is to use a function like `Array.isArray`: `...if (Array.isArray(x)) {...`
- type aliases: name for any type
  ```ts
  type Point = {
    x: number;
    y: number;
  };
  ```
  - alias can give a name to any type at all: `type ID = number | string;`
- interfaces: is another way to name an object type
  ```ts
  interface Point {
    x: number;
    y: number;
  }
  function getDimension(dim: Point): InterfaceName {}
  class NameofClass implements InterfaceName {}
  ```
- type aliases vs interfaces: he key distinction is that a type cannot be re-opened to add new properties vs an interface which is always extendable
  - interfaces will always be named in error messages
  - type aliases may not participate in declaration merging, but interfaces can
  - interfaces may only be used to declare the shapes of objects, not rename primitives
  - interface names will always appear in their original form in error messages, but only when they are used by name

**use `interface` until you need to use `features` from type**

## type assertions

specify a more specific type when TypeScript can’t know about the value

```ts
const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;
```

- angle-bracket syntax: `const myCanvas = <HTMLCanvasElement>document.getElementById("main_canvas");`

## literal types

combining literals into unions, you can express a much more useful concept - for example, functions that only accept a certain set of known values

- `function printText(s: string, alignment: "left" | "right" | "center") {...`
- `function compare(a: string, b: string): -1 | 0 | 1 {...`
- ```ts
  interface Options {
    width: number;
  }
  function configure(x: Options | "auto") {}
  ```

## literal inference

after initialize a variable with an object, TypeScript assumes that the properties of that object might change values later

```ts
const req = { url: "https://example.com", method: "GET" } as const;
handleRequest(req.url, req.method);
```

## `null` and `undefined`

- `strictNullChecks` off: values that might be `null` or `undefined` can still be accessed normally, and can be assigned to a property of any type
- `strictNullChecks` on: test for `null` or `undefined` before using methods or properties

  ```ts
  function doSomething(x: string | null) {
    if (x === null) {
      // do nothing
    } else {
      console.log("Hello, " + x.toUpperCase());
    }
  }
  ```

## non-null assertion operator (Postfix `!`)

writing `!` after any expression is effectively a type assertion that the value isn’t null or undefined

```ts
function liveDangerously(x?: number | null) {
  console.log(x!.toFixed());
}
```

## enums

allows for describing a value which could be one of a set of possible named constants

```ts
enum Direction {
  Up = 1,
  Down,
  Left,
  Right,
}
enum UserResponse {
  No = 0,
  Yes = 1,
}
function respond(recipient: string, message: UserResponse): void {}
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT",
}
enum Status {
  NotStarted = "notStarted",
  InProgress = "inProgress",
  Done = "done",
}
interface Task {
  id: string;
  status: Status;
}
```

# narrowing

process of refining types to more specific types than declared

```ts
function padLeft(padding: number | string, input: string) {
  if (typeof padding === "number") {
    return " ".repeat(padding) + input;
  }
  return padding + input;
}
```

## `typeof` type guards

In TypeScript, checking against the value returned by typeof is a type guard

- `string`
- `number`
- `bigint`
- `boolean`
- `symbol`
- `undefined`
- `object` (`typeof null` is actually `object`, users with enough experience might not be surprised)
- `function`

## truthiness narrowing

in JavaScript, constructs like `if` first "coerce" their conditions to `boolean`. `if (strs && typeof strs === "object") {}`

## equality narrowing

TypeScript also uses `switch` statements and equality checks like `===`, `!==`, `==`, and `!=` to narrow types

```ts
function example(x: string | number, y: string | boolean) {
  if (x === y) {
  }
}
```

## the `in` operator narrowing

the `in` operator, determining if an object has a property with a name. TypeScript takes this into account as a way to narrow down potential types

```ts
type Fish = { swim: () => void };
type Bird = { fly: () => void };
function move(animal: Fish | Bird) {
  if ("swim" in animal) {
    return animal.swim();
  }
  return animal.fly();
}
```

## `instanceof` narrowing

JavaScript has an operator for checking whether or not a value is an "instance" of another value

```ts
function logValue(x: Date | string) {
  if (x instanceof Date) {
    console.log(x.toUTCString());
  } else {
    console.log(x.toUpperCase());
  }
}
```

## assignments

when we assign to any variable, TypeScript looks at the right side of the assignment and narrows the left side appropriately

```ts
let x = Math.random() < 0.5 ? 10 : "hello world!";
// let x: string | number
x = 1;
console.log(x);
x = "goodbye!";
console.log(x);
x = true;
// 👆 Type 'boolean' is not assignable to type 'string | number'.
```

## type predicates

a predicate takes the form `parameterName is Type`, where `parameterName` must be the name of a parameter from the current function signature

```ts
function isFish(pet: Fish | Bird): pet is Fish {
  return (pet as Fish).swim !== undefined;
}
let pet = getSmallPet();
if (isFish(pet)) {
  pet.swim();
} else {
  pet.fly();
}
```

## discriminated unions

They’re good for representing any sort of messaging scheme in JavaScript

```ts
interface Circle {
  kind: "circle";
  radius: number;
}
interface Square {
  kind: "square";
  sideLength: number;
}
type Shape = Circle | Square;
function getArea(shape: Shape) {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.sideLength ** 2;
  }
}
```

exhaustiveness checking

The `never` type is assignable to every type; however, no type is assignable to `never` (except `never` itself).

```ts
interface Triangle {
  kind: "triangle";
  sideLength: number;
}
type Shape = Circle | Square | Triangle;
function getArea(shape: Shape) {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.sideLength ** 2;
    default:
      const _exhaustiveCheck: never = shape;
      // Type 'Triangle' is not assignable to type 'never'. 😉
      return _exhaustiveCheck;
  }
}
```

# more on functions

## function type expressions

the simplest way to describe a function

```ts
function greeter(fn: (a: string) => void) {
  fn("Hello, World");
}
function printToConsole(s: string) {
  console.log(s);
}
greeter(printToConsole);
```

### type alias to name a function type

```ts
type GreetFunction = (a: string) => void;
function greeter(fn: GreetFunction) {
  // ...
}
```

## call signatures

write a _call signature_ in an object type

```ts
type DescribableFunction = {
  description: string;
  (someArg: number): boolean;
};
function doSomething(fn: DescribableFunction) {
  console.log(fn.description + " returned " + fn(6));
}
```

## construct signatures

JavaScript functions can also be invoked with the `new` operator

```ts
type SomeConstructor = {
  new (s: string): SomeObject;
};
function fn(ctor: SomeConstructor) {
  return new ctor("hello");
}
```

## generic functions

In TypeScript, generics are used when we want to describe a correspondence between two values. We do this by declaring a _type parameter_ in the function signature:

```ts
function firstElement<Type>(arr: Type[]): Type | undefined {
  return arr[0];
}
// s is of type 'string'
const s = firstElement(["a", "b", "c"]);
// n is of type 'number'
const n = firstElement([1, 2, 3]);
// u is of type undefined
const u = firstElement([]);
```

# What is TypeScript?
- TypeScript = JavaScript + Type Safety + Extra Features
- Superset of JS
- Adds static typing
- Helps catch errors during development
- Compiles to JavaScript


## Types in TypeScript
Primitive Types
Basic, immutable values.
 - string
 - number
 - boolean
 - null
 - undefined
 - bigint
 - symbol
   ```ts
   let name: string = "Nishu";
   let age: number = 22;
   let isOk: boolean = true;
   ```

Reference Types
Store address/reference, not value.
- objects
- arrays
- functions

```ts
let obj: {name: string} = { name: "Nidhi" };
```

  ## Arrays
  ```ts
let numbers: number[] = [1, 2, 3];
let names: string[] = ["Nishu", "Nidhi"];
```
## Tuples
Definition:
Tuple is an array with fixed size + fixed types in each position.
(Hindi: Tuple ek aisa array hota hai jisme konsa element kis position pe aayega wo fixed hota hai.)
```ts
let arr: [string, number] = ["Nishu", 22];
```
## Enums
Enum (short for enumeration) is a feature in TypeScript that lets you define a group of named constant values.
Use enums when you have a fixed set of values that are related.
Enums make your code more readable, meaningful, and type-safe.
```ts
enum Role {
  ADMIN,
  USER,
  GUEST
}
```
# Special Types
## ANY
The any type is the most flexible and most permissive type in TypeScript.
- ✔ Meaning:
When a variable is typed as any, TypeScript disables all type checking for that variable.
- ✔ Effect:
The variable can hold any value — string, number, boolean, object, array, function, etc.
- 🧨 Why any is dangerous?
Because it removes all type safety — the main advantage of TypeScript.
Example:
```ts
let data: any = "Hello";
data = 10;
data.trim(); // ❌ No error in TS, but runtime error (10 has no trim)
```
No warnings → runtime crash → unsafe.
- ✔ When to use any (only when necessary):
  - When type is unknown or temporary
  - While gradually converting JavaScript → TypeScript
  - When you intentionally want to skip checks
 Best Practice:
- 👉 Use unknown instead of any whenever possible
 (because unknown requires type checking)

- 🔥 In One Line
any = turn off TypeScript’s type checking completely → maximum flexibility but minimum safety.

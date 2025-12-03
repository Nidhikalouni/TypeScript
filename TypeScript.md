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
# UNKNOWN
The unknown type represents a value whose type is not known at the time of writing the code, but unlike any, it does NOT allow unsafe operations.
It is the type-safe version of any.
⭐ Key Properties of unknown
✔ 1. You can assign anything to unknown
```ts
let value: unknown;
value = "Hello";
value = 42;
value = true;
value = { name: "Nidhi" };
```
✔ 2. But you cannot use the value without checking its type first
```
let data: unknown = "abc";
// ❌ Error: Cannot call method on unknown
data.toUpperCase();
```
⭐ To use an unknown variable → You Must Do Type Narrowing
```ts
let data: unknown = "Hello";
if (typeof data === "string") {
  console.log(data.toUpperCase()); // ✔ safe
}
```
###  unknown vs any 
<img width="1138" height="287" alt="image" src="https://github.com/user-attachments/assets/7dcc0ee3-f0fc-43f2-be60-fd5e2c57e1cd" />
Example:
```ts
let a: any = "hello";
a.trim();     // ✔ No error (unsafe)
let b: unknown = "hello";
b.trim();     // ❌ Error (must narrow type first)
```
⭐ Use Cases of unknown

 Use unknown when:
 -You are working with API data that may vary.
 You truly don’t know the type yet.
 You want flexibility with safety.

🔥 In One Line
unknown = safer alternative to any, flexible but requires type checking before use.

# VOID
The void type is used to represent the absence of a value.
✔ Mainly used for:
- Functions that do not return anything
- Rarely used for variables (not recommended)

#### ⭐ 1. void in Functions 
A function with return type void does not return a value.
```ts
function greet(): void {
  console.log("Hello, Nidhi!");
}
```

✔ This tells TypeScript:
“This function performs an action but does NOT return anything.”

If you try to return something, TS will give an error:
```ts
function test(): void {
  return 10;  // ❌ Error
}
```
#### ⭐ 2. void with variables (not useful)
```ts
let x: void = undefined;   // ✔ allowed
let y: void = null;        // ✔ allowed in non-strict mode
```
But variables of type void are not practical because they can only hold undefined (or null).
So we rarely use this.
⭐ Why void is important?
Because it clearly tells other developers:
👉 This function is for performing an operation, not giving a result.
Example: logging, printing, saving to DB, updating UI, etc.
## ⭐ Difference between void vs never (quick)
Type	Meaning
void	Function does not return a value
never	Function never returns at all (infinite loop / throws error)
# NULL
null is a primitive type in TypeScript that represents
👉 intentional absence of a value
or
👉 empty value.
It explicitly means:
“There is no value here.”

⭐ Example
```ts
let user: string | null = null;
```
Here, user intentionally has no value.
# UNDEFINED
undefined is a primitive type in TypeScript that represents:
👉 a variable that has been declared but not assigned a value yet
It means:
“Value is missing because nothing was assigned.”
```ts
let x;
console.log(x);  // undefined
```
Since x has no value, JavaScript automatically sets it to undefined.
# Difference b/w NULL & UNDEFINED
<img width="987" height="483" alt="image" src="https://github.com/user-attachments/assets/18d5e140-ffd1-4a94-919d-20350f3a79ae" />

# NEVER
never is a special type that represents a value that never occurs.

✔ It means:
- The function never returns
- The code never reaches that point
- A variable cannot have any possible value

## 🔥 Where is never used?
1. Functions that never return
Example: Functions that always throw an error.
```ts
function throwError(msg: string): never {
  throw new Error(msg);
}
```
This returns nothing, not even void, because it never finishes.

2. Infinite loops
```ts
function infiniteLoop(): never {
  while (true) {}
}
```
This function never ends, so the return type is never.

# Type Inference in TypeScript
Type inference means:
➡️ TypeScript automatically figures out the type of a variable without you explicitly writing it.
You don’t need to write:
```ts
let x: number = 10;
TypeScript can infer it:
let x = 10;   // TS infers: number
```
🔥 1. Variable Type Inference
let message = "Hello";
TypeScript infers:
message is a string
You cannot assign anything else:
message = 10;   // ❌ Error

🔥 2. Function Return Type Inference

You don’t need to specify return type:
```ts
function add(a: number, b: number) {
  return a + b;
}
```
TS infers return type as:
➡️ number

#  Type Annotations in TypeScript
Type Annotation means:
➡️ You explicitly tell TypeScript what the type of a variable, function parameter, or return value is.
You write the type manually.

Example:
```ts
let age: number = 20;
```
Here : number is the type annotation.
##### ✨ Why do we use Type Annotations?

✔ To make code more readable
✔ To avoid mistakes
✔ When TypeScript cannot infer the type automatically
✔ Useful in functions, objects, variables, arrays, parameters, classes, etc.
#### Type annotations are used to specify types manually.
They can be added to:
- ✔ Variables
- ✔ Functions (parameters + return type)
- ✔ Arrays
- ✔ Tuples
- ✔ Objects
- ✔ Class properties
- ✔ Function variables
- ✔ Interfaces & Type Aliases

# ⭐ Interfaces in TypeScript
Definition:
An interface in TypeScript is used to define the shape of an object.
It specifies what properties and methods an object should have.
Think of it as a contract — any object implementing an interface must follow the defined structure.
## 🔹 1. Basic Interface Example
```ts
interface Person {
  name: string;
  age: number;
}

let user: Person = {
  name: "Nidhi",
  age: 22
};
```
Here, user must have name (string) and age (number), otherwise TypeScript throws an error.

## 🔹 2. Optional Properties

Add ? to make a property optional:
```ts
interface Person {
  name: string;
  age?: number; // optional
}

let user1: Person = { name: "Aman" }; // ✔ valid
let user2: Person = { name: "Nidhi", age: 22 }; // ✔ valid
```
## 🔹 3. Readonly Properties
Make properties read-only (cannot be changed after initialization):
```ts
interface Person {
  readonly id: number;
  name: string;
}

let user: Person = { id: 101, name: "Nidhi" };
user.id = 102; // ❌ Error
```
## 🔹 4. Methods in Interface
Interfaces can define methods as well:
```ts
interface Person {
  name: string;
  age: number;
  greet(): void;
}

let user: Person = {
  name: "Nidhi",
  age: 22,
  greet() {
    console.log("Hello " + this.name);
  }
};
```
## 🔹 5. Extending Interfaces

Interfaces can inherit from other interfaces using extends.
```ts
interface Person {
  name: string;
  age: number;
}

interface Employee extends Person {
  salary: number;
}

let emp: Employee = {
  name: "Nidhi",
  age: 22,
  salary: 50000
};
```
## 🔹 6. Interface Merging

If two interfaces have the same name, TypeScript merges them automatically:
```ts
interface User {
  name: string;
}

interface User {
  age: number;
}

let u: User = { name: "Nidhi", age: 22 }; // ✔ merged interface
```
## 🔹 7. Implementing Interfaces in Classes

A class can implement an interface to ensure it follows the structure.
```ts
interface Person {
  name: string;
  greet(): void;
}

class Employee implements Person {
  constructor(public name: string) {}
  
  greet() {
    console.log("Hello " + this.name);
  }
}

let emp = new Employee("Nidhi");
emp.greet(); // Hello Nidhi
```
# ⭐ Type Aliases in TypeScript
Definition:
A type alias allows you to create a custom name for any type in TypeScript.
You use the type keyword to define:
- Primitive types
- Object types
- Union types
- Function types
- Tuple types
- Intersection types

Basically → type can name any type.

### ✅ 1. Basic Type Alias
```ts
type Name = string;
let userName: Name = "Nidhi";
```
### 2. Type Alias for Object
```ts
type User = {
  id: number;
  name: string;
};

let u1: User = {
  id: 1,
  name: "Nidhi"
};
```
### ✅ 3. Type Alias for Union Types
```ts
type ID = number | string;
let userId: ID = 101;
let orderId: ID = "ORD123";
```
Union means: value can be one of several types.

### ✅ 4. Type Alias for Function Types
```ts
type Add = (a: number, b: number) => number;
const sum: Add = (x, y) => x + y;
```
### ✅ 5. Type Alias for Tuple
```ts
type PersonTuple = [string, number];
let p: PersonTuple = ["Nidhi", 22];
```
### ✅ 6. Type Alias with Intersection Types

Combine multiple types:
```ts
type Person = {
  name: string;
};
type Employee = {
  salary: number;
};
type Staff = Person & Employee;

let s: Staff = {
  name: "Nidhi",
  salary: 50000
};
``` 
# ⭐ Difference Between Type Alias & Interface
<img width="1000" height="351" alt="image" src="https://github.com/user-attachments/assets/398c61b7-27bc-490b-8394-adfaa0bb2032" />

## ⭐ When to Use What?
 Use interface when:

- You are defining object shapes
- You need extendable structure
- A class will implement it
  
 Use type alias when:
- You need union, intersection
- You define primitive or function types
- You want more flexibility

🎯 In One Line

👉 interface = object structure
👉 type = can define ANY type (unions, primitives, objects, tuples, etc.)

# ⭐ Classes and Objects in TypeScript

A class is a blueprint for creating objects.
An object is an instance of a class.

### 🔹 1. Class Definition
```ts
class Person {
  name: string;
  age: number;

  showInfo() {
    console.log(this.name, this.age);
  }
}
```
### 🔹 2. Creating Objects
```ts
let p1 = new Person();
p1.name = "Nidhi";
p1.age = 22;
p1.showInfo();
```
### 🔹 3. Constructor

A constructor runs automatically when an object is created.
```ts
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
}

let p = new Person("Nidhi", 22);
```
### 🔹 4. this Keyword

Refers to the current object
Used to access class properties & methods
```ts
class Car {
  model: string;

  constructor(model: string) {
    this.model = model; // refers to the current object's model
  }
}
```

### 🔹 5. Access Modifiers
- Modifier	Meaning
- public	Accessible everywhere (default)
- private	Accessible ONLY inside the class
- protected	Accessible inside class + child classes
Example:
```ts
class Person {
  public name: string;
  private age: number;
  protected salary: number;
}
```
### 🔹 6. Readonly Properties

You cannot change them after initialization.
```ts
class Student {
  readonly rollNo: number;

  constructor(rollNo: number) {
    this.rollNo = rollNo;
  }
}

let s = new Student(101);
s.rollNo = 102; // ❌ Error
```
### 🔹 7. Optional Properties

Use ? inside class:
```ts
class Person {
  name: string;
  age?: number; // optional
}

let p = new Person();
p.name = "Nidhi";   // OK
p.age = 22;         // OK
```
### 🔹 8. Parameter Properties 

TS provides a shortcut to declare + assign properties directly inside constructor.
```ts
class Person {
  constructor(public name: string, private age: number) {}
}

let p = new Person("Nidhi", 22);
```
This single line:
constructor(public name: string, private age: number) {}
means:
- Create property name
- Create property age
- Assign values
- Set access modifiers

### 🔹 9. Getters and Setters

Used to control access to private properties.
```ts
class Employee {
  private _salary: number;

  constructor(salary: number) {
    this._salary = salary;
  }

  get salary() {
    return this._salary;
  }

  set salary(value: number) {
    if (value > 0) this._salary = value;
  }
}

let e = new Employee(50000);
console.log(e.salary); // getter
e.salary = 60000;      // setter
```
### 🔹 10. Static Members

static properties belong to the class itself, not the objects.
```ts
class Student {
  static collegeName = "DBUU";

  static getCollege() {
    return Student.collegeName;
  }
}

console.log(Student.getCollege());
```
### 🔹 11. Abstract Classes & Methods

Used as a base class → cannot be instantiated directly.

Abstract Class
```ts
abstract class Shape {
  abstract area(): number; // abstract method

  show() {
    console.log("Shape");
  }
}

Child Class must implement abstract methods
class Circle extends Shape {
  constructor(public radius: number) {
    super();
  }

  area() {
    return Math.PI * this.radius * this.radius;
  }
}

let c = new Circle(5);
console.log(c.area());
```


#  1. Functions in TypeScript

A function in TypeScript works like JavaScript but includes type checking for
- Parameters
- Return values

✔ Example:
```ts
function greet(name: string): string {
  return "Hello " + name;
}
```
Key Points:
name: string → parameter 
type: string → return type
You cannot return a number if return type is string
TS catches mistakes at compile time

# ✅ 2. Function Type (Function Signature)

A function type describes what a function should look like:
→ What parameters it accepts
→ What its return type is

It helps when assigning functions to variables.

✔ Example:
```ts
let calculate: (x: number, y: number) => number;
calculate = (a, b) => a + b;   // ✔ valid
calculate = (a, b) => a + b + ""; // ❌ error (string return)
```
Why use it?
- Gives structure
- Prevents assigning wrong functions
- Used heavily in callbacks, React, higher-order functions

# ✅ 3. Optional Parameter (?)

An optional parameter does not need to be passed when calling the function.

✔ Example:
```ts
function print(name: string, age?: number) {
  console.log(name, age);
}
print("Nidhi");        // OK
print("Nidhi", 22);    // OK
```
Rules:
- Use ? to mark as optional
- Optional parameters must come after required parameters

# ✅ 4. Default Parameter

A default parameter has a fallback value, used when that parameter is not passed.
```ts
✔ Example:
function multiply(a: number, b: number = 2) {
  return a * b;
}
multiply(5);     // 10 (uses default 2)
multiply(5, 4);  // 20
```
Difference from optional:
Optional	Default
Can be undefined	Never undefined (gets default value)
No automatic value	Has fallback value
# ✅ 5. Rest Parameter (...)

Used when you don't know how many arguments will be passed.
```ts
✔ Example:
function sum(...nums: number[]) {
  return nums.reduce((a, b) => a + b, 0);
}
sum(1, 2, 3);        // 6
sum(10, 20, 30, 40); // 100
```
Rules:

- Rest parameter must be the last parameter
- Type is always an array

# ✅ 6. Function Overloading

TypeScript allows multiple function signatures for one function.
This lets the same function accept different types of inputs.
```ts
✔ Example:
function show(x: string): string;
function show(x: number): number;

function show(x: any) {
  return x;
}
```
Explanation:

- First two lines are overload signatures
- Last function is actual implementation
- Only the overload types are allowed: string or number

Wrong usage:
show(true);   // ❌ Error -> boolean is not in overload list
Why use overloads?
When the same function should behave differently based on input type
Common in libraries (e.g., arrays, DOM, React)
Helps with strong type safety

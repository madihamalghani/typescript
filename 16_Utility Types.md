# Utility Types:

Another example:

```tsx
type PointPrinter = (p: { x: number; y: string; z: number }) => boolean;

type R = ReturnType<PointPrinter>;
// R = boolean

```

---

###  **Difference**


TypeScript comes with a large number of types that can help with some common type manipulation, usually referred to as utility types.

## Partial:

`Partial` changes all the properties in an object to be optional.

```tsx
interface Point {
  x: number;
  y: number;
}

let pointPart: Partial<Point> = {}; // `Partial` allows x and y to be optional
pointPart.x = 10;
```

### Why this matters

Normally, if you did:

```tsx
let p: Point = {};

```

You’d get an error ❌, because `x` and `y` are **required** in `Point`.

But with `Partial<Point>`, both `x` and `y` are **optional**, so you can start with an empty object `{}` and add properties later.

## Required

`Required` changes all the properties in an object to be required.

```tsx
interface Car {
  make: string;
  model: string;
  mileage?: number;
}

let myCar: Required<Car> = {
  make: 'Ford',
  model: 'Focus',
  mileage: 12000 // `Required` forces mileage to be defined
};
```

## **Record:**

`Record` is a shortcut to defining an object type with a specific key type and value type.

```tsx
const nameAgeMap: Record<string, number> = {
  'Alice': 21,
  'Bob': 25
}
```

Note:

<aside>

`Record<string, number>` is equivalent to `{ [key: string]: number }`

</aside>

## Omit

`Omit` removes keys from an object type.

```tsx
interface Person2 {
    name: string;
    age: number;
    location?: string;
}

const bob: Omit<Person2, 'age' | 'location'> = {
    name: 'Bob',
    // age: 30, // Error: Object literal may only specify known properties
    // `Omit` has removed age and location from the type and they can't be defined here
};
console.log(bob); // Output: { name: 'Bob' }
```

## Pick:

`Pick` removes all but the specified keys from an object type.

```tsx
interface Person {
  name: string;
  age: number;
  location?: string;
}

const bob: Pick<Person, 'name'> = {
  name: 'Bob'
  // `Pick` has only kept name, so age and location were removed from the type and they can't be defined here
};

```

## Exclude

`Exclude` removes types from a union.

```tsx
type Primitive = string | number | boolean
const value: Exclude<Primitive, string> = true; // a string cannot be used here since Exclude removed it from the type.
```

## ReturnType

`ReturnType` extracts the return type of a function type.

```tsx
type PointGenerator = () => { x: number; y: number; };
const point: ReturnType<PointGenerator> = {
  x: 10,
  y: 20
};
```

Another example:

```tsx
type PointPrinter = (p: { x: number; y: string; z: number }) => boolean;

type R = ReturnType<PointPrinter>;
// R = boolean

```

- Tells what is the return type.

## Parameters:

`Parameters` extracts the parameter types of a function type as an array.

```tsx
type PointPrinter = (p: { x: number; y: number; }) => void;
const point: Parameters<PointPrinter>[0] = {
  x: 10,
  y: 20
};
```

This means:

- `point` must have the same type as the first parameter of `PointPrinter`.
- That type is `{ x: number; y: number }`.

So `point` is correctly typed.

Note:

<aside>

- `Parameters<T>` → tells you *what goes in* (function’s input).
- `ReturnType<T>` → tells you *what comes out* (function’s output).
</aside>

## Readonly:

```tsx
interface Person {
  name: string;
  age: number;
}
const person: Readonly<Person> = {
  name: "Dylan",
  age: 35,
};
person.name = 'kpk'; // prog.ts(11,8): error TS2540: Cannot assign to 'name' because it is a read-only property.
```


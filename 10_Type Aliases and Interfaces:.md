# **Type Aliases and Interfaces:**

TypeScript allows types to be defined separately from the variables that use them.

Aliases and Interfaces allows types to be easily shared between different variables/objects.

⇒ Just like declaring structure to use in future.

## Type Aliases

Type Aliases allow defining types with a custom name (an Alias).

Type Aliases can be used for primitives like `string` or more complex types such as `objects` and `arrays`:

```jsx
type CarYear = number
type CarType = string
type CarModel = string
type Car = {
  year: CarYear,
  type: CarType,
  model: CarModel
}

const carYear: CarYear = 2001
const carType: CarType = "Toyota"
const carModel: CarModel = "Corolla"
const car: Car = {
  year: carYear,
  type: carType,
  model: carModel
};

console.log(car);

const anotherCar:Car ={
    year:2020,
    type:"honda",
    model:"civic"
}
console.log(anotherCar);
```

In more polished form:

```jsx
type CarName=string
type CarPrice=number
type CarModel=string
type Car={
    name:CarName,
    price:CarPrice,
    model?:CarModel //optional property
}
const car:Car={
    name:"Toyota",
    price:5000000
}
console.log(car);
const car2:Car={
    name:"Honda",
    price:4000000,
    model:"2022"}
console.log(car2);
```

- defining type and object structure
- using that structure writing other objects

## **Union and Intersection Types:**

```jsx
type Animal = { name: string };
type Bear = Animal & { honey: boolean };
const bear: Bear = { name: "Winnie", honey: true };

type Status = "success" | "error";
let response: Status = "success";
```

***What’s happing here?***

- defining type for Animal  where name =string
- type Bear = Animal (name: string) & honey: boolean
- so ⇒ Bear= name: string & honey : boolean

---

## **Interfaces:**

Interfaces are similar to type aliases, except they **only** apply to `object` types.

```jsx
interface Rectangle {
  height: number,
  width: number
}

const rectangle: Rectangle = {
  height: 20,
  width: 10
};
```

***Interface Merging***

```jsx
interface Animal { name: string; };
 interface Animal { age: number; } ;
 const dog: Animal = { name: "Fido", age: 5 };
 console.log(dog);
```

## Type vs Interface: Key Differences

- **Extending:** Both can be extended, but interfaces support declaration merging.
- **Unions/Intersections:** Only type aliases support union and intersection types.
- **Implements:** Classes can implement either.
- **Recommendation:** Use `interface` for objects, `type` for everything else.

**Best Practices:**

- Use `interface` for defining object shapes and public APIs.
- Use `type` for unions, intersections, and primitives.
- Favor composition over inheritance for types.
- Document your types and interfaces for clarity.

**Common Pitfalls:**

- Using `type` when you need declaration merging (use `interface`).
- Overcomplicating types, keep them simple and focused.
- Forgetting to update types/interfaces as code evolves.

## Extending Interfaces

Interfaces can extend each other's definition.

**Extending** an interface means you are creating a new interface with the same properties as the original, plus something new.

```jsx
interface Rectangle {
  height: number,
  width: number
}

interface ColoredRectangle extends Rectangle {
  color: string
}

const coloredRectangle: ColoredRectangle = {
  height: 20,
  width: 10,
  color: "red"
}
```


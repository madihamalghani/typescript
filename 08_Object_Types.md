# Object Types:

TypeScript has a specific syntax for typing objects.

**Define key type:**

```jsx
const car: { type: string, model: string, year: number } = {
  type: "Toyota",
  model: "Corolla",
  year: 2009
};
```

TypeScript can infer the types of properties based on their values.

```jsx
const car = {
  type: "Toyota",
};
car.type = "Ford"; // no error
car.type = 2; // Error: Type 'number' is not assignable to type 'string'.
```

🚫 TypeScript checks the object **immediately at creation**, not only later.

**Optional properties are properties that don't have to be defined in the object definition.**

```jsx
const car: { type: string, mileage?: number } = {
  type: "Toyota"
};
car.mileage = 2000; //now allowed
```

## Index Signatures:

Index signatures can be used for objects without a defined list of properties.

```jsx
const nameAgeMap: { [index: string]: number } = {};
nameAgeMap.Jack = 25; // no error
nameAgeMap.Mark = "Fifty"; // Error: Type 'string' is not assignable to type 'number'.
```


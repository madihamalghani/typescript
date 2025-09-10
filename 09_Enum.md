# Enum:

An **enum** is a special "class" that represents a group of constants (unchangeable variables).

Enums come in two flavors `string` and `numeric`.

### 1. Defining the enu

```tsx
enum CardinalDirections {
  North,
  East,
  South,
  West
}

```

- By default, TypeScript gives numbers (`0, 1, 2, 3`) to enum members if you don’t assign them.
- So internally this enum is like:
    
    ```tsx
    {
      North: 0,
      East: 1,
      South: 2,
      West: 3
    }
    
    ```
    

---

### 2. Using the enum

```tsx
let currentDirection = CardinalDirections.North;

```

Here:

- `CardinalDirections.North` equals `0`.
- But **its type** is `CardinalDirections`, not just `number`.
- So `currentDirection` can only hold **values from the enum** (`North, East, South, West`).

---

### 3. Console output

```tsx
console.log(currentDirection);
//logs 0
```

It logs `0` because enums are stored as numbers internally.

---

### 4. Why does this cause an error?

```tsx
currentDirection = 'North';
//  Error

```

- `'North'` is just a plain string, not a member of the enum.
- TypeScript doesn’t allow mixing a normal string with the special `CardinalDirections` type.
- Even though we humans think `"North"` and `CardinalDirections.North` are the same, the compiler sees:
    - `"North"` → string
    - `CardinalDirections.North` → enum member (number in this case)

That’s why ⇒ get the error.

---

### 5. How to use a string instead

If you want `"North"` instead of `0`, you must make it a **string enum**:

```tsx
enum CardinalDirections {
  North = "North",
  East = "East",
  South = "South",
  West = "West"
}

let currentDirection = CardinalDirections.North;
console.log(currentDirection); //  "North"

```

You can assign unique number values for each enum value.

Then the values will not be incremented automatically:

```jsx
enum StatusCodes {
  NotFound = 404,
  Success = 200,
  Accepted = 202,
  BadRequest = 400
}
// logs 404
console.log(StatusCodes.NotFound);
// logs 200
console.log(StatusCodes.Success);

```

🚫 Technically, you can mix and match string and numeric enum values, but it is recommended not to do so.

***Uses:***

We use **enums** for:

- **Readability** (clear names instead of magic numbers/strings).
- **Safety** (prevents invalid values & typos).
- **Maintainability** (easy to expand/change).

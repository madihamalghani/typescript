# Types:

## 1. **Variable Declaration & Type Annotations**

```tsx
let person_name: string;
let age: number;

```

- what type a variable can hold (`string`, `number`).
- Good practice because TypeScript **catches errors at compile time**.

---

## 2. **Union Types**

```tsx
let id: string | number;

```

- Means variable can hold **either string OR number**.
- Useful for things like IDs (`'123abc'` or `123`).

🔪 But don’t overuse unions everywhere. Use them when you really expect multiple types.

---

## 3. **Functions with Types**

```tsx
function welcome(person_name: string, age: number): string {
    return `Welcome dear ${person_name}! I know you are ${age} years old.`;
}

```

- Input parameters have types.
- Return type (`string`) is explicitly declared.
- If you try passing wrong types, TS gives an error → safer code.
- Always type both **parameters** and **return value** in real projects.

---

## 4. **BigInt**

```tsx
const bigNumber: bigint = 9007199254740991n;

```

- Used when numbers are **too large** for normal `number` (above `2^53 - 1`).
- Supported in modern JS/TS.
- You must add `n` at the end, or use `BigInt()`.

---

## 5. **Symbol**

```tsx
const uniqueKey: symbol = Symbol('test');

```

- A `Symbol` is always **unique**, even if you give it the same description.
- Commonly used as object keys to avoid property name clashes.
- Example: used in libraries to create “hidden” object properties.

```jsx
const uniqueKey: symbol = Symbol('symbol for test');
const obj = {
    [uniqueKey]: 'This is a unique property'
};
console.log(obj[uniqueKey]); //This is a unique property
```

---

## 6. **Arrays**

```tsx
let fruits: string[] = ['apple', 'banana'];
let digits: number[] = [1, 2, 3];

```

- `string[]` → array of strings.
- `number[]` → array of numbers.

Alternative syntax:

```tsx
let fruits: Array<string> = ['apple', 'banana'];

```

---

## 7. **Why `any` is Dangerous**

```tsx
let something: any;
something = "hello";
something = 42;

```

- `any` means “turn off TypeScript checks”.
- Compiler won’t protect you → behaves like plain JavaScript.
- Should only be used if:
    - Migrating old JS code to TS, or
    - You truly don’t know the type.

🔪 Overusing `any` = defeats the purpose of TypeScript.

---

## 8. **Better Alternative: `unknown`**

```tsx
let w: unknown = 1;
w = "string";

```

- Like `any`, `unknown` can hold anything.
- BUT: You **cannot use it directly** without checking its type.
- Forces you to do **type checks** (safer).
- Example:
    
    ```tsx
    if (typeof w === "string") {
      console.log(w.toUpperCase()); //  safe
    }
    
    ```
    

👉 Rule of thumb:

- Use `unknown` instead of `any` when possible.
- `unknown` forces safe type checking, `any` bypasses it.

---

## 9. **Type Casting (a.k.a Type Assertions)**

```tsx
(w as { runANonExistentMethod: Function }).runANonExistentMethod();

```

- You “tell” TypeScript: *trust me, this is the type*.
- Use when you know more than the compiler.

But always combine with checks:

```tsx
if (typeof w === "object" && w !== null) {
  (w as { runANonExistentMethod: () => void }).runANonExistentMethod();
}

```

This way, you don’t accidentally crash the program.

---

## 10. **JSON.parse & `any`**

```tsx
const data = JSON.parse('{ "name": "Alice", "age": 30 }');

```

- Returns `any`, because TypeScript doesn’t know the shape.
- Solution → give it a type:
    
    ```tsx
    type Person = { name: string; age: number };
    const data: Person = JSON.parse('{ "name": "Alice", "age": 30 }');
    
    ```
    

Much safer than letting it stay `any`.

---

***Why Avoid Any?***

<aside>

### Avoid `any` When Possible

Using `any` disables TypeScript's type checking.

Instead, consider these alternatives:

- Use type annotations
- Create interfaces for complex objects
- Use type guards for runtime type checking
- Enable `noImplicitAny` in your `tsconfig.json`
</aside>

*Unknown & Any:*

<aside>

**Key differences between `unknown` and `any`:**

- `unknown` must be type-checked before use
- You can't access properties on an `unknown` type without type assertion
- You can't call or construct values of type `unknown`
</aside>

### **11. Exhaustiveness checking with `never`**

```tsx
type Circle = { kind: 'circle'; radius: number };
type Square = { kind: 'square'; sideLength: number };
type Shape = Circle | Square;

function getArea(shape: Shape): number {
    switch (shape.kind) {
        case 'circle':
            return Math.PI * shape.radius ** 2;
        case 'square':
            return shape.sideLength ** 2;
        default:
            const _exhaustiveCheck: never = shape;
            return _exhaustiveCheck;
    }
}

```

- `Shape` is a **union type** → it can be either `Circle` or `Square`.
- In the `switch`, we check both cases.
- If later you **add another type** (e.g. `Triangle`) but forget to add it in the `switch`,
    
    → TypeScript will complain at the `default` case, because `shape` is **not `never` anymore**.
    
- `never` = means *this should never happen*.
    
    So it’s a **safety net** against forgetting cases.
    

---

**Never:**

<aside>

**Common use cases for `never`:**

- Functions that never return (always throw an error or enter an infinite loop)
- Type guards that never pass type checking
- Exhaustiveness checking in discriminated unions
</aside>

**Undefined & Null:**

<aside>

**Key points about `undefined` and `null`:**

- `undefined` means a variable has been declared but not assigned a value
- `null` is an explicit assignment that represents no value or no object
- In TypeScript, both have their own types: `undefined` and `null` respectively
- With `strictNullChecks` enabled, you must explicitly handle these types
</aside>

***Null & Undefined Check:***

<aside>

**Important:** These types are most useful when `strictNullChecks` is enabled in your `tsconfig.json` file.

This ensures that `null` and `undefined` are only assignable to themselves and `any`.

To enable strict null checks, add this to your `tsconfig.json`:

{  "compilerOptions": {    "strictNullChecks": true  }}

</aside>

### 12. **Optional Parameters**

```tsx
function stranger(name?: string) {
    return `Hello, ${name || 'stranger'}`;
}

```

- `name?: string` → parameter is **optional**.
- If caller doesn’t pass a value, it’s `undefined`.
- Example:
    
    ```tsx
    stranger("Madiha")  // "Hello, Madiha"
    stranger()          // "Hello, stranger"
    
    ```
    

---

## 14. Nullish Coalescing Operator

Think of `??` as:

👉 “If the left side is `null` or `undefined`, use the right side. Otherwise, keep the left side.”

### Example 1: Default value

```tsx
let input: string | null = null;
let result = input ?? "default";
console.log(result); // "default"

```

### Example 2: Difference from `||`

```tsx
let input = 0;

console.log(input || "default"); // "default" (because 0 is falsy )
console.log(input ?? "default"); // 0 (because 0 is not null/undefined )

```

Use `??` when you **only** want to check for `null` or `undefined`, not falsy values like `0`, `false`, or `""`.

---

## 14. Optional Chaining Operator

Think of `?.` as:

👉 “If what’s before `?.` exists, access the property. If not, return `undefined` instead of crashing.”

### Example 1: Nested object

```tsx
const user = { name: "Madiha" };

console.log(user.address.street);   //  Error: Cannot read 'street'
console.log(user?.address?.street); //  undefined (safe)

// in strict mode this will give error
//so use this instead:
type User = {
    name: string;
    address?: {
        street?: string;
    };
};

const user1: User = { name: "Madiha" };

console.log(user1?.address?.street);
```

### Example 2: Optional method call

```tsx
let user: any = {
    sayHi: () => "Hello!"
};

console.log(user.sayHi?.());  // "Hello!"
console.log(user.sayBye?.()); // undefined (doesn’t crash)

```

---

## `??` + `?.` Together

They are often used **together** for safe defaults.

```tsx
const user = {
    name: "Amna",
    address: { street: "" }
};

const street = user?.address?.street ?? "No street found";
console.log(street); // "" (empty string, not replaced because it's not null/undefined)

const city = user?.address?.city ?? "Unknown City";
console.log(city); // "Unknown City"

```

---

- `??` → gives a **default only when value is null/undefined**.
- `?.` → lets you **safely access deep properties** without crashing.
- Together → safe and clean handling of objects and missing data.

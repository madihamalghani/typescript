# **Basic Generics:**

Generics allow creating 'type variables' which can be used to create classes, functions & type aliases that don't need to explicitly define the types that they use.

Generics make it easier to write reusable code.

## Functions:

Generics with functions help create more general functions that accurately represent the input and return types.

```jsx
function createPair<S, T>(v1: S, v2: T): [S, T] {
  return [v1, v2];
}
console.log(createPair<string, number>('hello', 42)); // ['hello', 42]
```

### Explanation:

1. **`<S, T>`**
    - These are **generic type parameters**.
    - `S` is the type of the first value.
    - `T` is the type of the second value.
    - You can name them anything (`A, B` or `X, Y`), but `S` and `T` are common.

---

1. **Function signature**
    
    ```tsx
    function createPair<S, T>(v1: S, v2: T): [S, T]
    
    ```
    
    - `v1: S` → first argument has type `S`.
    - `v2: T` → second argument has type `T`.
    - Return type is `[S, T]` → a tuple with exactly two elements, first of type `S`, second of type `T`.

---

1. **When calling:**
    
    ```tsx
    createPair<string, number>('hello', 42)
    
    ```
    
    - Here we **tell** the function:
        - `S = string`
        - `T = number`
    - So it returns `[string, number]`.
    
    Output: `['hello', 42]`
    

---

### Why useful?

Without generics, you’d have to write separate functions for string+number, number+boolean, etc.

Generics let you **reuse one function** for many type combinations.

<aside>

TypeScript can also infer the type of the generic parameter from the function parameters.

</aside>

## **Classes:**

Generics can be used to create generalized classes

```tsx
class NamedValue<T> {
    private _value: T | undefined;   // can store a value of type T, or nothing (undefined)

    constructor(private name: string) { }   // every NamedValue also has a name

    public setValue(value: T) {   // set the value, but only of type T
        this._value = value;
    }

    public getValue(): T | undefined {   // get the value, might be undefined if not set
        return this._value;
    }

    public toString(): string {   // convert object to string
        return `${this.name}: ${this._value}`;
    }
}
let value1 = new NamedValue<number>('myNumber');  
// here T = number

value1.setValue(10);  
// _value = 10

console.log(value1.toString());  
// Output: "myNumber: 10"
```

Generics (`<T>`) are most useful in **classes (or functions)** where:

- The type of data is **not fixed**.
- You want to **reuse the same class** for different data types **without rewriting code**.

<aside>

TypeScript can also infer the type of the generic parameter if it's used in a constructor parameter.

</aside>

## **Type Aliases:**

Generics in type aliases allow creating types that are more reusable.

```tsx
type Wrapped<T> = { value: T };

const wrappedValue: Wrapped<number> = { value: 10 };
```

Here:

- <T>  represents type such as number, string etc
- So reusable

<aside>

This also works with interfaces with the following syntax: `interface Wrapped<T>` 

</aside>

## **Default Value:**

Generics can be assigned default values which apply if no other value is specified or inferred.

```tsx
class NamedValue<T = string> {
  private _value: T | undefined;

  constructor(private name: string) {}

  public setValue(value: T) {
    this._value = value;
  }

  public getValue(): T | undefined {
    return this._value;
  }

  public toString(): string {
    return `${this.name}: ${this._value}`;
  }
}

let value = new NamedValue('myNumber');
value.setValue('myValue');
console.log(value.toString()); // myNumber: myValue
```

Here :

<aside>

<T=string>  so type is written as default (string)

</aside>

# Extends

Constraints can be added to generics to limit what's allowed.

The constraints make it possible to rely on a more specific type when using the generic type.

 

```tsx
function createLoggedPair<S extends string | number, T extends string | number>(v1: S, v2: T): [S, T] {
  console.log(`creating pair: v1='${v1}', v2='${v2}'`);
  return [v1, v2];
}
```

This means

**S can only be either a `string` or a `number`**

<aside>

`S extends string | number`

</aside>

Note:

<aside>

**This can be combined with a default value.**

</aside>

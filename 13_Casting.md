# Typescript Casting:

Casting is the process of overriding a type.

## Casting with as

A straightforward way to cast a variable is using the `as` keyword, which will directly change the type of the given variable.

```jsx
const input = document.getElementById("my-input") as HTMLInputElement;
```

## Casting with <>

Using <> works the same as casting with `as`.

```jsx
let x: unknown = 'hello';
console.log((<string>x).length);
```

This type of casting will not work with TSX, such as when working on React files.

## Force casting:

To override type errors that TypeScript may throw when casting, first cast to `unknown`, then to the target type.

```jsx
let x = 'hello';
console.log(((x as unknown) as number).length); // x is not actually a number so this will return undefined
```

⇒ in strict mode ⇒ error

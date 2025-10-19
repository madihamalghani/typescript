# **Null & Undefined:**

TypeScript has a powerful system to deal with `null` or `undefined` values.

<aside>

By default `null` and `undefined` handling is disabled, and can be enabled by setting `strictNullChecks` to true.

The rest of this page applies for when `strictNullChecks` is enabled.

</aside>

## Types

`null` and `undefined` are primitive types and can be used like other types, such as `string`.

```tsx
let value: string | undefined | null = null;
value = 'hello';
value = undefined;
```

Note:

<aside>

When `strictNullChecks` is enabled, TypeScript requires values to be set unless `undefined` is explicitly added to the type.

</aside>

## **Optional Chaining:**

Optional chaining is a JavaScript feature that works well with TypeScript's null handling.

It allows accessing properties on an object that may or may not exist, using compact syntax.

It can be used with the `?.` operator when accessing properties.

```tsx
interface House {
  sqft: number;
  yard?: {
    sqft: number;
  };
}
function printYardSize(house: House) {
  const yardSize = house.yard?.sqft;
  if (yardSize === undefined) {
    console.log('No yard');
  } else {
    console.log(`Yard is ${yardSize} sqft`);
  }
}

let home: House = {
  sqft: 500
};

printYardSize(home); // Prints 'No yard'
```

## **Nullish Coalescing:**

Nullish coalescing is another JavaScript feature that also works well with TypeScript's null handling.

It allows writing expressions that have a fallback specifically when dealing with `null` or `undefined`.

This is useful when other falsy values can occur in the expression but are still valid.

It can be used with the `??` operator in an expression, similar to using the `&&` operator.

```tsx
function printMileage(mileage: number | null | undefined) {
  console.log(`Mileage: ${mileage ?? 'Not Available'}`);
}

printMileage(null); // Prints 'Mileage: Not Available'
printMileage(0);
```

## Null Assertion

TypeScript's inference system isn't perfect, there are times when it makes sense to ignore a value's possibility of being `null` or `undefined`.

An easy way to do this is to use casting, but TypeScript also provides the `!` operator as a convenient shortcut.

```tsx
function getValue(): string | undefined {
  return 'hello';
}
let value = getValue();
console.log('value length: ' + value!.length);
```

note:

<aside>

Just like casting, this can be unsafe and should be used with care.

</aside>

## **Array Bounds Handling:**

Even with `strictNullChecks` enabled, by default TypeScript assumes array access will never return `undefined` (unless `undefined` is part of the array type).

The config `noUncheckedIndexedAccess` can be used to change this behavior.

```tsx
let array: number[] = [1, 2, 3];
let value = array[0]; // with `noUncheckedIndexedAccess` this has the type `number | undefined`
```


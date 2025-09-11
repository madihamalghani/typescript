# Union Types:

**Union types** are used when a value can be more than a single type.

## Union | (OR)

Using the `|` we are saying our parameter is a `string` or `number`:

```jsx
let id: string | number
id =234 //no error 
id='amna' //no error
```

example 2:

```jsx
function printStatusCode(code: string | number):void {
  console.log(`My status code is ${code}.`)
}
printStatusCode(404);
printStatusCode('404');
```

***Union Error*** 

```jsx
function printStatusCode(code: string | number) {
  console.log(`My status code is ${code.toUpperCase()}.`) // error: Property 'toUpperCase' does not exist on type 'string | number'. Property 'toUpperCase' does not exist on type 'number'
}
```

⇒ As number can not be converted to uppercase.

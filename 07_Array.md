# Arrays:

**Readonly:**

The `readonly` keyword can prevent arrays from being changed.

```
const names: readonly string[] = ["Madiha"];
// names.push("Jack");// error because this array is readonly
```

## Typed Arrays:

A **tuple** is a typed array with a pre-defined length and types for each index.

Tuples are great because they allow each element in the array to be a known type of value.

To define a tuple, specify the type of each element in the array:

```jsx
let ourTuple: [number, boolean, string];
// initialize correctly
ourTuple = [5, false, 'Coding queen is here. '
```

As you can see we have a number, boolean and a string.

But what happens if we try to set them in the wrong order:

```jsx
// define our tuple
let ourTuple: [number, boolean, string];

// initialized incorrectly which throws an error
ourTuple = [false, 'Coding Queen was mistaken', 5];
```

🚫 Even though we have a `boolean`, `string`, and `number` the order matters in our tuple and will throw an error.

### Readonly Tuple:

A good practice is to make your **tuple** `readonly`.

Tuples only have strongly defined types for the initial values:

```jsx
// define our tuple
let ourTuple: [number, boolean, string];
// initialize correctly
ourTuple = [5, false, 'Coding Queen was here'];
// We have no type safety in our tuple for indexes 3+
ourTuple.push('Something new and wrong');
console.log(ourTuple);
```

add readonly instead:

```jsx
// define our readonly tuple
const ourReadonlyTuple: readonly [number, boolean, string] = [5, true, 'The Real Coding Queen'];
// throws error as it is readonly.
ourReadonlyTuple.push('Coding Queen took a day off');
```

Do you know?

<aside>

If you have ever used React before you have worked with tuples more than likely.

`useState` returns a tuple of the value and a setter function.

`const [firstName, setFirstName] = useState('Dylan')` is a common example.

Because of the structure we know our first value in our list will be a certain value type in this case a `string` and the second value a `function`.

</aside>

### **Named Tuples:**

**Named tuples** allow us to provide context for our values at each index.

```jsx
const graph: [x: number, y: number] = [55.2, 41.3];

```

### Destructuring Tuples

Since tuples are arrays we can also destructure them.

```jsx
const graph: [number, number] = [55.2, 41.3];
const [x, y] = graph;   //x=55.2, y=41.3
```


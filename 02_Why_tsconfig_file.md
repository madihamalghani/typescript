# Why tsconfig.json?

### Without `tsconfig.json`

- You have to write long commands every time, like:
    
    ```bash
    tsc script.ts --strict --target ES6 --outDir dist
    
    ```
    
- If you forget a flag (`-strict`, `-noImplicitAny`, etc.), TypeScript will allow loose code → bugs slip in.
- If your project has **many `.ts` files**, it becomes a headache to manage.

---

### With `tsconfig.json`

- You write the rules **once** in a file.
- Then you just run:
    
    ```bash
    tsc
    
    ```
    
    and it follows those rules for the whole project.
    

Example `tsconfig.json`:

```json
{
  "compilerOptions": {
    "target": "es6",         // output JS version
    "outDir": "dist",        // put compiled files in "dist"
    "strict": true,          // catch errors strictly
    "noImplicitAny": true    // force you to type variables
  },
  "include": ["src"]         // compile all files in "src" folder
}

```

---

### Why it’s highly recommended

1. **Less typing** → one command compiles everything.
2. **Strict rules enforced** → prevents bugs like your `return` issue or missing types.
3. **Organized project** → source files in `src`, output in `dist`.
4. **Team-friendly** → everyone follows the same settings automatically.

---

👉 In short:

You build `tsconfig.json` to **save time, enforce rules, and keep your project clean**.

## Example Case:

```jsx

function add(a,b) {
  return
    a + b; // JS : undefined, TS Error 'unreachable code detected'
}
```

### 1. Why no error in simple .ts file?

TypeScript **only checks types**, not logic.

Your code was:

```tsx
function add(a, b) {
    return
    a + b;
}

```

- No type annotations → `a` and `b` default to `any`.
- Returning on a new line → JavaScript **inserts a semicolon automatically** (`return;`) → function returns `undefined`.
- From TypeScript’s perspective:
    - Valid syntax
    - Valid typing (all `any`)
    - So **no compile error** 🚫

That’s why you don’t see an error, just a wrong runtime result (`undefined`).

---

### 2. How to force TypeScript to catch these issues

You need **strict mode**. When compiling, use:

```bash
tsc script.ts --strict

```

Or set it permanently in `tsconfig.json`***( here comes tsconfig.json )***

```json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true}
}

```

Now TypeScript will complain if you forget parameter types:

```
Parameter 'a' implicitly has an 'any' type.

```

---

### 3. Correct version

```tsx
let message: string = "Hello, TypeScript!";
console.log(message);

function add(a: number, b: number): number {
    return a + b;  //  no ASI issue
}

console.log(add(10, 3)); // 13

```

---

👉 So, the reason you saw no error is:

- TypeScript isn’t about catching **logic mistakes**, it’s about catching **type mistakes**.
- With `-strict`, it will be much stricter and warn you earlier.

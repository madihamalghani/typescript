# How to Install & Run:

### 1. Install TypeScript

First, make sure you have Node.js installed. Then open a terminal in VS Code and run:

```bash
npm install -g typescript

```

This installs TypeScript globally, so you can use the `tsc` command anywhere.

Check the installation with:

```bash
tsc -v

```

---

### 2. Create a TypeScript File

Make a new file, for example:

```bash
hello.ts

```

Inside it, write something simple:

```tsx
let message: string = "Hello, TypeScript!";
console.log(message);

```

---

### 3. Compile TypeScript → JavaScript

In the terminal, run:

```bash
tsc hello.ts

```

This creates a `hello.js` file in the same folder.

---

### 4. Run the JavaScript File

Use Node.js to run it:

```bash
node hello.js

```

You should see:

```
Hello, TypeScript!

```

---

## Watch Changes Without Calling again and again:

```jsx
tsc hello.ts --watch
```

### 5. (Optional) Auto-Compile with tsconfig.json

If you have many `.ts` files, create a `tsconfig.json` file:

```bash
tsc --init

```

Then just run:

```bash
tsc

```

It will compile all `.ts` files automatically.

---

### 6. (Optional) Run TypeScript Directly

Instead of compiling manually, you can install **ts-node**:

```bash
npm install -g ts-node

```

Now you can run:

```bash
ts-node hello.ts

```

It runs TypeScript directly without creating a `.js` file.

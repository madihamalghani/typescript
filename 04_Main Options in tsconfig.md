# Main Options in tsconfig.json

### 1. `"target"`

- Tells TypeScript **what version of JavaScript to output**.
- Example:
    
    ```json
    "target": "es6"
    
    ```
    
    → Compiles your TypeScript into **ES6 JavaScript** (modern).
    
- Common values:
    - `"es5"` → Old browsers support.
    - `"es6"` / `"es2015"` → Modern JavaScript.
    - `"esnext"` → Latest JS features.

---

### 2. `"module"`

- Defines **how modules are bundled/loaded**.
- Example:
    
    ```json
    "module": "commonjs"
    
    ```
    
    → Used in Node.js.
    
- Common values:
    - `"commonjs"` → Node.js style (`require`).
    - `"esnext"` or `"nodenext"` → Modern import/export.
    - `"amd"` / `"system"` → For special cases (older loaders).

---

### 3. `"rootDir"`

- Where your **TypeScript source files live**.
- Example:
    
    ```json
    "rootDir": "./src"
    
    ```
    
    → Tells compiler: "My `.ts` files are inside `src/`".
    

---

### 4. `"outDir"`

- Where to **put compiled JavaScript files**.
- Example:
    
    ```json
    "outDir": "./dist"
    
    ```
    
    → After compiling, `.js` files go into `dist/`.
    

---

### 5. `"strict"`

- Turns on **strict type-checking**.
- Example:
    
    ```json
    "strict": true
    
    ```
    
    → Helps catch more errors early (highly recommended).
    

---

### 6. `"esModuleInterop"`

- Makes it easier to **import CommonJS modules**.
- Example:
    
    ```json
    "esModuleInterop": true
    
    ```
    
    → Lets you write:
    
    ```tsx
    import express from "express";
    
    ```
    
    instead of
    
    ```tsx
    import * as express from "express";
    
    ```
    

---

### 7. `"allowJs"`

- Allows **JavaScript files** to be compiled too.
- Example:
    
    ```json
    "allowJs": true
    
    ```
    

---

### 8. `"checkJs"`

- Type-checks `.js` files too (if `"allowJs": true`).
- Example:
    
    ```json
    "checkJs": true
    
    ```
    

---

### 9. `"sourceMap"`

- Generates `.map` files to **debug TypeScript in browser/VSCode**.
- Example:
    
    ```json
    "sourceMap": true
    
    ```
    

---

### 10. `"noEmit"`

- Stops compiler from creating `.js` files — only checks for errors.
- Example:
    
    ```json
    "noEmit": true
    
    ```
    

---

### 11. `"skipLibCheck"`

- Skips type checking inside `node_modules`.
- Example:
    
    ```json
    "skipLibCheck": true
    
    ```
    
    → Faster compilation, fewer useless errors.
    

---

### 12. `"types"`

- Pick which type definitions (`@types/...`) to include.
- Example:
    
    ```json
    "types": ["node", "jest"]
    
    ```
    

---

### 13. `"lib"`

- Decides what built-in **JavaScript APIs** you can use.
- Example:
    
    ```json
    "lib": ["es6", "dom"]
    
    ```
    
    → Includes ES6 features + browser DOM APIs.
    

If you only want Node.js (no browser stuff):

```json
"lib": ["esnext"]

```

---

Example `tsconfig.json`:

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "rootDir": "./src",
    "outDir": "./dist",
    "strict": true,
    "esModuleInterop": true,
    "sourceMap": true,
    "skipLibCheck": true}
}

```

---


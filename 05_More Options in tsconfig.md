# More Options in `tsconfig.json`

```jsx
{
  "compilerOptions": {
    "forceConsistentCasingInFileNames": true,
    "noUncheckedIndexedAccess": true,
    "exactOptionalPropertyTypes": true,
    "jsx": "react-jsx",
    "verbatimModuleSyntax": true,
    "isolatedModules": true,
    "noUncheckedSideEffectImports": true,
    "moduleDetection": "force",
    "skipLibCheck": true
  },
  "include": ["src"]
}

```

- `"forceConsistentCasingInFileNames": true` → Prevents case mismatch in imports (`MyFile.ts` vs `myfile.ts`).
- `"noUncheckedIndexedAccess": true` → Indexing an array/object will add `undefined` in the type automatically.
- `"exactOptionalPropertyTypes": true` → Distinguishes between `prop?: string` and `prop: string | undefined`.
- `"jsx": "react-jsx"` → Needed for React 17+ (automatic JSX transform).
- `"verbatimModuleSyntax": true` → Requires `import type` for types and disallows synthetic imports.
- `"isolatedModules": true` → Ensures every file can be compiled in isolation (needed for tools like Babel/ESBuild).
- `"noUncheckedSideEffectImports": true` → Forces imports to be used (avoids side-effect-only imports).
- `"moduleDetection": "force"` → Treats every file as a module if it has imports/exports.
- `"skipLibCheck": true` → Skips type-checking of `.d.ts` files (speeds up build).
- `"resolveJsonModule": true`  —>If you ever want to `import data from "./file.json"`, this is needed.
- `"baseUrl"` + `"paths"` for Clean Imports
    - Instead of doing:

```tsx
import Button from "../../../components/ui/Button";

```

- you can configure:

```json
"baseUrl": "src",
"paths": {
  "@components/*": ["components/*"],
  "@utils/*": ["utils/*"]
}

```

and then:

```tsx
import Button from "@components/ui/Button";

```

Looks **much cleaner** and avoids deep `../` chains.

- **`tsconfig.json`** → strict, developer-focused
- **`tsconfig.build.json`** → for build output (skip extra checks for faster builds)

In `tsconfig.build.json` you can override like:

```json
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "noEmit": false,
    "incremental": false},
  "include": ["src"]
}

```


# Auto Changes Detector(- - watch):

### 1. If you **don’t have a `tsconfig.json`**

- Every time you open a new terminal, you need to type:
    
    ```bash
    tsc sandbox.ts(file_name)
    
    ```
    
    or
    
    ```bash
    tsc --watch sandbox.ts
    
    ```
    
    (because TypeScript doesn’t know which files to compile by default).
    

---

### 2. If you **create a `tsconfig.json`** (recommended )

- You only need to do this **once** in your project folder:
    
    ```bash
    tsc --init
    
    ```
    
    This creates a `tsconfig.json` file with default settings.
    
- After that, you can just run:
    
    ```bash
    tsc --watch
    
    ```
    
    - It will automatically watch **all `.ts` files in your project**.
    - No need to keep specifying `sandbox.ts`.
    - And you don’t have to write it every time you open the file — only when you want the compiler to run again (e.g. after restarting your terminal or PC).

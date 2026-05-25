shadcn/ui is a set of beautifully-designed, accessible components and a code distribution platform. Works with your favorite frameworks and AI models. Open Source. Open Code.

**This is not a component library. It is how you build your component library.**

## Installation
### 1 - Create Project

If you need a new Vite project, create one first and select the **React + TypeScript** template. Otherwise, skip this step.

```bash
npm create vite@latest
```

### 2 - Add Tailwind CSS

If your project already has Tailwind CSS configured, skip this step.

```bash
npm install tailwindcss @tailwindcss/vite
```

Replace everything in `src/index.css` with the following:
`@import "tailwindcss";`

### 3 - Edit tsconfig.json file

If your project already has the `@/*` alias configured, skip this step.

Vite splits TypeScript configuration across multiple files. Add the `baseUrl` and `paths` properties to the `compilerOptions` section of `tsconfig.json` and `tsconfig.app.json`:
```ts
"compilerOptions":
 {
  "baseUrl": ".",
  "paths": { "@/*": ["./src/*"] }
 }
```

### 4 - Edit tsconfig.app.json file

Add the same alias to `tsconfig.app.json` so your editor can resolve imports:
```json
"compilerOptions": 
{
 "baseUrl": ".",
 "paths": { 
	 "@/*": ["./src/*"]
 }
}
```
### 5 - Update vite.config.ts

Install `@types/node` and update `vite.config.ts` so Vite can resolve the `@` alias:

```bash
npm install -D @types/node
```


```ts
//vite.config.ts
import path from "path"
import tailwindcss from "@tailwindcss/vite"
import react from "@vitejs/plugin-react"
import { defineConfig } from "vite" 
// https://vite.dev/config/
export default defineConfig({
	plugins: [ react(), tailwindcss()],
	resolve: {    
		alias: {
		      "@": path.resolve(__dirname, "./src"),
		        },
		    },
	}
)

```
### 6 - Run the CLI

Run the `shadcn` init command to set up shadcn/ui in your project:

```bash
npx shadcn@latest init
```

### 7 - Add Components

You can now start adding components to your project.

```bash
npx shadcn@latest add button
```


## If you using JS instead of TS
replace step 3,4,5 with the following steps
### 1 - Add `jsconfig.json` file
```json
{

    "compilerOptions": {
        "baseUrl": ".",
        "paths": {
            "@/*": ["./src/*"]
        }
    }
}
```

### 2 - Update `vite.config.js`
Add the resolve for the alias

```js
resolve: {
    alias: {
      '@': new URL('./src', import.meta.url).pathname,
    },
  }
```
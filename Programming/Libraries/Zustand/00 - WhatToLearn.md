### 1. The Essentials (Setting Up)

- **Introduction** (Located under _Learn_ -> _Start here_): Covers the high-level overview and how to create your first store.
    
- **Updating state** (Located under _Learn_ -> Core Concepts): Explains how to update primitive values, nested objects, and arrays immutably.
    
- **create** (Located under _Reference_ -> _APIs_): The technical API reference for the core function used to build a store.
    

### 2. Reading State & Performance

- **Prevent rerenders with useShallow** (Located under _Learn_ -> _Guides_): The most important guide for keeping your application fast when selecting multiple pieces of state.
    
- **useShallow** (Located under _Reference_ -> _Hooks_): The API reference for the shallow comparison utility.
    

### 3. Handling Async Operations

Zustand does not require special middleware for asynchronous actions like Redux does, which is why there isn't a dedicated standalone page for it. You can simply review the async examples provided directly on the **Introduction** page to see how standard async/await syntax is used inside a store.

### 4. Middlewares

- **Persisting store data** (Located under _Reference_ -> _Integrations_): A deep dive into the persist middleware, including how to configure localStorage or sessionStorage, and how to handle version migrations.
    
- **devtools** and **persist** (Located under _Reference_ -> _Middlewares_): The direct API references for configuring these specific middlewares.
    

### 5. Architecture & Best Practices

- **Slices pattern** (Located under _Learn_ -> _Guides_): Essential reading for when your global state starts getting too large and needs to be split into modular, composable files.
    

### 6. Framework & Language Integration

- **Setup with Next.js** (Located under _Learn_ -> _Guides_): Crucial reading to properly initialize your store on the server and avoid hydration mismatches.
    
- **Beginner TypeScript Guide** (Located under _Learn_ -> _Guides_): Covers exactly how to strictly type your store, actions, and selectors to get full autocomplete and compile-time safety.
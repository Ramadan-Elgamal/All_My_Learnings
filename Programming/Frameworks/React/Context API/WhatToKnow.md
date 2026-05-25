### 1. The Core Concept: Escaping Prop Drilling

- **What to figure out:** Learn the three conceptual phases of the API: creating a context, using it in a deeply nested child, and providing it from a high-level parent. Understand the alternatives to Context and when _not_ to use it.
    
- **Documentation:** [Passing Data Deeply with Context](https://react.dev/learn/passing-data-deeply-with-context)
    

### 2. Initializing Context: `createContext`

- **What to figure out:**
    
    - How to call the function outside of your component hierarchy.
        
    - What the "default value" argument does and the specific scenarios where React actually falls back to it.
        
    - How to export this context object so other components can import it.
        
- **Documentation:** [createContext Reference](https://react.dev/reference/react/createContext)
    

### 3. Reading and Updating: `useContext`

- **What to figure out:**
    
    - How to pass your exported context object into the Hook to read the current value.
        
    - How to wrap a parent component with a Provider to supply dynamic state to the tree below it.
        
    - How to pass both state values and their updater functions down the tree so deeply nested children can trigger state changes in the parent.
        
- **Documentation:** [useContext Reference](https://react.dev/reference/react/useContext)
    

### 4. Intermediate Architecture: Combining with Reducers

- **What to figure out:**
    
    - How to extract your state update logic into a separate reducer function.
        
    - How to create two distinct contexts: one for the state data and one for the dispatch function.
        
    - How to organize your code by moving the reducer, the contexts, custom hooks, and the provider wrapper into a single, dedicated file to keep your component tree clean.
        
- **Documentation:** [Scaling Up with Reducer and Context](https://react.dev/learn/scaling-up-with-reducer-and-context)
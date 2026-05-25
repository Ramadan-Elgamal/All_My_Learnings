
### Getting started page link:
https://redux-toolkit.js.org/introduction/getting-started
### Phase 1: Core Architecture (The Store & Slices)

Before dealing with external data, you must understand how local state is structured, updated, and provided to the application tree.

- **What it is:** `configureStore` sets up the central state container. `createSlice` bundles your initial state, the reducer functions that update that state, and the action creators into a single logical unit.
    
- **Where to find it:** * **Tutorials → Quick Start** (For the full setup flow)
    
    - **API Reference → `configureStore`** and **`createSlice`**
        
- **Practice Step:** Initialize an empty store, wrap your application root with the `<Provider>`, and build a simple slice (e.g., a dark mode toggle or a multi-step form tracker). Dispatch actions to update the state and read it back using standard hooks.
    

### Phase 2: Strict Type Safety

Scaling an application requires robust type checking to catch errors during development. RTK is built to work seamlessly with strong typing, drastically reducing runtime bugs.

- **What it is:** Defining `RootState` and `AppDispatch` types, and creating custom typed versions of the standard Redux hooks (`useSelector` and `useDispatch`).
    
- **Where to find it:** * **Tutorials → TypeScript Quick Start**
    
- **Practice Step:** Create a central hooks file and export strongly typed versions (`useAppSelector`, `useAppDispatch`). Refactor your Phase 1 slice to strictly type the state interface and action payloads. From this point forward, exclusively use the typed hooks in your components.
    

### Phase 3: Handling Side Effects (Async Logic)

Most applications need to communicate with external APIs. You need a way to manage asynchronous logic and track loading states.

- **What it is:** `createAsyncThunk` allows you to write asynchronous functions (like fetch requests) that automatically dispatch `pending`, `fulfilled`, and `rejected` lifecycle actions. You handle these in your slice using `extraReducers`.
    
- **Where to find it:** * **API Reference → `createAsyncThunk`**
    
    - **Tutorials → Async Logic and Data Fetching**
        
- **Practice Step:** Build a feature that fetches a mock list of items. Create the thunk, and write the logic to independently manage the `loading`, `success`, and `error` states within your slice. Render UI feedback (spinners, error messages) based on those states.
    

### Phase 4: Data Fetching and Caching (RTK Query)

For intermediate applications, writing manual thunks for every API call becomes tedious. RTK Query is the modern standard for data fetching, caching, and state synchronization.

- **What it is:** An advanced data fetching tool built directly into RTK. `createApi` allows you to define a set of endpoints. It automatically generates React hooks (e.g., `useGetProductsQuery`) that handle loading states, caching, and background refetching entirely under the hood.
    
- **Where to find it:** * **RTK Query → Overview**
    
    - **Tutorials → RTK Query Quick Start**
        
- **Practice Step:** Replace the manual thunk from Phase 3 with an RTK Query API slice. Configure the `fetchBaseQuery`, define the endpoint, and use the auto-generated hook in your component. Observe how much boilerplate code this eliminates.
    

### Phase 5: State Normalization (Intermediate Mastery)

As data structures grow more complex—especially relational data like users, posts, and comments—storing them in simple arrays leads to performance bottlenecks and messy updates.

- **What it is:** `createEntityAdapter` provides pre-built reducers and selectors for managing normalized state. It structures your data like a database dictionary (using IDs as keys), enabling instant lookups and updates without iterating over large arrays.
    
- **Where to find it:** * **API Reference → `createEntityAdapter`**
    
- **Practice Step:** Refactor a feature that handles a large list of complex objects. Implement `createEntityAdapter` to store them by their IDs. Write a function to update a single nested property of one item and note how the dictionary structure simplifies the update logic.
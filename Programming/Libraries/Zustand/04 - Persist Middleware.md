### What `persist` Does

The `persist` middleware automatically saves your store's state to a storage medium (like `localStorage` or `sessionStorage`) so that the user's data survives page reloads or application restarts. When the app loads, it automatically "hydrates" (loads) the saved data back into your store.

### How to Use It (Basic Setup)

To use it, you import `persist` from `zustand/middleware` and wrap your standard state creator function in it. You must provide an options object as the second argument, and the `name` property is completely required to give the storage item a unique key.

```JS
import { create } from 'zustand'
import { persist } from 'zustand/middleware'

const useUserStore = create(
  persist(
    (set) => ({
      username: 'guest',
      theme: 'light',
      setTheme: (newTheme) => set({ theme: newTheme }),
    }),
    {
      name: 'user-settings-storage', // Required: unique key for localStorage
    }
  )
)
```

By default, the above code will automatically save the state to the browser's `localStorage`.

### Key Options (The `persistOptions` Object)

The second argument you pass to `persist` is an object where you configure how the storage behaves. Here are the most important properties:

- **`name`** (String): _Required._ The unique key used to save the item in storage.
    
- **`storage`** (Object): _Optional._ Changes where the data is saved. Defaults to `localStorage`. You can change it to `sessionStorage`, React Native's `AsyncStorage`, or even the URL search parameters.
    
- **`partialize`** (Function): _Optional._ Allows you to pick and choose exactly which parts of your state actually get saved.
    
- **`version`** & **`migrate`**: _Optional._ Used to handle versioning. If you update your app and change the shape of your state, these allow you to safely migrate old saved user data to the new format.
    
- **`skipHydration`**: _Optional._ (Defaults to `false`). If `true`, the state won't automatically load on initialization. This is heavily used in Server-Side Rendering (SSR) like Next.js to prevent UI mismatches.
    

### Useful Advanced Features (JavaScript Examples)

#### 1. Saving Only Specific Parts of State (`partialize`)

Often, you have temporary state (like UI loading spinners or search inputs) that you don't want to save to `localStorage`, mixed with data you _do_ want to save. Use `partialize` to filter what gets kept.

```JS
import { create } from 'zustand'
import { persist } from 'zustand/middleware'

const useCartStore = create(
  persist(
    (set) => ({
      cartItems: [],         // We want to save this
      isCartOpen: false,     // We DON'T want to save this
      addToCart: (item) => set((state) => ({ 
        cartItems: [...state.cartItems, item] 
      })),
    }),
    {
      name: 'cart-storage',
      // Only save the 'cartItems' property to localStorage
      partialize: (state) => ({ cartItems: state.cartItems }),
    }
  )
)
```

#### 2. Changing the Storage Type (e.g., Session Storage)

If you want the data to clear when the user closes the browser tab, you should use `sessionStorage` instead of the default `localStorage`. You use `createJSONStorage` to set this up.

```JS
import { create } from 'zustand'
import { persist, createJSONStorage } from 'zustand/middleware'

const useSessionStore = create(
  persist(
    (set) => ({
      temporaryTokens: [],
      // ...actions
    }),
    {
      name: 'session-only-storage',
      // Switch from localStorage to sessionStorage
      storage: createJSONStorage(() => sessionStorage),
    }
  )
)
```

#### 3. Manual Hydration (For Next.js / SSR)

If you are building an app with Next.js or Remix, automatic hydration can cause React "hydration mismatch" errors because the server renders a different state than what is saved in the browser. You can skip automatic hydration and do it manually in a `useEffect`.

```JS
import { create } from 'zustand'
import { persist } from 'zustand/middleware'

const useThemeStore = create(
  persist(
    (set) => ({ theme: 'dark' }),
    {
      name: 'theme-storage',
      skipHydration: true, // Prevents automatic loading
    }
  )
)

// Inside your React Component:
// useEffect(() => {
//   useThemeStore.persist.rehydrate()
// }, [])
```
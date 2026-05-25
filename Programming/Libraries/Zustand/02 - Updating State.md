

## Flat updates

Updating state with Zustand is simple! Call the provided `set` function with the new state, and it will be shallowly merged with the existing state in the store. **Note** See next section for nested state.

```tsx
import { create } from 'zustand'

type State = {
  firstName: string
  lastName: string
}

type Action = {
  updateFirstName: (firstName: State['firstName']) => void
  updateLastName: (lastName: State['lastName']) => void
}

// Create your store, which includes both state and (optionally) actions
const usePersonStore = create<State & Action>()((set) => ({
  firstName: '',
  lastName: '',
  updateFirstName: (firstName) => set(() => ({ firstName: firstName })),
  updateLastName: (lastName) => set(() => ({ lastName: lastName })),
}))

// In consuming app
function App() {
  // "select" the needed state and actions, in this case, the firstName value
  // and the action updateFirstName
  const firstName = usePersonStore((state) => state.firstName)
  const updateFirstName = usePersonStore((state) => state.updateFirstName)

  return (
    <main>
      <label>
        First name
        <input
          // Update the "firstName" state
          onChange={(e) => updateFirstName(e.currentTarget.value)}
          value={firstName}
        />
      </label>

      <p>
        Hello, <strong>{firstName}!</strong>
      </p>
    </main>
  )
}
```

[

## Deeply nested object

](https://zustand.docs.pmnd.rs/learn/guides/updating-state#deeply-nested-object)

If you have a deep state object like this:

```ts
type State = {
  deep: {
    nested: {
      obj: { count: number }
    }
  }
}
```

Updating nested state requires some effort to ensure the process is completed immutably.

[

### Normal approach

](https://zustand.docs.pmnd.rs/learn/guides/updating-state#normal-approach)

Similar to React or Redux, the normal approach is to copy each level of the state object. This is done with the spread operator `...`, and by manually merging that in with the new state values. Like so:

```ts
  normalInc: () =>
    set((state) => ({
      deep: {
        ...state.deep,
        nested: {
          ...state.deep.nested,
          obj: {
            ...state.deep.nested.obj,
            count: state.deep.nested.obj.count + 1
          }
        }
      }
    })),
```

This is very long! Let's explore some alternatives that will make your life easier.

[

### With Immer

](https://zustand.docs.pmnd.rs/learn/guides/updating-state#with-immer)

Many people use [Immer](https://github.com/immerjs/immer) to update nested values. Immer can be used anytime you need to update nested state such as in React, Redux and of course, Zustand!

You can use Immer to shorten your state updates for deeply nested object. Let's take a look at an example:

```ts
  immerInc: () =>
    set(produce((state: State) => { ++state.deep.nested.obj.count })),
```

What a reduction! Please take note of the [gotchas listed here](https://zustand.docs.pmnd.rs/reference/integrations/immer-middleware).

[

### With optics-ts

](https://zustand.docs.pmnd.rs/learn/guides/updating-state#with-optics-ts)

There is another option with [optics-ts](https://github.com/akheron/optics-ts/):

```ts
  opticsInc: () =>
    set(O.modify(O.optic<State>().path("deep.nested.obj.count"))((c) => c + 1)),
```

Unlike Immer, optics-ts doesn't use proxies or mutation syntax.

[

### With Ramda

](https://zustand.docs.pmnd.rs/learn/guides/updating-state#with-ramda)

You can also use [Ramda](https://ramdajs.com/):

```ts
  ramdaInc: () =>
    set(R.modifyPath(["deep", "nested", "obj", "count"], (c) => c + 1)),
```

Both ramda and optics-ts also work with types.

## Conclusion
### The Problem: Zustand is only "Shallow"

Zustand's default `set` function does a _shallow_ merge. It only looks at the very top level of your state object.

If you have a deeply nested object, React and Zustand still require you to treat state as **immutable**. To trigger a re-render, you cannot just change a value inside an existing object; you must create a completely new object reference for every level of nesting leading down to that value.

### Without Immer (The Spread Nightmare)

If you want to update a user's city in a nested object without Immer, you have to manually copy every single level of the object using the spread operator (`...`).

This is extremely boilerplate-heavy, hard to read, and prone to bugs. If you miss one spread operator, you might accidentally delete other data in your state.

### With Immer (The Magic Draft)

When you wrap your Zustand store in the Immer middleware, Immer intercepts your `set` function and passes you a temporary "draft" of your state.

You can interact with this draft exactly like a normal, mutable JavaScript object.
## What Immer Does Behind the Scenes

When you write `state.user.profile.address.city = newCity;` inside that Immer function, you aren't actually mutating the real state. You are mutating Immer's proxy "draft."

Once your function finishes, Immer automatically looks at the changes you made to the draft, does all the ugly, deep-level object copying (the spread operators) for you, and produces a safely immutable new state. It gives you the convenience of mutability with the performance and safety guarantees of immutability.
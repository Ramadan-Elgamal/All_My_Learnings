## Definition
^learnkit-983413865
CQ | A small, fast, and scalable bearbones state management solution. Zustand has a comfy **{{c1::API based on hooks}}**. It isn't boilerplatey or opinionated, but has enough convention to be explicit and flux-like. |

## First Steps
### Creating A Store
Your store is a hook! You can put anything in it: primitives, objects, functions. The `set` function _merges_ state.


```JS
import { create } from 'zustand'

const useCount = create((set) => {
	// state
	count: 0,
	
	//Actions
	increase: () => set((state) => ({count: state.count + 1})),
	decrease: () => set((state) => ({count: state.count - 1})),
	multiplyByValue: (value) => set((state) => {count: state.count * value})
	reset: () => set({ count: 0})
})
```

## Binding the components
^learnkit-249063176
CQ | You can use the hook anywhere, {{c1::without the need of providers}}. Select your state and the consuming component will re-render when that state changes. |
```JS
function Counter(){
	const count = useCount(state => state.count);
	<p>The count is {count}</p>
}

function increase(){
	const increase = useCount(state => state.increase);
	<button onclick={increase}> + </button>
}
```

## Example with Async Operations

### 1. The Store: Fetching Data

```JS
import { create } from 'zustand'

const useUserStore = create((set) => ({
  // 1. Initial State
  users: [],
  isLoading: false,
  error: null,

  // 2. The Async Action
  fetchUsers: async () => {
    // Step A: Set loading to true and clear past errors before fetching
    set({ isLoading: true, error: null })

    try {
      const response = await fetch('https://jsonplaceholder.typicode.com/users')
      
      if (!response.ok) {
        throw new Error('Failed to fetch users')
      }
      
      const data = await response.json()
      
      // Step B: Success! Save the data and turn off loading
      set({ users: data, isLoading: false })
      
    } catch (error) {
      // Step C: Failure! Save the error message and turn off loading
      set({ error: error.message, isLoading: false })
    }
  }
}))

export default useUserStore;
```

### 2. The Component: Consuming the Store

```JS
import { useEffect } from 'react'
import useUserStore from './useUserStore'

function UserList() {
  // Grab the state and the action from the store
  const { users, isLoading, error, fetchUsers } = useUserStore()

  useEffect(() => {
    // Trigger the fetch when the component mounts
    fetchUsers()
  }, []) // Empty array ensures it only runs once

  // 1. Handle the loading state
  if (isLoading) {
    return <p>Loading users...</p>
  }
  
  // 2. Handle the error state
  if (error) {
    return <p style={{ color: 'red' }}>Error: {error}</p>
  }

  // 3. Render the successful data
  return (
    <div>
      <h2>User Directory</h2>
      <ul>
        {users.map((user) => (
          <li key={user.id}>{user.name} - {user.email}</li>
        ))}
      </ul>
    </div>
  )
}

export default UserList;
```

## Flashcards
^learnkit-576036421
Q | Zustand allows using the hook "without the need of providers." What common React concept or library does this contrast with, and what step does this save you from doing? |
A | It contrasts with React's Context API and Redux. It saves you from having to wrap your component tree in a Provider component (e.g., ), avoiding "wrapper hell. |

^learnkit-242839205
Q | The set function merges state. If your store has count: 0 and userName: "Ramadan", and you fire set({ count: 1 }), what happens to userName? |
A | It remains completely unchanged. Zustand automatically performs a shallow merge of the new data with the existing data at the top level. |

^learnkit-686701737
Q | When binding components, what is the primary performance benefit of using a selector function like const count = useCount(state => state.count); instead of const state = useCount();? |
A | It ensures the component _only_ re-renders when that specific piece of state (count) changes, completely ignoring updates to any other variables in the store. |

^learnkit-305998569
Q | You use the set function to modify an immutable state object. Since the state is immutable, what is set actually doing behind the scenes? | 
A | It creates and returns a brand new state object containing the merged changes rather than altering the existing object in memory. This new object reference is what signals React to trigger a re-render. |
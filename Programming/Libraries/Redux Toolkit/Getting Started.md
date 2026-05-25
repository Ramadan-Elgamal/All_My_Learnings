The **Redux Toolkit** package is intended to be the standard way to write [Redux](https://redux.js.org/) logic. It was originally created to help address three common concerns about Redux:

- "Configuring a Redux store is too complicated"
- "I have to add a lot of packages to get Redux to do anything useful"
- "Redux requires too much boilerplate code"

Redux Toolkit also includes a powerful data fetching and caching capability that we've dubbed ["RTK Query"](https://redux-toolkit.js.org/introduction/getting-started#rtk-query). It's included in the package as a separate set of entry points. It's optional, but can eliminate the need to hand-write data fetching logic yourself.

## Prerequisites

- Familiarity with [HTML & CSS](https://internetingishard.netlify.app/html-and-css/index.html).
- Familiarity with [ES2015 syntax and features](https://www.taniarascia.com/es6-syntax-and-feature-overview/)
- Knowledge of React terminology: [JSX](https://react.dev/learn/writing-markup-with-jsx), [Function Components](https://react.dev/learn/your-first-component), [Props](https://react.dev/learn/passing-props-to-a-component), [State](https://react.dev/learn/state-a-components-memory), and [Hooks](https://react.dev/reference/react)
- Knowledge of [asynchronous JavaScript](https://javascript.info/promise-basics) and [making HTTP requests](https://javascript.info/fetch)
- Basic understanding of [TypeScript syntax and usage](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)

## Installation

```bash
npm install @reduxjs/toolkit
```

```bash
npm install react-redux
```
Redux can integrate with any UI framework, and is most frequently used with React. [**React-Redux**](https://react-redux.js.org/) is our official package that lets your React components interact with a Redux store by reading pieces of state and dispatching actions to update the store.

## What's Included

Redux Toolkit includes these APIs:

- [`configureStore()`](https://redux-toolkit.js.org/api/configureStore): wraps `createStore` to provide simplified configuration options and good defaults. It can automatically combine your slice reducers, adds whatever Redux middleware you supply, includes `redux-thunk` by default, and enables use of the Redux DevTools Extension.
- [`createReducer()`](https://redux-toolkit.js.org/api/createReducer): that lets you supply a lookup table of action types to case reducer functions, rather than writing switch statements. In addition, it automatically uses the [`immer` library](https://github.com/immerjs/immer) to let you write simpler immutable updates with normal mutative code, like `state.todos[3].completed = true`.
- [`createAction()`](https://redux-toolkit.js.org/api/createAction): generates an action creator function for the given action type string.
- [`createSlice()`](https://redux-toolkit.js.org/api/createSlice): accepts an object of reducer functions, a slice name, and an initial state value, and automatically generates a slice reducer with corresponding action creators and action types.
- [`combineSlices()`](https://redux-toolkit.js.org/api/combineSlices): combines multiple slices into a single reducer, and allows "lazy loading" of slices after initialisation.
- [`createAsyncThunk`](https://redux-toolkit.js.org/api/createAsyncThunk): accepts an action type string and a function that returns a promise, and generates a thunk that dispatches `pending/fulfilled/rejected` action types based on that promise
- [`createEntityAdapter`](https://redux-toolkit.js.org/api/createEntityAdapter): generates a set of reusable reducers and selectors to manage normalized data in the store
- The [`createSelector` utility](https://redux-toolkit.js.org/api/createSelector) from the [Reselect](https://github.com/reduxjs/reselect) library, re-exported for ease of use.
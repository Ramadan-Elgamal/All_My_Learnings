# Passing Data Deeply with Context

Usually, you will pass information from a parent component to a child component via props. But passing props can become verbose and inconvenient if you have to pass them through many components in the middle, or if many components in your app need the same information.

**Context** **API** lets a parent component make some information available to any component in the tree below it—no matter how deep—without passing it explicitly through props.

### The problem with passing props

Passing props is a great way to explicitly pipe data through your UI tree to the components that use it.

But passing props can become cumbersome when you need to pass some prop deeply through the tree, or if many components need the same prop. The nearest common ancestor could be far removed from the components that need data, and lifting state up that high can lead to a situation called **"prop drilling."**

Wouldn't it be great if there were a way to "teleport" data to the components in the tree that need it without passing props? With React's context feature, there is!

### Context: an alternative to passing props

Context lets a parent component provide data to the entire tree below it. There are many uses for context. Here is one example. Consider a `Heading` component that determines its visual size based on a `level` prop:

```JS
<Section>
  <Heading level={3}>About</Heading>
  <Heading level={3}>Photos</Heading>
  <Heading level={3}>Videos</Heading>
</Section>
```

Let's say you want multiple headings within the same `Section` to always have the same size. You could pass the `level` prop to the `<Section>` instead, but how can the `<Heading>` components inside of it know the level of their closest `<Section>`?

**That would require a way for a child to "ask" for data from somewhere above in the tree.**

You can do it with context. You will do it in three steps:

1. **Create** a context. (You can call it `LevelContext`).
    
2. **Use** that context from the component that needs the data. (`Heading` will use `LevelContext`).
    
3. **Provide** that context from the component that specifies the data. (`Section` will provide `LevelContext`).
    

Context lets a parent—even a distant one!—provide some data to the entire tree inside of it.

### Step 1: Create the context

First, you need to create the context. You'll need to export it from a file so that your components can use it.

```JS
import { createContext } from 'react';

export const LevelContext = createContext(1);
```

The only argument to `createContext` is the _default_ value. Here, `1` refers to the biggest heading level, but you could pass any kind of value (even an object). You will see the significance of the default value in the next step.

### Step 2: Use the context

Import the `useContext` Hook from React and your context:
```JS
import { useContext } from 'react';
import { LevelContext } from './LevelContext.js';
```

Currently, the `Heading` component reads `level` from props:

```JS
export default function Heading({ children, level }) {
  // ...
}
```

Instead, remove the `level` prop and read the value from the context you just imported:

```JS
export default function Heading({ children }) {
  const level = useContext(LevelContext);
  // ...
}
```

`useContext` is a Hook. Just like `useState` and `useReducer`, you can only call a Hook immediately inside a React component (not inside loops or conditions). `useContext` tells React that the `Heading` component wants to read the `LevelContext`.

Now that the `Heading` component doesn't have a `level` prop, you don't need to pass it to each `<Heading>` in your JSX anymore!

### Step 3: Provide the context

The `Heading` component now reads the context, but you still need to tell React _where_ to get it.

Wrap them with a context provider to provide the `LevelContext` to them:

```JS
import { LevelContext } from './LevelContext.js';

export default function Section({ level, children }) {
  return (
    <section className="section">
      <LevelContext.Provider value={level}>
        {children}
      </LevelContext.Provider>
    </section>
  );
}
```

This tells React: "if any component inside this `<Section>` asks for `LevelContext`, give them this `level`." The component will use the value of the nearest `<LevelContext.Provider>` in the UI tree above it.

### Context passes through intermediate components

You can insert as many components as you like between the component that provides context and the one that uses it.

Context lets you write components that "adapt to their surroundings" and display themselves differently depending on _where_ (or, in other words, in which context) they are being rendered.

> **Pitfall**
> 
> **Before you use context, try passing props or passing JSX as `children`.** >
> 
> Just because you need to pass some props several levels deep doesn't mean you should put that information into context. Passing props explicitly makes it very clear which components use which data. If your prop routing gets too complicated, often you can extract a component and pass that component as `children` to its parent instead.

### Recap

- Context lets a component provide some information to the entire tree below it.
    
- To pass context:
    
    1. Export and create it with `export const MyContext = createContext(defaultValue)`.
        
    2. Pass it to the `useContext(MyContext)` Hook to read it in any child component, no matter how deep.
        
    3. Wrap children into `<MyContext.Provider value={...}>` to provide it from a parent.
        
- Context passes through any components in the middle.
    
- Before you reach for context, try passing props or passing JSX as `children`.

## Notes

- **The `value` prop rule:** This is the most critical React concept here. A Context Provider is strictly designed to accept **only one prop** named `value`. You cannot pass custom props like `themeToggleFN` to it. To pass both your `theme` string and your `themeToggle` function down the tree, you need to bundle them together into a single JavaScript object, and pass that entire object into the `value` prop.
## Blueprint

### **1.Define the Context Shape:**

Create a dedicated file for your context (e.g., `ThemeContext.jsx`). Start by defining the shape of your context value. You will need a state variable to hold the current theme (usually a string like `'light'` or `'dark'`) and a function to trigger the change, like `toggleTheme`. Use `createContext` to initialize it.

```js
// ThemeContext.jsx
import { createContext } from 'react'

export const Theme = createContext('light');
```
### **2.Build the Provider Component:**

In the same file, create a `ThemeProvider` component that accepts `children` as a prop. Set up a `useState` hook inside it to track the active theme. Write the logic for your `toggleTheme` function to flip that state. Finally, return your `ThemeContext.Provider`, passing your state and toggle function into the `value` prop, and render the `children` inside it.

```js
import { createContext, useState, useContext, useEffect } from 'react';

export const ThemeContext = createContext(undefined);

export function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');

  // New addition: Sync the state with the DOM
  useEffect(() => {
    const root = document.documentElement;
    if (theme === 'dark') {
      root.classList.add('dark');
    } else {
      root.classList.remove('dark');
    }
  }, [theme]); // Re-run this effect whenever 'theme' changes

  const themeToggle = () => {
    setTheme(theme === 'light' ? 'dark' : 'light');
  };

  return (
    <ThemeContext.Provider value={{ theme, themeToggle }}>
      {children}
    </ThemeContext.Provider>
  );
}

// ... useTheme hook remains exactly the same ...
```
### 3.Create a Custom Consumption Hook: Recommended Best Practice.

Instead of exporting the Context object directly, write and export a custom hook called `useTheme`. Inside this hook, call `useContext`. Add a safety check: if the returned context is undefined, throw an error explaining that `useTheme` must be used within a `ThemeProvider`. This prevents silent failures later.

```js
export function useTheme() => {
	const context = useContext(ThemeContext);
	
	if(context === undefined){
		throw new Error('useTheme must be used within a ThemeProvider')
	}
	
	return contex;
}
```
### **4.Wrap Your Application Tree:**

Head to your application's root entry point (like `App.tsx` or your main `layout.tsx`). Import your `ThemeProvider` and wrap it around your main application component. This ensures the theme state is globally available to any component that asks for it.
```js
// App.jsx
import { ThemeProvider } from './ThemeContext';
import ThemeToggle from './ThemeToggle';

export default function App() {
  return (
    // Wrap the provider around the rest of your app components
    <ThemeProvider>
      <div className="app-container">
        <h1>My Application</h1>
        <ThemeToggle />
      </div>
    </ThemeProvider>
  );
}
```
### **5.Consume the Hook in the UI:**

Build a toggle button component anywhere in your app. Call your `useTheme` hook to grab the `toggleTheme` function and attach it to an `onClick` event. To handle the visual changes, you can use the current theme value from the hook to dynamically assign a CSS class to your main wrapper, or use a `useEffect` to toggle a class on `document.body` or `document.documentElement`.
```js
import { useTheme } from './ThemeContext';

export default function ThemeToggle() {
  const { theme, themeToggle } = useTheme();

  return (
    <button 
      onClick={themeToggle}
      className="px-5 py-2 border rounded-md cursor-pointer transition-colors duration-200
                 bg-white text-zinc-900 border-zinc-900 
                 dark:bg-zinc-900 dark:text-white dark:border-zinc-100"
    >
      Switch to {theme === 'light' ? 'Dark' : 'Light'} Mode
    </button>
  );
}
```

### **Tailwind v4 Configuration Note:** 
By default, Tailwind respects the user's OS system preference for dark mode. To enable the class-based manual toggle you just built, make sure you configure your CSS file to look for the class modifier. In your main CSS file (where you import Tailwind), you usually add:

```css
@import "tailwindcss";
@variant dark (&:where(.dark, .dark *));
```
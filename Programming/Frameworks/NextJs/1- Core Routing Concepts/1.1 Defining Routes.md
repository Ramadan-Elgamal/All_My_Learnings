# Defining Routes

Pull up your editor. Now that we have our Next.js project running and we know what the `app` folder is, it's time to actually build the pages of our application.

## Start with the "Why": Escaping the Routing Map

If you've built a standard React app before, you've probably used `react-router-dom`. Think about how you create a new page there. First, you create the component file. Then, you open a giant, central `App.js` file, import that component, and manually write a mapping: `<Route path="/about" element={<About />} />`.

Every time you add a page, you touch two places. As an app grows to hundreds of pages, that central routing file becomes a massive, merge-conflict-prone nightmare.

Next.js asks a simple question: **"What if the folder structure on your hard drive *was* the routing map?"** No central configuration file. Just folders.

## The Mental Model: The Tree and the Leaves

Think of your application's URLs like a tree.

* **The Trunk:** The `app` folder itself is the root URL of your website (`/`).
* **The Branches:** Any **folder** you create inside `app` becomes a segment of the URL.
* **The Leaves:** The special file named **`page.tsx`** is the actual UI (the React component) shown to the user when they visit that URL.

A branch cannot be seen by the user unless it has a leaf on it. A folder creates the *path*, but the `page.tsx` file creates the *destination*.

## Concept Before Syntax: Safe Colocation

This "folders are paths, pages are UI" separation is a massive superpower.

Because Next.js only creates a public web page when it sees a file explicitly named `page.tsx`, you can safely put anything else inside those folders. You can put your `Button.tsx` component, your `utils.ts` helper functions, and your `styles.css` right next to the page that uses them.

Next.js will completely ignore them when generating URLs. This pattern is called **Colocation**, and it keeps your codebase incredibly organized. You no longer need a giant `src/components` folder separated from a giant `src/pages` folder.

## Building Incrementally: Mapping Folders to URLs

Let's look at exactly how folders map to the browser URL:

1. **The Root Route:**
* File: `app/page.tsx`
* URL: `your-site.com/`


2. **A Standard Route:**
* File: `app/about/page.tsx`
* URL: `your-site.com/about`


3. **A Nested Route:**
* File: `app/blog/first-post/page.tsx`
* URL: `your-site.com/blog/first-post`



Notice the pattern? You just keep nesting folders, and eventually, drop a `page.tsx` at the end of the tunnel to render the UI.

## Mistakes to Avoid Before You Make Them

Here is where junior developers usually trip up in their first week:

* **Mistake 1: Naming the file `About.tsx` instead of `page.tsx`.**
* *Reality:* If you create `app/about/About.tsx`, going to `/about` will give you a 404 Error. Next.js is explicitly looking for the word `page`. The folder name determines the URL; the file must always be `page`.


* **Mistake 2: Thinking every folder *must* have a page.**
* *Reality:* Let's say you have `app/store/shoes/page.tsx`. You might think you also *need* an `app/store/page.tsx`. You don't. If you don't have a `page.tsx` in the `store` folder, visiting `/store` will 404, but `/store/shoes` will work perfectly. Folders can act solely as routing pathways.


* **Mistake 3: Forgetting to export default.**
* *Reality:* Next.js expects the main component inside `page.tsx` to be a `default` export. If you use a named export (e.g., `export function Page()`), Next.js won't know what to render and will throw an error.



## Practical Exercise

Let's build a small nested structure to lock this mental model in place. Make sure your local server is running (`npm run dev`).

1. Inside your `app` directory, create a new folder called `settings`.
2. Inside `settings`, create a file called `page.tsx`.
3. Add this code to `app/settings/page.tsx`:
```tsx
export default function SettingsPage() {
  return <h1>General Settings</h1>;
}

```


4. Now, inside the `settings` folder, create another folder called `profile`.
5. Inside `profile`, create *two* files: `page.tsx` and `ProfileAvatar.tsx`.
6. In `app/settings/profile/page.tsx`, write a quick component returning `<h1>Profile Settings</h1>`.
7. In your browser, visit `http://localhost:3000/settings`. You should see "General Settings".
8. Visit `http://localhost:3000/settings/profile`. You should see "Profile Settings".
9. Try to visit `http://localhost:3000/settings/profile/ProfileAvatar`. You will get a 404.

That 404 proves that Colocation works perfectly. The avatar component is safe from being accessed directly by the public, but the routes act exactly as the folders dictate.
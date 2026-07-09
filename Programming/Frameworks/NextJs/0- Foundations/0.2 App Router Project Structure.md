# App Router Project Structure

Open the project we just generated in your code editor. Before we start writing components, we need to understand the landscape. In vanilla React, how you name and organize your folders is entirely up to you. In Next.js, your folder structure *is* the application.

## Start with the "Why": File-System Routing

In a standard React app, you usually have one big file (like `App.js`) where you manually map URLs to components using a library like React Router. You write code that says, *"If the user goes to `/about`, load the `<About />` component."*

Next.js eliminates that file entirely.

Instead, it uses **file-system routing**. The framework looks at your folders and automatically creates the routes for you based on their names. If you create a folder named `about` inside the `app` directory, Next.js instantly creates a `/about` URL for your website. Your folders dictate the architecture.

## The Mental Model: The Retail Store

Think of your Next.js project directory as a physical retail store.

* **The Root Files (The Blueprint):** The files sitting loose at the bottom of your project (`next.config.js`, `package.json`, `tsconfig.json`) are the blueprints, lease agreements, and permits. They tell the building how to operate, but your customers (users) never see them.
* **The `public/` Directory (The Storefront Window):** This is where you put things you want anyone to see directly from the street. Images, favicon icons, and custom fonts go here.
* **The `app/` Directory (The Floor Plan):** This is the inside of your store. The folders here dictate the aisles and rooms the customer can walk into.

Let's break down the two most important folders.

## The `public/` Directory: Static Assets

If you open the `public` folder, you will see some SVG files Next.js put there by default. This folder is completely public-facing.

The pattern to remember here is **absolute paths**. When you want to use an image from this folder in your code, you don't write complicated relative paths like `../../../public/logo.png`. Because Next.js serves this folder directly to the root URL, you just write `/logo.png`.

## The `app/` Directory: Where the Magic Happens

This is the heart of the modern Next.js architecture (the "App Router"). Open it up.

Inside, you will notice a specific pattern. You won't just see generic component names. Next.js relies on **reserved filenames** to know what to do. The most important one is `page.tsx`.

* **Folders define the URL path.**
* **`page.tsx` defines the UI for that path.**

If you have a file at `app/page.tsx`, that is the homepage (`/`). If you create a folder called `dashboard` and put a `page.tsx` inside it (`app/dashboard/page.tsx`), Next.js automatically creates the `/dashboard` route.

We will dive deep into routing in the next module, but for now, just understand that you cannot name your routing files whatever you want. If you name it `view.tsx` or `Home.tsx` inside the `app` folder, Next.js will completely ignore it as a route. It *must* be `page.tsx`.

## Other Reserved Files (A Quick Preview)

Alongside `page.tsx`, Next.js uses a few other special filenames in the `app` directory to handle different states of your UI:

* `layout.tsx`: UI that wraps around your pages (like a persistent navigation bar).
* `loading.tsx`: A temporary loading spinner shown while your page prepares.
* `error.tsx`: A fallback screen shown if your page crashes.

You just drop these files into a folder, and Next.js automatically wires them up.

## Mistakes to Avoid Before You Make Them

* **Mistake 1: Cluttering the root directory.** *Reality:* Keep your components, utilities, and styles inside the `app` folder (or a dedicated `src` folder if you chose that during setup). The root directory should only be for configuration files.
* **Mistake 2: Forgetting the `page.tsx` file.** *Reality:* You can create a beautifully named folder structure like `app/marketing/about-us`, but if there is no `page.tsx` inside `about-us`, going to `/marketing/about-us` in the browser will result in a 404 Error. The folder is just the path; the `page` is the destination.
* **Mistake 3: Storing sensitive data in `public/`.** *Reality:* Anything in the `public` folder can be accessed by anyone typing the file name into their browser. Never put internal documents, `.env` backups, or private assets in there.

## Practical Exercise

Let's clean out the furnished house and make it ours.

1. Open `app/page.tsx` in your editor. This is the homepage you saw in the browser earlier.
2. Highlight everything inside that file and delete it.
3. Write a brand new, extremely simple React component:

```tsx
export default function Home() {
  return (
    <main>
      <h1>Welcome to my Next.js App</h1>
      <p>The boilerplate is gone.</p>
    </main>
  );
}

```

4. Save the file.
5. Go back to your browser (`http://localhost:3000`). Notice how it instantly updated without you having to refresh the page? That's Fast Refresh at work.

Next up, we will learn exactly how to build out the rest of the rooms in our house by diving into routing.
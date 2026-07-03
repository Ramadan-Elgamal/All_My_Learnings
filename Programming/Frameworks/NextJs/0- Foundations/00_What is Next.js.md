# What is Next.js?

Grab a chair. Before we write a single line of code, we need to talk about why we are even using Next.js in the first place. You already know React, so adding another tool on top might feel redundant. Let's break down exactly why it's not.

## Start with the "Why": The Problem with Vanilla React

React is fantastic for building interactive user interfaces. But standard, out-of-the-box React has a major blind spot: **how it delivers that UI to the browser.** When you build a standard React app (a Single Page Application, or SPA), the server sends the user an almost completely empty HTML file. It usually just contains `<div id="root"></div>` and a massive link to a JavaScript file.

The user's browser has to download that JavaScript, parse it, and execute it before it can draw the page. For a few seconds, your user is staring at a blank screen. Worse, search engine crawlers often see that same blank screen, which ruins your SEO.

Next.js exists to solve this exact delivery problem.

## The Mental Model: The Restaurant Analogy

To understand what Next.js actually does, think about a restaurant.

**Vanilla React is like cooking at the table.** The waiter brings a cart full of raw ingredients, pots, and pans to your table, and cooks the meal right in front of you. Yes, it's highly interactive and fresh, but you have to sit there and wait for the cooking to finish before you can take your first bite. This is **Client-Side Rendering (CSR)**.

**Next.js is like a traditional kitchen.** The chefs cook the meal in the back (on the server). The waiter brings out a fully prepared, hot plate of food. You can start eating immediately. While you take your first bite, the waiter drops off the salt, pepper, and hot sauce for you to customize it. This is **Server-Side Rendering (SSR)**.

Next.js renders your React components into actual HTML on the server, sends that fully formed HTML to the browser so the user sees it instantly, and *then* attaches the React interactivity in the background (a process called Hydration).

## Concepts Before Syntax: The Meta-Framework Pattern

Don't think of Next.js as a library you import into React. Think of it as the environment where your React code lives. Next.js is a **React framework** (often called a meta-framework).

React is just a view library; it doesn't care how you handle routing, data fetching, or building your final files. It leaves those choices up to you, which can lead to configuration fatigue.

Next.js gives you a highly opinionated, standardized architecture. It says: *"If you put your files in this specific folder structure, I will automatically handle the routing, the Webpack bundling, the server-rendering, and the performance optimizations for you."*

## Building Incrementally: What Next.js Adds

If you know React, you already know how to write the UI in Next.js. What you are learning now are the architectural pieces Next.js wraps around your UI:

1. **Routing:** No more `react-router-dom`. You just create a file, and Next.js creates the URL route based on the folder name.
2. **Rendering Strategies:** You can choose to render a page at build time (Static), on every request (Server), or in the browser (Client)—often mixing them on the exact same page.
3. **Data Fetching:** Next.js pushes you to fetch data securely on the server, right next to your database, rather than making the user's browser do the heavy lifting.

## Common Mistakes Before You Make Them

Before we move forward, let's clear up a few traps junior developers fall into when starting Next.js:

* **Mistake 1: Thinking Next.js replaces React.** * *Reality:* Next.js *is* React. You are still writing React components, using hooks, and managing state. Next.js just changes *where* those components are executed.
* **Mistake 2: Trying to install standard React tools.** * *Reality:* Do not install routing libraries or bundlers. Let go of the manual configuration. Trust the Next.js file system conventions.
* **Mistake 3: Putting everything on the server.** * *Reality:* Because Next.js defaults to the server, developers sometimes forget how to handle browser-specific things (like `onClick` events or `window` APIs). We will explicitly learn how to tell Next.js, *"Hey, this specific button needs to run in the browser."*

## Practical Exercise

Let's prove the mental model. We aren't going to write code; we are going to inspect reality.

1. Open an incognito window and go to a known standard React application (like [app.netlify.com](https://app.netlify.com) or a raw Create React App project if you have one).
2. Right-click the background and select **"View Page Source"**.
3. Look at the code. You will see a tiny HTML file with an empty `div` and a giant `<script>` tag. The content isn't there.
4. Now, go to a Next.js built site (like [nextjs.org](https://nextjs.org) or [notion.so](https://notion.so)).
5. Right-click and select **"View Page Source"**.
6. Look at the code. You will see massive amounts of HTML text containing the actual words and content of the page, fully formed before the browser even started running JavaScript.

That difference right there is why we are learning Next.js.
# Next.js Installation

Pull up your terminal. Now that we know *why* we are using Next.js, we need to actually get it running on your machine. We aren't going to build this from scratch. Let's talk about why.

## Start with the "Why": The Fully Furnished House

In the early days of React, starting a project meant spending three days configuring Webpack, setting up Babel to transpile modern JavaScript, and arguing with ESLint plugins. It was like buying bricks, lumber, and copper pipes just to build a kitchen before you could cook a meal.

Next.js flips this. Installing Next.js is like buying a fully furnished house with the plumbing and electricity already hooked up.

We use a scaffolding tool called `create-next-app`. It’s a command-line utility provided by the Next.js team that asks you a few questions and instantly generates a production-ready, perfectly configured project. You walk in, open the laptop, and just start writing code.

## The Concept: Scaffolding and Sensible Defaults

When you run an installer like `create-next-app`, you aren't just downloading code. You are adopting the Next.js team's "sensible defaults."

Instead of forcing you to piece together a tech stack, the installer assumes you probably want TypeScript for safety, ESLint for code formatting, and Tailwind CSS for styling. It pre-configures all of these tools so they play nicely together out of the box.

You *can* manually install Next.js by creating a `package.json` and adding `next`, `react`, and `react-dom` yourself—but in practice, almost nobody does this for a new project. We trust the scaffold.

## The Syntax: Running the Installer

To trigger this setup wizard, we use `npx`, which is a tool that comes with Node.js. It fetches the latest version of `create-next-app` from the internet and runs it without permanently installing the CLI on your computer.

Run this in your terminal:

```bash
npx create-next-app@latest my-first-next-app

```

## Making the Right Choices (The Prompts)

When you run that command, the terminal will ask you a series of yes/no questions. Here is the mental model for what to pick today:

* **Would you like to use TypeScript?** Say **Yes**. Even if you are still learning TS, the autocomplete and error-checking Next.js provides out-of-the-box will save you hours of debugging.
* **Would you like to use ESLint?** Say **Yes**. Let the linter catch your typos before they become bugs.
* **Would you like to use Tailwind CSS?** Say **Yes**. It's the community standard for Next.js styling right now.
* **Would you like to use `src/` directory?** Say **No** (or Yes, it's just a preference). For our learning path, we'll keep things at the root level to match most of the official documentation.
* **Would you like to use App Router? (recommended)** Say **YES**. This is the most critical question. We will talk about this more later, but Next.js has two different routing engines right now. The App Router is the modern standard.
* **Would you like to customize the default import alias?** Say **No**. The default `@/*` works perfectly.

## Mistakes to Avoid Before You Make Them

* **Mistake 1: Using an outdated Node version.** *Reality:* Next.js uses modern server features under the hood. If you get weird installation errors, check your Node version (`node -v`). You need Node.js 18.17 or later.
* **Mistake 2: Picking the "Pages Router" by accident.** *Reality:* If you hit "No" on the App Router question, you will generate a project using the legacy architecture. The mental model, file structure, and data fetching we are about to learn will not work.
* **Mistake 3: Trying to "Eject".** *Reality:* If you used Create React App in the past, you might remember an `eject` command that exposed all the messy Webpack configs. Next.js doesn't do that. You customize it through a specific file (`next.config.js`), not by ejecting.

## Practical Exercise

Let's get your local environment running.

1. Open your terminal and navigate to your standard coding folder.
2. Run `npx create-next-app@latest next-learning-sandbox`
3. Answer the prompts exactly as outlined above (Make absolutely sure you say **Yes** to the App Router).
4. Once it finishes downloading, navigate into your new folder: `cd next-learning-sandbox`
5. Start the local development server: `npm run dev`
6. Open your browser and go to `http://localhost:3000`.

If you see the dark, sleek Next.js starter page, your furnished house is ready. In the next file, we'll take a tour of the rooms and look at the project structure.
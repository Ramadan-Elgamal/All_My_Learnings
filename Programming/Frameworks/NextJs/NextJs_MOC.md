
| **Topic**                              | **Purpose**                                                                                     |
| -------------------------------------- | ----------------------------------------------------------------------------------------------- |
| **0. Foundations & Setup**             |                                                                                                 |
| [[0.0 What is Next.js]]                | High-level overview of the framework, its relationship with React, and Server Components        |
| [[0.1 Next.js Installation]]           | Setting up a new project via `create-next-app` and manual installation steps                    |
| [[0.2 App Router Project Structure]]   | Exploring the `app/` and `public/` directories, and understanding file-system conventions       |
| **1. Routing: Core Concepts**          |                                                                                                 |
| [[1.1 Defining Routes]]                | How folder structures translate to URL paths and leaf nodes (`page.tsx`)                        |
| [[1.2 Pages and Layouts]]              | Differentiating between unique UI (`page.tsx`) and shared, persistent UI (`layout.tsx`)         |
| [[1.3 Templates]]                      | Using `template.tsx` to create layouts that remount on every navigation                         |
| [[1.4 Linking and Navigating]]         | Client-side transitions using the `<Link>` component, `useRouter` hook, and native `<a>` tags   |
| [[1.5 Route Groups]]                   | Using `(folder)` syntax to organize project files logically without affecting URL paths         |
| [[1.6 Dynamic Routes]]                 | Generating paths from dynamic data using `[folder]` syntax                                      |
| [[1.7 Catch-all Segments]]             | Using `[...folder]` and `[[...folder]]` to capture multiple dynamic URL segments                |
| **2. Routing: UI States & Edge Cases** |                                                                                                 |
| [[2.1 Loading UI and Suspense]]        | Utilizing `loading.tsx` to show instant loading states with React Suspense boundaries           |
| [[2.2 Error Handling (Next.js)]]       | Catching unexpected exceptions using `error.tsx` and `global-error.tsx`                         |
| [[2.3 Not Found Pages]]                | Handling 404s via `not-found.tsx` and triggering them programmatically with `notFound()`        |
| **3. Routing: Advanced Patterns**      |                                                                                                 |
| [[Parallel Routes]]                    | Rendering multiple pages simultaneously in the same layout using `@folder` slots                |
| [[Intercepting Routes]]                | Loading a route inside the current layout (e.g., modals) using `(..)folder` syntax              |
| [[Route Handlers]]                     | Building backend API endpoints using `route.ts` (GET, POST, PUT, DELETE)                        |
| [[Middleware in Next.js]]              | Running code server-side before a request completes for auth, redirects, and rewrites           |
| [[Internationalization (i18n)]]        | Implementing dictionary routing, localized content, and language detection                      |
| **4. Architecture & Rendering**        |                                                                                                 |
| [[React Server Components (RSC)]]      | Understanding the default rendering behavior in App Router and its performance benefits         |
| [[Client Components]]                  | Opting into client-side interactivity and browser APIs using the `"use client"` directive       |
| [[Server and Client Composition]]      | Best practices for interleaving components and passing props between Server and Client          |
| [[Edge and Node.js Runtimes]]          | Comparing lightweight Edge runtime limitations with full Node.js API access                     |
| **5. Data Fetching & State**           |                                                                                                 |
| [[Fetching in Server Components]]      | Using native `fetch`, third-party libraries, and direct database queries on the server          |
| [[Caching Architecture (Next.js)]]     | How Next.js handles Request Memoization, Data Cache, Full Route Cache, and Router Cache         |
| [[Revalidating Data]]                  | Purging cached data using Time-based revalidation, `revalidatePath`, and `revalidateTag`        |
| [[Server Actions]]                     | Writing asynchronous server functions for form submissions and data mutations                   |
| [[Fetching in Client Components]]      | Fetching patterns on the client using SWR, React Query, and React's `use()` hook                |
| **6. Styling**                         |                                                                                                 |
| [[Global Styles]]                      | Applying baseline CSS and configuring global stylesheets                                        |
| [[CSS Modules (Next.js)]]              | Writing locally scoped CSS to prevent class name collisions                                     |
| [[Tailwind CSS in Next.js]]            | Configuring and optimizing utility-first styling with the App Router                            |
| [[Sass Implementation]]                | Setting up SCSS/Sass and utilizing module-level preprocessor styling                            |
| **7. Optimization**                    |                                                                                                 |
| [[Image Optimization (next-image)]]    | Using `<Image>` for automatic responsive resizing, WebP conversion, and blur placeholders       |
| [[Font Optimization (next-font)]]      | Self-hosting fonts automatically to eliminate layout shifts (CLS) and external network requests |
| [[Script Component (next-script)]]     | Loading third-party scripts (analytics, ads) with prioritized loading strategies                |
| [[Metadata and SEO]]                   | Utilizing the `metadata` object, `generateMetadata`, and Open Graph tags for search engines     |
| [[Lazy Loading Components]]            | Using `next/dynamic` to defer loading of heavy client or server components                      |
| [[Static Assets]]                      | Serving files like images, SVGs, and text files correctly from the `public/` directory          |
| **8. Configuration & Tooling**         |                                                                                                 |
| [[Environment Variables]]              | Securing secrets via `.env` and exposing safe variables to the browser via `NEXT_PUBLIC_`       |
| [[next.config.js]]                     | Customizing the webpack build, defining redirects, rewrites, and security headers               |
| [[TypeScript Configuration]]           | Utilizing Next.js built-in types, plugins, and the auto-generated `env.d.ts`                    |
| [[MDX Setup]]                          | Configuring `@next/mdx` to write Markdown inside React components                               |
| **9. Testing & Deployment**            |                                                                                                 |
| [[Unit Testing (Jest & RTL)]]          | Configuring Jest and React Testing Library for components and utility functions                 |
| [[E2E Testing (Playwright & Cypress)]] | Setting up End-to-End tests to simulate user flows across Next.js routes                        |
| [[Static HTML Export]]                 | Configuring `output: 'export'`, understanding its benefits, and learning its hard limitations   |
| [[Deploying Next.js]]                  | Hosting strategies: Vercel serverless deployment vs. self-hosting via Node.js or Docker         |

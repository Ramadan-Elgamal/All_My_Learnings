---
tags:
  - telegraf
  - telegram-bots
  - backend
  - documentation
  - flashcards/telegraf
aliases:
  - Telegraf.js MOC
  - Telegram Bot Documentation
---

# 🤖 Telegraf.js Master Index
A complete architectural guide and reference manual for building production-ready Telegram bots using Telegraf.js. 

---

## 🗺️ Map of Content (Phased Learning)

### Phase 1: The Foundation
* **[[01_Core_Basics]]**
  * **Concepts:** `Telegraf` instance, The `Context` (`ctx`) object, Middleware cascade (`next()`).
  * **Events:** Default Telegram event names (`'text'`, `'photo'`, `'document'`).
  * *Goal:* Setting up the ignition, catching basic inputs, and extending the TypeScript Context.

### Phase 2: Interactive UIs
* **[[02_Buttons_and_Actions]]**
  * **Concepts:** `Markup.inlineKeyboard`, Callback Data payloads.
  * **Events:** `bot.action()` nets.
  * **UX:** Managing spinners with `ctx.answerCbQuery()` and fluid updates via `ctx.editMessageText()`.

### Phase 3: Memory & Multi-Step Flows
* **[[03_State_and_Wizards]]**
  * **Concepts:** The Amnesia Problem, `session()` middleware.
  * **Architecture:** `Scenes.Stage`, `Scenes.WizardScene`.
  * **Execution:** Moving between steps (`ctx.wizard.next()`), storing temporary data (`ctx.wizard.state`), and exiting (`ctx.scene.leave()`).
* **[[04_Composers]]**
  * **Concepts:** Upgrading dumb wizard steps into mini-routers.
  * **Execution:** Catching specific commands (like `/cancel`) within a specific wizard step before falling back to standard text handlers.

### Phase 4: Production Standards
* **[[05_Project_Architecture]]**
  * **Concepts:** Breaking out of `index.ts`.
  * **Structure:** Separating concerns into `/commands`, `/actions`, `/middlewares`, and `/scenes` to maintain strict boundaries and aid AI-assisted vibe coding.
* **[[06_Webhooks_Deployment]]**
  * **Concepts:** Long Polling (Dev) vs. Webhooks (Prod).
  * **Execution:** Mounting Telegraf onto serverless HTTP handlers (e.g., Next.js App Router) to save compute costs.

### Phase 5: Persistence
* **[[07_Database_Integration]]**
  * **Concepts:** Dependency injection via global middleware.
  * **Execution:** Attaching a database client (like Supabase) directly to the `Context` object so it is globally available in every isolated scene or command.

---

## 🧠 Spaced Repetition Queue
*(Use this section to track which concepts need to be converted into LearnKit flashcards within their respective notes)*
- [ ] Diagram the Context (`ctx`) lifecycle.
- [ ] Flashcard: Long Polling vs Webhook tradeoffs.
- [ ] Flashcard: The necessity of `ctx.answerCbQuery()`.
- [ ] Diagram: Wizard Scene state progression.

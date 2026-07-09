
# The Context (`ctx`) Object Reference

The `Context` object (conventionally named `ctx`) is the heartbeat of Telegraf.js. Every time a user types a message, clicks a button, or triggers an event, Telegram sends an incoming payload called an `Update`. Telegraf intercepts this raw update, wraps it inside a massive instance of the `Context` class, and injects shortcuts and helper properties before delivering it to your handlers.

Instead of needing to keep track of chat IDs, user records, and message threads manually, `ctx` acts as your isolated environment for that single interaction.

---

## 1. Context Lifecycle Architecture

The context object is short-lived. It is instantiated when the update hits your server, flows sequentially through your middleware chain, and is garbage-collected after your code finishes responding.



---

## 2. Core State Namespaces

### A. `ctx.update`
The completely raw, unmodified JSON object sent directly from the Telegram Bot API. If you need to access experimental or deeply nested fields not parsed by Telegraf's core wrappers, you dig into the raw update.
* **Type:** `Update` JSON Object

### B. `ctx.state`
A temporary, plain JavaScript object (`{}`) created fresh for every single incoming update. It is shared across all middlewares *only for the duration of that specific update*. 
* **Why use it:** Great for passing data calculated in an early middleware (like fetching user roles or language preferences from Supabase) down to your specific commands or wizard steps.
* **Note:** Unlike `session`, `ctx.state` is completely wiped clean the moment the bot finishes processing the current message.

```typescript
// Middleware 1: Geolocation decoding
bot.use(async (ctx, next) => {
    ctx.state.userLanguage = 'es'; // Passing a property down the pipeline
    await next();

```
## 3. Dynamic Getters (Payload Extractors)
These properties extract structural information from the underlying update. Because Telegram updates can vary heavily, **these properties may be undefined** depending on what action triggered the event.
 * **ctx.from**: The User object representing who caused this update. Always available on messages, commands, and button clicks. Contains .id, .is_bot, .first_name, .last_name, .username, and .language_code.
 * **ctx.chat**: The Chat object where the interaction occurred. Can represent a private DM with the bot, a group chat, a supergroup, or a channel. Contains .id, .type ("private" | "group" | "supergroup" | "channel"), .title, and .username.
 * **ctx.message**: The full data wrapper for incoming messages. Only exists if the update type is a standard message or command. It gives you access to sub-payloads like ctx.message.text, ctx.message.photo, or ctx.message.document.
 * **ctx.callbackQuery**: The raw data object payload returned when a user clicks an inline keyboard button. Contains the .data payload string and the original .message layout the button was attached to.
## 4. Context Shortcut Methods (Action Engine)
The true power of ctx lies in its shortcuts. Instead of invoking the raw API like bot.telegram.sendMessage(chatId, text), shortcuts automatically abstract away target parameters by extracting the exact chat and message context implicitly.
### A. Core Communication Shortcuts
#### ctx.reply(text, extra) / ctx.replyWithHTML(text)
Sends a standard text response directly back into the originating chat.
```typescript
// Sending a simple message with custom typography parsing
await ctx.replyWithHTML('<b>Welcome, Teacher!</b>\nYour request has been filed.');

```
#### ctx.replyWithPhoto(photo, extra) / ctx.replyWithDocument(doc)
Uploads visual or generic attachments. The target payload can be a public URL string, a local file pathway, or an in-memory file buffer.
```typescript
// Sending a local document file using a stream pathway
await ctx.replyWithDocument({ source: './templates/exam_template.pdf' }, {
    caption: 'Here is your structural template.'
});

```
### B. UI Manipulation & Editing Shortcuts
#### ctx.editMessageText(newText, extra)
Updates the text layer of an active message in-place without generating a new chat block. **Crucial rule:** This can only be called if the context update was triggered by an inline button click (bot.action).
```typescript
bot.action('confirm_save', async (ctx) => {
    await ctx.answerCbQuery();
    // Updates the confirmation screen seamlessly
    await ctx.editMessageText('✅ Exam successfully synced into the cloud vault.');
});

```
#### ctx.editMessageReplyMarkup(markup)
Changes, swaps, or completely deletes the button layout attached to an existing message without touching the text content.
```typescript
// Removes all buttons from the message after selection is finished
await ctx.editMessageReplyMarkup(undefined);

```
#### ctx.deleteMessage(messageId?)
Deletes a message from the chat history. If no explicit messageId is passed, it attempts to delete the message that triggered the current update context.
```typescript
bot.hears('clear_spam', async (ctx) => {
    // Vaporizes the user's triggering text message instantly
    await ctx.deleteMessage();
});

```
### C. Feedback & UX Shortcuts
#### ctx.answerCbQuery(text?, options?)
**Mandatory lifecycle requirement for buttons.** When a user taps an inline button, their Telegram client goes into a loading state (spinning clock icon). Calling this method immediately halts that spinner.
 * Passing a text string creates a clean toast notification popup at the top of the app interface.
 * Setting { show_alert: true } forces a modal alert block that the user must manually dismiss.
```typescript
bot.action('wrong_answer', async (ctx) => {
    // Halts loading and forces a structural alert modal popup
    await ctx.answerCbQuery('Incorrect Choice! ❌', { show_alert: true });
});

```
#### ctx.sendChatAction(action)
Triggers a temporary status flag visible at the top bar of the user's interface, letting them know the bot is actively processing an asset.
 * Available Actions: 'typing' | 'upload_photo' | 'record_video' | 'find_location' | 'upload_document'
```typescript
bot.command('download_report', async (ctx) => {
    // Shows "bot is uploading a document..." while your database generates files
    await ctx.sendChatAction('upload_document');
    // ... complete long-running file compilation tasks ...
    await ctx.replyWithDocument({ source: './report.xlsx' });
});

```
## 5. Bypassing Context: ctx.telegram
Sometimes, you need to break out of the incoming update sandbox entirely. If your database fires a webhook notification that an exam window has opened, or an admin wants to push a forced message to a specific user, you do not have an active ctx tracking loop.
ctx.telegram acts as a gateway access key to the underlying **raw Telegram Bot API wrapper**. It exposes every structural method available on the bot instance, but **requires explicit passing of destination target keys**.
```typescript
// Broadcasting an out-of-band notification directly to a targeted user ID
const targetTeacherChatId = '592019481';

await ctx.telegram.sendMessage(
    targetTeacherChatId, 
    '⚠️ Security Alert: A new login was registered on your exam builder panel.'
);

```
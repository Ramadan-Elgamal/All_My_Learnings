#  The Telegraf Instance (The Engine)

The `Telegraf` class is the main engine of your application. It acts as the root orchestrator: it holds your secret token, sets up global configurations, manages incoming connections, and handles routing to downstream files.

---
## 1. Instantiation

To initialize the bot, you import the class and pass your secret token. In typescript, you also pass your custom context interface so that all downstream files inherit your database clients, session types, and state models.

```typescript
import { Telegraf } from 'telegraf';
import { TeacherContext } from './types/context';

const bot = new Telegraf<TeacherContext>(process.env.TELEGRAM_TOKEN);

```
## 2. Comprehensive Method Reference & Examples
### A. Global Middleware: bot.use()
Registers a function that intercepts **every single update** coming from Telegram (text, photos, button clicks, channel posts) before any specific command or event handlers see it.
 * **Why use it:** Global authorization checks, injecting database clients (Supabase), logging, or rate-limiting.
```typescript
// Example: Global logger and metric injector
bot.use(async (ctx, next) => {
    console.log(`Incoming update ID: ${ctx.update.update_id} from Chat ID: ${ctx.chat?.id}`);
    
    // Injecting a custom timestamp parameter into state for processing speed metrics
    ctx.state.receivedAt = Date.now();
    
    // Non-negotiable: passes control to the next handler down the chain
    await next(); 
});

```
### B. Command Listener: bot.command()
Listens specifically for text messages that begin with a forward slash (/). Telegram automatically treats these as special clickable commands.
 * **Why use it:** Entry points for menus, starting forms (/create), displaying help dialogs, or resetting sessions.
```typescript
// Example: Handling a standard /start command with custom context properties
bot.command('start', async (ctx) => {
    await ctx.reply('Welcome! Use /create to build a new exam or /help for guidance.');
});

// Example: Multiple aliases pointing to the same handler
bot.command(['help', 'info', 'guide'], async (ctx) => {
    await ctx.reply('This bot allows teachers to create custom exams. Commands:\n/create - Start wizard');
});

```
### C. Predefined Event Listener: bot.on()
Listens for specific Telegram event categories (Update Types or Message Subtypes). You cannot pass custom strings here; you must use predefined types.
 * **Why use it:** Catching assets (images, documents), handling text input, or managing group events (users joining/leaving).
```typescript
// Example 1: Catching text input that isn't a command
bot.on('text', async (ctx) => {
    const text = ctx.message.text;
    await ctx.reply(`You typed: "${text}". Use a command if you want to perform an action.`);
});

// Example 2: Handling photo attachments for exam questions
bot.on('photo', async (ctx) => {
    // Grab the highest resolution version of the photo
    const photoId = ctx.message.photo[ctx.message.photo.length - 1].file_id;
    await ctx.reply(`Photo received! System ID: ${photoId}. Saving to exam attachments...`);
});

// Example 3: Housekeeping when someone is removed from a group chat
bot.on('left_chat_member', async (ctx) => {
    const user = ctx.message.left_chat_member;
    console.log(`User ${user.first_name} (ID: ${user.id}) left the group.`);
});

```
### D. Text Matcher: bot.hears()
Listens to standard text messages. Unlike bot.command, it does not require a slash. It checks if the text matches a specific string or a regular expression (Regex).
 * **Why use it:** Creating natural text interfaces, catching custom keyboard button labels, or simple filtering.
```typescript
// Example 1: Direct String Match
bot.hears('Cancel', async (ctx) => {
    await ctx.reply('Operation cancelled.');
});

// Example 2: Regular Expression (Case-Insensitive Match)
// Matches "hi bot", "hello bot", "hey bot", etc.
bot.hears(/^(hi|hello|hey)\s+bot/i, async (ctx) => {
    await ctx.reply(`Hello ${ctx.from?.first_name}! How can I help you today?`);
});

```
### E. Interactive Button Click Listener: bot.action()
Listens for callback queries. This event triggers exclusively when a user clicks an inline keyboard button attached to a message.
 * **Why use it:** Capturing choice selections, quiz answers, pagination clicks, or form submissions without adding text clutter to the chat.
```typescript
// Example 1: Specific Action Payload
bot.action('accept_terms', async (ctx) => {
    await ctx.answerCbQuery('Terms accepted!'); // Clears button loading wheel
    await ctx.editMessageText('Thank you for accepting the terms. You may now continue.');
});

// Example 2: Dynamic Regex Action Payload
// Matches buttons returning payloads like "delete_exam_102" or "delete_exam_405"
bot.action(/^delete_exam_(\d+)$/, async (ctx) => {
    await ctx.answerCbQuery();
    
    // Extracting the captured digits from the regex match array
    const examId = ctx.match[1]; 
    
    await ctx.reply(`Request received to permanently delete exam record #${examId}.`);
});

```
## 3. Running the Engine
### A. Development Mode: bot.launch()
Establishes a connection to Telegram via **Long Polling**. Your application loops continuously, asking Telegram's servers if there are any new updates.
```typescript
// Turning on the engine locally
bot.launch(() => {
    console.log('--- Bot Engine Successfully Ignited (Long Polling) ---');
});

// Graceful Termination Process (Prevents locked processes in your terminal)
process.once('SIGINT', () => bot.stop('SIGINT'));
process.once('SIGTERM', () => bot.stop('SIGTERM'));

```
### B. Production Mode: bot.handleUpdate()
Bypasses long polling completely. Instead of your server polling Telegram, Telegram sends an HTTP POST request containing the update payload directly to your serverless endpoint. You pass that payload directly to this method to handle execution.
```typescript
// Example: Conceptual representation inside an HTTP Server Router or Next.js API route
export async function POST(request: Request) {
    const jsonPayload = await request.json();
    
    // Feed the update directly to the Telegraf router processing engine
    await bot.handleUpdate(jsonPayload); 
    
    return Response.json({ status: 'processed' });
}

```
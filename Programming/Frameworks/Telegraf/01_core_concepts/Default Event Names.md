
# Predefined Event Names & Filters

Telegraf uses explicit event filtering via the `bot.on()` method. When an update arrives from Telegram, it is categorized into specific structural buckets based on its payload type. You cannot pass arbitrary strings to these filters; you must use the predefined event names defined by the Telegram Bot API and Telegraf's type definitions.

---

## 1. Primary Update Types

These are the highest-level categories. Every single interaction falls into exactly one of these root buckets.

```typescript
// Catching the absolute root update container
bot.on('message', async (ctx) => {
    await ctx.reply('You sent a standard message interaction.');
});

bot.on('edited_message', async (ctx) => {
    await ctx.reply('I saw that you edited your previous message.');
});

bot.on('callback_query', async (ctx) => {
    // Triggers on any inline button click if no specific bot.action() matched it
    await ctx.answerCbQuery();
});

```
## 2. Message Subtypes (Granular Filters)
When an incoming update is classified under the primary 'message' type, Telegraf looks inside the payload to see what specific kind of media or data it contains. You can target these directly.
### Media & Input Filters
#### 'text'
Triggers exclusively when a user sends a plain text message, a markdown-formatted message, or an unrecognized command string.
```typescript
bot.on('text', async (ctx) => {
    const textData = ctx.message.text;
    await ctx.reply(`Processing plain text input: ${textData}`);
});

```
#### 'photo'
Triggers when an image file is sent through the chat (compressed by Telegram's native optimization). Telegram provides an array of photo objects representing different resolutions of the same image.
```typescript
bot.on('photo', async (ctx) => {
    // The last element in the array is always the highest available resolution
    const highestResPhoto = ctx.message.photo[ctx.message.photo.length - 1];
    const fileId = highestResPhoto.file_id;
    await ctx.reply(`Photo asset captured. System reference key: ${fileId}`);
});

```
#### 'document'
Triggers when an uncompressed file, a PDF, a spreadsheet, a configuration file, or an image sent as a "File" attachment arrives.
```typescript
bot.on('document', async (ctx) => {
    const docName = ctx.message.document.file_name;
    const docMime = ctx.message.document.mime_type;
    await ctx.reply(`Document received: ${docName} (Format: ${docMime})`);
});

```
#### 'voice' & 'video_note'
Triggers on voice messages recorded natively inside the chat interface ('voice') or circular video messages ('video_note').
```typescript
bot.on('voice', async (ctx) => {
    const duration = ctx.message.voice.duration;
    await ctx.reply(`Audio payload received. Duration: ${duration} seconds.`);
});

```
## 3. Metadata & System Event Filters
These event names do not listen for content created by users, but rather for infrastructure changes within the chat environment itself.
| Event Name | Triggering Condition | Common Use Case |
|---|---|---|
| 'new_chat_members' | A new user or bot joins a group chat where the bot resides. | Triggering automated onboarding or welcome panels. |
| 'left_chat_member' | A user leaves or is kicked from a group chat environment. | Syncing local group rosters or clearing permissions. |
| 'my_chat_member' | The bot's own access state changes (promoted, demoted, blocked). | Handling database lifecycle flags when a user blocks the bot. |
| 'pinned_message' | An administrator pins a message inside a group or channel. | Logging group announcements or modifying configuration state. |
```typescript
// Example: Tracking block/unblock states
bot.on('my_chat_member', async (ctx) => {
    const oldStatus = ctx.myChatMember.old_chat_member.status;
    const newStatus = ctx.myChatMember.new_chat_member.status;
    
    if (newStatus === 'kicked') {
        console.log(`User ${ctx.from?.id} has blocked the bot. Mark record inactive.`);
    } else if (newStatus === 'member') {
        console.log(`User ${ctx.from?.id} has unblocked/restarted the bot.`);
    }
});

```
## 4. Advanced: Combining Filters
Telegraf allow you to pass an array of event names to a single handler function. The code execution block will trigger if **any** of the conditions listed inside the array are successfully met.
```typescript
// Example: Blocking media uploads during strict testing configurations
bot.on(['photo', 'document', 'video', 'voice'], async (ctx) => {
    await ctx.reply('❌ System Warning: Media submissions are closed during an active exam block.');
});

```
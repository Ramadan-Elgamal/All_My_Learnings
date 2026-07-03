### Phase 1: Create the Slack Bot

1. Open your browser and go to the [Slack API Dashboard](https://api.slack.com/apps). Ensure you are logged into your workspace.
2. Click the green **Create New App** button.
3. Select **From scratch**
4. **App Name:** Give it a clear name.
5. **Workspace:** Select the workspace where Sara's agency operates (or your test workspace), and click **Create App**.

### Phase 2: Give the Bot Permission to Speak

Right now, your bot exists, but it isn't allowed to do anything. We need to give it permission to write messages.

1. On the left-hand sidebar of your new app's settings, click on **OAuth & Permissions**.
2. Scroll down to the section titled **Scopes**, and specifically look for **Bot Token Scopes**.
3. Click the **Add an OAuth Scope** button.
4. Type in `chat:write` and select it. _(This is the strict permission that allows your bot to post messages in channels)._
5. Scroll back up to the OAuth Tokens section of that same page and click the **Install to Workspace** button.
6. Slack will ask you to confirm that the bot can access the workspace. Click **Allow**.
7. You will immediately be brought back to the OAuth page, and you will see a newly generated **Bot User OAuth Token** that starts with `xoxb-`. **Copy this token.**

### Phase 3: Connect to n8n

Now we hand that token to n8n so it can act as the bot.

1. Open your n8n canvas and drag a **Slack** node onto the screen (connect it after your GitHub node for now).
2. In the node configuration panel on the right, under **Authentication**, ensure **Access Token** is selected (do not use OAuth2 for this setup).
3. Under **Credential to connect with**, click the dropdown and select **Create New Credential**.
4. A new window will pop up. Paste your `xoxb-` token into the **Access Token** field.
5. Click **Save**.

### ⚠️ The "Not in Channel" Error

There is one massive trap that catches almost every beginner building a Slack automation: **Bots cannot post in channels they haven't been invited to!**

Even after your credentials are fully connected and green in n8n, if you try to send a message to `#engineering-alerts`, it will fail unless the bot is physically sitting in that room.

**How to fix it before it happens:**

1. Open your actual Slack application.
2. Go to the whatever channel you are testing with or the client own channel.
3. Type `/invite` in the message bar and hit enter and choose the Third option to add an app.
4. Search for your bot's name (e.g., `GitHub Issue Notifier`) and add it to the channel.

Your n8n workflow is now fully authorized to speak in your Slack workspace!
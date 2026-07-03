### Phase 1: Generate the Token in GitHub

1. Log in to your GitHub account and click your profile picture in the top-right corner, then select **Settings**.
2. Scroll all the way down the left sidebar and click **Developer settings**.
3. In the left menu, expand **Personal access tokens** and select **Tokens (classic)**. _(Instructor Note: While GitHub offers new "fine-grained" tokens, the Classic tokens are much easier to configure for n8n webhook triggers on your first try)._
4. Click the **Generate new token** dropdown button and select **Generate new token (classic)**.
5. **Note:** Name it something recognizable, like `n8n Slack Notifier`.
6. **Expiration:** Set this to whatever you are comfortable with (e.g., 90 days or No expiration for a permanent local testing token).
7. **The Crucial Step (Scopes):** You must check two specific boxes so n8n has the right permissions:
    - Check **`repo`** (This grants access to read your repositories and issues).
    - Check **`admin:repo_hook`** (This is strictly required. It allows n8n to automatically create and manage the webhook that listens for new issues).
8. Scroll to the bottom and click **Generate token**.
9. **Copy the token immediately.** It will start with `ghp_`. GitHub will never show you this token again once you leave the page!
    

### Phase 2: Add the Credentials to n8n
1. Open your n8n canvas and drag a **GitHub Trigger** node onto the screen.
2. In the node configuration panel on the right, look for **Credential to connect with**.
3. Click the dropdown and select **Create New Credential**.
4. A new window will pop up. Fill in the two required fields:
    - **User:** Type in your exact GitHub username.
    - **Access Token:** Paste the `ghp_` token you just copied from GitHub.
5. Click **Save** in the top right corner.
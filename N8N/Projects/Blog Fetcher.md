## Description
Fetches the latest articles from a favorite blog and emails them to your inbox daily.

## Blueprint
1. **Schedule Trigger** (Runs every 3 hours)
2. **Google Sheets** (Gets the 5 URLs)
3. **Loop Over Items** _--> Loop branch goes to:_
    - **RSS Read** (Fetches the feed)
    - **Filter** (Is the article strictly from the last 3 hours?)
    - _(Wire goes back to Loop Over Items)_

## Nodes Used


## Tutorials & Notes

### How to add Google Sheets Credentials

#### 1. Create a Google Cloud Project

1. Go to [Google Cloud Console](https://console.cloud.google.com/?utm_source=chatgpt.com)
2. Create a new project or use existing one.
3. Open **APIs & Services → Library**.
4. Enable:
    - **Google Sheets API**
    - **Google Drive API** (recommended because n8n often uses it to find spreadsheets)
---
#### 2. Create OAuth Credentials

1. Go to **APIs & Services → Credentials**.
2. Click **Create Credentials → OAuth Client ID**.
3. If prompted, configure the OAuth consent screen:
    - External (for personal use)
    - Fill in the required fields
    - Add yourself as a test user if Google asks
4. Create an **OAuth Client ID**:
    - Application Type: **Web Application**
5. Add the redirect URL from n8n.
    
For self-hosted n8n, it usually looks like:

```text
https://your-n8n-domain/rest/oauth2-credential/callback
```

For local development:

```text
http://localhost:5678/rest/oauth2-credential/callback
```

You can find the exact URL inside n8n when creating the credential.

---
#### 3. Create the Credential in n8n

1. In n8n:
    - Open **Credentials**
    - Click **Create Credential**
    - Search for **Google Sheets OAuth2 API**
2. Copy:
    - Client ID
    - Client Secret
    
    from Google Cloud into n8n. Make sure you copy the Client Secret because if you close the modal, you won't be able to copy again.
1. Click **Connect my account**.
2. Sign in with your Google account and approve access.

---
## Common Issue (Self-Hosted)

#### 1 - If the Google login page says:

> Error 400: redirect_uri_mismatch

it means the callback URL in Google Cloud does not exactly match the callback URL shown by n8n.

Copy the callback URL displayed in the n8n credential page and paste it into the **Authorized Redirect URIs** section in Google Cloud exactly as shown.

---
#### 2 - If you got the following message:
(your-domain) has not completed the Google verification process. The app is currently being tested, and can only be accessed by developer-approved testers. If you think you should have access, contact the developer.

If you are a developer of (your-domain), see error details.
Error 403: access_denied

That means your Google OAuth app is in **Testing** mode and the Google account you're using is **not listed as a test user**.
##### Fix
1. Go to Google Cloud Console.
2. Open **APIs & Services → OAuth consent screen**.
3. Scroll to **Test users**.
4. Add the Gmail address you're trying to log in with.
5. Save.
6. Wait a minute or two.
7. Try connecting from n8n again.
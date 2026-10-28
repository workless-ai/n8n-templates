# 02 · Connect Gmail to self-hosted n8n: checklist

There's no workflow file for this one. Video 2 connects Gmail credentials, and credentials are private to each person. Instead, here's every step from the Workless video **"Fix n8n Gmail 'Access Blocked': Connect Google Credentials (Self-Hosted, 2026)"** as a checklist. Tested on n8n 2.44 and 2.45, running on a computer (localhost), in October 2026.

## Checklist

**In Google Cloud ([console.cloud.google.com](https://console.cloud.google.com))**

- [ ] Create a new project (for example, *n8n Gmail*).
- [ ] **Library** → search **Gmail API** → **Enable**.
- [ ] Consent screen (**Google Auth Platform**): click **Get started**, name the app, and pick your email. For a normal Gmail account, choose **External**. Then finish.
- [ ] **Audience** → **Test users** → add **your own Gmail address**. *Skip this, and Google says "Access blocked".*
- [ ] **Clients** → **Create client** → type **Web application**.

**In n8n**

- [ ] Create a **Gmail** credential and copy its **OAuth Redirect URL**.
- [ ] Back in Google Cloud, paste it into **Authorized redirect URIs**. It must match exactly. On your own computer, it is:
  ```
  http://localhost:5678/rest/oauth2-credential/callback
  ```
- [ ] Click **Create**, then copy the **Client ID** and **Client Secret** into the n8n credential.
- [ ] Click **Sign in with Google**, pick your account, check what n8n is asking for, and click **Allow**. If Google says it hasn't verified the app, continue: it's your own app.
- [ ] You should see **Connection successful**.

## Errors this fixes

| Error | Cause | Fix |
|---|---|---|
| `Access blocked: … has not completed the Google verification process` / `Error 403: access_denied` | Your address isn't a test user | Audience → Test users → add yourself |
| `Error 400: redirect_uri_mismatch` | The redirect URI in Google doesn't exactly match n8n's | Copy n8n's OAuth Redirect URL again and paste it exactly |
| A Gmail node says the token expired, about a week later | Apps in **Testing** are signed out every 7 days | Open the credential in n8n and click **Reconnect** |

## Why not just publish the app?

Google only lifts the 7-day limit for published apps. Publishing now needs a home page, a privacy policy and terms of service under **Branding**, and Google keeps the **Publish app** button disabled until those are filled in. For a personal setup, reconnecting once a week is simpler.

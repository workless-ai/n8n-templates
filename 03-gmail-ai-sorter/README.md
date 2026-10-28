# 03 · AI inbox sorter (Gmail + free Gemini)

A free AI reads each new email and labels it **Clients**, **Invoices** or **Newsletters**. Anything else is left alone. This is the workflow from the Workless video **"Auto-Label Gmail with Free AI in n8n (Gemini, No OpenAI)"**.

**Nodes:** Gmail Trigger → Text Classifier (Google Gemini Chat Model) → Gmail "Add label" ×3

- **Needs:** a Gmail credential in n8n (video 2 shows how) and a free Gemini API key from [Google AI Studio](https://aistudio.google.com).
- **Tested on:** self-hosted n8n 2.45 with Gemini 3.5 Flash Lite (October 2026). We imported this exact file, connected it, published it and sent three test emails. Each one landed in the right label.

## Use it

1. Download [`workflow.json`](workflow.json) (**Download raw file** button).
2. In n8n, create a new workflow, then go to **⋯ → Import → From file** and choose the file. If n8n asks *"Importing this from an AI tool?"*, click **Skip**.
3. Open **Gmail Trigger** and each **Label** node, and pick your Gmail credential. Open **Google Gemini Chat Model** and pick (or create) your Gemini credential. If you have only one, n8n fills it in for you.
4. In Gmail, create the labels **Clients**, **Invoices** and **Newsletters**. Then, in each Label node, pick its label under **Label Names or IDs**.
5. Click **Publish**. n8n checks for new mail every minute.

## Before you use it on your real inbox

- **It only sorts test emails at first.** The Gmail Trigger has the Search filter `from:me to:me`, so it only sorts emails you send to yourself. Send yourself a test email or two, and when you're happy, delete that filter so it sorts all new mail.
- **Change the categories:** edit them in the Text Classifier. A clear description for each one helps the AI most. Add a Label node for each new output.
- **Free tier:** Gemini's free tier has daily limits, and Google may use what you send to improve its products.
- **Self-hosted n8n with Gmail in "Testing" mode:** Google signs n8n out every 7 days, so open the credential and click **Reconnect** (video 2 explains this).

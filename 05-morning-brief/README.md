# 05 · Morning brief (Hacker News → free Gemini → Gmail)

Every morning at 7:00, this workflow reads the Hacker News front page, keeps the 10 newest stories, has Google Gemini write 5 short bullet points for a freelancer, and emails them to you. It's the workflow from the Workless video **"Free AI Builds Your n8n Workflow: The Prompt That Works (ChatGPT, Claude, Gemini)"**. Claude (free plan) built it from the prompt below, and it worked on the first try.

**Nodes:** Schedule Trigger → RSS Read → Limit (10) → Aggregate → Google Gemini (Message a model) → Gmail

- **Needs:** a free Gemini API key from [Google AI Studio](https://aistudio.google.com) and a Gmail credential in n8n ([02 checklist](../02-gmail-connect) for self-hosted n8n).
- **Tested on:** self-hosted n8n 2.45.4 with Gemini 3.5 Flash (October 2026). We imported this exact file, connected Gemini and ran it: 30 stories in, 10 kept, a real 5-bullet summary out. The email step stops until you put in your own address.

## Use it

1. Download [`workflow.json`](workflow.json) (**Download raw file** button).
2. In n8n, create a new workflow, then go to **⋯ → Import → From file** and choose the file. If n8n asks *"Importing this from an AI tool?"*, click **Skip**.
3. **Message a model:** pick your Gemini credential.
4. **Send a message:** connect Gmail and replace `YOUR EMAIL ADDRESS` in **To** with your address.
5. **⋯ → Settings → Timezone:** choose yours, so 7:00 is your 7:00 (a fresh self-hosted install uses New York time).
6. Click **Execute** once, read the email, then **Publish**.

## Good to know

- **Retry On Fail is on** in the Gemini node (5 tries, 5 s apart). Google's free tier sometimes answers *"This model is currently experiencing high demand"*; the retry gets past it.
- **Make your own version with free AI:** the full prompt is in the video's description. Copy your own empty nodes from n8n into it, add one sample item from a test run, and keep the rules. Then check the 5 things: trigger, model, expressions, fields after the AI step, and the actual output.
- **Free tier:** Gemini's free tier has daily limits per model, and Google may use what you send to improve its products.

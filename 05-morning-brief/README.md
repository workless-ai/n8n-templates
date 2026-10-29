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
- **Make your own version with free AI:** use the prompt below. Copy your own empty nodes from n8n into it, add one sample item from a test run, and keep the rules. Then check the 5 things: trigger, model, expressions, fields after the AI step, and the actual output.
- **Free tier:** Gemini's free tier has daily limits per model, and Google may use what you send to improve its products.

## The prompt that works

From the video, word for word (YouTube doesn't allow its curly brackets in descriptions, so it lives here). Fill in the parts in CAPITALS.

```
Fill in this n8n workflow so I can paste it straight back into n8n.

GOAL: YOUR GOAL, e.g. every day at 7:00, read https://news.ycombinator.com/rss, keep the 10 newest stories, have Google Gemini (model models/gemini-3.5-flash) write 5 short bullet points for a freelancer, and email them to me@example.com with Gmail.

SAMPLE DATA from a test run:
- One item from RSS Read: PASTE ONE ITEM FROM THE NODE'S JSON OUTPUT
- What 'Message a model' outputs: {"content": {"parts": [{"text": "..."}], "role": "model"}}

RULES:
1. Use exactly these nodes. Keep every node's type and typeVersion, fill in its parameters, and add the connections.
2. Only reference fields that appear in the sample data. Any parameter that uses {{ }} must start with =.
3. Don't change the model name. Reply with the complete workflow JSON in one code block, and nothing else.
4. An AI node replaces each item with its answer. To use fields from before it (like title or link), read them from the earlier node, e.g. {{ $('Limit').item.json.title }}.

MY NODES (copied from n8n):
PASTE YOUR EMPTY NODES HERE (add them in n8n, select all, Ctrl/Cmd+C, Skip)
```

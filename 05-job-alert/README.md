# 05 · Job alert (We Work Remotely → free Gemini YES/NO → Gmail)

Every weekday at 8:00, this workflow reads the remote design jobs feed from We Work Remotely, keeps the 15 newest jobs, asks Google Gemini whether each one suits a freelance web designer (YES or NO), keeps the YES jobs and emails you one list of titles and links. It's the second workflow from the Workless video **"Free AI Builds Your n8n Workflow: The Prompt That Works (ChatGPT, Claude, Gemini)"**.

**Nodes:** Schedule Trigger → RSS Read → Limit (15) → Google Gemini → **Edit Fields** → Filter (YES) → Aggregate → Gmail

- **Needs:** a free Gemini API key from [Google AI Studio](https://aistudio.google.com) and a Gmail credential in n8n ([02 checklist](../02-gmail-connect) for self-hosted n8n).
- **Tested on:** self-hosted n8n 2.45.4 with Gemini 3.5 Flash Lite (October 2026). We imported this exact file, connected Gemini and ran it: 23 jobs in the feed, 15 checked, 1 YES with its title and link. The email step stops until you put in your own address.

## Use it

1. Download [`workflow.json`](workflow.json) (**Download raw file** button).
2. In n8n, create a new workflow, then go to **⋯ → Import → From file** and choose the file. If n8n asks *"Importing this from an AI tool?"*, click **Skip**.
3. **Message a model:** pick your Gemini credential, and change the question to match the jobs you want.
4. Want a different field? Swap the feed URL in **RSS Read** for another We Work Remotely category feed.
5. **Send a message:** connect Gmail and replace `YOUR EMAIL ADDRESS` in **To** with your address.
6. **⋯ → Settings → Timezone:** choose yours. Click **Execute** once, then **Publish**.

## Good to know

- **Why the Edit Fields node:** an AI node replaces each item with its answer, so after Gemini the job's title and link are gone. Edit Fields puts them back next to the answer (`{{ $('Limit').item.json.title }}`). Without it, the email gets only "YES".
- **Free tier:** this workflow makes 15 Gemini calls every run, and the free key has a daily limit per model. That's why it uses gemini-3.5-flash-lite, with Retry On Fail on (5 tries, 5 s apart).
- **Results vary:** the same jobs can get a different number of YES answers from run to run. If you get none, make the question less strict.
- Google may use what you send on the free tier to improve its products.

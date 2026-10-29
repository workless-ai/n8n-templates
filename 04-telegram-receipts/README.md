# 04 · Receipt bookkeeper (Telegram + free Gemini + Google Sheets)

Send a receipt photo to your own Telegram bot. Free AI (Google Gemini) reads it, adds a row to Google Sheets (date, shop, category, total, currency) and replies to confirm. Type **/total** to get your spending by category. This is the workflow from the Workless video **"Snap a Receipt, It Lands in Google Sheets: Free AI Bookkeeper (Telegram + Gemini + n8n)"**.

**Nodes:** Telegram Trigger → Switch (photo or /total) → Basic LLM Chain (Gemini + Structured Output Parser) → Google Sheets → Telegram reply; and for /total: Google Sheets → Summarize → Telegram reply.

- **Needs:**
  - a Telegram bot token from [@BotFather](https://t.me/BotFather)
  - a free Gemini API key from [Google AI Studio](https://aistudio.google.com)
  - a Google Sheets credential in n8n
  - a public **https** address for n8n, so Telegram can reach it: n8n Cloud, or a tunnel if n8n runs on your own computer
- **Tested on:** self-hosted n8n 2.45 through a temporary tunnel, with Gemini 3.5 Flash Lite (October 2026). We imported this exact file, connected it and published it. Then we sent three receipt photos and /total from Telegram: every receipt got a row and a reply, and /total added them up correctly.

## Use it

1. Download [`workflow.json`](workflow.json) (**Download raw file** button).
2. In n8n, create a new workflow, then go to **⋯ → Import → From file** and choose the file. If n8n asks *"Importing this from an AI tool?"*, click **Skip**.
3. Make a Google Sheet whose first row is: `Date` `Merchant` `Category` `Total` `Currency` `Logged`. Keep the tab's name **Sheet1**.
4. Connect your credentials: Telegram in the trigger and both reply nodes, Gemini in **Google Gemini Chat Model**, and Google Sheets in both Sheets nodes.
5. In **Append row in sheet** and **Get row(s) in sheet**, replace the placeholder link under **Document** with your sheet's link. The column mapping is already filled in, and it stays when you paste your link.
6. Click **Publish**, open your bot in Telegram, and send it a receipt photo.

## /total report text

The video says this expression is in the description, but YouTube doesn't allow its `=>` arrows there, so here it is. It's already set up in the template's **Send the total** node (Expression mode, with **Execute Once** on in Settings):

```
Spending by category:
{{ $input.all().map(i => i.json.Category + ': ' + i.json.sum_Total.toFixed(2)).join('\n') + '\n\nTotal: ' + $input.all().reduce((a, i) => a + i.json.sum_Total, 0).toFixed(2) }}
```

## Good to know

- **The prompt includes today's date, which isn't in the video.** We tested a receipt that prints only "29 OCT". Without the date in the prompt, Gemini filled in the wrong year (2024) all 3 times. With it, all 3 were correct (2026).
- **Time zone:** the date in the prompt and the **Logged** time use n8n's time zone. On a fresh self-hosted install that's New York time, so set your own in the workflow's settings.
- **Self-hosted Google Sheets credential:** use the same Google Cloud steps as for Gmail ([02 checklist](../02-gmail-connect)), but enable the **Google Sheets API** instead of the Gmail API.
- **Categories:** edit the list in the prompt (Meals, Office, Travel, Software, Other). A fixed list keeps your totals adding up.
- **Free tier:** Gemini's free tier has daily limits, and Google may use what you send to improve its products. Don't send receipts you need to keep private.

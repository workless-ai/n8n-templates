# Workless n8n templates

Free n8n workflows from the **Workless** YouTube channel: free AI automation tutorials, step by step.

Every workflow here was built and tested in a real n8n install for its video. No sign-up and no email needed: download and import.

## How to import a workflow

1. Open the video's folder and the `workflow.json` file, then click **Download raw file**.
2. In n8n, create a new workflow, then go to **⋯ → Import → From file** and choose the file. If n8n asks *"Importing this from an AI tool?"*, click **Skip**.
3. Open each node with a warning and connect **your own** credentials (Gmail, Google Sheets, Gemini…). No credentials or keys are included.
4. Click **Execute** once to test, then **Publish**.

## Workflows

| # | Video | Folder |
|---|---|---|
| 01 | n8n's one-command install: weather check form | [01-weather-form](01-weather-form) |
| 02 | Connect Gmail to self-hosted n8n (checklist, no workflow) | [02-gmail-connect](02-gmail-connect) |
| 03 | Auto-label Gmail with free AI (Gemini) | [03-gmail-ai-sorter](03-gmail-ai-sorter) |

## Notes

- Built for self-hosted n8n 2.x (the free one-line install) and n8n Cloud.
- AI steps use Google's free Gemini API unless the README says otherwise. Free tiers have daily limits.
- Found a problem? Open an issue and say which n8n version you're on.

## License

MIT: use, change and share these freely, including in client work.

# 01 · Weather check form

Type a city into a form and get its weather back. This is the first workflow from the Workless video **"n8n's New One-Command Install: Run It Free on Your Own Computer"**.

**Nodes:** Form trigger → HTTP Request → Form ending

- **Needs:** nothing. It uses [wttr.in](https://wttr.in), which is free and needs no account and no API key.
- **Tested on:** self-hosted n8n 2.45 (October 2026). We imported this exact file into an empty workflow and ran it.

## Use it

1. Download [`workflow.json`](workflow.json) (**Download raw file** button).
2. In n8n, create a new workflow, then go to **⋯ → Import → From file** and choose the file.
3. If n8n asks *"Importing this from an AI tool?"*, click **Skip**.
4. Click **Execute** at the bottom and type a city in the form that opens.

You'll get a line like `London: ☁️ +15°C`.

## Make it yours

- **Different weather format:** change `?format=3` in the HTTP Request URL. For example, `?format=4` adds wind ([all formats](https://github.com/chubin/wttr.in#one-line-output)).
- **Always on:** click **Publish**. The form then gets a permanent link you can bookmark or share.

## Copy-paste from the video

YouTube doesn't allow curly brackets in descriptions, so the copy-paste text from the video lives here.

Weather URL (HTTP Request node, Expression mode):

```
https://wttr.in/{{ $json.City }}?format=3
```

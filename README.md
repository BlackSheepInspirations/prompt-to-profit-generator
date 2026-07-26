# Prompt to Profit Generator

An AI **marketing-prompt studio** for creators and small product sellers. Describe
your product once, choose what you want to create, and get professional,
copy-and-paste-ready AI prompts — tuned to your brand, offer, and the exact AI
tool you use.

No build step, no dependencies. It's a static site (HTML + CSS + vanilla JS) that
runs by opening a file.

## Run it

```bash
open index.html
```

Or serve it locally (any static server works), e.g.:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## What it does

1. **Your product** — enter product, audience, pricing, and brand voice. Most
   choices are quick tap-to-select pills (single- and multi-select).
2. **What to make** — pick up to four "creators" from a 35-item library
   (sales copy, social, images, video, launch) and fine-tune each.
3. **Get your pack** — choose your AI platform and delivery format, then
   **Generate**. A sticky rail keeps your readiness checklist and the Generate
   button in view the whole time.

You get multiple prompt options per creator, an assembled package (standalone /
separate / combined / hybrid), and a quality score.

### Premium Output Modules

Every generation also produces four complete, ready-to-use deliverables from the
same inputs:

- **Suno AI Music Prompt** — a style prompt plus full, structured lyrics.
- **Video Script Prompt** — a full short-form script with shot list and hashtags.
- **Marketing Campaign Prompt** — one prompt that yields email, social, an ad,
  and subject lines.
- **Custom GPT Builder** — a complete GPT configuration: instructions, knowledge
  files, conversation starters, welcome message, rules, and a testing checklist.

Use **Download Everything (.txt)** to export the final package plus all premium
modules in a single file.

## Project structure

```
index.html      Markup and content
css/style.css   Design system (teal + gold tokens, light + dark) and all styling
js/script.js    All behavior — state, generation, pills, premium modules, export
assets/         Hero walkthrough video (how-to.mp4) and poster
```

## Add your walkthrough video

Drop a file at `assets/how-to.mp4` (H.264/AAC MP4, 16:9). The hero player picks it
up automatically; an optional `assets/how-to-poster.jpg` sets the thumbnail.

## Notes

- Everything is saved locally in your browser (no account, no server). Your
  current project, product/brand profiles, and saved packages persist on the
  device via `localStorage`.
- Fonts load from Fontshare with system-font fallbacks if offline.
- Light and dark themes follow your OS preference.

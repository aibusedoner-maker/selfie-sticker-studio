# Selfie Sticker Studio

One selfie in, eight chat stickers that actually look like you out. A 2-day 0→1 prototype.

**Live:** https://selfie-sticker-studio-ai-buse-doner.vercel.app

- Single static `index.html`, no build step.
- Bring-your-own Gemini API key (kept in the browser, sent only to Google).
- 3 styles (real / 3D animated / vinyl toy) × 8 expressions.
- Client-side chroma-key background removal + white sticker outline, 512×512 PNG.
- Save via Web Share (→ WhatsApp "Create sticker") or ZIP fallback.
- Fake-door test for a paid 12-expression pack.
- Lab drawer: time-to-first-sticker, 👍 rate, background-removal rate, cost per pack, and a vision-model judge (identity / expression / quality, 1–5).

# Selfie Sticker Studio

One selfie in, eight chat stickers that actually look like you out. A 2-day 0→1 prototype by Buse Doner (October 2026).

**Live:** https://selfie-sticker-studio-ai-buse-doner.vercel.app

## What it is

A mobile-first web page that turns a single selfie into a pack of 8 expressive stickers (laughing, facepalm, shocked, crying, in love, eye roll, thumbs up, suspicious) in one of three styles: real photo cutout, 3D animated, or vinyl toy. Stickers are exported as 512×512 transparent PNGs and added to WhatsApp through its built-in "Create sticker" flow, so no native app is needed.

It was built as a **test bench for the riskiest assumption**: can an image model keep a person recognisable across exaggerated expressions, fast and cheaply enough for a free first pack?

## What the test found

| | Cheapest image model | Top-tier image model |
|---|---|---|
| Same person across the pack | ✅ | ✅ |
| **Looks like the user** | ❌ a consistent stranger | ✅ 7 of 8 |
| Time to first sticker | – | 18.6s (target < 60s) |
| Full pack of 8 | – | 52.9s |

- **Likeness is a model-tier problem, not a prompt problem.** Same prompt, very different identity preservation.
- **Real selfies broke the background removal** when hair or shoulders touched the frame. Fixed by sampling the key colour from the top edge, clearing green pockets in hair, and prompting for a wider crop.
- **Next open risk: unit economics** of the top-tier model against a ≤ $0.40-per-pack target.

Full case study (problem, discovery, PRD, decisions): see the Notion portfolio.

## How it works

- Single static `index.html`, no build step, no backend.
- Bring-your-own Gemini API key, kept in the browser and sent only to Google.
- 8 image-generation calls, 3 in parallel, revealed progressively.
- Client-side chroma-key removal → white sticker outline → 512×512 PNG.
- Save via the Web Share API (phone → Photos → WhatsApp) or a ZIP fallback.
- Fake-door test for a paid 12-expression pack (nothing is charged).
- **Lab drawer:** time to first sticker, 👍 rate, background-removal rate, cost per pack, and a vision-model judge scoring identity / expression / quality (1–5). Runs export as JSON.

## Not built yet

A serverless proxy so testers don't need their own key, central event logging, and the user test with a real friend group (north star: ≥ 5 of 10 testers send a sticker to a group within 24 hours).

# Booth Day Runbook — Leonyx Interactive Demo
Northside TCG card show · Aug 29–30, 2026

## The demo
One file: `demo/index.html`. No install, no build, no server. Works fully offline
except the AI receptionist chat when you connect a live model.

## Morning setup (10 minutes)
1. Copy `demo/index.html` to the show laptop's Desktop (don't rely on the repo or wifi).
2. Double-click it — it opens in the browser from disk (`file://`). Everything except
   live LLM answers works with wifi OFF.
3. Optional but recommended — live AI answers:
   - Click **⚙ SETTINGS** in the chat panel.
   - Provider preset: **OpenRouter (default)**. Paste your OpenRouter API key. **SAVE**.
   - Tap the Charizard chip once and confirm a real answer streams in.
   - The key is stored only in that browser (localStorage). Never put it in the file.
4. Do one full dry run: all three scenario chips, tier switcher up and down,
   before/after wipe, collection chip → watch the appointment appear in the calendar.

## During the pitch
- Default view is **Full Stack** (everything unlocked) — start there, then walk DOWN:
  Starter → "this alone is $997" → Growth → "+$500 gets the website and bookings" →
  Full Stack → "+$500 more automates the busywork". Locked panels show the price delta.
- Shortcuts: `demo/index.html?tier=starter` / `?tier=growth` / `?tier=fullstack`.
- The receptionist is labeled SIMULATED everywhere. Say "demo data" freely — it's honest.

## If something goes wrong
| Symptom | Meaning | Fix |
|---|---|---|
| Orange "OFFLINE DEMO MODE" banner | No key set, wifi down, or endpoint unreachable | Nothing to fix — scripted answers continue, still labeled. Pitch on. |
| Banner appears mid-conversation | Venue wifi dropped or endpoint stalled | Keep demoing (scripted mode); check wifi when convenient. Reconnect in SETTINGS to go live again — no reload needed. |
| Chat ignores a tap | Previous answer still streaming (guard) | It's intentional — one answer at a time. Settles in seconds. |
| Page looks odd after hours idle | Browser memory | Ctrl+R refresh. Calendar/chat reset to pristine state. |
| Laptop dies | — | The file is on your phone too (airdrop/cable copy); opens in mobile browser. |

## Facts for prospect questions
- Tiers: Starter $997 (receptionist) · Growth $1,497 (+ website/SEO, booking integration) ·
  Full Stack $1,997 (+ SMS reminders, price watch, auto-posting). One-time, no subscription.
- The buylist prices, "Northside Cards", and all market data are fictional demo content.
- Live mode: answers come from a real LLM grounded in the fictional shop script.

## Verified before the show (automated, this build)
- Tier gating matrix exact at all three tiers; instant switching, no reload
- Offline scripted answers < 1s, labeled; live streaming verified against a real
  OpenAI-compatible endpoint (local Ollama); OpenRouter uses the identical code path
- Wifi death mid-answer: request aborts ~20s, falls back to scripted mode automatically,
  demo never freezes
- Rapid tap/double-submit guarded; no duplicate answers
- No horizontal overflow at 1280×800 (laptop) and 820×1180 (iPad portrait); clean console

## Publishing online (optional — booth runs fine without it)
Confirmed facts: GitHub Pages serves this repo from the `main` branch, repo root,
at https://rashed-albatayneh.github.io/leonyx-booth/. The demo adds only
`demo/index.html` (+ runbook); it changes nothing on the existing site. The demo
uses no repo-relative asset paths, so it works unchanged at the `/demo/` subpath.

When ready (`feature/demo` is a clean fast-forward of origin/main):

    git checkout main && git merge feature/demo && git push origin main

Then check https://rashed-albatayneh.github.io/leonyx-booth/demo/ renders
(allow ~1 min for the Pages rebuild). Rollback if ever needed:

    git revert <merge-commit-sha> && git push origin main

## Extras included
- **Screen stays awake:** the demo holds a screen wake-lock while visible, so a booth
  tablet/laptop won't dim mid-pitch. Needs no setup; silently skips itself on browsers
  that don't support it.
- **QR table card:** print `demo/BOOTH-QR-CARD.html` (A6 landscape table-tent size)
  alongside `demo/qr-leonyx-demo.png`. Prospects scan and try the demo on their own
  phones — the URL points at the published live site.

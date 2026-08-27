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
  Starter → "this alone is $997" → Growth → "+$500 gets the website, bookings, and
  customer-facing automation" → Full Stack → "+$500 more automates pricing, inventory,
  and the back office". Locked panels show the price delta.
- Shortcuts: `demo/index.html?tier=starter` / `?tier=growth` / `?tier=fullstack`.
- Everything is labeled SIMULATED except **Live Inventory Value Tracker** (real card
  prices, real API) and the **Buylist Offers** calculator (computes off that same real
  feed). Say "demo data" freely for the rest — it's honest, and prospects notice.

### Panel guide (13 total) — what to say if someone asks "does it do X?"
| # | Panel | Tier | One line |
|---|---|---|---|
| 1 | AI Phone Receptionist | All | Answers every call, quotes buylist, books valuations 24/7 |
| 2 | Website Redesign & SEO | Growth+ | Before/after — found on page one instead of buried |
| 3 | Booking Automation | Growth+ | Calendar + automated SMS reminders, no more empty slots |
| 4 | Price Watch + Auto-Post | Full Stack | Auto-posts new inventory to social while you're busy |
| 5 | **Live Inventory Value Tracker** | Full Stack | **Real** live card prices, client sets the refresh rate |
| 6 | Review Request Automation | Growth+ | Auto-texts a review link after every purchase |
| 7 | Restock & Want-List Alerts | Growth+ | Customer signs up once, gets notified the moment it's in |
| 8 | Loyalty & Rewards | Growth+ | Automatic punch card, reward applied at checkout |
| 9 | Grading Submission Tracker | Growth+ | Customer self-checks PSA status instead of calling |
| 10 | Event & Tournament Mgmt | Growth+ | Real Northside TCG dates — shows automated show promotion |
| 11 | Multi-Platform Inventory Sync | Full Stack | One inventory, no more overselling across TCGplayer/eBay/Shopify |
| 12 | **Auto-Generated Buylist Offers** | Full Stack | Instant cash/credit offer off the **real** live price feed |
| 13 | Authenticity Pre-Check | Full Stack | First-pass "super fake" screen before accepting a buy |

Panels 5 and 12 are the two to point at if someone's skeptical the demo is "just slides" —
open Settings-free, no key needed, prices update from a real public API right in front of them.

## If something goes wrong
| Symptom | Meaning | Fix |
|---|---|---|
| Orange "OFFLINE DEMO MODE" banner | No key set, wifi down, or endpoint unreachable | Nothing to fix — scripted answers continue, still labeled. Pitch on. |
| Banner appears mid-conversation | Venue wifi dropped or endpoint stalled | Keep demoing (scripted mode); check wifi when convenient. Reconnect in SETTINGS to go live again — no reload needed. |
| Chat ignores a tap | Previous answer still streaming (guard) | It's intentional — one answer at a time. Settles in seconds. |
| Page looks odd after hours idle | Browser memory | Ctrl+R refresh. Calendar/chat reset to pristine state. |
| Laptop dies | — | The file is on your phone too (airdrop/cable copy); opens in mobile browser. |
| Live Inventory panel shows "RECONNECTING" | The real public pricing API (api.pokemontcg.io) is genuinely flaky sometimes — this is expected occasionally, not a bug | It auto-retries and falls back to last-known prices, clearly labeled. Say "showing last known values" and move on, or tap REFRESH NOW after a few seconds. Never blank/broken. |
| Live Inventory / Buylist panel needs wifi | Both use a real internet API, unlike every other panel | Everything else in the demo works fully offline — only these two need the venue wifi. If wifi is down, skip straight to "and this one runs on live market data too" without opening them. |

## Facts for prospect questions
- Tiers: Starter $997 (AI receptionist) · Growth $1,497 (+ website/SEO, booking + SMS,
  review requests, want-list alerts, loyalty, submission tracker, event promotion) ·
  Full Stack $1,997 (+ live price tracking, auto-posting, multi-platform inventory sync,
  instant buylist offers, authenticity pre-check). One-time, no subscription.
- "Northside Cards" and the receptionist script/buylist are fictional demo content.
  The Live Inventory panel and Buylist calculator use **real** live market prices from
  a public pricing API — not fictional, and not simulated.
- Live receptionist mode: answers come from a real LLM grounded in the fictional shop script.
- Northside TCG Expo dates shown in the Events panel are the real show dates — everything
  else in that panel (RSVP count, reminder timing) is an illustrative simulated example.

## Verified before the show (automated, this build)
- Tier gating matrix exact at all three tiers across all 13 panels; instant switching, no reload
- Offline scripted answers < 1s, labeled; live streaming verified against a real
  OpenAI-compatible endpoint (local Ollama); OpenRouter uses the identical code path
- Wifi death mid-answer: request aborts ~20s, falls back to scripted mode automatically,
  demo never freezes
- Rapid tap/double-submit guarded; no duplicate answers
- Live Inventory panel: real fetch against api.pokemontcg.io verified working end-to-end
  in-browser (real prices rendered, not mocked); retry/backoff verified against the
  API's real intermittent failures; "reconnecting" fallback never shows blank/broken
- Want-list form, submission status lookup, and buylist offer calculator all verified
  interactively — correct output, no console errors
- No horizontal overflow at 1280×800 (laptop), 820×1180 (iPad portrait), or 390px
  (phone-width, iframe-tested); clean console at every width

## Publishing online (optional — booth runs fine without it)
Confirmed facts: GitHub Pages serves this repo from the `main` branch, repo root,
at https://rashed-albatayneh.github.io/leonyx-booth/. The demo lives at
`demo/index.html`, live at https://rashed-albatayneh.github.io/leonyx-booth/demo/.
All demo work is committed and pushed directly to `main` (no feature branch in use).

To publish a change: commit it, then `git push origin main` — allow ~1 min for the
Pages rebuild, then check the live `/demo/` URL renders. Rollback if ever needed:

    git revert <commit-sha> && git push origin main

## Day-of checklist (90 seconds, at the table)
1. Double-click the file — greeting bubble shows; OFFLINE MODE banner is normal
2. Tap each scenario chip once — three answers appear
3. Switch tiers Starter → Growth → Full Stack — all 13 panels lock/unlock correctly
4. Paste your OpenRouter key in ⚙ SETTINGS, tap Charizard — confirm a live answer streams
5. Scroll to Live Inventory — confirm real prices load (needs wifi); tap REFRESH NOW once
6. Try the Buylist calculator once (pick any card, GET OFFER) and the Submission Tracker
   once (type 4471, CHECK STATUS) — confirms the interactive panels are responsive
7. QR card + a stack of leave-behinds on the table, demo open on the tablet, charger plugged in

## Extras included
- **Screen stays awake:** the demo holds a screen wake-lock while visible, so a booth
  tablet/laptop won't dim mid-pitch. Needs no setup; silently skips itself on browsers
  that don't support it.
- **QR table card:** print `demo/BOOTH-QR-CARD.html` (A6 landscape table-tent size)
  alongside `demo/qr-leonyx-demo.png`. Prospects scan and try the demo on their own
  phones — the URL points at the published live site.
- **Leave-behind flyer:** print `demo/LEAVE-BEHIND.html` (A5 portrait). Tier recap,
  QR, honest-label fineprint. Give one to every serious conversation.
- **Lead capture in the demo:** the gold "Want this for your shop?" button (bottom
  right) takes name + shop + phone/email and quietly delivers it to the SAME Google
  Sheet as the deck's lead form. Leads submitted from prospect phones via the QR also
  land there. Check the sheet Friday night and follow up Saturday.

# CLAUDE.md

Guidance for Claude Code when working in this repo.

## What this is

Nagenthiran's freelance/skill-monetization business — pricing, positioning, delivery operations, and WhatsApp launch flyers for freelance services (web dev, mobile/desktop apps, document/presentation design, AI content editing). Distributed through a UK friend network via WhatsApp, not SEO/virality. Separate from the user's product/SaaS ideas, which live in a different repo.

Read `README.md` first for the file map, then the two docs below for full context before making any pricing or scope changes.

## Key files

- **`freelance-monetization.md`** — pricing, positioning, the academic-work legal boundary, launch plan, and a dated status log of every change and why. This is the source of truth for what each service costs and why it's priced that way (market research is cited inline).
- **`freelance-operations.md`** — the operational playbook: how each service actually gets delivered and maintained (hosting, backups, care-plan fulfillment cadence), plus explicitly unresolved open decisions (hosting platform default, payment method, edit-tracking for care plans, app delivery workflow). Check this before assuming something is handled.
- **`posts/`** — the WhatsApp flyers themselves, each an A4 HTML file rendered to PDF.

## Critical boundary — read before touching pricing or scope

The user is adjacent to student communities who could ask for essay writing or graded coursework help. **This is explicitly excluded**, on every post and in every service description — see `freelance-monetization.md` → "Explicit boundary — academic ghostwriting excluded". The UK's Skills and Post-16 Education Act 2022 makes *advertising* contract-cheating services to English/Welsh HE students a criminal offence, tied to the user's real name and identifiable friend network regardless of channel (public site or private WhatsApp group). This is why `ai-content-humanizing.html` carries an explicit on-flyer scope line ("business and professional writing only... not offered for academic coursework"). Never add or imply an academic-work framing to any service, post, or price without the user explicitly re-opening that decision.

## Flyer conventions (all posts in `posts/`)

Each flyer is a single self-contained A4 HTML file, dark theme, rendered to PDF via headless Chrome — no build step, no dependencies beyond Google Fonts (Inter + Fira Code, loaded via CDN `<link>`).

- **Palette:** `--bg-primary: #0a192f`, `--accent: #64ffda` (teal), `--text-main: #ccd6f6`, `--text-dim: #a8b2d1`. Consistent across every post — don't introduce a different palette per post.
- **Icons:** hand-written inline SVG line-icons (Feather-icon style: 24×24 viewBox, `stroke="currentColor"`, no fill), teal-colored via the `.build-icon` wrapper. **Never use emoji for icons** — an earlier pass used emoji and one (🪄) silently failed to render in headless Chrome's font fallback (rendered as an empty box). SVG avoids that failure mode entirely and was a deliberate fix, not a style preference.
- **Pricing layout:** two patterns depending on tier count — `.price-row` (full-width stacked rows) for ≤4 tiers, `.price-grid`/`.price-card` (compact 2–4 column grid) when there are more tiers than fit as stacked rows without overflowing to a second page.
- **Page-fit is the recurring failure mode.** Every time content was added (a new pricing tier, extra build-grid cards, extra includes items), the post overflowed to page 2. Fix pattern used repeatedly: tighten section `margin-top` values, `price-row` padding/margin, `.spacer` min-height, `.cta` padding, `.footer` margin-top — in that order, smallest change first. **Always verify page count after any edit to a post**, not just visually:
  ```bash
  CHROME="/c/Program Files (x86)/Google/Chrome/Application/chrome.exe"
  "$CHROME" --headless --disable-gpu --no-pdf-header-footer --print-to-pdf="posts/NAME.pdf" --print-to-pdf-no-header --no-margins "file:///$(pwd)/posts/NAME.html"
  python3 -c "
  import re
  with open('posts/NAME.pdf','rb') as f: data = f.read()
  print('pages:', len(re.findall(rb'/Type\s*/Page[^s]', data)))
  "
  ```
  If it's not exactly 1, tighten spacing and re-render before doing anything else.
- **Visual verification:** after any layout change, screenshot and Read the image back — page count alone doesn't catch overlapping text or a broken icon path:
  ```bash
  "$CHROME" --headless --disable-gpu --window-size=794,1250 --screenshot="posts/NAME-check.png" "file:///$(pwd)/posts/NAME.html"
  ```
  Delete the `-check.png` afterward — it's a temp file, not a deliverable.

## Pricing philosophy

Every price is a **heavy friend-network discount off researched market rates**, not a guess. When adding a new service or revisiting an existing price, look up actual UK/US/Canada/Australia freelance market rates first (Upwork/Fiverr data, industry pricing guides), then price at roughly 20–50% of the beginner-freelancer floor — cite the sources inline in `freelance-monetization.md`'s status log the way every prior pricing decision has been. Don't price purely on vibes; the whole point of the discount is that it's *deliberately* below market, not *accidentally* below it (the original launch prices were an accidental-underpricing mistake that got corrected 2026-08-31 — see that file's "Pricing revision" section for what that looked like and why it mattered).

The guiding question for whether something belongs in this lineup at all: would someone pay a stranger to do this rather than do it themselves? The pulls that make that "yes" are skill gap, tedium, infrequency, high stakes if done wrong, or infra/bureaucracy avoidance. See `freelance-monetization.md`'s "What do people pay someone else to do" section for how this was applied to pick the domain/hosting and app-store-submission add-ons.

## Working conventions

- Log every substantive change (new service, pricing change, new post) in `freelance-monetization.md`'s dated status log, same style as existing entries — what changed, why, what it replaced. This file is the project's memory across sessions.
- Don't add new services without checking the academic-work boundary above first.
- Keep every post visually consistent (same header, same CTA button style, same footer) — a client seeing two posts should recognize them as the same person's work.

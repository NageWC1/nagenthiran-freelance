# CLAUDE.md

Guidance for Claude Code when working in this repo.

## What this is

Nagenthiran's freelance/skill-monetization business — pricing, positioning, delivery operations, and WhatsApp launch flyers for freelance services (web dev, mobile/desktop apps, document/presentation design, AI content editing). Distributed through a UK friend network via WhatsApp, not SEO/virality. Separate from the user's product/SaaS ideas, which live in a different repo.

Read `README.md` first for the file map, then the two docs below for full context before making any pricing or scope changes.

## Key files

- **`freelance-monetization.md`** — pricing, positioning, the academic-work legal boundary, launch plan, and a dated status log of every change and why. This is the source of truth for what each service costs and why it's priced that way (market research is cited inline).
- **`freelance-operations.md`** — the operational playbook: how each service actually gets delivered and maintained (hosting, backups, care-plan fulfillment cadence), plus explicitly unresolved open decisions (hosting platform default, payment method, edit-tracking for care plans, app delivery workflow). Check this before assuming something is handled.
- **`posts/`** — the WhatsApp flyers themselves, each an A4 HTML source file + rendered PDF.
- **`flyer-image/`** — PNG renders of every post (1654×2339px, ~200dpi), one per post, same base filename. These are what actually get sent on WhatsApp — the PDFs are the source of truth, the PNGs are the sendable artifact.

## Critical boundary — read before touching pricing or scope

The user is adjacent to student communities who could ask for essay writing or graded coursework help. **This is explicitly excluded**, on every post and in every service description — see `freelance-monetization.md` → "Explicit boundary — academic ghostwriting excluded". The UK's Skills and Post-16 Education Act 2022 makes *advertising* contract-cheating services to English/Welsh HE students a criminal offence, tied to the user's real name and identifiable friend network regardless of channel (public site or private WhatsApp group). This is why `ai-content-humanizing.html` carries an explicit on-flyer scope line ("business and professional writing only... not offered for academic coursework"). Never add or imply an academic-work framing to any service, post, or price without the user explicitly re-opening that decision.

## Flyer conventions (all posts in `posts/`)

Each flyer is a single self-contained A4 HTML file, dark theme, rendered to PDF via headless Chrome — no build step, no dependencies beyond Google Fonts (Inter + Fira Code, loaded via CDN `<link>`).

- **Palette:** `--bg-primary: #0a192f`, `--accent: #64ffda` (teal), `--text-main: #ccd6f6`, `--text-dim: #a8b2d1`. Consistent across every post — don't introduce a different palette per post.
- **Icons:** hand-written inline SVG line-icons (Feather-icon style: 24×24 viewBox, `stroke="currentColor"`, no fill), teal-colored via the `.build-icon` wrapper. **Never use emoji for icons** — an earlier pass used emoji and one (🪄) silently failed to render in headless Chrome's font fallback (rendered as an empty box). SVG avoids that failure mode entirely and was a deliberate fix, not a style preference.
- **Pricing layout:** two patterns depending on tier count — `.price-row` (full-width stacked rows) for ≤4 tiers, `.price-grid`/`.price-card` (compact 2–4 column grid) when there are more tiers than fit as stacked rows without overflowing to a second page.
- **Page-fit is the recurring failure mode.** Every time content was added (a new pricing tier, extra build-grid cards, extra includes items), the post overflowed to page 2. Fix pattern used repeatedly: tighten section `margin-top` values, `price-row` padding/margin, `.spacer` min-height, `.cta` padding, `.footer` margin-top — in that order, smallest change first.

- **NEVER use `--print-to-pdf` to render these flyers — it silently miscenters content.** Discovered 2026-08-31: Chrome's headless print-to-pdf pipeline shrinks the page content to ~82% and anchors it top-left instead of centering it on the A4 canvas, even though the underlying HTML/CSS layout is genuinely symmetric (confirmed via `getBoundingClientRect()` — every content element has identical left/right gaps) and the PDF's own `/MediaBox` is exactly correct A4 dimensions. The bug is specific to the print rendering path; a normal windowed/screenshot render of the exact same HTML is correctly centered. This reproduced identically under both `--headless` and `--headless=new`, so it's not a headless-mode difference — don't waste time re-testing that. The symptom looks exactly like "content is shifted left with too much empty space on the right," which is easy to mistake for a CSS bug and manually crop around — don't; fix it by not using that pipeline at all.

  **The correct render pipeline** — screenshot at a device-scale-factor tuned to land on ~200dpi for an A4 page, then build the PDF directly from that verified-centered PNG (PIL's PDF writer, not Chrome's):
  ```bash
  CHROME="/c/Program Files (x86)/Google/Chrome/Application/chrome.exe"
  UDD="/tmp/chrome-udd"; mkdir -p "$UDD"   # a user-data-dir is required or Chrome errors out
  "$CHROME" --headless --disable-gpu --user-data-dir="$UDD" \
    --window-size=794,1123 --force-device-scale-factor=2.083 \
    --screenshot="flyer-image/NAME.png" "file:///$(pwd)/posts/NAME.html"
  python3 -c "
  from PIL import Image
  im = Image.open('flyer-image/NAME.png').convert('RGB')
  print('size', im.size)   # should be (1654, 2339) — if not, the window-size/scale-factor above is off
  im.save('posts/NAME.pdf', resolution=200.0)
  "
  ```
  This produces both the sendable PNG and the PDF from a single verified-correct render — no separate print step, nothing to drift out of sync between them.

- **Page-count check** (still needed — screenshot mode doesn't paginate, but a page that's grown too tall will just get cut off at the bottom of the fixed 1123px-tall window instead of flowing to page 2, which is a silent failure worth checking for explicitly): open the PNG and confirm the CTA button and footer are both fully visible and not clipped at the bottom edge. If they're missing or cut off, the content overflowed — tighten spacing per the pattern above and re-render.
- **Visual verification:** always Read the regenerated PNG back after any layout change — dimensions/page-count checks don't catch overlapping text, a broken icon path, or (per the bug above) miscentering. Compare against the palette/spacing conventions in this doc.
- **Centering sanity check**, if anything ever looks off again: measure left vs. right margins directly rather than trusting the eye —
  ```python
  from PIL import Image
  import numpy as np
  im = Image.open('flyer-image/NAME.png').convert('RGB')
  arr = np.array(im).astype(int)
  w = arr.shape[1]
  row = arr[700]  # any y that crosses a card row
  grad = np.abs(np.diff(row.sum(axis=1)))
  strong = np.where(grad > 40)[0]
  L, R = strong[0], strong[-1]
  print('left margin', L, 'right margin', w-1-R)  # should match within a few px
  ```

## Pricing philosophy

Every price is a **heavy friend-network discount off researched market rates**, not a guess. When adding a new service or revisiting an existing price, look up actual UK/US/Canada/Australia freelance market rates first (Upwork/Fiverr data, industry pricing guides), then price at roughly 20–50% of the beginner-freelancer floor — cite the sources inline in `freelance-monetization.md`'s status log the way every prior pricing decision has been. Don't price purely on vibes; the whole point of the discount is that it's *deliberately* below market, not *accidentally* below it (the original launch prices were an accidental-underpricing mistake that got corrected 2026-08-31 — see that file's "Pricing revision" section for what that looked like and why it mattered).

The guiding question for whether something belongs in this lineup at all: would someone pay a stranger to do this rather than do it themselves? The pulls that make that "yes" are skill gap, tedium, infrequency, high stakes if done wrong, or infra/bureaucracy avoidance. See `freelance-monetization.md`'s "What do people pay someone else to do" section for how this was applied to pick the domain/hosting and app-store-submission add-ons.

## Working conventions

- Log every substantive change (new service, pricing change, new post) in `freelance-monetization.md`'s dated status log, same style as existing entries — what changed, why, what it replaced. This file is the project's memory across sessions.
- Don't add new services without checking the academic-work boundary above first.
- Keep every post visually consistent (same header, same CTA button style, same footer) — a client seeing two posts should recognize them as the same person's work.

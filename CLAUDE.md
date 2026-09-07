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

Each flyer is a single self-contained A4 HTML file, rendered to PDF via headless Chrome — no build step, no dependencies beyond Google Fonts (Inter, loaded via CDN `<link>`).

- **Palette (revised 2026-09-07):** light Apple-style theme, matching `nagenthiran-portfolio`'s redesigned site so the flyers and the website read as one brand — `--white: #ffffff`, `--off-white: #f5f5f7`, `--ink: #1d1d1f`, `--ink-soft: #6e6e73`, `--line-soft: #e8e8ed`, `--blue: #0071e3` (accent), `--blue-tint: rgba(0,113,227,0.08)`, `--whatsapp: #25d366` (CTA button only). Body background is a subtle white→off-white gradient. Pulled directly from `nagenthiran-portfolio/css/styles.css` — if that palette changes, update here too. Superseded the old dark navy/teal theme (`#0a192f` / `#64ffda`), which was a leftover from the pre-redesign portfolio and no longer matches it.
- **No personal photo.** A GitHub-avatar photo was tried in the header on 2026-09-07 and removed the same day — it rendered blurry at flyer size (a small avatar upscaled at the render pipeline's 2.083 device-scale-factor) and the user didn't want their photo on these anyway. The brand header is text-only: name + the "TAKING NEW CLIENTS" pill. Don't reintroduce a photo without the user asking for one.
- **Reassurance box:** every flyer carries one blue-tinted box under the hero copy that directly targets hesitation-to-start for that specific service (e.g. "Not sure what kind of site you need? You don't have to know yet."). This was a deliberate addition — the pre-2026-09-07 flyers were priced and informative but gave a hesitant reader no explicit permission to message without having it all figured out. Keep one per flyer, worded to the specific uncertainty that service's clients would have, not a generic copy-paste line.
- **Icons:** hand-written inline SVG line-icons (Feather-icon style: 24×24 viewBox, `stroke="currentColor"`, no fill), blue-colored via the `.build-icon` wrapper. **Never use emoji for icons** — an earlier pass used emoji and one (🪄) silently failed to render in headless Chrome's font fallback (rendered as an empty box). SVG avoids that failure mode entirely and was a deliberate fix, not a style preference.
- **Pricing layout:** two patterns depending on tier count — `.price-row` (full-width stacked rows) for ≤4 tiers, `.price-grid`/`.price-card` (compact 2–4 column grid) when there are more tiers than fit as stacked rows without overflowing to a second page.
- **Page-fit is the recurring failure mode.** Every time content was added (a new pricing tier, extra build-grid cards, extra includes items, the reassurance box) the post overflowed the fixed A4 window. Fix pattern used repeatedly: tighten section `margin-top` values, `price-row` padding/margin, `.spacer` min-height, `.cta` padding, `.footer` margin-top — in that order, smallest change first.
- **Overflow-measurement pitfall (found 2026-09-07):** don't measure overflow by scanning for specific known text colors (e.g. "the ink color or the WhatsApp green") — white text on the dark `.cta` box and grey `.footer`/`.price-sub` text won't match and the last real content row will be under-counted, silently passing a render that's actually clipping the footer. Measure by row *variance* instead (background is a smooth gradient, so any row containing text/icons/boxes has meaningfully higher pixel std-dev than a pure-background row) — see the render pipeline below.

- **NEVER use `--print-to-pdf` to render these flyers — it silently miscenters content.** Discovered 2026-08-31: Chrome's headless print-to-pdf pipeline shrinks the page content to ~82% and anchors it top-left instead of centering it on the A4 canvas, even though the underlying HTML/CSS layout is genuinely symmetric (confirmed via `getBoundingClientRect()` — every content element has identical left/right gaps) and the PDF's own `/MediaBox` is exactly correct A4 dimensions. The bug is specific to the print rendering path; a normal windowed/screenshot render of the exact same HTML is correctly centered. This reproduced identically under both `--headless` and `--headless=new`, so it's not a headless-mode difference — don't waste time re-testing that. The symptom looks exactly like "content is shifted left with too much empty space on the right," which is easy to mistake for a CSS bug and manually crop around — don't; fix it by not using that pipeline at all.

  **The correct render pipeline** — screenshot at a device-scale-factor tuned to land on ~200dpi for an A4 page, then build the PDF directly from that verified-centered PNG (PIL's PDF writer, not Chrome's). **Use a Windows-style `file:///C:/...` URL, not Git Bash's `/c/...` form** — found 2026-09-07: passing `file:///$(pwd)/...` when `pwd` is Git-Bash-style silently loads Chrome's own "file not found" error page instead of the flyer, and the screenshot step still "succeeds" (writes a small ~40KB PNG of that error page) with no error surfaced — always sanity-check the output file size (a real flyer render is 300–450KB; anything under ~100KB is almost certainly an error-page screenshot, not the flyer):
  ```bash
  BASE_WIN="C:/Users/ACHC/Desktop/Mine/webtools/nagenthiran-freelance"
  CHROME="/c/Program Files (x86)/Google/Chrome/Application/chrome.exe"
  UDD="/tmp/chrome-udd"; mkdir -p "$UDD"   # a user-data-dir is required or Chrome errors out
  "$CHROME" --headless --disable-gpu --user-data-dir="$UDD" \
    --window-size=794,1123 --force-device-scale-factor=5.0 \
    --screenshot="$BASE_WIN/flyer-image/NAME.png" "file:///$BASE_WIN/posts/NAME.html"
  python3 -c "
  from PIL import Image
  im = Image.open('$BASE_WIN/flyer-image/NAME.png').convert('RGB')
  print('size', im.size)   # should be (3970, 5615) — if not, the window-size/scale-factor above is off
  im.save('$BASE_WIN/posts/NAME.pdf', resolution=480.0)
  "
  ```
  This produces both the sendable PNG and the PDF from a single verified-correct render — no separate print step, nothing to drift out of sync between them. **Device-scale-factor was raised from 2.083 (200 DPI-equivalent, 1654×2339px) to 5.0 (480 DPI-equivalent, 3970×5615px) on 2026-09-07** — the original scale produced visibly soft/pixelated text and icon edges once zoomed in on a phone (WhatsApp's own compression on send makes this worse, not better, so the source needs to start sharp). Each PNG is ~1.2–1.5MB at this scale, still comfortably within WhatsApp's image limits. Don't lower the scale factor to save render time/file size without checking with the user first — sharpness was an explicit, repeated complaint.
  For the overflow-check step (tall render) below, only the `--window-size` matters for measuring fit — CSS layout and overflow are scale-independent, so the tall-render step can stay at a lower scale factor (e.g. 2.083) for speed; only the *final* render needs the high scale factor above.

- **Overflow check before the final render** — render tall (e.g. `--window-size=794,1700`) and measure by row variance (not by scanning for specific text colors — see the pitfall above), to catch overflow before wasting a final render:
  ```python
  from PIL import Image
  import numpy as np
  im = Image.open('flyer-image/_debug_tall.png').convert('L')
  arr = np.array(im).astype(int)
  row_std = arr.std(axis=1)                      # background rows (smooth gradient) have near-zero std
  content_rows = np.where(row_std > 3)[0]
  last = content_rows[-1]
  overflow_mm = (last - 2339) / 2.083 / (96/25.4)  # 2339 = target px height at this scale factor
  print(f'overflow_mm={overflow_mm:.1f}')          # negative = fits, with that much margin to spare
  ```
  If positive, tighten spacing (smallest change first, per the pattern above) and re-measure before doing the final A4-window render.
- **Page-count check** (still needed even after the overflow measurement above — belt and braces): open the final PNG and confirm the CTA button and footer are both fully visible and not clipped at the bottom edge. If they're missing or cut off, the content overflowed — tighten spacing per the pattern above and re-render.
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

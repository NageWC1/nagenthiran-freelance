# Freelance / Skill Monetization

A different track from the rest of this repo — not a new web-tools SaaS bet, but monetizing existing skills (dev, design, docs/presentations) as freelance services, distributed through the user's own network rather than SEO/virality. Started 2026-08-30.

This file covers pricing, positioning, and the launch posts. For the operational side — how each service actually gets delivered and maintained over time (backups, hosting, care-plan fulfillment, open TODOs) — see `freelance-operations.md`.

## Assets already in place
- **Portfolio site** — live at `nagenthiran.com` (repo: `github.com/NageWC1/nagenthiran-portfolio`, local: `C:\Users\pc\Desktop\works\webtools\nagenthiran-portfolio`). Already has a Services section (University Projects · Web Development · Mobile Apps) and 10 real GitHub projects shown. Its own backlog (Phase 6 in the project's `PROGRESS.md`) is still open: no pricing section, no testimonials, no CV download, no analytics — not required to launch into a warm network, but worth closing before pointing cold traffic at it.
- **UK friend groups** — the real distribution channel here; a warm network beats any of the SEO/virality plays explored in the rest of this repo. Launch plan is WhatsApp posts into these groups, not the website cold.
- **Skillset** — web, mobile, and desktop app development; document/presentation design.

## Explicit boundary — academic ghostwriting excluded
User is a member of/adjacent to student communities who could plausibly want "someone to write my essay" or "build my graded coursework project." **Deliberately not offering this, on the website or via WhatsApp.** The UK's Skills and Post-16 Education Act 2022 makes *providing or advertising* contract-cheating services to English/Welsh HE students a criminal offence — the channel (public site vs. private WhatsApp group) doesn't change that, and it's tied to the user's real name and identifiable friend network either way. Whatever happens as an individual private favor between friends is their own business; it is not being built out as a monetized, repeatable offering, and this repo/assistant won't help price, market, or productize it.

## Legitimate service lineup
Everything below is fine to promote publicly, on the site or via WhatsApp, no restriction.

| Service | Launch/starter price | Notes |
|---|---|---|
| CV / résumé rewrite & design | £15–20 | +£5 for a matching cover letter |
| LinkedIn profile optimization | £10–15 | Bundle discount with CV |
| Portfolio website (single long page) | £150 | Reuses the template built for `nagenthiran.com` |
| Business/landing page site (up to 5 pages) | £250 | Repriced 2026-08-31 — see below |
| Larger brand site (6+ pages) | £300 | Repriced 2026-08-31 — see below |
| Simple online store | from £350 or custom quote | Repriced 2026-08-31; scope varies too much for a flat number |
| Mobile/desktop app | "Starting from £150 — quote after a call" | Too variable to fix-price up front |
| Slide deck, up to 10 slides | £40 | Repriced 2026-08-31 — see below |
| Slide deck, 11–20 slides | £60 | Repriced 2026-08-31 — see below |
| Report/document formatting | £35 | Repriced 2026-08-31 — see below |
| Deck + report bundle (matching style) | £85 | Repriced 2026-08-31 — see below |
| AI content humanizing / editing | from £60 | New service, added 2026-08-31 — up to 10,000 words, +£5 per extra 1,000 |
| Website Care Plan — Basic | £10/mo | New, added 2026-08-31 — uptime monitoring + automated backups, add-on to any site build |
| Website Care Plan — Standard | £20/mo | + up to 2 small edits/month |
| Website Care Plan — Priority | £35/mo | + up to 5 edits/month, 48hr turnaround |
| Domain & Hosting Setup (standalone) | £15 one-time | New, added 2026-08-31 — for an existing site that just needs pointing/configuring, no build required |
| App Store / Play Store Submission Handling | from £30/platform | New, added 2026-08-31 — for an already-built app, client holds their own developer account |

Payment/currency method for UK→Sri Lanka transfers not yet decided — Wise/Revolut are the obvious candidates, needs a decision before the first real order.

### Pricing revision — 2026-08-31
User flagged the launch prices as underpriced, specifically presentation/document design (£10–20) and multi-page business sites (£150–200). Researched entry-level freelance market rates (UK/USA/Canada/Australia — Upwork, Fiverr, industry pricing guides):
- **Slide decks:** beginner freelancers charge $75–250 (≈£60–200) for a ~10-slide deck, or $10–50/slide. Old £10–20/deck was far below even entry-level market.
- **Multi-page business sites (5+ pages):** market guidance for a freelancer *just starting out* is $500–1,500 (≈£400–1,200) for 5–10 pages; established freelancers/agencies charge $2,000–8,000+. Old £150–200 was ~3–8x under the "just starting" floor.
- **Single-page portfolio sites:** freelancer-built portfolios average $500–2,000, but a templated single-page reuse (same template as `nagenthiran.com`) is cheap to produce — £150 is a fair friend-network price, not underpriced.
- Australia/Canada confirm the same shape but the actual client base (UK friend groups) means pricing stays in GBP, not chased in AUD/USD.

New prices above are still a heavy discount vs. open-market rates (friend-network pricing, not cold-client pricing) but no longer under even the beginner-freelancer floor. CV/résumé/LinkedIn and mobile/desktop app pricing were not revisited — user's complaint was specifically about slides/documents and multi-page/brand sites.

### New service — AI content humanizing (added 2026-08-31)
User asked to add AI-content humanizing (rewriting AI-drafted text so it reads natural, plus general proofreading/editing) to the Document/Presentation post, and proposed £60 starting price for 10,000 words. Checked against market: UK professional editing runs £13–22/1,000 words (≈£130–220 for 10k), proofreading £9.50–13/1,000 — so £60 sits at roughly half the professional editing floor, in line with the discount already applied elsewhere. Flagged one risk: industry time estimates for manual line-editing run 40–60 min per 500 words (13–20 hours for 10,000 words), which would make £60 badly underpaid per hour if done as full manual rewriting — so this is scoped as tool-assisted (detect AI-sounding phrasing + targeted rewrite pass, not manual line-by-line editing) so the time actually matches the price. Added as its own line item in `posts/documents-presentations.html`/`.pdf`, with a +£5/extra-1,000-words rate for longer documents so length doesn't quietly erode the discount.

Adding the 4th tier plus 2 new "what I design" cards overflowed the post to 2 pages. Fixed by: reorganizing the build grid from 3 to 4 columns (2 rows instead of 3), and restructuring pricing from 5 stacked full-width rows into a 2×2 grid of compact cards + one full-width featured row for the bundle — reclaimed enough height to fit back on one A4 page. Also caught the 🪄 magic-wand emoji not rendering in headless Chrome's font fallback (showed as an empty box) and swapped it for ✨.

### Standalone AI humanizing post — 2026-08-31
User then reconsidered bundling it and asked how to split it into its own post/quote. Flagged the risk directly: a standalone "AI Content Humanizer" flyer reads very differently from a line item buried in a general document-design post — it's an open invitation for "make my AI-written essay undetectable," which is exactly the contract-cheating-adjacent territory excluded above. User chose to build the standalone post anyway (with guardrails) **and** keep the bundled line item in the Documents/Presentations post — both now exist.

`posts/ai-content-humanizing.html`/`.pdf` drafted as its own A4 flyer, same theme/template, with two things the bundled version doesn't have:
- **Explicit scope line** at the bottom: "For business and professional writing only — reports, emails, proposals, marketing and web copy. Not offered for academic coursework, essays, or exam submissions." — makes the boundary visible on the flyer itself, not just internal policy.
- **Finer pricing tiers** since it has a full page to itself: Short Document (≤2,500 words) £20, Standard Document (≤10,000 words) £60 (featured), Longer Document (10,000+) custom/+£5 per extra 1,000. Same £60/10k anchor as the bundled version, just split into more granular steps.

Rendered single-page on the second pass (first pass fit fine — this one didn't need the spacing-tightening fight the bundled post did, since it only carries 3 price tiers).

### Website care plans — 2026-08-31
Explored other in-demand/low-competition services to pitch (research: care plans, AI chatbot setup, Google Business Profile/local SEO, social media templates, wedding sites). Care plans ranked #1 — zero new skill, turns one-time site sales into recurring income, and most freelancers don't bother offering them. User confirmed: yes, it's a genuine monthly commitment (that's the point), workload is light and mostly automatable (uptime/backups) except for the edits-included tiers.

Added as a "Monthly Care Plans" section to `posts/websites.html`/`.pdf`, priced as 3 tiers at the same friend-network discount ratio as the rest of the lineup (market floor for small-biz plans is $50–100/mo basic per [YSR Studio](https://www.ysrstudio.com/blog/website-maintenance-cost-small-business-2026)/[FatLab](https://fatlabwebsupport.com/blog/website-maintenance/website-maintenance-packages-compared-your-complete-buyers-guide/)):
- Basic — £10/mo — uptime monitoring + automated backups (near-zero hands-on time)
- Standard — £20/mo — + up to 2 small edits/month included
- Priority — £35/mo — + up to 5 edits/month, 48hr turnaround

Adding this section overflowed the post to 2 pages (new .price-grid/.price-card compact-tile pattern reused from the documents-presentations post). Fixed with another round of spacing tightening (body padding, section margins, cta padding, footer margin) — back to single page, verified visually.

**Other researched ideas not yet built:** AI chatbot/automation setup for small business sites (demand +71–109% YoY, fits web dev skillset — [Upwork](https://www.upwork.com/resources/is-chatbot-development-in-demand)), Google Business Profile + local SEO setup (fragmented competition, easy entry point), social media template packages (adjacent to document-design skill). Wedding/event websites explicitly *not* recommended — 90% adoption but dominated by free builders (Zola/Knot/Joy), real competition there is free, not other freelancers.

Two more ideas surfaced from the user's other product builds (RepoAtlas → codebase documentation/architecture diagrams; StreamScore → YouTube/streaming creator tools), not yet built out as services — real skill-gap fit, no pricing drafted yet.

### "What do people pay someone else to do" framing — 2026-08-31
User asked for the underlying pattern behind why the current lineup works as freelance services rather than products. Landed on five pulls that make someone pay rather than DIY: skill gap, tedium, infrequency (not worth learning a tool for a one-off), high stakes if done wrong, and infra/bureaucracy avoidance (the confusing step between "I have the thing" and "it's live"). The existing lineup fits cleanly on this; the gap it surfaced was the last category — the boring unblock-me step people avoid entirely.

Added two lightweight add-ons on that basis (not full flyers — small print-style notes so they didn't force another spacing-tightening fight):
- **Domain & Hosting Setup — £15 one-time**, added to `posts/websites.html` under the Care Plans section. For someone who already has a site (built elsewhere, or by someone else) and just needs the domain pointed/hosting configured — no build required. Distinct from the "help getting it live" already bundled free into a site build.
- **App Store / Play Store Submission Handling — from £30/platform**, added to `posts/mobile-desktop-apps.html` under the includes list. For an already-built app (client holds their own developer account) that just needs the submission/review process handled. Same distinction — separate from the free "help publishing" bundled into an app build.

Both rendered single-page, verified visually.

### Icons — 2026-08-31
User asked to replace the emoji icons across all posts (build-grid cards) with "standard icons" — emoji rendering isn't reliable across fonts/platforms (already caught 🪄 failing to render in headless Chrome, see above). Swapped all 26 emoji icons across `posts/websites.html`, `posts/mobile-desktop-apps.html`, `posts/documents-presentations.html`, and `posts/ai-content-humanizing.html` for hand-written inline SVG line-icons (Feather-icon style: 24×24 viewBox, `stroke="currentColor"`, teal accent color) — same approach already used for the WhatsApp icon in every CTA button. No external icon font/library dependency, so nothing to fail to load at render time. Verified visually on all 4 files — every icon renders correctly, still single-page on each.

## Launch plan — WhatsApp posts
Each post designed as a print-ready one-pager, exported as PDF, converted to an image for WhatsApp by the user. Staggered send (not all in one day to the same group — reads as spam even from a friend).

Planned posts, in send order:
1. **CV / Résumé / LinkedIn** — CV writing & redesign, LinkedIn optimization, cover letters.
2. **Websites** — show range: portfolio, small business, landing pages, booking/appointment sites, blogs, simple online stores (not just portfolio).
3. **Custom Software — Mobile & Desktop Apps** — Android/iOS/cross-platform, Windows/Mac desktop.
4. **Document, Report & Presentation Design** — PPT/report layout and formatting, client supplies content. Framed as a general design service, not tied to academic use.
5. **AI Content Humanizing** (added 2026-08-31, not in original launch order) — standalone post, business/professional writing only, explicit non-academic scope line on the flyer itself. Send order/whether to send at all not yet decided by user.

## Status
- 2026-08-30: direction opened, service boundary agreed, pricing drafted, post list and send order agreed.
- 2026-08-30: Post 1 (CV/Résumé/LinkedIn) and Post 2 (Websites) drafted as A4 flyers, rendered to PDF via headless Chrome (`posts/cv-resume-linkedin.html`/`.pdf`, `posts/websites.html`/`.pdf`). First pass was left-aligned on a non-standard page size; fixed by switching to A4, centering every section (brand, pricing rows, includes list, footer), and rendering at 2x scale for sharper output — the Websites post briefly overflowed to a second page after centering added height, caught and fixed before delivery.
- 2026-08-31: Post 3 (Custom Software — Mobile & Desktop) and Post 4 (Document, Report & Presentation Design) drafted, reusing the Websites post's layout (hero + "what I build/design" icon grid + pricing + includes + CTA), same A4 dark theme and brand header. Both rendered to single-page PDF on first pass (`posts/mobile-desktop-apps.html`/`.pdf`, `posts/documents-presentations.html`/`.pdf`). Post 4 pricing (£10–20 range) kept to the general-design framing agreed in the boundary section above — no academic-specific language.
- All 4 planned posts now drafted. Next: user reviews all four PDFs and sends them (converted to image, staggered across days) to UK WhatsApp groups.

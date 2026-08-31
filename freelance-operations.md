# Freelance Operations Playbook

The "how do we actually deliver this" doc — companion to `freelance-monetization.md` (pricing/positioning/boundary) and `progress-report.md` (status). This one is operational: the mechanics for running each service over time, so a future session (or the user, months from now) can pick this up without re-deriving it. Started 2026-08-31.

## Websites (portfolio / business / brand)

**Delivery:**
- Each client gets their own private GitHub repo (free, unlimited private repos on a free account).
- Deployed via a static host with a free tier (Netlify / Vercel / Cloudflare Pages / GitHub Pages — pick one as default; not yet decided which, see Open Decisions below).
- Client owns nothing to install or maintain — source code + hosting account access handed over per the "no lock-in" promise on the flyer.

**Backups — no separate storage needed:**
- The GitHub repo *is* the backup. Full history, every change, restorable anytime, £0.
- The hosting platform is a second layer for free — Netlify/Vercel/Cloudflare Pages/GitHub Pages all keep every deployment and allow one-click rollback.
- This only covers static sites (no database). See Online Stores below for the one case where this doesn't apply.

**Uptime monitoring:**
- UptimeRobot free tier — up to 50 monitors, checks every 5 minutes, emails on downtime. Covers the "uptime monitoring" line in the Care Plan without any paid tooling.

**Online Stores — different backup model:**
- If a store has real order/customer data (a database), git does not back that up.
- Don't build custom backup infrastructure for this — pick a store platform that already backs up its own database (Shopify, or Supabase/Firebase if building a custom store). The backup is inherited from the platform, not something built or paid for separately.

## Monthly Care Plans (Basic / Standard / Priority)

Defined in `posts/websites.html` at £10 / £20 / £35 per month. Operational cadence:
- **Basic (£10/mo):** fully automated — UptimeRobot + git/host backups run themselves. No manual monthly work unless something breaks.
- **Standard (£20/mo):** + up to 2 small edits/month. Needs a lightweight way to track "how many edits has this client used this month" — not yet set up (see Open Decisions).
- **Priority (£35/mo):** + up to 5 edits/month, 48hr turnaround on requests — same tracking need, plus a personal commitment to respond within 48hrs.
- Bigger changes (new pages, redesigns) are explicitly out of scope for any tier and quoted separately — don't let care-plan clients scope-creep into free extra work.

## Documents, Presentations & AI Content Humanizing

- Client sends content (text/outline) via WhatsApp or email; delivered back as PDF + editable file (PowerPoint/Word/Google Docs).
- **AI Content Humanizing** is scoped as tool-assisted (detect AI-sounding phrasing + targeted rewrite pass), not full manual line-editing — this is what makes the £60/10,000-word price match the actual time spent. See `freelance-monetization.md` for the market-rate math behind that.
- Turnaround stated on flyers: 2–3 days standard.

## Mobile & Desktop Apps

- Not yet operationally scoped — no defined delivery/publishing workflow (e.g., Play Store/App Store submission process, who holds the developer account, how updates get pushed post-launch). Flag as a TODO before the first real app client, since "help publishing to Play Store / App Store" is promised on the flyer.

## CV / Résumé / LinkedIn

- Delivered as PDF + editable file. 2–3 day turnaround, 2 rounds of free revisions, as stated on the flyer. No operational gaps identified yet — this is the simplest service to fulfill (no hosting/infra involved).

## Client Onboarding (all services)

Not yet formalized. Worth having a short intake step before quoting anything, so scope is clear before work starts:
- What exactly do they want (site type / page count, deck length, app scope, etc.) — matches directly to the pricing tiers already defined per service.
- Timeline expectations.
- For websites: does the client want a Care Plan from day one, or decide later.

## Open Decisions (not yet resolved)

- **Hosting platform default** — which of Netlify/Vercel/Cloudflare Pages/GitHub Pages to standardize on for client sites. Any works for the backup model above; pick one for consistency once the first real client lands.
- **Payment/currency method** — UK→Sri Lanka transfers not yet decided. Wise/Revolut are the obvious candidates (carried over from `freelance-monetization.md`).
- **Edit-tracking for Care Plans** — need a lightweight way (shared note, spreadsheet, or just a per-client WhatsApp thread) to track how many included edits a Standard/Priority client has used in a given month, so it doesn't quietly become unlimited free work.
- **Mobile/desktop app delivery workflow** — see above.

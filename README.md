# Handoff: Roadmates Motorbike Rental Website

## Overview
Marketing/lead-gen website for Roadmates, a motorbike & scooter rental shop in Bangkok (Sathorn 19). Goal: drive leads to WhatsApp/LINE chat and showcase the fleet, pricing, and rental policy. 7 pages, red/white brand theme.

## About these files
Unlike a typical design handoff, **these HTML files are production-ready** — they are the actual site, already deployed once via Cloudflare Pages (Direct Upload) at roadmates-website.pages.dev. This is NOT a design reference to recreate in another framework — Claude Code's job here is to:
1. Take ownership of this static site's source in the connected GitHub repo (roadmatesmotorbike-design/roadmates-website)
2. Set up Cloudflare Pages "Connect to Git" so future edits auto-deploy on push (no manual re-upload)
3. Make ongoing content edits (new blog/guide articles, pricing changes, photo swaps, copy edits) directly in these HTML files and push them

## Current deployment
- Live at: https://roadmates-website.pages.dev (Cloudflare Pages, Direct Upload — not yet Git-connected)
- GitHub repo: roadmatesmotorbike-design/roadmates-website (branch: main) — created but the earlier "Connect to Git" attempt failed because Cloudflare auto-detected a Workers/wrangler build step. This is a **plain static site — no build step, no framework, no dependencies**. When reconnecting via Git, Build command and Deploy command must both be left EMPTY, and Root directory must be "/".

## Pages (all flat static HTML, no router/framework)
| File | Purpose |
|---|---|
| index.html | Home — hero carousel, services, FAQ (schema), reviews, Our Story, favorite spots, rental policy teaser, Moments with riders |
| fleet.html | Fleet/Pricing — bikes grouped by engine class, real prices + deposits |
| rental-policy.html | Standalone rental policy detail |
| guide-index.html | Index/hub linking to the 3 guide articles below |
| bangkok-guide.html | "Renting a Motorbike in Bangkok" guide article |
| bike-routes-bangkok.html | "5 Motorbike Day Trips" guide article |
| long-term-rental-bangkok.html | "Monthly Rental for Expats" guide article |

## Tech notes
- Pure HTML/CSS (inline styles) + a couple of small JS files — no build tooling, no npm, no bundler. Any static host works.
- `image-slot.js` — a custom drag-and-drop image component used throughout for photo placeholders. Filled images are stored as base64 data URIs in `.image-slots.state.json` (a hidden sidecar file) — this file MUST be deployed alongside the HTML or photos will revert to placeholders.
- `support.js` — runtime helper the pages depend on; keep it in the root alongside the HTML files.
- `assets/` — logo files (logo.png, logo-icon.png). Note: logo.png currently has an opaque grey background baked in (not transparent) — a cleaner transparent-background logo would improve the header, but this wasn't provided during design.
- `sitemap.xml` / `robots.txt` — already reference the placeholder domain `roadmatesbangkok.com`; update these to whatever domain is actually purchased and connected.

## Content system / brand
- Color: red oklch(0.52 0.22 25) primary, warm off-white oklch(0.98 0.006 60) background, near-black oklch(0.22 0.01 60) text.
- Fonts: 'Space Grotesk' (headings) + 'Manrope' (body), loaded via Google Fonts link in each page's <head>.
- Contact channels used throughout: WhatsApp (wa.me/66924212922), LINE (line.me/R/ti/p/@221heidd), phone (tel:+66924212922), Instagram, TikTok, Facebook — same links repeated in header, hero, footer, and inline CTAs on every page. Keep these consistent if any change (e.g. new LINE ID) — they appear in 5-8 places per page.
- SEO: each page has title/meta description, and Home has LocalBusiness + FAQPage JSON-LD schema with static FAQ content matching visible copy (7 Q&As) — keep visible FAQ text and schema JSON in sync if edited.

## Known open items
- Google Business Profile widget (live reviews) was never wired up — Home has a fallback static block prompting for a Google Places API key + Place ID in "Tweaks", with 4 real testimonials shown as a fallback in the meantime. Place ID lookup proved difficult for the client; this may be worth revisiting with mapdevelopers.com's Place ID finder or the Places API "Text Search" endpoint directly instead of the finder UI.
- Domain: client intends to buy a .com domain (recommended via Cloudflare Registrar) and attach it to the Cloudflare Pages project's Custom Domains tab. sitemap.xml/robots.txt need the real domain once purchased.
- Mobile header nav was iterated on: WhatsApp CTA button removed from header (kept only as floating action button + inline page CTAs), nav links now a single compact horizontally-scrollable row on mobile (not a hamburger, not a wrapped stack) — preserve this pattern if the header is touched further.

## Suggested first task for Claude Code
1. Clone roadmatesmotorbike-design/roadmates-website
2. Verify the site runs by opening index.html directly (no server needed)
3. In Cloudflare Pages, delete the current Direct Upload deployment history if desired, then redo "Connect to Git" pointing at this repo with empty build/deploy commands and root "/" — confirm it deploys clean
4. Take over future content edits (new guide articles, pricing/policy updates, photo swaps) directly in these files going forward

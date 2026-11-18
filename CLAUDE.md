# BestVPNs (bestvpns.shmor.ai)

A Shmor marketplace (shared rules in `../../CLAUDE.md`): its own brand, design and SEO. Compares the best VPNs for privacy, streaming, speed, gaming and travel, with plain-English guides for US, UK and EU users. Repo: `Shmorai/shmor-bestvpns` (private until launch). Status: **live**, with NordVPN (CJ) referral links (see "Affiliate partners").

## Where things are
| What | Where |
|---|---|
| Card on shmor.ai, search keywords, **referral links**, offers, SEO defaults | `shmor-site.json` |
| Pages (1 JSON file = 1 Google landing page) | `content/` (`home.json` = homepage, `content/blog/x.json` → `/blog/x/`) |
| Design: header, logo, footer | `templates/layout.html` |
| Design: styles | `assets/site.css` (kit defaults at the top; **BestVPNs theme** block at the bottom) |
| "VPN for" field in every search box | `assets/site.js` |
| Generated output (don't edit by hand) | `index.html`, `*/index.html`, `sitemap.xml`, `robots.txt`, `404.html`, `search/`, `search-index.json`, `blog/feed.xml` |

## Pages (18)
Home · best-vpn (VPN checklist hub) · vpn-for-streaming · vpn-for-gaming · vpn-for-travel · free-vpn · vpn-for-iphone-android · vpn-for-windows-mac · vpn-router-smart-tv · no-logs-vpn · vpn-features-explained · what-is-a-vpn · public-wifi-security · is-a-vpn-legal · blog (+3 posts: WireGuard vs OpenVPN, VPN leak test, VPN vs Tor vs proxy).
Top menu = pages with `navOrder` (VPN checklist [mobile/tablet only; desktop shows the lime "VPN checklist" header button instead], Streaming, Privacy, Travel, Free VPNs, VPN basics, Blog). The rest are in the footer and linked via `related`, the "Find a VPN for…" tiles and the feature cards.
**Home blocks:** trust strip → Find a VPN for… (9 tiles) → What makes a VPN worth paying for (8 feature cards) → Why compare → How it works → latest posts → Popular VPN questions → guide text (visual order set with CSS `order`).

## Design
"Encrypted tunnel" (created 2026-10-13): near-black graphite pages (#090C12, surfaces #11161F, lines #222B38), electric lime #A3E635 (links, buttons, the shmor.ai card accent), cyan #38BDF8 (badges, step icons), Space Grotesk headings + Inter body + JetBrains Mono eyebrows/labels (eyebrows start with a cyan "> "). Logo = lime outline shield with a keyhole in a dark rounded square + "Best*VPNs*" (VPNs in lime) + "by Shmor.ai" pill. Home: dark network-panel photo hero with a dark-glass search card (Search VPN guides + "VPN for" select folded into `?q=`), quick chips. "Why compare" numbers are lime shield shapes. Bottom CTA = lime/cyan glow band. Tables in `.prose` scroll horizontally on phones. Mobile checked at 375px on all page types (no horizontal scroll).
**Photos:** every page has a free-licence Unsplash `"image"` (hotlinked, resized by URL): banner + card + og:image. To change one, swap `src`/`credit`/`creditUrl` and rebuild.

## Content rules
Factual and evergreen: **no invented rankings, star scores, speed results, prices or reviews**. The best-vpn page lists well-known providers alphabetically, explicitly unranked, with an ownership note (Nord Security: NordVPN + Surfshark; Kape: ExpressVPN, CyberGhost, PIA). Streaming copy explains that using a VPN to reach other countries' catalogues can break service terms, and covers the EU Portability Regulation (EU residents; UK no longer covered after Brexit). Never advise using a VPN to bypass age checks, bans or safety measures. Legal page uses "as of October 2026" wording; re-check it periodically. Blog posts list official/technical `"sources"`.

## Commands (run here)
```bash
node tools/build.js           # rebuild after ANY change to content/, templates/ or shmor-site.json
node tools/build.js --check   # validate only
node tools/serve.js 4004      # preview http://localhost:4004  (preview config "bestvpns")
```
After changing `shmor-site.json` (links, keywords, card), also run `node tools/sync-network.js` in `../../shmor-ai`.

## Adding referral links
1. Add to `shmor-site.json` → `"links"`: `"slug": { "merchant", "network": "awin|cj|impact|…", "url": "https://…" }` (or `"url": { "us", "uk", "eu" }`). Prefix slugs with the merchant name.
2. Show it on pages: add the slug to a page's `"partners": [...]`, or add an `"offers"` entry (`"pages": ["slug"]` to limit where it shows).
3. `node tools/build.js`, then sync the master, then commit both repos.
Likely programmes: most major VPN brands run affiliate programmes directly or via Impact, CJ, Awin or PartnerStack.

## Affiliate partners (live)
- **NordVPN** (CJ advertiser 4837117, joined; added 2026-11-18). 40% of new 1-month/1-year/2-year plans, 30-day cookie. Terms: no "NordVPN" in our domain or page URLs (slugs/images `cj4837117-*`; no `/nordvpn/` pages), no brand bidding, coupons only from the programme.
- Codes for the **BestVPNs property (PID 101926897)**: homepage (US) / Special UK Landing (UK) `cj4837117-home` (featured), pricing, Threat Protection (now nordvpn.com/next-gen-antivirus/), deep links via link 13914989 (destination `go.nordvpn.net/aff_c?offer_id=449&aff_id=2495&url=` + encoded NordVPN page) to downloads (all, iOS, Android, Windows, Mac, Fire TV Stick). Banners (self-hosted PNGs): "Faster than ever" 729x90 + 300x250; antivirus campaign UK 728x90 + 320x50 showing NordVPN's "75% off + 3 months extra" offer (no end date in CJ: re-check it's still current, used only on free-vpn and vpn-features-explained).
- Placed on 14 pages/posts (home banner + card, best-vpn list "NordVPN (partner link)" keeping alphabetical/unranked order + partner note, buttons on what-is-a-vpn/public-wifi/free-vpn, device app links, Threat Protection link, careful streaming/no-logs wording with no claims). `.aff-btn` uses dark text on lime here (theme override at the end of site.css).
- Surfshark (also Nord Security) not added yet: its terms 2.2.10 restrict working with direct competitors; confirm with Surfshark first.

## Ideas / next
More VPN partners (Surfshark after confirmation) · provider pages built only from verifiable facts (audits, apps, jurisdiction) · more device pages (Linux, Chromebook, Apple TV) · a social share image (`seo.image`) · a weekly blog task like the other sites.

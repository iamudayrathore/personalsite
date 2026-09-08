# DECISIONS

Append-only. One line per decision, newest at the bottom. If you're about to propose something, search here first.

| Date | Decision | Why | Alternatives rejected |
|---|---|---|---|
| 2026-09-07 | Build with Claude Code, static site, base first, features later | Speed; content volume is small | Template fork (inherits someone's art direction) |
| 2026-09-07 | No LinkedIn/X API integration; manual `posts.json` | LinkedIn has no read API; X read access is paid and fragile | Scraping (ToS), paid X API |
| 2026-09-07 | Concept: "agent security control plane" | Metaphor matches the work; motion carries information | Hacker/CTF persona (friend's site), Awwwards brutalism |
| 2026-09-08 | Palette: pure black `#000`, single accent `#F2755C` | x.ai reference; true black + hairlines reads engineered | Cream/coral (creator vibe), near-black navy, Apple blue |
| 2026-09-08 | Fonts: Inter Tight / Inter / Geist Mono, self-hosted | Closest free match to the reference; two weights only | Instrument Serif pairing, Bricolage, Space Grotesk |
| 2026-09-08 | Tools shown as captured output (fixtures), not live runs | Honest, deterministic, no runtime API or liability | Live scheduled scans, fabricated output |
| 2026-09-08 | Home layout v7: x.ai top (headline + tiles) + article/video row + icon tool cards | Approved by Uday as final | v1–v6 sketches |
| 2026-09-08 | Host on Cloudflare Pages; repo on GitHub | Free, branch previews, no non-commercial clause | GitHub Pages (no functions, clunkier domains), Vercel (free tier terms) |
| 2026-09-08 | DNS moves to Cloudflare; domain stays at Namecheap | One dashboard for DNS/SSL/hosting; no transfer cost | CNAME-only at Namecheap |
| 2026-09-08 | Astro + React islands + MDX + Tailwind v4 + Motion | Static, fast, reuses React diagram system | Next.js, GSAP/Lenis stack |
| 2026-09-08 | Videos page links out; no embedded players | Speed, no Google tracking, still counts views | Embeds |
| 2026-09-08 | Tool pages (F7) are v1 scope | Cards without pages make the site a redirect layer | Cards → GitHub only |
| 2026-09-08 | In-browser scanner demo parked to v1.1 | Highest-value differentiator, ~1 week of work | Ship in v1 |
| 2026-09-08 | No light mode, ever | The design is black | Toggle |
| 2026-09-08 | Brand is a config value in `src/data/site.ts`; never a string literal elsewhere; CI grep guard (F12) | @TheLLMArchitect is being retired; rebrand must be a one-file edit | Find-and-replace later |
| 2026-09-08 | YouTube out of v1: no fetch, no Videos page, no key. F13 in v1.1 | Channel not ready; ship GitHub + writing first | Videos page with placeholder grid |
| 2026-09-08 | Home row = latest article + latest GitHub release (was latest video); nav button → GitHub profile | Both come from data already fetched for F4; no dead links | Empty second card, "Subscribe" with no list |
| 2026-09-08 | Build with sketch placeholders (`docs/PLACEHOLDERS.md`); real copy/links swapped in session 6 | Unblocks the build; one pass to replace | Waiting on content |

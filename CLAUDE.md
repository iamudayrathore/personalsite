# CLAUDE.md — personalsite

Read before doing anything: `docs/CONCEPT.md`, `docs/DESIGN.md`, `docs/ARCHITECTURE.md`, `docs/FEATURES.md`. Check `docs/DECISIONS.md` before proposing a change of direction — it may already be decided.

## What this is
Uday's personal site: agent-security tooling, writing, and video. Public handle: @TheLLMArchitect. Domain: owned at Namecheap, DNS on Cloudflare, hosted on Cloudflare Pages.

## Stack (fixed)
Astro (static output) · React islands only where `docs/ARCHITECTURE.md` says so · MDX for writing · Tailwind v4 with tokens from `docs/DESIGN.md` · Motion (motion.dev) for animation · Self-hosted fonts · GitHub Actions for build + nightly refresh.

Do not add: GSAP, Lenis, Three.js, a CMS, a database, auth, or a dark/light toggle.

## Design rules (non-negotiable)
- Background is `#000`. Not `#0a0a0a`, not navy.
- Two type weights: 400 and 500. Never 600+.
- No gradients, glows, blur, glassmorphism, particles, cursor trails, or emoji icons.
- Motion budget is exactly the list in `docs/CONCEPT.md`. Nothing else animates.
- Tools are shown as captured output, not descriptions. See `docs/CONCEPT.md` → "Output, not description".
- Accent `#F2755C` appears only where `docs/DESIGN.md` says it does.

## Working agreement
- One feature per branch, named `feat/F<number>-<slug>` matching `docs/FEATURES.md`.
- Open a PR; Cloudflare posts a preview URL; Uday approves on the preview.
- Never commit secrets. Build-time keys come from GitHub Actions secrets.
- When a decision is made in a session, append it to `docs/DECISIONS.md` in the same PR.
- Don't mention Uday's employer anywhere in site content.
- Ask before creating any non-Markdown doc in `docs/`.

## Commands
```
pnpm install
pnpm dev          # local
pnpm build        # static build to dist/
pnpm check        # astro check + lint
pnpm fixtures     # regenerate captured tool output (see ARCHITECTURE F2)
```

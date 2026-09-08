# FEATURES — agreed 2026-09-08, revised same day (video → v1.1)

Branch names follow `feat/F<n>-<slug>`. Status column is updated in the PR that ships the feature.

## Release plan
| # | Feature | Visitor gets | Release | Status |
|---|---|---|---|---|
| F1 | Home headline | Cycling threat verb, bio line, two CTAs, "New" ticker | v1 | todo |
| F2 | Live tool tiles | Scanner run + agent trace from fixtures; type-in on scroll; trace replays on hover | v1 | todo |
| F3 | Latest article + latest release | Two cards: newest post, newest GitHub release across launch tools | v1 | todo |
| F4 | Tools I've shipped | Icon cards: tint by category, status badge, install line, stars, hover expand | v1 | todo |
| F5 | Nav + footer | Tools / Writing / Now; configurable button; socials; RSS | v1 | todo |
| F6 | Writing | MDX posts, reading time, tags, copyable code, embedded diagrams, prev/next | v1 | todo |
| F7 | Tools index + pages | Full list; per-tool page with catches, install, output, related posts | v1 | todo |
| F8 | Now | Hand-written monthly page, dated | v1 | todo |
| F9 | SEO plumbing | Sitemap, RSS, canonicals, OG image per page — all from `site.brand` | v1 | todo |
| F10 | Analytics | Cloudflare Web Analytics | v1 | todo |
| F11 | Nightly refresh | Cron rebuild for stars and releases | v1 | todo |
| F12 | Brand swap readiness | `site.ts` is the only identity source; build-time grep guard fails if the brand string appears outside it | v1 | todo |
| F13 | Videos | Thumbnail grid from YouTube, newest first, links out; Videos in nav; latest-video card replaces latest-release on home | v1.1 | parked |
| F14 | Newsletter | Real list + archive; nav button switches from GitHub | v1.1 | parked |
| F15 | Social post log | `posts.json` stream; slash command to append from URL | v1.1 | parked |
| F16 | In-browser tool demo | Run mcp-scopecheck on a pasted config (Pyodide/WASM) | v1.1 | parked |
| F17 | Search | Client-side, writing + tools | v1.1 | parked |
| F18 | Talks / appearances | Dated list | later | parked |
| F19 | Uses / setup | Hardware, software, Claude Code config | later | parked |
| F20 | Light mode | — | never | — |

## Per-feature architecture (v1)
| # | Data in | Components | Build step | Island? |
|---|---|---|---|---|
| F1 | `site.ts` (verbs, bio, ticker, ctas) | `Hero.astro`, `VerbCycle.tsx` | none | `VerbCycle` |
| F2 | `fixtures/scopecheck.txt`, `fixtures/trace.json` | `Tile.astro`, `ScannerTile.tsx`, `TraceTile.tsx` | `pnpm fixtures` (manual) | both tiles |
| F3 | newest of `content/writing`; newest release in `github.generated.json` | `CardArticle.astro`, `CardRelease.astro` | fetch-github in prebuild | no |
| F4 | `content/tools/*.md` + `github.generated.json` | `CardTool.astro`, `ToolHover.tsx` | fetch-github in prebuild | hover only |
| F5 | `site.ts` (nav, followButton, socials) | `Nav.astro`, `Footer.astro` | none | no |
| F6 | `content/writing/*.mdx` | `PostLayout.astro`, `Prose.css`, `diagrams/*` | reading time via remark plugin | diagrams only |
| F7 | `content/tools/*.md`, fixtures, related-by-tag | `ToolPage.astro`, `pages/tools/[slug].astro` | none | reuses F2 tiles |
| F8 | `content/now.md` | `pages/now.astro` | none | no |
| F9 | all pages + `site.brand` | `@astrojs/sitemap`, `@astrojs/rss`, `scripts/og.ts` | og render postbuild | no |
| F10 | — | one script tag in `BaseLayout.astro` | none | no |
| F11 | — | `.github/workflows/nightly.yml` | cron → deploy hook | no |
| F12 | `site.ts` | `scripts/brand-guard.ts` | postbuild grep of `dist/` for the brand string outside expected chrome; fails CI on hit | no |

## Content collection schemas
```ts
// tools
{ name, slug, repo, category: 'scanner'|'orchestrator'|'research',
  status: 'shipped'|'poc'|'archived', install?: string, catches: string,
  fixture?: string, tags: string[] }

// writing
{ title, slug, date, summary, tags: string[], diagram?: string, draft?: boolean }
```

## Build order (sessions)
1. Scaffold + tokens + fonts + `site.ts` with placeholders + F5 + F1 — page exists, headline cycles.
2. F2 fixtures + tiles — the "wow" is real.
3. F4 + F7 + fetch-github (stars, last commit, releases) — tools end to end.
4. F6 + first two posts migrated — writing end to end.
5. F3 + F8 + F9 — home cards, Now page, SEO.
6. F10 + F11 + F12 — analytics, nightly, brand guard. Replace placeholders from `docs/PLACEHOLDERS.md`.
7. DNS cutover + launch.

v1.1 starts with F13 (videos) once the channel is ready — it's additive: one fetch script, one page, one card swap, one nav item.

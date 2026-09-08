# FEATURES — agreed 2026-09-08

Branch names follow `feat/F<n>-<slug>`. Status column is updated in the PR that ships the feature.

## Release plan
| # | Feature | Visitor gets | Release | Status |
|---|---|---|---|---|
| F1 | Home headline | Cycling threat verb, bio line, two CTAs, "New" ticker | v1 | todo |
| F2 | Live tool tiles | Scanner run + agent trace from fixtures; type-in on scroll; trace replays on hover | v1 | todo |
| F3 | Latest article + video | Two cards auto-filled from F6 and F8 | v1 | todo |
| F4 | Tools I've shipped | Icon cards: tint by category, status badge, install line, stars, hover expand | v1 | todo |
| F5 | Nav + footer | Tools / Writing / Videos / Now; Follow button; socials; RSS | v1 | todo |
| F6 | Writing | MDX posts, reading time, tags, copyable code, embedded diagrams, prev/next | v1 | todo |
| F7 | Tools index + pages | Full list; per-tool page with catches, install, output, related posts/videos | v1 | todo |
| F8 | Videos | Thumbnail grid from YouTube, newest first, links out, no embeds | v1 | todo |
| F9 | Now | Hand-written monthly page, dated | v1 | todo |
| F10 | SEO plumbing | Sitemap, RSS, canonicals, OG image per page | v1 | todo |
| F11 | Analytics | Cloudflare Web Analytics | v1 | todo |
| F12 | Nightly refresh | Cron rebuild for stars and videos | v1 | todo |
| F13 | Follow / Subscribe | → YouTube in v1; newsletter embed in v1.1 | v1 → v1.1 | todo |
| F14 | Social post log | `posts.json` stream; slash command to append from URL | v1.1 | parked |
| F15 | In-browser tool demo | Run mcp-scopecheck on a pasted config (Pyodide/WASM) | v1.1 | parked |
| F16 | Search | Client-side, writing + tools | v1.1 | parked |
| F17 | Newsletter | Real list + archive | v1.1 | parked |
| F18 | Talks / appearances | Dated list | later | parked |
| F19 | Uses / setup | Hardware, software, Claude Code config | later | parked |
| F20 | Light mode | — | never | — |

## Per-feature architecture (v1)
| # | Data in | Components | Build step | Island? |
|---|---|---|---|---|
| F1 | `src/data/site.ts` (verbs, bio, ticker) | `Hero.astro`, `VerbCycle.tsx` | none | `VerbCycle` only |
| F2 | `fixtures/scopecheck.txt`, `fixtures/trace.json` | `Tile.astro`, `ScannerTile.tsx`, `TraceTile.tsx` | `pnpm fixtures` (manual) | both tiles |
| F3 | newest of `content/writing`, newest of `youtube.generated.json` | `CardArticle.astro`, `CardVideo.astro` | reads generated data | no |
| F4 | `content/tools/*.md` + `github.generated.json` | `CardTool.astro`, `ToolHover.tsx` | fetch-github in prebuild | hover only |
| F5 | `site.ts` | `Nav.astro`, `Footer.astro` | none | no |
| F6 | `content/writing/*.mdx` | `PostLayout.astro`, `Prose.css`, `diagrams/*` | reading time via remark plugin | diagrams only |
| F7 | `content/tools/*.md`, fixtures, related-by-tag | `ToolPage.astro`, `pages/tools/[slug].astro` | none | reuse F2 tiles |
| F8 | `youtube.generated.json` | `VideoGrid.astro` | fetch-youtube in prebuild | no |
| F9 | `content/now.md` | `pages/now.astro` | none | no |
| F10 | all pages | `@astrojs/sitemap`, `@astrojs/rss`, `scripts/og.ts` | og render postbuild | no |
| F11 | — | one script tag in `BaseLayout.astro` | none | no |
| F12 | — | `.github/workflows/nightly.yml` | cron → deploy hook | no |
| F13 | `site.ts` link | `Nav.astro` button | none | no |

## Content collection schemas
```ts
// tools
{ name, slug, repo, category: 'scanner'|'orchestrator'|'research',
  status: 'shipped'|'poc'|'archived', install?: string, catches: string,
  fixture?: string, tags: string[] }

// writing
{ title, slug, date, summary, tags: string[], diagram?: string, draft?: boolean }
```

## Build order (proposed sessions)
1. Scaffold + tokens + fonts + F5 + F1 — the page exists and the headline cycles.
2. F2 fixtures + tiles — the "wow" is real.
3. F4 + F7 + fetch-github — tools end to end.
4. F6 + first two posts migrated — writing end to end.
5. F8 + F3 + fetch-youtube — videos and home cards.
6. F9, F10, F11, F12, F13 — launch plumbing.
7. DNS cutover + launch.

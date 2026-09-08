# ARCHITECTURE — agreed 2026-09-08

## System
| # | Layer | Component | Decision | Notes |
|---|---|---|---|---|
| 1 | Domain | Registrar | Namecheap (existing) | No transfer |
| 2 | Domain | DNS | Cloudflare — change nameservers at Namecheap | Proxy on; SSL Full (strict) |
| 3 | Hosting | Static + CDN | Cloudflare Pages | Free tier, branch previews |
| 4 | Hosting | Serverless | Cloudflare Pages Functions | Not used in v1 |
| 5 | Source | Repo | `github.com/iamudayrathore/personalsite`, private until launch | |
| 6 | Source | Branching | `main` = prod; `feat/F<n>-<slug>` → PR → preview → merge | |
| 7 | Framework | Generator | Astro, `output: 'static'` | |
| 8 | Framework | Islands | React, `client:visible` only | Headline verb, scanner tile, trace tile, tool-card hover |
| 9 | Framework | Motion | Motion + CSS transitions | |
| 10 | Framework | Styling | Tailwind v4, tokens from DESIGN.md | |
| 11 | Framework | Fonts | Self-hosted woff2 | |
| 12 | Config | Site identity | `src/data/site.ts` — brand, domain, bio, socials, nav, CTAs, stats, verbs | **Only** place the brand is named. See CLAUDE.md. |
| 13 | Content | Writing | MDX in `src/content/writing/` | Astro content collections |
| 14 | Content | Diagrams | React diagram system as MDX components | `src/components/diagrams/` |
| 15 | Content | Tools | `src/content/tools/*.md` | Frontmatter schema in FEATURES.md |
| 16 | Content | Social log | `src/data/posts.json`, manual append | v1.1 |
| 17 | Data | GitHub | REST at build → `src/data/github.generated.json` | Stars, last commit, **latest release** per tool. Token: `GITHUB_TOKEN` |
| 18 | Data | YouTube | **Parked to v1.1.** `scripts/fetch-youtube.ts` not written in v1 | No key needed yet |
| 19 | Data | Tool output | Committed fixtures in `fixtures/` | `pnpm fixtures`; never runtime |
| 20 | Build | CI | GitHub Actions: on push + nightly cron (07:00 UTC) → Cloudflare deploy hook | |
| 21 | Build | Secrets | GitHub Actions secrets → Cloudflare build env | v1 needs only `GITHUB_TOKEN` |
| 22 | Build | Gates | `astro check`, eslint, Lighthouse CI ≥ 95 perf on PR | |
| 23 | Growth | Newsletter | v1.1 (Buttondown or Kit) | Nav button → GitHub in v1 |
| 24 | Growth | Analytics | Cloudflare Web Analytics | Cookieless |
| 25 | Growth | SEO | RSS, sitemap, canonicals, OG images via satori at build | All read `site.brand` |
| 26 | Ops | AI context | `CLAUDE.md`, `docs/*.md` | |
| 27 | Ops | Backup | Repo + Cloudflare deploy history | |

## Repo layout
```
personalsite/
  CLAUDE.md
  docs/            CONCEPT, DESIGN, ARCHITECTURE, FEATURES, DECISIONS, PLACEHOLDERS, DNS-CUTOVER
  fixtures/        scopecheck.txt, trace.json
  public/fonts/    woff2
  public/favicon.svg
  scripts/         fetch-github.ts, capture-fixtures.ts, og.ts   (fetch-youtube.ts in v1.1)
  src/
    data/site.ts            brand + copy + links  ← single source of identity
    data/                   *.generated.json (gitignored), snapshots/
    content/writing/*.mdx
    content/tools/*.md
    components/             islands + static components
    components/diagrams/    React diagram system
    layouts/
    pages/                  index, writing/, tools/, now   (videos/ in v1.1)
    styles/tokens.css
  .github/workflows/       build.yml, nightly.yml
```

## `site.ts` shape
```ts
export const site = {
  brand: { name: 'TheLLMArchitect', handle: '@TheLLMArchitect', domain: 'example.com' }, // PLACEHOLDER
  bio: '...',                                   // PLACEHOLDER
  ticker: 'New · ...',                          // PLACEHOLDER until F3 automates it
  verbs: ['touch', 'read', 'call', 'leak', 'ship'],
  ctas: [{ label: 'Explore the tools', href: '/tools' }, { label: 'Read the writing', href: '/writing' }],
  stats: ['3 tools shipped', '42 servers audited', '1/wk post'],   // PLACEHOLDER; [] hides the row
  nav: [{ label: 'Tools', href: '/tools' }, { label: 'Writing', href: '/writing' }, { label: 'Now', href: '/now' }],
  followButton: { label: 'GitHub', href: 'https://github.com/iamudayrathore' },   // newsletter in v1.1
  socials: { github: '...', x: '#', linkedin: '#', youtube: '#' },   // '#' = hidden
};
```

## Build pipeline
1. `scripts/fetch-github.ts` runs in `prebuild`, writes `github.generated.json` (stars, pushed_at, latest release per tool repo). On API failure it falls back to `src/data/snapshots/github.json` so a rate limit never fails the build.
2. `astro build` reads `site.ts`, content collections, generated data.
3. `scripts/og.ts` renders one OG image per page using `site.brand`.
4. Cloudflare Pages deploys `dist/`.
5. `nightly.yml` calls the Cloudflare deploy hook so stars and releases stay current.

## DNS cutover
See `docs/DNS-CUTOVER.md`.

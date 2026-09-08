# PLACEHOLDERS

Everything below is a stand-in copied from the approved v7 sketch. It ships in previews, not to production. Each row is replaced by editing the file in the "Lives in" column — nothing else. Tick the box when the real value is in.

## Brand (will change — see procedure at bottom)
| | Placeholder | Lives in | Replace with |
|---|---|---|---|
| [ ] | `site.brand.name = "TheLLMArchitect"` | `src/data/site.ts` | New brand name |
| [ ] | `site.brand.handle = "@TheLLMArchitect"` | `src/data/site.ts` | New handle |
| [ ] | `site.brand.domain = "example.com"` | `src/data/site.ts`, `astro.config.mjs` | Real domain |
| [ ] | Favicon: mono "T" glyph | `public/favicon.svg` | New mark |

## Copy
| | Placeholder | Lives in | Replace with |
|---|---|---|---|
| [ ] | Ticker: `New · mcp-scopecheck 0.4 — audits remote MCP servers` | `site.ts → ticker` | Auto from latest GitHub release once F3 lands; until then manual |
| [ ] | Bio: `Open-source security tooling and writing on agent and MCP attack surface. Built in public.` | `site.ts → bio` | Real one-liner |
| [ ] | CTAs: `Explore the tools` / `Read the writing` | `site.ts → ctas` | Keep or reword |
| [ ] | Stats row: `3 tools shipped · 42 servers audited · 1/wk post` | `site.ts → stats` | Real numbers, or set to `[]` to hide the row |
| [ ] | Nav button: `GitHub` → GitHub profile | `site.ts → followButton` | Newsletter in v1.1 |

## Social links
| | Placeholder | Lives in |
|---|---|---|
| [ ] | `github: "https://github.com/iamudayrathore"` | `site.ts → socials` |
| [ ] | `x: "#"` | `site.ts → socials` |
| [ ] | `linkedin: "#"` | `site.ts → socials` |
| [ ] | `youtube: "#"` (hidden until v1.1) | `site.ts → socials` |

## Tools (three launch cards)
| | Name | Category | Status | Install line | Catches | Lives in |
|---|---|---|---|---|---|---|
| [ ] | mcp-scopecheck | scanner | shipped | `pip install mcp-scopecheck` (real) | Catches over-scoped tool permissions before you install. | `src/content/tools/mcp-scopecheck.md` |
| [ ] | LoopForge | orchestrator | shipped | `npx loopforge init` (**not real**) | Runs multi-agent loops with bounded tool access. | `src/content/tools/loopforge.md` |
| [ ] | Glassworm | research | poc | — (`worm + paired detector`) | Shows agent-to-agent propagation and how to detect it. | `src/content/tools/glassworm.md` |

Each needs its real `repo:` URL in frontmatter; stars and last-commit pull from it. Repos must be public.

## Fixtures (captured output for the home tiles)
| | Placeholder | Lives in | Replace with |
|---|---|---|---|
| [ ] | Scanner run: `mcp-scopecheck audit ./server.json` → 14 tools, `fs.read_file` warn, `http.fetch` fail, `git.commit` pass, `2 findings · 0.8s` | `fixtures/scopecheck.txt` | Output of a real run via `pnpm fixtures` |
| [ ] | Trace: `Rotate the leaked token.` → read_file, grep, `http.post blocked outside tool budget`, `Thought for 3.2s · budget 4/6` | `fixtures/trace.json` | A real LoopForge trace with a blocked call |

## Writing
| | Placeholder | Lives in | Replace with |
|---|---|---|---|
| [ ] | `The 5-S audit for MCP servers` — lorem body, tagged `agent-security` | `src/content/writing/5s-audit.mdx` | Two real posts migrated in session 4 |

## Videos — parked to v1.1
No YouTube key, channel ID, or video cards in v1. `socials.youtube` stays `#` and the footer hides it while it's `#`.

## Rebrand procedure (when the new name is ready)
1. Edit `src/data/site.ts` — `brand.name`, `brand.handle`, `brand.domain`, socials.
2. Replace `public/favicon.svg`.
3. Update `site` in `astro.config.mjs` (or make it read from `site.ts` — preferred).
4. `pnpm build` and grep `dist/` for the old name. If it appears anywhere, that's a bug: something hardcoded the brand. Fix the source, not the output.
5. DNS/domain per `docs/DNS-CUTOVER.md` if the domain changes too.
6. Log it in `docs/DECISIONS.md`.

The repo name `personalsite` does not need to change.

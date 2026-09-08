# CONCEPT — approved 2026-09-08

## The metaphor
The site is an agent-security control plane, seen from the outside. The visitor isn't reading *about* the tools; they're looking at the tools running. Everything on the home page above the fold is output.

## Where the design came from
Iterated through six sketches: Tokyo Night control-plane wireframe → aliabdaal.com-style cream/coral → dark Apple Keynote → index/ledger (Rauno/Linear grammar) → x.ai-style black with live tiles → **v7: x.ai top + icon tool cards bottom (approved)**.

What was rejected and why, so it isn't re-proposed:
- Centered hero + pill buttons + card grid with badges as the whole page — "AI sloppy."
- Cream/coral palette — reads "creator," not "engineer."
- Brutalist/glitch — wrong audience (staff engineers and frontier-lab hiring managers, not design studios).
- Terminal-as-about-page, click-to-enter video, hidden game — CTF-hacker dialect, not ours.

## Home page, top to bottom (v1)
1. **Nav** — `site.brand.name` left; Tools / Writing / Now; one filled button (`site.followButton`: GitHub in v1, newsletter in v1.1). Videos appears in v1.1.
2. **Ticker line** — mono, `New · <latest shipped thing>`. Accent only on the word "New".
3. **Headline** — three lines, Inter Tight 500, ~52px desktop, tracking -0.035em:
   ```
   Agents run.
   I watch what they
   <verb>.
   ```
   `<verb>` cycles: `touch · read · call · leak · ship`. Underlined in accent. 1.8s interval, 250ms crossfade. Threat verbs only; do not add cute ones.
4. **Sub + CTAs** — one sentence, two buttons (white filled, hairline outline). Copy from `site.ts`.
5. **Live tiles** (2-up) — see "Output, not description."
6. **Latest article + latest release** — two cards. Article from the writing collection; release from the GitHub API (newest release across the launch tools: tag, repo, date). In v1.1 the second card becomes latest video.
7. **Tools I've shipped** — icon cards. Icon tint = category, badge = status, mono install line, GitHub stars, hover expands "what it catches."
8. **Footer** — socials (any link set to `#` is hidden), RSS. No sitemap dump.

## Output, not description
Every tool on the site is represented by real captured output, committed to the repo as fixtures:
- **Scanner tile** — a real `mcp-scopecheck audit` run: prompt line, progress line, warn/fail/pass findings, summary line.
- **Trace tile** — a real LoopForge trace: user instruction, "Thinking…", tool calls, one call **blocked** by the tool budget, "Thought for Ns · budget n/m."
Fixtures are regenerated with `pnpm fixtures` when tools change. Never live API calls at runtime, never fabricated. During the build they are the sketch placeholders in `docs/PLACEHOLDERS.md`.

## Motion budget (complete list)
1. Headline verb cycle.
2. Tile lines type in on scroll (once per page load).
3. Trace tile replays on hover.
4. Tool card lift + expand on hover; icon rotates in on first reveal.
5. Row/link hover color shift.
6. Page-load stagger on the home page only, first visit only (no replay on back-navigation).

Easing: `cubic-bezier(0.16, 1, 0.3, 1)`, 500–800ms for reveals, 120–150ms for hovers. No bounce, no spring overshoot, no glitch.

## Voice
Sentence case everywhere. Short. Claims must be demonstrable. No "leverage," "seamless," "unlock," no "hey guys." The brand name never appears in body copy — only via `site.brand` in chrome (nav, footer, meta).

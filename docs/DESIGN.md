# DESIGN — tokens and components (v7, approved 2026-09-08)

Implement as CSS variables in `src/styles/tokens.css`; Tailwind v4 reads them via `@theme`.

## Color
| Token | Value | Use |
|---|---|---|
| `--bg` | `#000000` | Page. Never anything else. |
| `--surface` | `#0A0A0A` | Tiles, cards |
| `--surface-2` | `#161616` | Video thumb placeholder, inset blocks |
| `--line` | `#1C1C1C` | Hairlines, card borders |
| `--line-faint` | `#141414` | Section dividers |
| `--line-hover` | `#3A3A3A` | Card/tile border on hover |
| `--text` | `#F2F2F2` | Primary |
| `--text-2` | `#8A8A8A` | Secondary |
| `--text-3` | `#555555` | Metadata, labels |
| `--mono` | `#BDBDBD` | Mono output text |
| `--accent` | `#F2755C` | Verb underline, "New", `fail`, blocked, hover on titles. **Nowhere else.** |
| `--ok` | `#7AD98C` | `pass`, "Shipped" badge text |
| `--warn` | `#FAC775` | `warn`, "PoC" badge text |

Tool category tints (icon container bg / icon color):
| Category | bg | fg |
|---|---|---|
| Scanner | `#0E1F2C` | `#5DCDF1` |
| Orchestrator | `#1A1730` | `#AFA9EC` |
| Research | `#2A1712` | `#F2755C` |
Add new categories here before using them.

Badge backgrounds: Shipped `#0F2417`, PoC `#2A2010`, Archived `#161616` with `--text-2`.

## Type
| Role | Font | Size | Weight | Tracking |
|---|---|---|---|---|
| Headline | Inter Tight | clamp(36px, 7vw, 52px) | 500 | -0.035em |
| Section title | Inter Tight | 24px | 500 | -0.025em |
| Card title | Inter | 14–19px | 500 | -0.005em |
| Body | Inter | 13–15px | 400 | -0.005em |
| Mono / output / meta | Geist Mono | 11.5px | 400 | 0 |

Line-height: headline 0.98, body 1.5, mono output 1.7. Self-host all three as woff2 in `public/fonts/`.

## Shape and spacing
- Radius: buttons 6px, tiles 10px, cards 14px, icon containers 10px, badges 999px.
- Borders: 1px `--line` everywhere. No shadows.
- Page gutter 28px desktop / 16px mobile. Max content width 1040px.
- Section vertical rhythm: 28–44px.

## Components
**Button.filled** — `--text` bg, `--bg` text, 9px 16px.
**Button.outline** — 1px `#333`, `--text` text.
**Tile** — `--surface`, 1px `--line`, header row (name left, mono meta right), mono body min-height 150px, footer row ("Explore →" left, mono note right).
**Card.article / Card.video** — `--surface`, label in `--text-3` 11px, title Inter Tight, meta `--text-2` 12px.
**Card.tool** — icon container 38px, name + category, status badge right, mono install line in `--bg` with `--line` border, stars line, hidden "what it catches" revealed on hover.
**Row** — for lists: title left, mono date right, 1px `--line-faint` bottom, title turns `--accent` on hover.

## Responsive
- ≤768px: tiles stack, tool cards single column, headline 36px, nav collapses to name + Follow button + a menu.
- Verb cycle and hover animations respect `prefers-reduced-motion`: show static "touch", no typing effect.

## Reference
The approved sketch lives in the chat history as `control_plane_homepage_v7_xai_top_icon_cards_bottom`. Ask Uday for the HTML export if a pixel reference is needed.

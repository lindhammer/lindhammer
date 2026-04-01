# GitHub Profile README — Design Spec

**Date:** 2026-04-01
**Repo:** `lindhammer/lindhammer` (GitHub profile special repo)
**Output files:** `README.md`, `banner.svg`

---

## Goal

A visually distinctive GitHub profile README for lindhammer / LLH. Presents two identities equally: music artist (LLH) and AI-assisted builder. Tone is self-aware, editorial, and unhurried — not a CV, not a portfolio, not vibecoding showcase. The README should look intentional and communicate a clear personal methodology without being cringe or "sweaty."

---

## Design Tokens

Sourced from the live llhmusic.com artist site (`artist-site/src/styles/tokens.css`):

| Token        | Value                  | Role                                 |
| ------------ | ---------------------- | ------------------------------------ |
| Background   | `#0d1117`              | GitHub dark theme background         |
| Surface      | `#0b0907` / `#161b22`  | Cards, code blocks                   |
| Text primary | `#e8e3dc`              | Headings, names, strong              |
| Text body    | `#918880`              | Paragraphs, descriptions             |
| Text muted   | `#6b6158`              | Meta, tags, fingerprint              |
| Border       | `#21262d`              | Dividers, table borders              |
| Border warm  | `#2c2520`              | Warm hairlines                       |
| Accent       | `#c41e1e`              | Section heads, dashes, phase numbers |
| Accent glow  | `rgba(196,30,30,0.24)` | Banner radial gradient               |

**Typography in SVG banner:**

- Display: Georgia / Times New Roman serif (system fallback — no web font loading in SVG)
- Letter-spacing: `0.07em` on the name
- Subtext: italic, 13px, `#918880`

---

## File Structure

```
lindhammer/
  README.md       ← the profile README
  banner.svg      ← atmospheric header image
```

The `.superpowers/` directory should be added to `.gitignore`.

---

## Structure & Content

### 1. Banner (SVG image)

File: `banner.svg`, referenced in README as:

```html
<p align="center">
  <img src="banner.svg" alt="LLH" width="100%" />
</p>
```

**Visual spec:**

- Full-width SVG, `viewBox="0 0 800 160"`, `width="100%"`
- Background: `linear-gradient(165deg, #1c0a0a 0%, #0d1117 55%)`
- Red radial glow: `radial-gradient` ellipse at top-center, `rgba(196,30,30,0.24)`, fades to transparent at 55%
- Hairline bottom border: `linear-gradient(90deg, transparent, rgba(196,30,30,0.45), transparent)`, 1px tall, full width
- Grain overlay: SVG `feTurbulence` fractalNoise filter rect, `opacity="0.04"`, `mix-blend-mode: overlay` (soft-light as fallback)
- Main text: "LLH" in Georgia serif, `font-size="52"`, `font-weight="700"`, `fill="#e8e3dc"`, `letter-spacing="0.07em"`, centered
- Subtext: _music & tools for making it_ in Georgia italic, `font-size="15"`, `fill="#918880"`, centered at `y="105"` (approx 18px below baseline of main text at `y="88"`)

### 2. Two-column section

Implemented as an HTML `<table>` (GitHub renders this reliably):

```html
<table>
  <tr>
    <td width="50%" valign="top">
      <!-- Music column -->
    </td>
    <td width="4%"></td>
    <td width="50%" valign="top">
      <!-- Projects column -->
    </td>
  </tr>
</table>
```

**Music column content:**

- Section head: `### Music` markdown heading (GitHub renders this as a styled `<h3>`)
- Link: [llhmusic.com](https://llhmusic.com)
- Description: "Artist site, discography, and releases. Electronic music released as LLH."
- Tech tag: `Eleventy · PostCSS`

**Projects column content:**

**Songwriter**

> Local workspace for writing lyrics to an instrumental. Phase-by-phase: brief → themes → structure → sections → export. Built because I kept abandoning songs halfway through.
> `Next.js · Anthropic · Gemini · SQLite`

**Anchor**

> Day planner for low-energy, overwhelmed, or depressive states. Not productivity. Recovery.
> `React Native · Expo · Firebase`

### 3. Process section: "How it gets built"

#### Intro (paragraph)

> **Architect + Builder.** Claude acts as the senior engineer — planning, authoring prompts, reviewing output. Cursor and Kilo Code act as the hands that execute. Every session follows a structured prompt template. No code gets merged without a self-critique pass.

#### Phase table

Rendered as an HTML table with 2 columns: phase label (left) | detail + tags (right). Four rows:

| Phase              | Content                                                                                                                                                   |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **01 — Ideation**  | Define scope, name the mode. Claude plans first — architecture, constraints, what not to touch. Tags: `Explore vs. production` · `Plan before generating` |
| **02 — Prompt**    | Every prompt follows the 4-block template: Goal · Constraints · Context · What I want now. One module only. Tags: `4-block template` · `No scope creep`   |
| **03 — Execution** | Claude owns the prompt and review. Cursor / Kilo Code executes within that scaffold. Tags: `Architect + Builder` · `Cursor · Kilo Code · Copilot`         |
| **04 — Gate**      | Force the model to critique its own output. Pass → merge. Fail → revise the prompt and repeat. Tags: `Self-critique` · `Clean rewrite over patch`         |

#### 4-block prompt template (fenced code block)

Presented with a small label above it ("4-block prompt template"), as a stealable markdown code block:

```
# Goal
[What to build, in one sentence.]

# Constraints
[Tech stack, limits, style rules, things to avoid.]

# Existing context
[Relevant files, current state of the module, what already works.]

# What I want now
[Single next action. One module only. No refactoring scope creep.]
```

#### Core principles

Markdown list with em-dash style (achieved via plain `—` prefix, no bullet markers):

- **Clean rewrites over patches** — if it's broken, rewrite the module, don't layer fixes on debt
- **One module at a time** — scope stays locked until the current unit is done
- **Name the mode before starting** — exploration (loose, iterative) vs. production (strict, reviewable)
- **Force self-critique after generation** — the model reviews its own output before anything gets merged

#### Tech fingerprint

Centered, two lines:

> **Stack —** Next.js · React Native · Eleventy · SQLite · Firebase · TypeScript
> **Tooling —** Claude · Cursor · Kilo Code · GitHub Copilot · Codex

### 4. Footer

Centered, italic, muted:

> _I don't write code. I describe what I want until something builds it._
> _These are the things worth describing._

---

## GitHub README Constraints

- No `<style>` tags — GitHub strips all CSS
- No `<script>` tags
- `<table>`, `<tr>`, `<td>`, `<p align="center">`, `<img>`, `<br>`, `<strong>`, `<em>`, `<sub>`, `<sup>`, `<a>` all render
- SVG files committed to the repo render inline via `<img src="banner.svg">`
- SVG CSS animations are stripped by GitHub's sanitizer — keep the SVG static
- Fenced code blocks render with syntax highlighting
- `---` renders as a horizontal rule
- The two-column layout requires `<table>` — CSS grid/flex is not available

### Achieving the visual style in plain markdown + HTML:

- Section heads (MUSIC, PROJECTS, HOW IT GETS BUILT): Use `<br><sub>MUSIC</sub>` or bold + em-dash. The red color cannot be applied via inline HTML in GitHub.
- Dividers: `---` markdown horizontal rule, or `<hr>` in HTML
- Phase numbers: Plain text `01`, `02` etc. in the table
- Tags below phase descriptions: As `\`backtick code spans\`` — GitHub renders these with a subtle background that approximates the tag style
- Tech stack: Plain `·`-separated text
- Footer italics: Standard markdown `*italic*`

---

## Implementation Notes

1. **Build the SVG banner first** — it's the most complex piece and the visual anchor for everything else. Keep it purely declarative (no JS, no external fonts, no CSS animations).
2. **The table layout is fragile** — GitHub's markdown renderer collapses whitespace inside `<td>` differently across themes. Test in both light and dark mode. Use `valign="top"` on all `<td>` elements.
3. **The phase table in the process section** — also an HTML `<table>`. Use `<code>` spans for the tags inside cells.
4. **Fenced code block** — use plain ` ``` ` without a language tag so GitHub doesn't attempt syntax highlighting on the template.
5. **No color** — the warm palette exists in the SVG banner only. The rest of the README is GitHub's default rendering. Design the content to not depend on color for hierarchy.
6. **`.gitignore`** — add `.superpowers/` to the repo's `.gitignore`.


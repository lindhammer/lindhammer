# GitHub Profile README Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build the `lindhammer/lindhammer` GitHub profile README — an SVG banner and a full-content README.md.

**Architecture:** Three static files committed to the repo root: `.gitignore`, `banner.svg`, and `README.md`. The SVG banner is the only place custom color/typography lives; the README body uses GitHub's default markdown rendering. No build step, no dependencies.

**Tech Stack:** SVG (static, no animations), GitHub-flavored Markdown, HTML table layout

---

## File Map

| File         | Action    | Responsibility                                       |
| ------------ | --------- | ---------------------------------------------------- |
| `.gitignore` | Create    | Exclude `.superpowers/` from version control         |
| `banner.svg` | Create    | Atmospheric header — all color and custom typography |
| `README.md`  | Overwrite | Full profile README content                          |

---

### Task 1: Create `.gitignore`

**Files:**

- Create: `.gitignore`

- [ ] **Step 1: Write the file**

  Exact content:

  ```
  .superpowers/
  ```

- [ ] **Step 2: Verify it was written**

  Run:

  ```bash
  cat .gitignore
  ```

  Expected: `.superpowers/` on its own line.

- [ ] **Step 3: Commit**

  ```bash
  git add .gitignore
  git commit -m "chore: add .gitignore — exclude .superpowers/"
  ```

---

### Task 2: Create `banner.svg`

The SVG is the visual anchor of the README. It must be fully static (no CSS animations, no JS, no external fonts — GitHub strips them). All colors and gradients are embedded in `<defs>`.

**Files:**

- Create: `banner.svg`

- [ ] **Step 1: Write `banner.svg`**

  ```xml
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 800 160" width="100%" role="img" aria-label="LLH — music &amp; tools for making it">
    <defs>
      <!-- Background: linear-gradient(165deg, #1c0a0a 0%, #0d1117 55%) -->
      <linearGradient id="bg" x1="0" y1="0" x2="0.6" y2="1">
        <stop offset="0%" stop-color="#1c0a0a"/>
        <stop offset="55%" stop-color="#0d1117"/>
        <stop offset="100%" stop-color="#0d1117"/>
      </linearGradient>
      <!-- Red radial glow: ellipse at top-center, rgba(196,30,30,0.24), fades at 55% -->
      <radialGradient id="glow" gradientUnits="userSpaceOnUse" cx="400" cy="-8" r="380">
        <stop offset="0%" stop-color="#c41e1e" stop-opacity="0.24"/>
        <stop offset="55%" stop-color="#c41e1e" stop-opacity="0"/>
        <stop offset="100%" stop-color="#c41e1e" stop-opacity="0"/>
      </radialGradient>
      <!-- Bottom hairline: transparent → red → transparent -->
      <linearGradient id="hairline" x1="0" y1="0" x2="1" y2="0">
        <stop offset="0%" stop-color="#c41e1e" stop-opacity="0"/>
        <stop offset="50%" stop-color="#c41e1e" stop-opacity="0.45"/>
        <stop offset="100%" stop-color="#c41e1e" stop-opacity="0"/>
      </linearGradient>
      <!-- Grain: fractalNoise, very low opacity -->
      <filter id="grain" x="0%" y="0%" width="100%" height="100%">
        <feTurbulence type="fractalNoise" baseFrequency="0.65" numOctaves="3" stitchTiles="stitch" result="noise"/>
        <feColorMatrix type="saturate" values="0" in="noise" result="mono"/>
        <feBlend in="SourceGraphic" in2="mono" mode="overlay"/>
      </filter>
    </defs>

    <!-- Background fill -->
    <rect width="800" height="160" fill="url(#bg)"/>
    <!-- Glow overlay -->
    <rect width="800" height="160" fill="url(#glow)"/>
    <!-- Grain overlay -->
    <rect width="800" height="160" filter="url(#grain)" opacity="0.04" style="mix-blend-mode: overlay"/>
    <!-- Bottom hairline (1px) -->
    <rect y="159" width="800" height="1" fill="url(#hairline)"/>

    <!-- Name: LLH -->
    <text
      x="400" y="88"
      text-anchor="middle"
      font-family="Georgia, 'Times New Roman', serif"
      font-size="52"
      font-weight="700"
      fill="#e8e3dc"
      letter-spacing="0.07em"
    >LLH</text>

    <!-- Subtext -->
    <text
      x="400" y="105"
      text-anchor="middle"
      font-family="Georgia, 'Times New Roman', serif"
      font-size="15"
      font-style="italic"
      fill="#918880"
    >music &amp; tools for making it</text>
  </svg>
  ```

- [ ] **Step 2: Open in browser and verify visually**

  Open `banner.svg` directly in a web browser (drag into browser or use `File > Open`).

  Check:
  - Background: deep red-black in the upper-left corner, fading to dark GitHub blue-black
  - Faint red glow emanating from top-center
  - "LLH" in serif, large, warm off-white
  - Italic subtext below: "music & tools for making it" in muted warm gray
  - A faint red hairline across the very bottom edge
  - No errors or broken rendering

- [ ] **Step 3: Commit**

  ```bash
  git add banner.svg
  git commit -m "feat: add SVG banner"
  ```

---

### Task 3: Write `README.md`

The README is a complete overwrite of the default stub. All color lives in the SVG. The body uses GitHub's default markdown rendering — no `<style>` tags.

**GitHub rendering rules that apply here:**

- `<table>`, `<tr>`, `<td valign>`, `<p align="center">`, `<img>`, `<br>`, `<strong>`, `<em>`, `<code>`, `<a>` all render
- Markdown headings/bold/italic/code-spans render inside `<td>` when surrounded by blank lines
- Fenced code blocks render (no language tag = no syntax highlighting)
- `---` renders as `<hr>`
- No `<style>`, no `<script>`

**Files:**

- Modify: `README.md`

- [ ] **Step 1: Overwrite `README.md` with the full content**

  Complete file content — copy exactly:

  ````markdown
  <p align="center">
    <img src="banner.svg" alt="LLH" width="100%" />
  </p>

  <table>
    <tr>
      <td width="50%" valign="top">

  ### Music

  [llhmusic.com](https://llhmusic.com)

  Artist site, discography, and releases. Electronic music released as LLH.

  `Eleventy · PostCSS`

      </td>
      <td width="4%"></td>
      <td width="50%" valign="top">

  ### Projects

  **Songwriter**

  Local workspace for writing lyrics to an instrumental. Phase-by-phase: brief → themes → structure → sections → export. Built because I kept abandoning songs halfway through.

  `Next.js · Anthropic · Gemini · SQLite`

  **Anchor**

  Day planner for low-energy, overwhelmed, or depressive states. Not productivity. Recovery.

  `React Native · Expo · Firebase`

      </td>

    </tr>
  </table>

  ---

  ### How it gets built

  **Architect + Builder.** Claude acts as the senior engineer — planning, authoring prompts, reviewing output. Cursor and Kilo Code act as the hands that execute. Every session follows a structured prompt template. No code gets merged without a self-critique pass.

  <table>
    <tr>
      <td valign="top" width="20%"><strong>01 — Ideation</strong></td>
      <td valign="top">Define scope, name the mode. Claude plans first — architecture, constraints, what not to touch.<br><code>Explore vs. production</code> &nbsp;·&nbsp; <code>Plan before generating</code></td>
    </tr>
    <tr>
      <td valign="top"><strong>02 — Prompt</strong></td>
      <td valign="top">Every prompt follows the 4-block template: Goal · Constraints · Context · What I want now. One module only.<br><code>4-block template</code> &nbsp;·&nbsp; <code>No scope creep</code></td>
    </tr>
    <tr>
      <td valign="top"><strong>03 — Execution</strong></td>
      <td valign="top">Claude owns the prompt and review. Cursor / Kilo Code executes within that scaffold.<br><code>Architect + Builder</code> &nbsp;·&nbsp; <code>Cursor · Kilo Code · Copilot</code></td>
    </tr>
    <tr>
      <td valign="top"><strong>04 — Gate</strong></td>
      <td valign="top">Force the model to critique its own output. Pass → merge. Fail → revise the prompt and repeat.<br><code>Self-critique</code> &nbsp;·&nbsp; <code>Clean rewrite over patch</code></td>
    </tr>
  </table>

  4-block prompt template

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

  — **Clean rewrites over patches** — if it's broken, rewrite the module, don't layer fixes on debt

  — **One module at a time** — scope stays locked until the current unit is done

  — **Name the mode before starting** — exploration (loose, iterative) vs. production (strict, reviewable)

  — **Force self-critique after generation** — the model reviews its own output before anything gets merged

  <p align="center">
  <strong>Stack —</strong> Next.js · React Native · Eleventy · SQLite · Firebase · TypeScript<br>
  <strong>Tooling —</strong> Claude · Cursor · Kilo Code · GitHub Copilot · Codex
  </p>

  ---

  <p align="center">

  _I don't write code. I describe what I want until something builds it._<br>
  _These are the things worth describing._

  </p>
  ````

- [ ] **Step 2: Spot-check the file**

  Run:

  ```bash
  head -5 README.md
  ```

  Expected: starts with `<p align="center">` (not the old `## Hi there 👋` stub).

- [ ] **Step 3: Commit**

  ```bash
  git add README.md
  git commit -m "feat: github profile README — LLH"
  ```

---

### Task 4: Push and verify

- [ ] **Step 1: Push to GitHub**

  ```bash
  git push
  ```

- [ ] **Step 2: Open GitHub profile in browser**

  Navigate to `https://github.com/lindhammer`.

  Check in order:
  1. Banner SVG renders — visual, no broken image icon
  2. "LLH" serif display text is visible
  3. Two-column Music / Projects layout is side-by-side (not stacked)
  4. Phase table rows are properly aligned (left label, right detail)
  5. Code block (4-block template) renders with monospace font, no syntax highlighting
  6. Em-dash principles lines appear as plain text paragraphs (not bullet lists)
  7. Footer is centered and italic
  8. No raw HTML visible (all table/img tags render correctly)

- [ ] **Step 3: Check both light and dark mode**

  GitHub has a theme toggle in settings. Switch to light mode and verify:
  - The SVG banner still looks intentional (it will be lighter, but the text "LLH" should still be readable)
  - No content is invisible due to color assumptions

  Switch back to preferred mode.

---

## Known Rendering Quirks

- **SVG grain filter**: The `feBlend` mode `overlay` may not apply in all SVG renderers, but this is cosmetic. The banner is designed to look correct without the grain.
- **Letter-spacing in SVG**: The `style="letter-spacing: 0.07em"` attribute on the `<text>` element uses CSS shorthand. If a renderer doesn't support this, the spacing will fall back to default — the text will still be legible.
- **Markdown inside `<td>`**: GitHub renders block markdown (headings, bold, code) inside `<td>` only when the content is separated from the `<td>` tag by blank lines. The template above includes these blank lines — do not collapse them.
- **The `width="4%"` spacer column**: This is a visual gutter between the two content columns. It renders as an empty cell. Some renderers may collapse it; if the columns appear too close, increase to `width="6%"`.


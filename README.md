<p align="center">
  <img src="banner.svg" alt="LLH" width="100%" />
</p>

<table><tr>
<td width="35%" valign="top">
<h3>Music</h3>
<p><a href="https://llhmusic.com">llhmusic.com</a></p>
<p>Artist site, discography, and releases. Electronic music released as LLH.</p>
<p><code>Eleventy · PostCSS</code></p>
</td>
<td width="65%" valign="top">
<h3>Projects</h3>
<p><strong>Songwriter</strong></p>
<p>Local workspace for writing lyrics to an instrumental. Phase-by-phase: brief → themes → structure → sections → export. Built because I kept abandoning songs halfway through.</p>
<p><code>Next.js · Anthropic · Gemini · SQLite</code></p>
<p><strong>Anchor</strong></p>
<p>Day planner for low-energy, overwhelmed, or depressive states. Not productivity. Recovery.</p>
<p><code>React Native · Expo · Firebase</code></p>
<p></p>
</td>
</tr></table>

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


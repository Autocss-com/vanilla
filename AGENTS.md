# AGENTS.md — Autocss-com/vanilla (project-specific ONLY)

**The canonical laws are NOT here.** They live in ONE file, once, for every project and
every AI vendor: **`Autocss-com/ai` → `AGENTS.md`** (Response Integrity Charter `C0`–`C8`
+ AutoCSS Architecture `1`–`15`). Never copy or restate them here.

**How they reach you:** clone the ai repo once and import it from your user-level memory —
then every repo on the machine gets them automatically, no per-repo file:

```bash
git clone https://github.com/Autocss-com/ai ~/.claude/ai
# ~/.claude/CLAUDE.md  ->  @~/.claude/ai/AGENTS.md
git -C ~/.claude/ai pull      # refresh the laws for ALL projects at once
```

**Conflict priority:** `Autocss-com/ai` AGENTS.md > this file > `.agents/SESSION-HANDOFF.md`.
On conflict, surface it to the user. **Never resolve silently.**

This file declares only what is TRUE OF THIS REPO and nothing else.

## What this repo is

The **vanilla marketing-site demo** of the AutoCSS remote-rendering phase — a real
ballet-studio site (**Étoile Ballet Studio**) served as the CURRENT AutoCSS architecture
**AS-IS** (no host CMS/framework), self-hosted as a static SPA on **GitHub Pages**. It is
the vanilla baseline the three framework reference demos (`react`/`vue`/`angular`) are
compared against. **Read-only:** the "API" is a folder of static JSON (`data/`), so there
is no backend for the read path.

**Custom domain — NOT wired yet.** The intended production home is **international.dance**,
but a live site still occupies that domain. Until this version is approved to replace it,
testing is via the plain GitHub Pages URL (`https://autocss-com.github.io/vanilla/`); there
is deliberately **no `CNAME` file** so Pages never claims the real domain.

## 9. Project Structure

```html
<app-container>
  <app-banner></app-banner>
  <header>
    <app-logo></app-logo>
    <!-- 3-state Light/Dark/System color-scheme control (radio group) -->
  </header>
  <nav><details open><summary></summary><section>
    <!-- 5 nav radios: home, classes, about, faculty, tuition -->
  </section></details></nav>
  <main><article>
    <h1></h1><p></p>
    <section></section> <section></section> <section></section> <section></section>
    <!-- 4 marketing content regions (layout only); empty ones hide via CSS -->
    <input type="search" name="filter">   <!-- Classes tab filter -->
    <ul aria-hidden="true"><li></li></ul>  <!-- table header row -->
    <ul></ul>                              <!-- table body rows -->
  </article></main>
  <aside><!-- DETAILS: row-click form (fieldset), read-only --></aside>
  <footer><app-legal></app-legal><app-version></app-version></footer>
  <app-banner></app-banner>
</app-container>
<template><!-- inert content-element pool: h1/h2/h3/p/blockquote + app-card + app-carousel --></template>
<script type="module" src="./assets/js/app.js"></script>
```

## 10. Files

- `index.html` — full DOM + the inert `<template>` content-element pool.
- `assets/css/*.css` — base AutoCSS layers (`reset`, `fonts`, `color-scheme`,
  `color-theme-66ccff`, `layout`, `inputs`, `media`, `typography`, `scrolling`, `a11y`,
  `forms`, `fallbacks`, `loading`) + marketing composites (`cards`, `carousel`, `gallery`,
  `contact`). One `@layer` per file; the `<link>` order in `index.html` IS the cascade.
- `assets/js/*.js` — the canonical five (`app`, `oninput`, `api`, `storage`, `tour`) plus
  the demo's data-shaping/rendering modules (`config`, `env`, `inject`, `profile`, `rules`,
  `schema`, `forms`, `utils`). `API_BASE_URL = "./data"`; `resolveEndpoint` appends `.json`.
- `data/*.json` — the static read-only "API": `shell`, `home`, `classes`, `about`,
  `faculty`, `tuition`.
- `test/*.mjs` — Playwright verify harnesses (`app`, `carousel`, `gallery`, `rowform`).
- `.nojekyll` — disables Jekyll processing (plain static site).
- **No `CNAME`** — intentional; the custom domain (`international.dance`) is not wired yet
  (see above). Testing is via `https://autocss-com.github.io/vanilla/`.

## Known divergences from canonical (surface, do not resolve silently)

Per the conflict rule above, these are flagged, not fixed here — they are AS-IS debt
tracked against the canonical `Autocss-com/ai`:

- **JS files exceed canonical §5's "five files."** The AS-IS port carries extra
  data-shaping modules (`config`/`env`/`inject`/`profile`/`rules`/`schema`/`forms`/`utils`).
- **State-machine markup uses `role="button"` / `aria-hidden` on labels/inputs**, which
  canonical §3 now forbids (it mandates keeping the `<input>` focusable, no `role="button"`,
  no `aria-hidden`). Reconcile when the demo is brought to full compliance.

## 13. Session Continuity

If a `.agents/SESSION-HANDOFF.md` exists, read it at session start and re-assert its
Constraint Lock before coding. If it conflicts with the canonical `ai` AGENTS.md, STOP and ask.

## 14. Routing — Which Skill Owns This Task

Skills are universal and live in `Autocss-com/ai`. Route each task to its skill there; if a
task touches more than one concern, do each part inside its own skill.

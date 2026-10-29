# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Single-page static HTML portfolio site for Santiago Miranda (Senior QA Analyst — API & Accessibility Testing). No build tooling, no package manager, no framework — `index.html` is the entire site: CSS lives in an inline `<style>` block, and a small vanilla `<script>` block at the end of `<body>` drives the background/typewriter effects (see Animations below).

This is a **portfolio**, not a CV mirror: it exists to show hiring managers how Santiago tests and what role he's after, not just where he worked. The CV (Onetree/Globant employers, metrics) grounds the content, but two sections go beyond it — `02. como_trabajo` (testing judgment/criteria, not a tool list) and `04. evidencia` (a sample defect report). Don't collapse the site back into a CV summary.

## Development

There is no build/lint/test tooling. To preview changes, just open `index.html` directly in a browser (or serve the folder with any static file server).

## Structure

- `index.html` — the entire site (markup, styles, scripts) in one file.
- `assets/avatar.jpg` — header avatar, also referenced by Open Graph/Twitter meta tags. **Not present in this folder yet** — the `<img>` and OG/Twitter `content` links will 404 until the real photo is copied to `assets/avatar.jpg` before publishing.
- `assets/Santiago-Miranda-Resume.pdf` — linked from the "Descargar CV" button (see the HTML comment right above that link). **Not present in this folder yet** — copy the real CV PDF to `assets/Santiago-Miranda-Resume.pdf` before publishing, or the download link 404s. Don't invent or stub this file; leave the href as-is until the real PDF is dropped in.

## Content notes

- Text content is in Spanish.
- Profile: Senior QA Analyst, API & Accessibility, ISTQB CTFL 4.0, WCAG A/AA/AAA, 5+ years experience. Current employer Onetree; before that four years at Globant (Stride Inc, Warner Bros). AI tools (Claude, Claude Code, Cursor, ChatGPT) are mentioned in "sobre_mi" as a way of working — do not list them as Automation chips next to Playwright.
- The "proyectos_destacados" section (`03. proyectos_destacados`) has four cards: CIMA (BID · Onetree), COE/COE Mobile unified (ACT · Onetree), KZN Fitness (Consertus · Onetree), Teachsuite/Big Universe (Stride Inc · Globant).
  - CIMA/ACT/KZN impact copy is intentionally kept qualitative (no per-project numbers) because the CV only gives aggregate Onetree metrics — those aggregate numbers (85%+ critical-flow regression coverage, ~30% less repro time, 150+ defects/quarter) live in the "sobre_mi" section instead. Don't attribute them to a single client, and don't invent numbers the CV doesn't state.
  - Each Onetree card has a distinct angle so they don't read as three copies of the same sentence: CIMA = traceability/reproducible evidence in an institutional context; COE/COE Mobile = cross-platform (web/mobile/data) consistency; KZN Fitness = API + data-integrity quality in a consumer subscription app. Keep that differentiation when editing.
  - The Stride card uses its own measured metrics from the CV (30% triage efficiency, ~40% fewer prod defects, <5% reopen rate, ~25% less manual regression time) — those stay as-is, don't touch.
- `04. evidencia` holds six small, fictional work samples in a `.evidence-grid` of `.project-card.evidence-item` cards, deliberately senior-level rather than entry-level QA tasks (no plain test case / risk matrix — those read as junior), ordered to read as a narrative arc: (1) a risk-based test strategy approach for a new product (week-1 mapping, prioritization, coverage decisions, "ready for release" criteria agreed with dev/PO), (2) a WCAG accessibility audit finding with criterion/impact/remediation, (3) a root-cause-analysis of an intermittent production bug (race condition between a webhook and a DB commit), (4) a Jira-style bug report ticket (summary/repro steps/expected-vs-actual/environment/severity) showing day-to-day report quality, (5) a Playwright fixture that seeds state via API + Page Object pattern (not clicking through the UI), and (6) a SQL query detecting orphaned records between two systems (web/mobile). The intro paragraph (`.evidence-note`) states plainly these are portfolio samples, not real client data. Keep future additions to this section at the same "shows judgment/depth" bar and preserve the strategy→finding→investigation→report→automation→verification order — never swap any of them for real client tickets/code, and don't regress to generic textbook QA artifacts (basic test case, simple risk list).
- `02. como_trabajo` covers testing judgment (prioritization by risk, what makes a bug report good, when to automate vs. not, how AI fits in, and — a 5th block, `principle-block--wide`, spanning the full grid width — process ownership: being the informal QA↔dev/PO technical reference, having authored the team's bug-report standard and test-plan/onboarding documentation) in first person — it's criteria, not a second tools/skills list. The AI line here intentionally doesn't re-list tool names; those already appear once in `01. sobre_mi`. Santiago has no CI/CD pipeline experience — don't add claims about it.
- Section numbering is `01. sobre_mi` → `02. como_trabajo` → `03. proyectos_destacados` → `04. evidencia` → `05. stack_&_certs`. Keep the `NN.` prefixes in sync if sections are reordered.
- `og:url` meta tag contains a `REEMPLAZAR-URL-DEL-SITIO` placeholder — replace with the real domain when the site is deployed, and switch `og:image`/`twitter:image` to absolute URLs at the same time.
- `05. stack_&_certs` gives each stack group (Testing/Automation/Tools) a one-line `.stack-group-note` under the group title, so the chip lists don't read as a bare skills dump — connect it to actual usage, don't just restate the chips.
- No testimonial/recommendation quote section exists on purpose — Santiago doesn't have one lined up yet. Don't add a placeholder or invented quote; only add this if he supplies a real one.

## Animations

All in the inline `<style>`/`<script>` blocks, no dependencies, and all respect `prefers-reduced-motion: reduce`:

- Scroll-reveal fade/slide-in via `.reveal` + `IntersectionObserver` (header, sections, project cards).
- Background: panning grid (`grid-pan`), three drifting/hue-rotating aurora blobs (`.bg-glow`), and randomly-generated rising particles (`.bg-particles`, populated in JS).
- Statusbar path (`#typewriter`) cycles through `santiago-miranda` / `senior_qa_analyst` / `istqb_ctfl` with a letter-by-letter type/delete loop; first word holds longer (8s) than the others (5s).
- Small hover/idle details: status-dot pulse, role-pill sheen sweep, project-card top-border grow-on-hover.

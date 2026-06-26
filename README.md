# Handoff: Enterprise Operating System — Cinematic Narrative Deck

## Overview
A full-screen, 22-slide cinematic presentation that tells the story of the "Enterprise
Operating System" — a vision of the company as a living, cognitive system driven by AI
agents — and closes with a **live SEM demo** section and a real product showcase
(MazingerOS + TwinVerse). It is built as a single self-contained slide deck (1920×1080
design size) with animated `<canvas>` scenes behind every slide, a typed-terminal eyebrow
treatment, live-updating telemetry, and count-up metrics.

The deck is in Spanish/English mix (the narrative spine is in English; the Demo section is
in Spanish, matching the audience).

## About the Design Files
The files in this bundle are **design references created in HTML** — a working prototype
showing the intended look, motion, and behavior. They are **not** production code to copy
verbatim. The task is to **recreate this design in the target codebase's environment**
(React/Vue/Svelte/etc.) using its established patterns, or — if there is no existing app —
to pick the most appropriate framework and rebuild it there.

> ⚠️ The main deck is authored as a "Design Component" (`.dc.html`). It depends on a custom
> runtime (`support.js`) and a slide-shell web component (`deck-stage.js`). Those are
> prototype scaffolding. When rebuilding, replace the DC runtime with your framework's
> component model and replace `deck-stage` with your own slide/scroll controller (or a
> library like Reveal.js / Swiper). Keep the **visual system, canvas scenes, copy, and
> motion** — drop the DC plumbing.

## Fidelity
**High-fidelity (hifi).** Final colors, typography, spacing, copy, motion timings, and
canvas animations are all here and should be reproduced faithfully. Exact values are
documented below; where in doubt, read the source.

## Tech / Structure at a glance
- **Design size:** 1920 × 1080, scaled to fit viewport by `deck-stage`. All coordinates in
  the source are authored in this 1920×1080 space (absolute positioning).
- **One file, many slides:** each slide is a `<section data-label … data-screen-label …
  data-speaker-notes …>` inside the `<deck-stage>` element.
- **Per-slide canvas scene:** every section contains `<canvas class="scene"
  data-scene="…">`. A single JS controller (`class Component`) drives the active slide's
  scene via `requestAnimationFrame`, switching on `slidechange` events.
- **Reveals & typing:** elements with `.reveal` fade/slide in on a `data-delay` (ms);
  elements with `.type-line` are typed out terminal-style (also `data-delay`, optional
  `data-cursor="1"` to keep a blinking caret).
- **Telemetry:** a small mono status line is injected at the bottom-left of each slide from
  a `this.telemetry` array (indexed by slide order). Some tokens live-update
  (`tel-tasks`, `tel-ctx`).

## Design Tokens

### Deck (primary narrative)
| Token | Value | Use |
|---|---|---|
| Background | `#050505` (and `#000000` on the final "Online" slide) | slide bg |
| Ink / foreground | `#F4F6F8` | primary text |
| Accent — Soft Cyan (default) | `#74d4cb` / `rgba(122,212,203,…)` | highlights, dots, arrows |
| Accent alt — Emerald | `#5fc79a` / `rgba(96,196,150,…)` | finance/positive flows |
| Accent alt — Electric Blue | `rgb(61,139,255)` | ambient particles |
| Hairline / dim text | `rgba(255,255,255,0.3)` → `0.13` | mono labels, borders, corners |
| Muted body | `rgba(255,255,255,0.4–0.55)` | secondary lines |

The accent is themeable via a deck prop `primaryAccent` ∈ {Soft Cyan, Emerald, Electric
Blue}; a `calm` boolean reduces motion intensity. Default = Soft Cyan, calm = false.

### Typography
- **Display:** `Space Grotesk`, weights 300 / 400 / 500. Headlines use weight **300** with
  `letter-spacing: -0.01em` to `-0.02em`. Sizes range 44–94px on titles, 24–40px on subs.
- **Mono:** `JetBrains Mono`, weights 400 / 500. Used for all eyebrows, telemetry, metrics,
  step numbers, and "SYS://…" labels. Letter-spacing 0.14em–0.52em; sizes 24–30px.
- Load: `https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=JetBrains+Mono:wght@300;400;500;600&display=swap`

### Recurring chrome (on every slide)
- **Corner brackets:** four 26×26px L-shaped marks inset 38px from each corner, border
  `1px solid rgba(255,255,255,0.13)`.
- **Top-left eyebrow:** a glowing 8px cyan dot + `MONO://LABEL` in mono, `rgba(255,255,255,0.3)`,
  letter-spacing 0.34em, at top:56px left:66px.
- **Top-right act label:** e.g. `ACT II — THE NERVOUS SYSTEM`, mono `rgba(255,255,255,0.26)`,
  top:56px right:66px.
- **Bottom-left telemetry:** injected mono status tokens, font 24px, gap 28px, bottom:52px
  left:66px.

## Screens / Views (slide order)

The narrative is structured in **Acts**. Each slide = one `<section>`; the `data-label`
(thumbnail) and `data-screen-label` (01–22) are noted. Full speaker notes are in each
section's `data-speaker-notes`.

**ACT I — AWAKENING**
1. `01 Invisible` — "Every company already has thousands of processes. / Most of them are invisible." Centered hero. Scene: ambient particles.
2. `02 Awakes` — "Every company already has a nervous system. / It just doesn't know it." Scene: network of nodes lighting + connecting.
3. `03 Orchestrator` — "ENTERPRISE ORCHESTRATOR / One intelligence. Thousands of decisions." Scene: network converging to one core.
4. `04 Agents` — "Specialized intelligence." Scene: core emitting beams to agent nodes.

**ACT II — THE NERVOUS SYSTEM**
5. `05 A Day` — "A day inside a cognitive company." → "Nobody coordinated this. The Enterprise OS did." Scene: signal traveling a pipeline.
6. `06 Marketing` — "Marketing never sleeps." Scene: flow with live counters (visitors→qualified→meetings).
7. `07 Finance` — "Finance as an autonomous system." → "No humans, unless judgment is required." Scene: invoice flow (emerald accent).
8. `08 Digital Twin` — "The company can finally see tomorrow." Scene: galaxy.
9. `09 Nervous System` — "The enterprise nervous system." → "Thousands of invisible events, every hour." Scene: complaint→deployment flow.

**ACT III — THE COGNITIVE ENTERPRISE**
10. `10 Cognitive Mirror` — 9 floating mission-control metrics that live-update (Revenue, Predicted Revenue, Confidence, Inventory Risk, Hiring, Marketing ROI, Cash Flow, Customer Sentiment). IDs `m-rev … m-sent`.
11. `11 Time` — "Time becomes the new KPI." Four before→after rows (3 Days→6 Minutes, etc.) → "The real ROI is time."

**ACT IV — THE REALITY LAYER**
12. `12 Accessing` — Terminal boot sequence ("ACCESSING LIVE SYSTEMS… ACCESS GRANTED…") revealing two case files.
13. `13 Two Brains` — "Should we enter Brazil?" routes to MazingerOS (execute today) + TwinVerse (predict tomorrow). "Two organs. One operating system."
14. `14 MazingerOS` — Case file 01: full pipeline (Human→WhatsApp→Orchestrator→Model Router→Agents→Tools→Approval→Output), live agent/integration chips, and a live "OUTPUT STREAM" event log (`#maz-events`).
15. `15 TwinVerse` — Case file 02. **Heading uses the real TwinVerse logo image** (see Assets) in place of the wordmark text, followed by "PREDICTIVE BRAIN" + the Reactive/Proactive/Predictive comparison.
16. `16 Foresight` — TwinVerse splits into Engine A (synthetic society) + Engine B (quantitative prediction) → "87% DECISION CONFIDENCE".
17. `17 Evolution` — 7-stage maturity curve (Manual work → Living companies), "MazingerOS + TwinVerse · TODAY" marker.

**ACT V — THE HORIZON**
18. `18 Alive` — "Every company will have two brains. / One to execute. One to predict."
19. `19 Online` — `#000000` bg. "Enterprise Operating System / ONLINE / The company is awake."

**ACT VI — LIVE DEMO** *(added section — Spanish, audience-facing)*
20. `20 Demo` — Centered hero: eyebrow "DEMO EN VIVO", headline **"SEM con agentes, en directo."**, sub "Una campaña de Google Ads real, sobre una web sin preparar, montada por un agente mientras la audiencia mira.", and 3 chips: `web real · umbratech.es`, `sin preparación`, `un comando`. Scene: cyan ambient.
21. `21 Pasos` — Eyebrow "EL AGENTE, PASO A PASO" + title "Cinco pasos, en segundos." Five numbered rows (01 Lee la web · 02 Investiga keywords y competencia · 03 Escribe los anuncios · 04 Estructura la campaña · 05 Exporta el CSV), each with a mono sub-caption. **Discreet link bottom-right:** "VER GUÍA · CÓMO SE HACE →" → opens `guide-how-its-done.html` in a new tab. Styled to match telemetry (mono 24px, `rgba(255,255,255,0.34)`, cyan arrow, hover → cyan).
22. `22 Outcome` — Eyebrow "OUTCOME · EL ROI ES TIEMPO". "≈ 18 h → **320×** más rápido" with the **320 number animating up (count-up)** on slide-enter (`#demo-bignum`, ~1.7s ease-out cubic). Sub "≈ 18 h hombre → ≈ 3,4 min reales" and kicker "El ROI no se mide en dinero. **Se mide en tiempo.**" Scene: blue ambient.

## Interactions & Behavior
- **Navigation:** arrow keys / on-screen via `deck-stage`; programmatic `deckStage.goTo(n)`
  (0-indexed). Mobile portrait rotates the stage 90° (see the `fit()` script in `<helmet>`).
- **Reveals:** opacity 0→1 + slight translate, `data-delay` ms after slide activates,
  ~1100ms smoothstep. Respect `prefers-reduced-motion` (jump to final state).
- **Typing:** `.type-line` types ~0.028 chars/ms; `data-cursor="1"` keeps a caret.
- **Canvas scenes:** continuous rAF while the slide is active; ambient dust layer behind
  every scene; intensity scales with slide index ("aliveFactor") so the deck "wakes up" as
  it progresses.
- **Live metrics (slide 10):** updated every 1500ms with bounded random walk; sentiment
  word cycles. Telemetry `tel-tasks` counts up, `tel-ctx` jitters 90–97%.
- **MazingerOS stream (slide 14):** prepends a new timestamped event every 1500ms, keeps
  last 4 with fading opacity.
- **Demo count-up (slide 22):** triggers on activate, animates 0→320, holds at 320; skips
  to 320 under reduced motion.
- **Guide link (slide 21):** `target="_blank"` to a separate standalone HTML guide.

## State Management (what a rebuild needs)
- `currentSlide` index → drives which scene animates, which reveals/typing run, which
  telemetry shows.
- Per-scene state objects (cached so scenes resume cleanly).
- Timers: one rAF loop, one 1500ms metric/telemetry interval.
- Reduced-motion flag.
- Theme props: `primaryAccent` (enum), `calm` (boolean).

## Assets
- `assets/twinverse-wordmark.png` — the **real TwinVerse wordmark** (1275×235, transparent
  background). Cropped from a user-supplied brand lockup (PNG) and keyed to transparency;
  used on slide 15. Orange-glitch "TwinVerse" lettering. If your app has the original
  vector/brand asset, prefer that. Brand accent in the logo is orange `~#EA3C00`.
- `guide-how-its-done.html` — the standalone **how-to guide** the slide-21 link points
  to. Different visual system (orange `#EA3C00` accent, Space Grotesk + Inter + JetBrains
  Mono). Self-contained; treat as a separate page.
- `reference_sem-demo-standalone.html` — the original standalone 3-panel SEM demo this
  Act VI section was adapted from (for reference only; the deck version is canonical).
- Fonts: Google Fonts (Space Grotesk, JetBrains Mono; the guide also uses Inter).
- No icon library — all marks are CSS/canvas. No emoji.

## Files in this bundle
- `Enterprise Operating System.dc.html` — **the deck** (all 22 slides + the JS controller
  with every canvas scene). Primary source of truth.
- `support.js` — DC runtime (prototype scaffolding; replace in production).
- `deck-stage.js` — slide-shell web component: scaling, keyboard nav, thumbnails, speaker
  notes, print (prototype scaffolding; replace with your slide controller).
- `assets/twinverse-wordmark.png` — TwinVerse logo (slide 15).
- `guide-how-its-done.html` — linked how-to guide (slide 21).
- `reference_sem-demo-standalone.html` — original SEM demo reference.

## How to run the prototype
Open `Enterprise Operating System.dc.html` in a browser (it loads `support.js` and
`deck-stage.js` from the same folder). Use arrow keys to navigate. The slide-21 "VER GUÍA"
link opens `guide-how-its-done.html`.

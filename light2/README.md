# Enterprise OS — Light2 version

A second, alternative "light" deck (Claude Design build) — a 9-slide,
startup-focused re-cut (MazingerOS framing, no TwinVerse). Lives in its own
folder so it sits **alongside** the full deck and the first light version;
none of the others are touched.

- Full deck:   `https://mchuecaw.github.io/enterprise-os-deck/`
- Light deck:  `https://mchuecaw.github.io/enterprise-os-deck/light/`
- Light2 deck: `https://mchuecaw.github.io/enterprise-os-deck/light2/`

## Live demo timer (slide 9 · Outcome)

Same fix applied as in the first light version: the **"× faster"** number now
recalculates live while the clock runs as `18 man-hours ÷ elapsed real time`,
counting down toward ~**320×** at ~3.4 real minutes, and back to `320` on
Reset. Start / Stop / Reset all work.

## Files

- `index.html` — the deck (`.dc.html` renamed to index for Pages).
- `support.js`, `deck-stage.js` — prototype slide runtimes (loaded relatively).
- `guia-sem-como-se-hace.html` — the SEM "how it's done" guide linked from slide 8.

Like the full deck, the slide runtime loads React from unpkg.com at view time.

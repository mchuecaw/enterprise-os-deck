# Enterprise OS — Light version

A simpler, no-frills variant of the deck (built from Claude Design), kept in
its own folder so it lives **alongside** the full deck — the original is not
touched or removed.

- Full deck:  `https://mchuecaw.github.io/enterprise-os-deck/`
- Light deck: `https://mchuecaw.github.io/enterprise-os-deck/light/`

## Live demo timer

The "Outcome" slide reuses the same live timer as the full deck:

- **Start / Stop / Reset** buttons.
- The big **"× faster"** number recalculates live while the clock runs as
  `18 man-hours ÷ elapsed real time` — so it counts down toward ~**320×** at
  ~3.4 real minutes, and back to `320` on Reset.

`index.html` is a single self-contained file (assets are inlined). Like the
full deck, the slide runtime loads React from unpkg.com at view time.

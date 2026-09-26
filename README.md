# cyPollock

**A seed-based generative system for scattered recursive branch compositions.**

A catalogue of computational textile compositions for fashion, textile and surface design — algorithmically drawn, seed-documented, and ready for production.

---

## Overview

cyPollock is a generative design system rather than a single artwork. Each composition is built from a set of recursive branches, scattered freely across the frame — every branch grows in any direction, every branch forks on its own schedule, every branch carries its own colour from a palette of sixty-eight tones.

Where Celestial Grove grows a quiet grove from the ground upward, cyPollock scatters its branches in every direction — a cybernetic Pollock, dripped from a point into a field.

The system is designed for:

- **Fashion houses** adapting gestural ornament for apparel and accessories
- **Textile studios** developing repeat patterns and yardage
- **Surface designers** working across print, wallpaper, and interior applications

Every composition can be licensed, adapted, or commissioned to a brief.

---

## Concept

A gesture, when it is *computed* rather than performed, becomes a field — turbulent, calm, quietly yours.

The gestural mark — irregular, energetic, endlessly variable — has always carried the trace of a body in motion. From the brushstrokes of the Abstract Expressionists to the woven patterns of tribal rugs, the loose scattered mark is one of the oldest forms of expression we have. cyPollock translates that gesture into code. Each composition begins with a set of anchors and unfolds through recursion, rotation, and scale until the frame fills with a turbulent field of branches.

The palette, the branch count, and the background are all derived from a single numeric seed.

Like the other still volumes in this series (Girih, Arachne, Celestial Grove, ChaotiColor, Citrus Mosaic, Crazy Knight Curve, Crazy Knight Line, Crazy Letter), **cyPollock is a static composition.** The plate, the framed plate, the surfaces, and the archive are all static frames. A gesture field is something you read; its character is stillness, not motion.

---

## Features

- **Seed-based generation** — every composition is defined by a numeric seed and can be regenerated exactly
- **Deterministic output** — the same seed always produces the same composition
- **Scattered recursive branches** — every branch grows in any direction, with a full-π angle range at each step
- **Sixty-eight colour palette** — vivid tones (whites, blues, greens, warm colours) plus a full set of dark tones
- **22 dark background tones** — from deep maroon through midnight, plum, and forest greens
- **Adaptive branch count** — 10 to 60 branches per composition, derived from the seed
- **Adaptive surfaces** — one seed applied across print, scarf, textile, and wall formats
- **Archive** — eight curated seeds available for immediate loading
- **Download** — export the composition as a high-resolution PNG
- **Keyboard shortcuts** — `R` for new seed, `S` to save

---

## Project Structure

```
.
├── index.html          # Main catalogue page
├── images/
│   ├── fav.svg         # Favicon
│   ├── tote.png        # Mockup: tote bag
│   ├── tee.png         # Mockup: t-shirt
│   └── cushion.png     # Mockup: cushion
└── README.md
```

---

## How It Works

### The Seed

A numeric seed (a large integer) initializes a deterministic pseudo-random generator. From this seed, the system derives:

- Background colour (from a palette of 22 dark tones)
- Branch count (10–60)
- Per-branch colour (from a palette of 68 tones)
- Branch geometry (angles, scaling, fork schedule)

Because the generator is deterministic, the same seed always produces the same composition — on any device, at any time.

### The Branches

Each branch is drawn recursively, like a tree limb:

1. A short stroke is drawn from the current position, upward and slightly compressed.
2. The system then moves forward, rotates by a random angle, and either:
   - **Forks** into two sub-branches, each rotated away from the parent, or
   - **Continues** as a single branch.
3. The recursion stops at a fixed depth (13 steps).

The key difference from Celestial Grove is the **angle range**. Where Celestial Grove constrains branch angles to a narrow upward wedge (so trees grow from the ground), cyPollock allows a **full π range** — the branch can turn in any direction. This means branches wander freely across the frame, crossing and overlapping like brushstrokes.

### The Colours

The palette is intentionally wide:

- **68 branch colours** — spanning from bright whites and pale blues, through vivid greens and yellows, through warm reds and oranges, all the way to deep maroons, plums, and forest greens.
- **22 background tones** — deep, dark, and saturated: maroon, midnight, black-blue, night-blue, deep teal, gunmetal, forest green, purple, chocolate, and more.

Where the bright branches meet the dark background, the composition reads as a luminous field — like a night sky with sparks scattered across it.

### The Surfaces

The same seed is rendered across four surface formats. These are static frames — they represent the print-ready composition.

| Surface  | Aspect | Material          |
|----------|--------|-------------------|
| Print    | 1 : 1  | Cotton rag        |
| Scarf    | 3 : 1  | Twill silk        |
| Textile  | 4 : 3  | Fabric yardage    |
| Wall     | 2 : 3  | Wallpaper         |

Each surface uses the same underlying seed and structural logic — only the repeat, orientation, and scale change.

### Stillness

Like the rest of the still volumes, cyPollock does not animate. The plate is a single frozen frame — the composition is complete the moment it is generated.

This is a deliberate design choice. A gesture field is not a swarm. It is not a rotation. It is a stack of strokes, drawn once and left. Its stillness is what makes it print-ready in the strictest sense: what you see is what you get.

---

## Usage

### In the browser

1. Open `index.html` in any modern browser.
2. Click **New Seed** to generate a new composition.
3. Click **Download** to save the composition as a PNG.
4. Scroll to the **Archive** section and click any plate to load it into Plate 001.

### Keyboard shortcuts

| Key | Action          |
|-----|-----------------|
| `R` | New seed        |
| `S` | Save as PNG     |

### Reproducing a composition

Each composition is identified by an 8-digit seed label displayed in the metadata panel. To reproduce a specific composition, note the seed and regenerate it programmatically:

```js
const rng = new RandomGenerator(seed);
const features = buildFeatures(rng);
renderComposition(canvas, features, rng);
```

Because the generator is deterministic, this will produce the identical composition on any device.

---

## Technical Notes

- **No build step.** The system is a single HTML file with inline CSS and JavaScript.
- **No dependencies.** All drawing is done with the native Canvas 2D API.
- **Deterministic.** The `RandomGenerator` class uses a xorshift-based PRNG seeded by an integer, so identical seeds produce identical outputs.
- **Static rendering.** Every canvas renders a single frame. There is no animation loop.
- **Feature isolation.** Cover, framed plate, surfaces, and archive thumbnails each derive their own feature set from their own local RNG, without disturbing the main plate's state.
- **Bounded recursion.** The branch recursion has a hard depth limit of 13, preventing stack overflow even with 60 branches.
- **Full-angle scatter.** Unlike Celestial Grove, the branch angles are drawn from the full π range — this is what gives cyPollock its turbulent, gestural character.
- **Responsive.** The layout adapts from large desktop down to very small mobile devices (tested at 360px viewport width).
- **Accessible.** Supports `prefers-reduced-motion`. Pinch-zoom is enabled.

### Browser support

Tested in current versions of:

- Chrome / Edge
- Firefox
- Safari (desktop and iOS)

---

## Difference from Celestial Grove

cyPollock and Celestial Grove share the same recursive tree-drawing logic, but differ in three important ways:

| Aspect      | Celestial Grove          | cyPollock                        |
|-------------|--------------------------|----------------------------------|
| Anchor      | Bottom of the frame      | Random point in the frame        |
| Angle range | Narrow upward wedge      | Full π (any direction)           |
| Character   | Quiet grove, moonlit     | Turbulent gesture, night-lit     |
| Palette     | Warm and lunar           | Dark backgrounds, vivid branches |

The result: Celestial Grove reads as a forest under a night sky; cyPollock reads as sparks in the dark — a field of gesture rather than a grove of trees.

---

## Licensing

All cyPollock compositions are **seed-documented** and available for licensing across textile, surface, and print applications.

- **Standard licenses** cover single-product production runs.
- **Commercial use, custom editions, or exclusive rights** are available on request.

Each license is issued against a specific seed ID. Regeneration of the same seed produces the identical composition — ensuring reproducibility between artist, studio, and manufacturer.

For licensing enquiries: [reyhanehdaneshdoost@gmail.com](mailto:reyhanehdaneshdoost@gmail.com)

---

## Commission

cyPollock is a generative design system, not a fixed artwork. It can be adapted for specific briefs:

| Service     | Description                                                       |
|-------------|-------------------------------------------------------------------|
| Licensing   | Existing seeds from the archive, licensed for production use      |
| Commission  | New compositions designed to your palette, repeat, and product    |
| Systems     | A private generative tool built for your studio's ongoing use     |

To begin a conversation: [reyhanehdaneshdoost@gmail.com](mailto:reyhanehdaneshdoost@gmail.com)

---

## Series

cyPollock is part of a computational textile series. Each volume approaches ornament from a different structural angle:

| Volume                | Structure                    | Motion                     |
|-----------------------|------------------------------|----------------------------|
| Girih 1               | Islamic geometric            | Static                     |
| Arachne               | Rotating rings               | Static                     |
| Baroque Me Baby       | Baroque frames               | Static                     |
| Bezier 1              | Concentric curves            | Static                     |
| Bezier 2              | Single rotating curve        | Animated (plate)           |
| Brownian Graphe       | Graph networks               | Animated + interactive     |
| Celestial Grove       | Recursive branch trees       | Static                     |
| ChaotiColor           | Cellular automata            | Static                     |
| Citrus Mosaic         | Arc-and-triangle tiles       | Static                     |
| Crazy Knight Curve    | Knight's-tour smooth path    | Static                     |
| Crazy Knight Line     | Knight's-tour gradient       | Static                     |
| Crazy Letter          | Framed wavy lines            | Static                     |
| **cyPollock**         | **Scattered branch field**   | **Static**                 |

The series is designed as a coherent whole — same page structure, same seed logic, same licensing and commission terms — so that each volume can be presented individually or as part of a larger body of work.

---

## Credits

- **Design & Generative System** — Reyhaneh Daneshdoost
- **Typefaces** — Cormorant Garamond · DM Mono
- **Platform** — Reyrove Studio
- **Edition** — cyPollock, Autumn 2026

### On AI tools

Where technical obstacles were encountered, AI tools were used for debugging and code optimization. Every structural, aesthetic, and conceptual decision remained the artist's own.

---

## Links

- Website — [reyrove.github.io](https://reyrove.github.io/)
- Instagram — [@rey._.rove](https://www.instagram.com/rey._.rove/)
- LinkedIn — [Reyhaneh Daneshdoost](https://www.linkedin.com/in/reyhaneh-daneshdoost-730481160/)
- X — [@reyrove](https://x.com/reyrove)

---

© cyPollock · All compositions reproducible by seed · Computational Textile Design
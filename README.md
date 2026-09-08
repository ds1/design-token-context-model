# Design Token Context Model
### Draft 0.1 January 20, 2026

> **The theory has moved.** The specification, the coordinate-system thesis, and the companion pages now live in [`gitfig-community/single-source-of-taste`](https://github.com/ds1/gitfig-community/blob/main/single-source-of-taste/README.md), together with the Single Source of Taste sequence that grew out of them. The wiki pages here are pointers. This repository remains the home of the [token collections](tokens/) that project the ontology into Figma, and of the [archive](archive/) of working drafts.

Exploration of a robust specification for multi-dimensional design token resolution with full Figma Variables support.

## The Problem

Design tokens have become foundational infrastructure for scalable design systems. The industry has converged on a tiered abstraction model—primitives, options, decisions, components, instances—but **context-awareness remains fragmented**.

Current systems treat context as flat modes (`light`/`dark`, `desktop`/`mobile`) rather than as a **multidimensional coordinate system** with inheritance, intersection, and resolution rules. When a button needs to resolve its background color, the answer depends on:

- Color scheme preference (light, dark, high-contrast)
- Density mode (compact, comfortable, spacious)
- Interaction state (rest, hover, active, disabled)
- Accessibility requirements (forced colors, reduced motion)
- Platform capabilities (color gamut, touch input)
- Locale considerations (RTL, text expansion)
- Container context (available space, scroll position)
- And dozens more dimensions...

**This project provides the missing specification.**

## What's Included

### [Specification](https://github.com/ds1/gitfig-community/blob/main/single-source-of-taste/05-design-token-context-ontology-specification.md)

The complete specification defining:

| Aspect | Description |
|--------|-------------|
| **12 Context Categories** | Appearance, Density, Viewport, Container, Interaction States, Combinable States, Accessibility, Locale, Platform, Elevation, Semantic, Structural |
| **93 Dimensions** | Complete enumeration with values, volatility class, and detection mechanism |
| **5 Volatility Classes** | Immutable → Stable → Semi-stable → Volatile → Inherited |
| **78 Cross-Category Dependencies** | Documented relationships requiring coordination |
| **52 Conflict Scenarios** | Resolution rules for dimension intersections |
| **Named Context Types** | Governed shortcuts for common patterns (mobile-dark, kiosk, print) |
| **Resolution Algorithm** | Explicit precedence ordering for token resolution |

### [Token Collections](tokens/)

W3C Design Tokens format implementation with 10 collections (~2,750 tokens):

```
tokens/
├── collections/
│   ├── primitives.json  # Raw color palette (blue-500, gray-200, etc.)
│   ├── theme.json       # Light / Dark / Dim color schemes
│   ├── density.json     # Compact / Comfortable / Spacious spacing
│   ├── viewport.json    # Mobile / Tablet / Desktop layouts
│   ├── contrast.json    # Standard / High / Forced accessibility
│   ├── motion.json      # Full / Reduced / None animations
│   ├── elevation.json   # Base / Raised / Elevated surfaces
│   ├── typography.json  # Default / Editorial / Technical styles
│   ├── state.json       # Rest / Hover / Active / Disabled states
│   └── brand.json       # Primary / Secondary / Partner identities
└── manifest.json        # Collection metadata & GitFig mappings
```

### Additional Documentation

The theory pages, in reading order, in their canonical home:

- [Token Systems Should Adopt CSS's Model](https://github.com/ds1/gitfig-community/blob/main/single-source-of-taste/01-token-systems-should-adopt-the-css-model.md) — Why flat modes explode combinatorially and what CSS already solved
- [Context as Coordinate System](https://github.com/ds1/gitfig-community/blob/main/single-source-of-taste/02-context-as-coordinate-system.md) — Foundational argument that tokens are policies mapping context coordinates to values
- [Coordinate Model and the Three-Tier Taxonomy](https://github.com/ds1/gitfig-community/blob/main/single-source-of-taste/03-coordinate-model-and-the-three-tier-taxonomy.md) — How the coordinate model fits within the standard 3-tier token taxonomy
- [Design Token Context Ontology](https://github.com/ds1/gitfig-community/blob/main/single-source-of-taste/04-design-token-context-ontology.md) — Overview of the ontology (this README, as published)
- [Design Token Context Ontology: Specification](https://github.com/ds1/gitfig-community/blob/main/single-source-of-taste/05-design-token-context-ontology-specification.md) — The full specification: 12 categories, 93 dimensions, resolution algorithm
- [The Single Source of Taste](https://github.com/ds1/gitfig-community/blob/main/single-source-of-taste/06-the-single-source-of-taste.md) — Aesthetic intent as a policy class with a `judged` validation regime and a single design authority
- [Carrying Judged Policies Through Figma](https://github.com/ds1/gitfig-community/blob/main/single-source-of-taste/07-carrying-judged-policies-through-figma.md) — How taste metadata survives the Figma round-trip
- [Compound Conditions Beyond Figma](https://github.com/ds1/gitfig-community/blob/main/single-source-of-taste/08-compound-conditions-beyond-figma.md) — The structural residue Figma cannot represent and a code-resident resolver for it
- [Glossary](https://github.com/ds1/gitfig-community/blob/main/single-source-of-taste/GLOSSARY.md) — Every term across the pages

Supporting material:

- [Coordinate Model Working Notes](https://github.com/ds1/gitfig-community/blob/main/single-source-of-taste/appendix/coordinate-model-working-notes.md) — Application of embodied AI principles to design tokens (the notes behind the thesis)
- [Design Tokens for Embodied AI](https://github.com/ds1/gitfig-community/blob/main/single-source-of-taste/appendix/design-tokens-for-embodied-ai.md) — Theoretical bridge between UI design tokens and AI/robotics representations
- [Design Systems: Single Source of Truth](archive/Design%20Systems_%20Single%20Source%20of%20Truth.md) — Analysis of SSOT architecture and data normalization principles (archived research report)

The `archive/` folder keeps the original working drafts for history; the copies under `gitfig-community/single-source-of-taste` are canonical.

## Collections Overview

| Collection | Modes | Purpose |
|------------|-------|---------|
| **Primitives** | — | Raw color palette: 22 scales (gray→rose) × 11 steps (50-950) |
| **Theme** | light, dark, dim | Color schemes with surfaces, foregrounds, borders, status colors |
| **Density** | compact, comfortable, spacious | Spacing, sizing, touch targets, component dimensions |
| **Viewport** | mobile, tablet, desktop | Responsive layouts, grids, breakpoints, navigation patterns |
| **Contrast** | standard, high, forced | Accessibility colors, focus rings, border widths |
| **Motion** | full, reduced, none | Durations, easings, animations, scroll behaviors |
| **Elevation** | base, raised, elevated | Shadows, z-indices, glass effects, surface treatments |
| **Typography** | default, editorial, technical | Font families, text styles, line heights, spacing |
| **State** | rest, hover, active, disabled | Interaction states for buttons, inputs, links, cards |
| **Brand** | primary, secondary, partner | Brand colors, gradients, radii, typography per brand |

## Architecture

Each collection represents an **independent context dimension** with its own modes:

```
┌──────────────────────────────────────────────────────────────────────────┐
│  Collection: Theme                                                       │
│  Modes: [light, dark, dim]                                               │
│  Detection: prefers-color-scheme, user preference                        │
├──────────────────────────────────────────────────────────────────────────┤
│  Collection: Density                                                     │
│  Modes: [compact, comfortable, spacious]                                 │
│  Detection: pointer type, user preference                                │
├──────────────────────────────────────────────────────────────────────────┤
│  Collection: Viewport                                                    │
│  Modes: [mobile, tablet, desktop]                                        │
│  Detection: viewport width, container queries                            │
├──────────────────────────────────────────────────────────────────────────┤
│  ...additional collections...                                            │
└──────────────────────────────────────────────────────────────────────────┘

Each token has explicit values for ALL modes in its collection:

{
  "surface.default": {
    "$type": "color",
    "$value": "#ffffff",
    "$extensions": {
      "mode": {
        "light": "#ffffff",
        "dark": "#0a0a0a",
        "dim": "#1a1a1a"
      }
    }
  }
}
```

## Quick Start

### Import to Figma with GitFig

1. Install the [GitFig](https://www.figma.com/community/plugin/1584467274034932618) plugin in Figma and connect a repository containing the `tokens/` folder
2. In GitFig's **Mapping** section, add a Variables target for each collection file, using the collection name from `manifest.json`
3. **Pull**: each collection file becomes a Figma Variable Collection, and each `mode` key becomes a mode

This projects the ontology onto Figma's flat mode model; compound conditions, specificity, and precedence do not survive the projection. See [Carrying Judged Policies Through Figma](https://github.com/ds1/gitfig-community/blob/main/single-source-of-taste/07-carrying-judged-policies-through-figma.md).

### Use with Style Dictionary

```json
{
  "source": ["tokens/collections/*.json"],
  "platforms": {
    "css": {
      "transformGroup": "css",
      "buildPath": "dist/",
      "files": [{ "destination": "tokens.css", "format": "css/variables" }]
    }
  }
}
```

### Use Directly

```javascript
import primitives from './tokens/collections/primitives.json';
import theme from './tokens/collections/theme.json';
import density from './tokens/collections/density.json';

// Access raw color primitives
const blue500 = primitives.blue['500'].$value; // #3b82f6
const gray200 = primitives.gray['200'].$value; // #e5e5e5

// Get light mode surface color
const surfaceLight = theme.surface.default.$extensions.mode.light; // #ffffff

// Get dark mode surface color
const surfaceDark = theme.surface.default.$extensions.mode.dark; // #0a0a0a

// Get spacing for comfortable density
const spacing4 = density.spacing['4'].$extensions.mode.comfortable; // 16px

// Get spacing for compact density
const spacing4Compact = density.spacing['4'].$extensions.mode.compact; // 12px
```

## Design Philosophy

This ontology supports a **Single Source of Truth (SSOT) architecture** with controlled contextual variation:

1. **Explicit chains** — Every resolved token value traces back through a documented path
2. **Governed types** — Context types are finite and governed, not arbitrary
3. **Learnable friction** — Exceptions are logged and promoted to tokens when patterns emerge
4. **Predictable blast radius** — Changes at any tier have bounded, knowable effects
5. **Full mode coverage** — Every token has explicit values for all modes (no fallbacks needed)

## Resolution Precedence

When dimensions conflict, resolution follows this order (highest to lowest):

1. **Accessibility overrides** — `forced-colors`, `prefers-contrast`, minimum targets
2. **Explicit declarations** — Dimensions set directly on element
3. **Context type** — Dimensions from applied named context type
4. **Inherited context** — Dimensions from ancestor chain
5. **Platform defaults** — Platform-specific default values
6. **System defaults** — Ontology-defined defaults

## Named Context Types

Pre-defined combinations for common scenarios:

| Context Type | Dimensions |
|--------------|------------|
| `mobile-dark` | viewport: mobile, theme: dark, density: comfortable |
| `desktop-light` | viewport: desktop, theme: light, density: comfortable |
| `kiosk` | viewport: desktop, theme: dark, density: spacious, contrast: high |
| `print` | theme: light, contrast: high, motion: none, elevation: base |
| `high-contrast` | contrast: high, elevation: base |
| `reduced-motion` | motion: reduced |
| `compact-ui` | density: compact, typography: technical |
| `editorial-reading` | density: spacious, typography: editorial |

## License

MIT

## Contributing

Issues and pull requests welcome. See the [specification](https://github.com/ds1/gitfig-community/blob/main/single-source-of-taste/05-design-token-context-ontology-specification.md) for the complete ontology that implementations should follow.

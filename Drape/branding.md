# Brand & Design System

## Brand Identity

**Product Name:** Drape
**Tagline:** The Sensory Digital Fabric Atelier
**Brand Personality:** Tactile, Sculptural, Prestigious, Atmospheric, Unhurried
**Tone of Voice:** Editorial, authoritative, and refined. Drape speaks with the calm, knowledgeable register of a private European or Milanese textile salon curator, emphasizing material provenance, tactile qualities, and tailoring craftsmanship without hyperbole or jargon.

## Design Character

**Audience:** Bespoke occasionwear clients, luxury gala and bridal patrons, and independent boutique couture directors (defined in [user-personas](user-personas.md)).

**Feels like:** Haute-couture editorial, weightless fluidity, rich tactile materiality, and sculptural elegance.

**Must not feel like:** A discount hobbyist craft store, a cluttered wholesale textile warehouse, or cold, sterile 3D engineering CAD software.

**Motion character:** Physically weighted and fluid—mimicking the natural gravitational cascade, inertia, and aerodynamic resistance of real silks, heavy cashmeres, and crisp structured taffetas.

**Research basis:**
- [Loro Piana](https://loropiana.com) — Understated luxury, generous typographic pacing, and reverence for raw fiber craftsmanship and tactile provenance.
- [Bottega Veneta](https://www.bottegaveneta.com) — Sculptural silhouette presentation, visceral material focus, and bold editorial negative space.

## Brand Mark & Logo System

**Mark type:** Monogram / negative-space letterform

**Category shorthand:** Scissors, spools of thread, thimbles, or sewing needles.

**Concept:** A sculpted capital letter "D" whose inner counter is carved by a single suspended fold of draped fabric.

**Direction:** A singular, continuous ribbon of luxury textile rendered as a capital "D". The outer stem is clean, architectural, and vertical, while the curving right bowl turns inward upon itself, creating a flowing cloth fold that casts a soft shadow to reveal the inner negative space. The form is monolithic, weighted, and singular, balancing tailoring structure with fluid softness.

**Intended reading:** The effortless elegance of fine cloth falling into graceful form.

**Failure reading:** An abstract paper loop, a generic mobius strip, or a corporate ribbon bookmark.

**Type treatment:** Set in a custom-drawn high-contrast modern serif wordmark. Features razor-sharp vertical serifs, delicate hairline cross-strokes, and generous optical kerning. The wordmark and monogram pair seamlessly or stand independently.

**Usage rules:** The "D" monogram stands alone as the web favicon, mobile touch icon, and physical seal on fabric packaging. In primary desktop header lockups, the monogram precedes the full "Drape" wordmark separated by `space-md`. The mark is never rotated, shadowed with harsh drop-shadows, or enclosed within a generic circular badge.

**Required forms:**
- Monogram mark-only (app icon, favicon, luxury embossed seal)
- Horizontal primary lockup (Monogram + Wordmark)
- Wordmark-only (editorial masthead)
- Knockout / single-tone ink version
- Transparent vector SVG assets

**Surfaces:** The mark holds authority over warm alabaster (`grey-50`), deep obsidian velvet (`grey-900`), and full-bleed high-resolution textile photography. On busy textile textures, the mark is presented over an opaque or subtly frosted background pill using `surface-secondary`.

**One tone & reversal:** The mark reads crisply in solid couture ink (`#111318`) on light surfaces, reversing cleanly to warm ecru (`#FBF9F5`) on dark surfaces.

**Scale & recognition:** The monogram maintains clear optical recognition down to 16x16px (favicon size) without losing the inner counter fold.

## Responsive & Device Targets

| Device class | Breakpoint / Width | Input modality | Layout posture |
|---|---|---|---|
| Mobile | < 600px (Base) | Touch | Single column, sticky bottom action bar, gesture-driven cloth manipulation |
| Tablet | 600px–1024px | Touch + pointer | Split viewport (interactive canvas left/top, technical specs right/bottom) |
| Desktop | > 1024px | Pointer + keyboard | Multi-column cinematic layout, persistent WebGPU 3D canvas with floating inspection drawer |

**Base:** Mobile-first — mobile values are the base; larger classes override them.

## Color Palette

### Primary Colors — 9-shade Couture Ink scale
Derived from deep European dye vats and tailoring ink, providing structural anchor across all interfaces.

| Token | Light | Dark | Role |
|---|---|---|---|
| `primary-900` | `#111318` | `#F2F4F8` | Darkest — primary typography, prominent structural frames |
| `primary-800` | `#1C1F26` | `#E2E6EF` | Deep headings, high-contrast borders |
| `primary-700` | `#282D37` | `#C6CDDC` | Hover states on primary controls |
| `primary-600` | `#3A414F` | `#A4AFC4` | Pressed states, active toggles |
| `primary-500` | `#4F596C` | `#7E8BA4` | **Base** — structural buttons, primary interaction rings |
| `primary-400` | `#707C94` | `#5C677C` | Muted icons, tertiary borders |
| `primary-300` | `#9AA4B8` | `#3F4756` | Selected swatch outlines, subtle divide rules |
| `primary-200` | `#C9D0DD` | `#282E39` | Hover fills on table rows and secondary pills |
| `primary-100` | `#EAEFF5` | `#181B22` | Lightest — subtle container fills, highlighted cards |

### Neutral Colors — 9-shade Warm Ecru & Charcoal scale
Tinted with the organic warmth of unbleached raw silk and fine wool fiber, preventing cold sterile grays.

| Token | Light | Dark | Role |
|---|---|---|---|
| `grey-900` | `#141312` | `#FAF8F5` | Darkest text in light mode / Lightest text in dark mode |
| `grey-800` | `#262422` | `#ECE8E1` | Secondary headings, modal titles |
| `grey-700` | `#403D39` | `#D6D0C5` | Subtitles, editorial captions |
| `grey-600` | `#635F59` | `#B0AAA0` | Secondary body text, textile specifications |
| `grey-500` | `#8C867D` | `#8C867D` | Midtone dividers, placeholder text |
| `grey-400` | `#B8B1A5` | `#635F59` | Inactive controls, slider tracks |
| `grey-300` | `#DCD6CC` | `#3E3B37` | Surface borders, card dividing lines |
| `grey-200` | `#EFECE6` | `#262422` | Tertiary surfaces, swatch metadata chips |
| `grey-100` | `#F6F4F0` | `#1B1A18` | Secondary surfaces, input backgrounds, sidebars |
| `grey-50` | `#FBF9F5` | `#11100F` | Base canvas surface (Warm Ecru in light / Velvet Noir in dark) |

### Structural Role Mappings
- `surface` = `grey-50`
- `surface-secondary` = `grey-100`
- `text-primary` = `grey-900`
- `text-secondary` = `grey-600`
- `border` = `grey-300`
- `theme-color` = `surface`

### Accent Colors — Spun Gold Metallic scale
Evoking fine metallic filigree, brass tailor pins, and bullion embroidery.

| Token | Light | Dark | Role |
|---|---|---|---|
| `accent-900` | `#5E4B24` | `#F4E2BD` | High-contrast gold text on pale cards |
| `accent-700` | `#8C7136` | `#E8C988` | Active luxury badges, hover rings |
| `accent-500` | `#C5A059` | `#DFBA72` | **Base** — Haute couture highlights, swatch badges, verified seals |
| `accent-300` | `#E0C792` | `#937435` | Secondary decorative borders, subtle light highlights |
| `accent-100` | `#F9F4EA` | `#2D2310` | Lightest luxury tint — VIP banners, swatch certification backdrops |

### Semantic Colors — 5-shade scales

| Token | Light | Dark | Role |
|---|---|---|---|
| `success-900` | `#14462B` | `#B6F0D0` | Success banner text |
| `success-500` | `#287D4E` | `#48B978` | In-stock status, yardage verified |
| `success-100` | `#EAF7F0` | `#132B1D` | Positive feedback background |
| `warning-900` | `#5A3807` | `#FCE1B6` | Low-stock warning text |
| `warning-500` | `#A66B13` | `#DFA13D` | Low inventory alert (<5 yards remaining on bolt) |
| `warning-100` | `#FCF5EA` | `#332107` | Caution notice background |
| `error-900` | `#5A1A1A` | `#FBC5C5` | Cutting error or upload failure text |
| `error-500` | `#A83232` | `#E65A5A` | Form validation error, drape simulation retry |
| `error-100` | `#FBEFEF` | `#361111` | Error alert background |
| `info-900` | `#1C3B5E` | `#C2DCFB` | Technical advisory text |
| `info-500` | `#326AA5` | `#5E9EE0` | Textile care guide, fiber origin information |
| `info-100` | `#EFF5FB` | `#122438` | Informational tooltip background |


## Typography

### Font Family
| Role | Font | Fallback |
|---|---|---|
| Display / Headings | `Playfair Display` | `Didot`, `Georgia`, `serif` |
| Body / Controls | `Inter` | `-apple-system`, `BlinkMacSystemFont`, `sans-serif` |
| Monospace / Technical | `JetBrains Mono` | `SFMono-Regular`, `Consolas`, `monospace` |

### Type Scale
| Token | Mobile | Tablet | Desktop | Weight | Line Height | Usage |
|---|---|---|---|---|---|---|
| `display` | 32px | 44px | 56px | 600 | 1.15 | Atelier hero statements, seasonal collection launches |
| `h1` | 26px | 32px | 38px | 600 | 1.25 | Textile product titles, Neural Tailor header |
| `h2` | 22px | 26px | 30px | 600 | 1.3 | Collection categories, modal headers |
| `h3` | 18px | 20px | 22px | 500 | 1.35 | Swatch card titles, weave attribute sections |
| `body-large` | 17px | 18px | 19px | 400 | 1.55 | Editorial textile descriptions, curator notes |
| `body` | 15px | 16px | 16px | 400 | 1.5 | General interface text, checkout reviews, instructions |
| `body-small` | 13px | 14px | 14px | 400 | 1.5 | Technical weave specs, GSM data, shipping options |
| `caption` | 11px | 12px | 12px | 500 | 1.4 | Mill badges, yardage tags, photo upload disclaimer |

## Spacing & Sizing

### Spacing Scale
| Token | Mobile | Tablet | Desktop | Usage |
|---|---|---|---|---|
| `space-xs` | 4px | 4px | 4px | Inline icon padding, badge interior margins |
| `space-sm` | 8px | 8px | 10px | Space between related textile tags, button gap |
| `space-md` | 14px | 16px | 20px | Form field padding, card content padding |
| `space-lg` | 20px | 24px | 32px | Grid gap between swatch cards, section headers |
| `space-xl` | 28px | 36px | 48px | Page margins, primary atelier panel padding |
| `space-2xl` | 40px | 56px | 72px | Major separation between collection rails |
| `space-3xl` | 60px | 80px | 120px | Editorial hero breathing room, footer buffer |

### Sizing Scale

#### Scales by device
| Token | Mobile | Tablet | Desktop | Usage |
|---|---|---|---|---|
| `button-height` | 48px | 44px | 42px | Touch-friendly primary action buttons |
| `input-height` | 50px | 46px | 44px | Yardage selectors, search bars, style prompts |
| `icon-sm` | 16px | 16px | 16px | Micro metadata icons (fiber icons, grainline) |
| `icon-md` | 24px | 24px | 24px | Navigation controls, tool toggles |
| `icon-lg` | 32px | 36px | 40px | Neural Tailor step markers, upload dropzones |

#### Fixed
| Token | Value | Usage |
|---|---|---|
| `radius-none` | 0px | Architectural couture image containers |
| `radius-sm` | 3px | Micro textile chips, grainline arrows |
| `radius-md` | 6px | Interactive buttons, inputs, modal dialogs |
| `radius-lg` | 12px | Floating inspection drawer, floating action bar |
| `radius-full` | 9999px | Circular swatch selectors, pill filters |

## Shadows & Elevation

| Token | Light | Dark | Usage |
|---|---|---|---|
| `shadow-none` | `none` | `none` | Flat editorial surfaces |
| `shadow-sm` | `0 1px 3px rgba(20,19,18,0.04)` | `0 1px 3px rgba(0,0,0,0.5)` | Swatch cards at rest |
| `shadow-md` | `0 6px 16px rgba(20,19,18,0.06)` | `0 6px 16px rgba(0,0,0,0.6)` | Active hover on fabric bolts, dropdowns |
| `shadow-lg` | `0 16px 36px rgba(20,19,18,0.09)` | `0 16px 36px rgba(0,0,0,0.7)` | Floating Neural Tailor tools, quick-view sheets |
| `shadow-xl` | `0 28px 64px rgba(20,19,18,0.14)` | `0 28px 64px rgba(0,0,0,0.85)` | Fullscreen photo upload modal, 3D viewport overlay |

## Component Tokens

### Buttons

| Variant | Background | Text | Border | Radius | Height | Padding |
|---|---|---|---|---|---|---|
| Primary | `primary-900` | `grey-50` | none | `radius-md` | `button-height` | `space-md space-xl` |
| Secondary | `grey-100` | `primary-900` | 1px `border` | `radius-md` | `button-height` | `space-md space-lg` |
| Outline | transparent | `primary-900` | 1.5px `primary-900` | `radius-md` | `button-height` | `space-md space-lg` |
| Ghost | transparent | `text-secondary` | none | `radius-md` | `button-height` | `space-sm space-md` |
| Destructive | `error-500` | `#FFFFFF` | none | `radius-md` | `button-height` | `space-md space-lg` |

### Inputs
| State | Border | Background | Text |
|---|---|---|---|
| Default | `border` | `surface-secondary` | `text-primary` |
| Focus | `accent-500` | `surface` | `text-primary` (2px focus ring) |
| Error | `error-500` | `surface` | `text-primary` |
| Disabled | `border` | `surface-secondary` | `text-secondary` (opacity 0.45) |

## Accessibility

**Target:** WCAG 2.2 Level AA conformance across all digital surfaces.

- **Contrast ratios:** All normal body and UI text guarantees a minimum 4.7:1 contrast ratio against respective light and dark backgrounds; large display headings guarantee a minimum 3.2:1 ratio.
- **Touch targets:** Touch targets on mobile and tablet maintain a strict 48x48px hit area, even for visually delicate hairline icons.
- **Focus indicators:** Keyboard navigation triggers a high-visibility 2px focus ring styled with `accent-500` and a 2px offset.
- **Color independence:** Fabric stock levels, simulation errors, and yardage validity are signaled with distinct iconography and clear text labels, never color alone.
- **Screen reader announcements:** WebGPU cloth sandbox provides accessible fallback text describing the fabric's GSM, composition, weave type, and drape coefficient for non-visual exploration. Dynamic neural generation updates use `aria-live="polite"` regions.

## Asset Style Guide

### Iconography Direction
| Aspect | Direction |
|---|---|
| **Grid & stroke** | 24x24px grid, 1.5px consistent hairline stroke, squared terminals with micro-rounded joins (0.5px). |
| **Style** | Minimalist outline style emphasizing precision and artisanal tailoring tools (grainline marks, scissors, thread weaves). |
| **Corner radius** | Crisp 1.5px radius. |
| **Set** | Custom Drape Haute Couture Icon Set, complemented by Lucide Icons for standard utilitarian actions. |
| **States** | Inactive = `grey-400`; active/hover = `primary-900` (or `accent-500` for couture features). |

### Photography Direction
| Aspect | Direction |
|---|---|
| **Style** | Editorial high-fashion still life paired with extreme tactile macro photography. |
| **Lighting** | Raking directional natural side-lighting (golden hour or overcast studio) to accentuate textile texture, fiber nap, and weave relief. |
| **Color treatment** | True-to-life color grading with calibrated white balance to ensure 99% color fidelity between screen preview and physical dye lot. |
| **Subject matter** | Fluid cloth swatches draped over architectural plinths, unrolled bolts showing raw selvage, and tailored garments on diverse body types. |
| **Composition** | Generous negative space, asymmetric editorial framing, dynamic diagonal folds. |
| **Depth of field** | Shallow depth of field on micro-weave details; deep depth of field on full-garment draping scenes. |

### Motion Direction
| Aspect | Direction |
|---|---|
| **Shot grammar** | Slow, elegant camera dolly and orbit around the draped fabric; no aggressive rapid zooms or jittery cuts. |
| **Camera feel** | Smooth cinematic motion simulating an anamorphic prime lens on a robotic arm. |
| **Pacing** | Measured, luxurious, and deliberate; allows the eye to appreciate the weight of the textile. |
| **Loop character** | Seamless 4-second turn-around loop for the 360° motion viewer. |
| **Grade** | Warm, velvety shadows with luminous highlights that reveal the specular sheen of silk and wool fibers. |

### 3D Direction
| Aspect | Direction |
|---|---|
| **Form language** | Organic, physically accurate cloth simulation with high-density mesh subdivision. |
| **Material & finish** | Physically Based Rendering (PBR) utilizing bidirectional reflectance distribution (BRDF), subsurface scattering (SSS) for silks/chiffons, and anisotropic velvet micro-fibers. |
| **Realism** | Photorealistic simulation calibrated against laboratory physical textile testing data (GSM weight, bending stiffness, shear stiffness). |
| **Scale** | Real-world millimeter precision with accurate warp and weft density mapping. |
| **Orientation** | Y-up coordinate orientation, draped across realistic 3D anatomical mannequins. |

### Texture / Background / Pattern
| Aspect | Direction |
|---|---|
| **Type** | Subtle micro-noise procedural grain simulating raw woven parchment or handmade washi paper. |
| **Scale & repeat** | Non-repeating full-screen subtle procedural shader or 512px seamless low-contrast noise. |
| **Contrast budget** | Extremely subtle (1.5% to 2.5% opacity) to add physical warmth without competing with high-resolution textile photography. |
| **Palette** | Monochrome tone tinted to `grey-100` in light mode and `grey-900` in dark mode. |

## Screen 3: Fabric Detail View

**Route:** `/fabrics/:id`
**Platform:** Web
**Presentation:** Page
**Purpose:** Serves as the interactive sensory hub for an individual textile, providing real-time WebGPU cloth physics simulation, microscopic weave inspection, technical mill specifications, and the gateway to neural garment draping.
**Visual Focus:** Central interactive 3D WebGPU cloth physics canvas allowing direct cursor/touch manipulation of the draped fabric.
**Action Hierarchy:** Primary: Tailor on My Silhouette; Secondary: Order Swatch Sample ($25); Tertiary: Inspect Weave (10x Optical).
**Entry Points:** [Fabric Catalog](02-fabric-catalog.md), [Atelier Home](01-atelier-home.md), [Digital Wardrobe](09-digital-wardrobe.md).
**Exit Points:** [Neural Fitting Screen](04-neural-fitting-screen.md), [Atelier Checkout](06-atelier-checkout.md).

### Layout

**Mobile layout:**
- Sticky top bar with back navigation, fabric title, and audio mute toggle.
- Top half of viewport: Interactive touch-driven 3D cloth canvas with gravity toggle ("Breeze", "Drape", "Drop").
- Bottom half: Scrollable card stack with verified mill specs (GSM, width, fiber), price per yard, and two prominent sticky CTA buttons: "Tailor on My Silhouette" and "Order Swatch".

**Web layout:**
- Split-screen cinematic layout:
  - Left 60%: High-resolution interactive WebGPU 3D canvas rendering the selected textile draped over a minimalist architectural pedestal. Interactive controls: drag gesture to wave/pull, light rotation slider, gravity mode selector, and fullscreen toggle.
  - Right 40%: Editorial textile dossier including title, mill heritage, fiber purity certification, GSM meter, transparency scale, continuous yardage availability indicator, swatch sample ordering button, and the primary "Tailor on My Silhouette" action button.

### Components

| Component | Type | Platform | Purpose | Data Source |
|---|---|---|---|---|
| WebGPU Cloth Viewport | Canvas | Web | 60 FPS real-time cloth simulation | Local WGSL shader + PBR textures |
| Mill Specification Panel | Panel | Web | Displays certified fiber and weave data | GET `/api/fabrics/:id` |
| Micro-Weave Trigger | Button | Web | Launches 10x microscopic inspection | Static |
| Tailor on Silhouette CTA | Button | Web | Initiates the Neural Tailor fitting flow | Static |
| Swatch Sample Button | Button | Web | Adds physical swatch box to cart | POST `/api/cart` |

### Declared Assets

| Asset | Direction | Where it appears | Style pointer |
|---|---|---|---|
| Fabric Macro Studio Portrait | Extreme macro shot of the textile's woven edge and raw selvage, illuminated by warm raking light. | Specification panel background | Photography Direction |

### Overlays

| Overlay | Pattern | Trigger | Behavior | States |
|---|---|---|---|---|
| Micro-Weave Inspector | Modal dialog | Click "Inspect Weave" | Fullscreen dark modal with 10x deep zoom and draggable virtual spotlight | Default, Zooming, Spotlight Active |
| Swatch Added Toast | Toast | Click "Order Swatch" | Non-blocking notification confirming swatch box added with credit reminder | Default |

### Data Requirements

**Data Needed:**
- Fabric detail record (id, name, mill_name, country_of_origin, fiber_breakdown, gsm, width_inches, drape_coefficient, stiffness_rating, price_per_yard, stock_continuous_yards, pbr_maps_urls)

**Data Flow:**
1. Screen mounts &rarr; parse `:id`
2. Fetch fabric details from `GET /api/fabrics/:id`
3. Load PBR normal/roughness textures into WebGPU canvas
4. Initialize Verlet physics simulation loop

### States

| State | Condition | What the User Sees |
|---|---|---|
| **Loading** | Initial fetch & shader compile | Minimalist loading spinner with "Calibrating textile physics..." |
| **Loaded** | Shader active | Full interactive 3D cloth responding to touch/cursor |
| **Low Stock** | Continuous yards < 5 | Amber warning chip: "Only 3.5 continuous yards remaining on bolt" |
| **Error** | Fabric SKU not found | Uses shared Error State with "Textile archive unavailable" |

**Edge Cases:**
- Browser lacks WebGPU &rarr; Automatically switches to WebGL 2.0 shader or plays high-res looping video clip with zero crash.

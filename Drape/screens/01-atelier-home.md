## Screen 1: Atelier Home

**Route:** `/`
**Platform:** Web
**Presentation:** Page
**Purpose:** Welcomes visitors to Drape with an editorial visual showcase of luxury textiles, seasonal couture curations, and an immediate entry into sensory fabric discovery.
**Visual Focus:** Full-width hero banner featuring cascading high-contrast textiles with subtle ambient physics ripples.
**Action Hierarchy:** Primary: Explore Catalog; Secondary: How Neural Draping Works; Tertiary: Order Sample Box.
**Entry Points:** Cold browser entry, external fashion press links, social lookbooks.
**Exit Points:** [Fabric Catalog](02-fabric-catalog.md), [Fabric Detail View](03-fabric-detail-view.md), [Digital Wardrobe](09-digital-wardrobe.md).

### Layout

**Mobile layout:**
- Top navigation bar with monogram mark, audio toggle, and cart icon.
- Hero editorial card with high-impact textile imagery and primary call-to-action button.
- Horizontal swipeable carousel of featured fabric swatches with real-time micro-physics previews.
- "The Neural Atelier" value proposition block explaining virtual garment fitting.
- Curated seasonal rail ("Autumn Gala Brocades", "Savile Row Woolens").
- Sticky bottom action bar with quick catalog search trigger.

**Web layout:**
- Sticky luxury Navbar with monogram + wordmark, collection links, search trigger, soundscape mute toggle, and wardrobe icon.
- Full-bleed cinematic hero section with interactive background cloth ripple responding to cursor momentum.
- Three-column editorial curation grid displaying featured textile rolls with GSM, fiber origin, and real-time hover physics.
- Interactive split showcase: "From Raw Bolt to Bespoke Silhouette" demonstrating a before/after of raw silk transformed into a tailored gown.
- Footer with provenance commitments, mill guild accreditations, and legal privacy notices.

### Components

| Component | Type | Platform | Purpose | Data Source |
|---|---|---|---|---|
| Atelier Header | Navbar | Web | Brand identity, audio toggle, navigation | Static / Context |
| Hero Presentation | Container | Web | Captures visual authority and core value proposition | GET `/api/curations/hero` |
| Featured Swatch Rail | Grid / Carousel | Web | Highlights top seasonal luxury textiles | GET `/api/fabrics?featured=true` |
| Provenance Trust Bar | Flex | Web | Mill origin certifications and ethical sourcing stamps | Static |

### Declared Assets

| Asset | Direction | Where it appears | Style pointer |
|---|---|---|---|
| Hero Cascade Filmstrip | High-fashion editorial video loop of midnight silk and raw linen catching golden raking studio light. | Hero section background | Motion Direction |

### Overlays

| Overlay | Pattern | Trigger | Behavior | States |
|---|---|---|---|---|
| Quick Search Drawer | Drawer | Click Search icon | Slides down from top; live auto-complete search for fibers and occasions | Default, Typing, Results |

### Data Requirements

**Data Needed:**
- Hero curation metadata (headline, featured SKU, video asset URL)
- Top 6 featured fabric cards (title, mill, GSM, price per yard, thumbnail texture)

**Data Flow:**
1. Screen mounts &rarr; render static shell and play cached hero video
2. Fetch featured fabrics from `/api/curations/hero`
3. Hydrate interactive WebGPU canvas when visible in viewport

### States

| State | Condition | What the User Sees |
|---|---|---|
| **Loading** | Initial network fetch | Shimmering warm ecru skeleton blocks |
| **Loaded** | Data fetched successfully | Full editorial content and active cloth previews |
| **Error** | Network failure | Cached offline catalog with reload button |
| **Offline** | No connection | Top notification banner: "Viewing offline archive" |

**Edge Cases:**
- Device does not support WebGPU &rarr; Displays static editorial photography with subtle CSS parallax instead of live 3D physics.

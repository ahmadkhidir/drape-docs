## Screen 2: Fabric Catalog

**Route:** `/catalog`
**Platform:** Web
**Presentation:** Page
**Purpose:** Enables shoppers and designers to discover, filter, and sort luxury textiles across multiple physical parameters including fiber composition, weight (GSM), weave type, and occasion.
**Visual Focus:** Clean, multi-column grid of tactile fabric swatch cards showing macro weave texture and real-time hover ripple.
**Action Hierarchy:** Primary: Select Fabric Card; Secondary: Filter by Fiber / GSM; Tertiary: Reset Filters.
**Entry Points:** [Atelier Home](01-atelier-home.md), search bar, external direct links.
**Exit Points:** [Fabric Detail View](03-fabric-detail-view.md), [Atelier Home](01-atelier-home.md).

### Layout

**Mobile layout:**
- Sticky top header with back button, search bar, and "Filters (3)" pill button.
- Horizontal pill filter rail for fast category switching ("Silk", "Wool", "Linen", "Velvet", "Brocade").
- Single-column vertical list of fabric cards with large square macro thumbnails, GSM badges, and price per yard.
- Floating bottom sheet trigger for full faceted filter drawer.

**Web layout:**
- Left sticky sidebar with multi-faceted filtering: Fiber Purity (100% Silk, Virgin Wool, Blends), Weight / GSM slider (50 GSM to 600 GSM), Weave Structure (Twill, Satin, Jacquard, Crepe), Bolt Width, and Occasion tags.
- Main area: 3-column responsive grid of luxury fabric cards.
- Each card features high-res texture imagery, live hover physics deformation, fiber composition chip, and continuous yardage stock indicator.
- Top bar with active filter chips, total SKU count, and sorting dropdown ("Heaviest to Lightest", "Featured", "Price").

### Components

| Component | Type | Platform | Purpose | Data Source |
|---|---|---|---|---|
| Filter Sidebar | Sidebar / Drawer | Web | Faceted filtering controls | Static / Query parameters |
| Fabric Swatch Card | Card | Web | Visual and tactile card presenting textile attributes | GET `/api/fabrics` |
| Active Filter Pill Bar | Flex / Chips | Web | Shows active constraints with one-click dismiss | State |
| Sorting Selector | Select | Web | Controls catalog display sequence | State |

### Declared Assets
Uses the shared empty state illustration defined in `[screens.md](../screens.md)`.

### Overlays

| Overlay | Pattern | Trigger | Behavior | States |
|---|---|---|---|---|
| Mobile Filter Sheet | Bottom sheet | Click "Filters" on mobile | Full-height sheet with accordion filter categories | Default, Applied |

### Data Requirements

**Data Needed:**
- Paginated list of fabric SKUs (ID, name, mill, fiber, GSM, width, price_per_yard, remaining_yards, thumbnail_url, normal_map_url)
- Total count of results matching query

**Data Flow:**
1. Screen mounts &rarr; parse URL query parameters
2. Fetch filtered results via `GET /api/fabrics?...`
3. Render grid and update filter counts dynamically

### States

| State | Condition | What the User Sees |
|---|---|---|
| **Loading** | Query executing | Grid of 9 warm ecru pulsing skeleton cards |
| **Loaded** | Results returned | Populated fabric cards with interactive hover effects |
| **Empty** | No matching textiles | Uses shared Empty State with "No textiles match this exact combination" |
| **Error** | API error | Uses shared Error State with "Unable to load collection" |

**Edge Cases:**
- Filter combination results in zero matches &rarr; Empty state automatically suggests relaxing GSM constraints or removing weave restrictions.

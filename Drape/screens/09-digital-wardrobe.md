## Screen 9: Digital Wardrobe

**Route:** `/wardrobe`
**Platform:** Web
**Presentation:** Page
**Purpose:** Serves as the customer's personal fashion vault, archiving saved neural fitting renders, purchased fabric orders, downloadable technical spec cards, and reorder links.
**Visual Focus:** Interactive wardrobe gallery displaying the user's custom-fitted garments on dressmaker mannequins with real-time cloth shaders.
**Action Hierarchy:** Primary: View Fitting & Specs; Secondary: Reorder Fabric Yardage; Tertiary: Route to Master Tailor.
**Entry Points:** [Atelier Home](01-atelier-home.md), [Order Confirmation](07-order-confirmation.md).
**Exit Points:** [Fitting Results View](05-fitting-results-view.md), [Fabric Detail View](03-fabric-detail-view.md), [Master Tailor Directory](08-master-tailor-directory.md).

### Layout

**Mobile layout:**
- Two tabs: "Saved Fittings" and "Purchased Orders".
- Vertical card feed with large fitting preview cards, fabric name, date saved, and quick actions ("Download PDF", "Reorder Fabric").
- Floating action button to start a new fitting.

**Web layout:**
- Hero summary banner: User profile status, active orders in cutting room, and count of saved bespoke fittings.
- Two-tab layout:
  - Tab 1 ("Saved Fittings"): 3-column grid of client fitting cards. Each card presents the neural garment preview, selected textile swatch chip, silhouette name, and buttons to "Inspect 3D Drape", "View 360° Walk", and "Download Tailor PDF".
  - Tab 2 ("Purchased Orders"): Detailed history of all past fabric orders, tracking numbers, dye-lot batch records, and one-click repeat bolt yardage ordering.

### Components

| Component | Type | Platform | Purpose | Data Source |
|---|---|---|---|---|
| Wardrobe Tabs | Tabs | Web | Toggles between fittings and order history | State |
| Wardrobe Fitting Card | Card | Web | Displays saved neural fitting with quick actions | GET `/api/v1/wardrobe?tab=fittings` |
| Order History Table | Table | Web | Displays past fabric purchases and dye-lot codes | GET `/api/v1/wardrobe?tab=orders` |
| Download Spec Button | Button | Web | Re-downloads the technical tailor PDF | GET `/api/v1/fittings/:id/tailor-spec/pdf` |

### Declared Assets

| Asset | Direction | Where it appears | Style pointer |
|---|---|---|---|
| Empty Wardrobe Artwork | An antique wooden tailor valet stand holding a clean brass hanger in an airy, sunlit Parisian studio. | Empty state, centered | Photography Direction |

### Overlays
None (uses shared delete confirmation dialog when removing saved fittings).

### Data Requirements

**Data Needed:**
- List of saved fittings (id, render_url, fabric_id, fabric_name, silhouette_name, created_at, has_motion)
- List of past orders (id, order_number, yards, fabric_name, status, tracking_url)

**Data Flow:**
1. Screen mounts &rarr; authenticate user session
2. Fetch saved wardrobe items via `GET /api/v1/wardrobe`
3. Render fitting cards and past orders

### States

| State | Condition | What the User Sees |
|---|---|---|
| **Loading** | Fetching wardrobe | Grid of 6 pulsing cards |
| **Loaded** | Fittings present | Full gallery of saved garments and order history |
| **Empty** | Zero saved items | Uses Empty Wardrobe Artwork + headline "Your wardrobe is awaiting its first commission" + CTA button "Explore Textiles" |
| **Unauthenticated** | Guest user | Prompts user to log in or enter order email to look up past orders |

**Edge Cases:**
- Guest user accesses wardrobe &rarr; Displays order lookup form allowing one-time access via order number and billing email.

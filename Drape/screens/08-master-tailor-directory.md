## Screen 8: Master Tailor Directory

**Route:** `/tailors`
**Platform:** Web
**Presentation:** Page
**Purpose:** Allows customers to discover, evaluate, and select accredited master tailors and couture dressmakers to receive their fabric order directly with cutting specifications.
**Visual Focus:** Curated gallery of verified master tailor studio cards showcasing atelier credentials, garment specialties, and client review scores.
**Action Hierarchy:** Primary: Route Fabric to This Atelier; Secondary: Filter by City / Specialty; Tertiary: View Tailor Lookbook.
**Entry Points:** [Order Confirmation](07-order-confirmation.md), [Digital Wardrobe](09-digital-wardrobe.md), [Atelier Home](01-atelier-home.md).
**Exit Points:** [Order Confirmation](07-order-confirmation.md), [Digital Wardrobe](09-digital-wardrobe.md).

### Layout

**Mobile layout:**
- Header with city selector dropdown ("London", "New York", "Paris", "Milan", "Lagos").
- Specialty pill filters ("Bridal & Gowns", "Bespoke Suiting", "Corsetry", "Traditional Cultural Attire").
- Vertical stack of atelier profile cards with studio exterior photography, master cutter bio, turnaround times, and "Select Atelier" button.

**Web layout:**
- Top filter bar with city multi-select, specialty tabs, turnaround filter (2 weeks vs. 4 weeks), and price tier indicators.
- 3-column grid of accredited atelier cards:
  - Header: Studio photography, studio name, master cutter name, guild badge (e.g., Savile Row Bespoke Association, Chambre Syndicale).
  - Body: Specialties, typical labor cost estimates, turnaround time, verified client rating (e.g., 4.9/5.0).
  - Footer: "View Atelier Portfolio" link and primary "Route Fabric to This Atelier" button.

### Components

| Component | Type | Platform | Purpose | Data Source |
|---|---|---|---|---|
| City & Specialty Filter | DropdownMenu / Tabs | Web | Filters tailor listings by location | State |
| Tailor Studio Card | Card | Web | Displays atelier credentials and booking terms | GET `/api/tailors` |
| Handoff Confirmation Modal | Modal dialog | Web | Confirms destination update and appointment link | POST `/api/orders/:id/route-tailor` |

### Declared Assets
Uses the shared Empty State defined in `[screens.md](../screens.md)`.

### Overlays

| Overlay | Pattern | Trigger | Behavior | States |
|---|---|---|---|---|
| Tailor Handoff Summary | Modal dialog | Click "Route Fabric to This Atelier" | Displays studio shipping confirmation, turnaround SLA, and booking calendar link | Default, Submitting, Confirmed |

### Data Requirements

**Data Needed:**
- List of accredited partner tailors (id, studio_name, master_cutter, city, address, specialties, turnaround_weeks, rating, portfolio_images, booking_capacity)
- Active order reference (if routed from checkout)

**Data Flow:**
1. Screen mounts &rarr; parse query parameter `?order_id=...`
2. Fetch tailors via `GET /api/tailors`
3. User selects tailor &rarr; submit update via `POST /api/orders/:order_id/route-tailor`

### States

| State | Condition | What the User Sees |
|---|---|---|
| **Loading** | Fetching tailor network | Grid of pulsing studio cards |
| **Loaded** | Directory loaded | Populated studio listings with active routing buttons |
| **Filtered Empty** | No tailors in selected city | Empty state: "No accredited ateliers in this city yet" with invitation to nominate a local tailor |

**Edge Cases:**
- Partner tailor has reached seasonal capacity &rarr; Displays a "Waitlist Only" badge with an estimated opening date and recommends comparable sister ateliers in the same metro area.

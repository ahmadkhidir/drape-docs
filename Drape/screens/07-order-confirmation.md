## Screen 7: Order Confirmation

**Route:** `/orders/:id/confirmation`
**Platform:** Web
**Presentation:** Page
**Purpose:** Reassures the customer with an authoritative order receipt, verified dye-lot certificate, digital tailor specification dossier download, and concierge handoff prompt.
**Visual Focus:** Elegant confirmation card featuring the order tracking number, verified dye-lot certification seal, and cutting queue status.
**Action Hierarchy:** Primary: Download Tailor Spec Dossier (PDF); Secondary: Route Fabric to Master Tailor; Tertiary: Return to Atelier Home.
**Entry Points:** [Atelier Checkout](06-atelier-checkout.md).
**Exit Points:** [Master Tailor Directory](08-master-tailor-directory.md), [Digital Wardrobe](09-digital-wardrobe.md), [Atelier Home](01-atelier-home.md).

### Layout

**Mobile layout:**
- Centered gold checkmark animation with order number and delivery estimate.
- Order details card: fabric cut length, bolt ID, and packaging status.
- Prominent button: "Download Tailor Spec Card (PDF)".
- Banner: "Need a master tailor in your city? Route this order directly to an accredited atelier."
- Secondary action: "Save to My Wardrobe".

**Web layout:**
- Centered luxury editorial receipt presentation:
  - Top Section: Animated bespoke seal, personalized greeting ("Thank you, Amara"), order reference number, and real-time cutting queue tracker ("In cutting room &rarr; Laser measurement verified &rarr; Archival boxing &rarr; Carrier dispatch").
  - Two-Column Summary:
    - Left Column (50%): Order invoice breakdown, delivery address, carrier tracking link, and official digital Dye-Lot Verification Certificate.
    - Right Column (50%): Technical Tailor Dossier preview with direct vector PDF download button, QR code for tailor scanning, and the "Route Order to Master Tailor" concierge banner ([FEAT-010](../features/FEAT-010.md)).

### Components

| Component | Type | Platform | Purpose | Data Source |
|---|---|---|---|---|
| Order Status Tracker | Stepper | Web | Visual progress of cutting and dispatch | GET `/api/orders/:id` |
| Dye-Lot Certificate Card | Card | Web | Authenticates roll purity and batch | Order metadata |
| Download Spec Button | Button | Web | Downloads technical PDF for personal tailor | GET `/api/orders/:id/spec-pdf` |
| Route to Tailor Banner | Container | Web | Launches concierge partner tailor flow | Static / Link |

### Declared Assets
Uses the shared Navigation Shell and Biometric Shield Emblem defined in `[screens.md](../screens.md)`.

### Overlays
None (dedicated confirmation page).

### Data Requirements

**Data Needed:**
- Order record (id, order_number, user_email, items, total_amount, shipping_address, cutting_status, dye_lot_code, spec_dossier_url)

**Data Flow:**
1. Screen mounts &rarr; parse `:id`
2. Fetch confirmed order details from `GET /api/orders/:id`
3. Generate signed PDF download URL

### States

| State | Condition | What the User Sees |
|---|---|---|
| **Loading** | Fetching confirmation | Shimmering receipt skeleton |
| **Loaded** | Order record verified | Full confirmation card with active PDF download |
| **PDF Generating** | Background compilation | Button displays spinner: "Compiling tailor blueprint..." |

**Edge Cases:**
- Browser blocks automatic PDF download &rarr; Displays explicit fallback link and sends a copy to the customer's email automatically.

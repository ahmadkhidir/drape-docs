## Screen 10: Cutting Room Dashboard

**Route:** `/ops/cutting-room`
**Platform:** Web (Optimized for Industrial Touchscreen Tablets & Workstations)
**Presentation:** Page
**Purpose:** Operates as the central fulfillment interface for cutting room master cutters, enabling barcode bolt verification, optical laser projection alignment, flaw tracking, and dispatch packaging.
**Visual Focus:** Active cutting work ticket displaying live warehouse bolt barcode, cutting length in eighths of a yard, grainline orientation, and laser alignment triggers.
**Action Hierarchy:** Primary: Scan Bolt & Verify; Secondary: Activate Laser Guide; Tertiary: Flag Flaw & Quarantine.
**Entry Points:** Ops portal login, direct cutting room tablet URL.
**Exit Points:** Order dispatch queue, bolt inventory reconciliation.

### Layout

**Tablet layout (Industrial Touch Focus):**
- Top operational bar: Master cutter badge (Elena Rostova), active table number ("Table 02"), and queue counters: "Pending Cuts (8)", "Urgent Bridal (3)", "Dispatched Today (24)".
- Split-screen workspace:
  - Left Panel (35%): Priority cutting queue list sorted by delivery deadline, showing order number, fabric SKU, yardage, and destination (Customer vs. Partner Tailor).
  - Right Panel (65%): Active Work Ticket detail view:
    - Large bold yardage cut target (e.g., "4.25 YARDS / 3.88 METERS")
    - Continuous bolt barcode scanner input zone with visual pass/fail indicator
    - Laser projection alignment controls ("Project Cut Line", "Project Grainline Grid")
    - Textile flaw logger button ("Flag Snag / Spot")
    - Primary action button: "Mark Cut Complete & Print Dye Certificate".

### Components

| Component | Type | Platform | Purpose | Data Source |
|---|---|---|---|---|
| Cutting Queue Rail | List | Web | Displays pending orders sorted by urgency | GET `/api/v1/ops/cutting-queue` |
| Active Work Ticket Panel | Panel | Web | Shows cutting dimensions and bolt requirements | GET `/api/v1/ops/cutting-ticket/:id` |
| Barcode Verification Scanner | Input / Status | Web | Validates scanned roll against order specifications | Barcode hardware / API |
| Laser Guide Controller | ButtonGroup | Web | Triggers physical overhead optical projection | Hardware WebSocket API |
| Flag Flaw Action | Button | Web | Quarantines defective rolls and triggers sister bolt reorder | POST `/api/v1/ops/bolts/:id/quarantine` |

### Declared Assets
None (operational interface utilizing functional system icons).

### Overlays

| Overlay | Pattern | Trigger | Behavior | States |
|---|---|---|---|---|
| Bolt Mismatch Modal | Modal dialog | Wrong bolt scanned | Flashes screen red with audible alarm; halts cutting until dismissed | Error |
| Flaw Logging Sheet | Bottom sheet | Click "Flag Flaw" | Logs linear flaw coordinate and prompts for sister roll allocation | Default, Submitting |

### Data Requirements

**Data Needed:**
- Active queue items (order_id, priority, fabric_name, yards, bolt_id, dye_lot, destination_type)
- Active bolt hardware state (measured_length, verified_status)

**Data Flow:**
1. Screen mounts &rarr; authenticate master cutter credentials (MFA required)
2. Stream live queue via WebSocket `/ws/v1/ops/cutting-room`
3. Elena selects order &rarr; scan barcode &rarr; verify against `bolt_id`
4. On cut complete &rarr; trigger label printer and update order status to `DISPATCHED`

### States

| State | Condition | What the User Sees |
|---|---|---|
| **Live Queue** | Orders pending | Active orders list with color-coded urgency badges |
| **Ready to Scan** | Order selected | Large barcode prompt awaiting scanner input |
| **Laser Active** | Bolt verified | Green confirmation banner; overhead laser guides illuminated |
| **Flaw Flagged** | Fabric flaw logged | Yellow quarantine card prompting sister bolt swap |

**Edge Cases:**
- Physical barcode scanner disconnected &rarr; Allows manual keyboard override with mandatory supervisor PIN verification.

## Screen 6: Atelier Checkout

**Route:** `/checkout`
**Platform:** Web
**Presentation:** Page
**Purpose:** Processes commercial orders for custom-cut fabric yardage (to 1/8 yard precision) and luxury swatch boxes, holding a 15-minute continuous bolt reservation lock.
**Visual Focus:** Clear order summary card showing continuous yardage on active warehouse bolt, cutting diagram preview, and final price.
**Action Hierarchy:** Primary: Authorize & Place Order; Secondary: Apply Swatch Credit; Tertiary: Return to Fitting.
**Entry Points:** [Fitting Results View](05-fitting-results-view.md), [Fabric Detail View](03-fabric-detail-view.md).
**Exit Points:** [Order Confirmation](07-order-confirmation.md), [Fabric Detail View](03-fabric-detail-view.md).

### Layout

**Mobile layout:**
- Top bar with back arrow and lock security icon.
- Order summary accordion displaying ordered fabric, yardage (e.g., 4.25 yds), bolt roll code, and cedar box packaging.
- Shipping address form with country selector.
- Non-returnable cut yardage policy acknowledgement checkbox.
- Stripe Express Checkout buttons (Apple Pay, Google Pay).
- Credit card input fields with auto-formatting.
- Sticky bottom total bar with "Pay $510.00" button.

**Web layout:**
- Two-column luxury checkout layout:
  - Left Column (60%): Shipping destination form, optional concierge tailoring address toggle ("Ship to Master Tailor"), shipping method selection (Express DHL / Standard White-Glove), and payment input (Stripe Elements with 3D Secure support).
  - Right Column (40%): Sticky order review container detailing fabric thumbnail, verified dye-lot number, continuous bolt ID, fractional yardage breakdown, $25 swatch credit redemption input, non-returnable cut policy disclaimer checkbox, and 15-minute active inventory reservation timer.

### Components

| Component | Type | Platform | Purpose | Data Source |
|---|---|---|---|---|
| Order Summary Card | Card | Web | Displays items, yardage, and pricing | Cart state / GET `/api/cart` |
| Bolt Reservation Timer | Chip | Web | Shows remaining seconds on 15-min Redis lock | State / Timer |
| Shipping Address Form | TextInput / Select | Web | Collects delivery coordinates | User input |
| Non-Returnable Disclaimer | Checkbox | Web | Enforces legal non-returnable acknowledgement | State |
| Payment Gateway Box | Container | Web | Hosts secure Stripe Elements card fields | Stripe SDK |
| Swatch Credit Input | TextInput + Button | Web | Redeems $25 previous swatch purchases | POST `/api/credits/apply` |

### Declared Assets
Uses the shared Error State defined in `[screens.md](../screens.md)`.

### Overlays

| Overlay | Pattern | Trigger | Behavior | States |
|---|---|---|---|---|
| Lock Expired Modal | Modal dialog | 15-minute timer reaches 0:00 | Informs user bolt reservation expired; offers 1-click re-lock | Default, Refreshing |
| Split-Bolt Notice Sheet | Bottom sheet | Selected yardage exceeds continuous roll | Prompts user to accept a split cut or switch to a full sister roll | Default |

### Data Requirements

**Data Needed:**
- Cart items list (fabric_id, bolt_id, yards, price_per_yard, swatch_box_flag)
- Applied swatch credit amount
- Active bolt lock expiration timestamp (`expires_at`)

**Data Flow:**
1. Screen mounts &rarr; verify active Redis bolt lock via `POST /api/checkout/lock`
2. Start 15-minute countdown clock
3. User fills shipping & payment details
4. On submit &rarr; dispatch payment to Stripe
5. On payment success &rarr; commit order and transition to [Order Confirmation](07-order-confirmation.md)

### States

| State | Condition | What the User Sees |
|---|---|---|
| **Default** | Form ready | Unfilled inputs with locked cart totals |
| **Submitting** | Payment in flight | Spinner on pay button, inputs disabled |
| **Payment Error** | Card declined / 3DS failure | Inline red alert with specific decline reason |
| **Lock Expired** | Session exceeds 15 mins | Modal overlay prompting to re-verify continuous yardage |

**Edge Cases:**
- Continuous yardage allocated to another shopper during expired lock &rarr; Alerts customer immediately and auto-selects the nearest verified sister bolt in the same dye lot.

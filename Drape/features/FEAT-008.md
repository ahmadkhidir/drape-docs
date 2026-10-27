## FEAT-008: Luxury Swatch & Cut-to-Order Custom Yardage Checkout

**Priority:** P0
**Driver:** Elena Rostova
**Effort:** L
**Depends On:** FEAT-001, FEAT-007

**User Story:**
As Elena Rostova, I want the e-commerce checkout to support precise fractional cut lengths to 1/8th of a yard and sample swatch box ordering with dye-lot tracking so that customers receive accurate cuts and the cutting room operates with zero inventory ambiguity.

**Description:**
A specialized textile e-commerce checkout pipeline. Supports ordering individual 4"x4" swatch cards, curated luxury sample boxes (5 swatches in presentation packaging with embossed fabric cards), and custom cut yardage in 1/8-yard (0.125 yd) fractional increments. Each order item records the specific warehouse bolt ID and dye-lot batch number to prevent variations between multiple cuts of the same project. Features explicit non-returnable cut-yardage disclaimers prior to payment submission.

**Acceptance Criteria:**
- **Given** a customer on the checkout screen,
  **When** purchasing cut yardage,
  **Then** the quantity input allows increments of 0.125 yards (e.g., 3.125, 3.25, 3.375 yards) with dynamic real-time price calculation.
- **Given** an order containing cut yardage,
  **When** reviewing the final payment step,
  **Then** the customer must acknowledge a clear disclaimer confirming that custom-cut yardage is non-returnable once cut from the bolt.
- **Given** a customer who previously ordered a swatch of a fabric SKU,
  **When** they return to order full yardage within 30 days,
  **Then** the system automatically applies their sample swatch cost as a credit against the full fabric order.

**Edge Cases & Failure States:**
- Requested yardage exceeds remaining continuous yardage on active bolt &rarr; System detects split-bolt condition and alerts user: "Only 3.2 yards remaining on current bolt. Would you like a split cut or to wait for the next full bolt?"
- Payment gateway error during checkout &rarr; Retains cart state and inventory lock for 15 minutes while prompting customer to retry payment.

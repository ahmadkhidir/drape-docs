## FEAT-007: Automated Yardage & Pattern Spec Estimator

**Priority:** P0
**Driver:** Amara Okafor
**Effort:** M
**Depends On:** FEAT-001

**User Story:**
As Amara Okafor, I want an automatic calculation of how many yards of fabric I need for my chosen dress style and body dimensions so that I do not overpay for excess luxury fabric or run short at the dressmaker.

**Description:**
An algorithmic cutting calculator that translates customer body height, bust/waist/hip measurements, selected dress silhouette, and specific fabric bolt width (e.g., 45" vs. 54" vs. 60") into precise recommended yardage. The estimator accounts for pattern grainline orientation, nap/directional weave restrictions (e.g., velvet or directional prints requiring one-way cuts), skirt flares, and seam allowances, outputting a recommended cut length rounded to the nearest 1/8th of a yard with an optional safety margin buffer (typically 0.25–0.5 yd).

**Acceptance Criteria:**
- **Given** a user who has chosen a floor-length mermaid gown silhouette,
  **When** they input their height (e.g., 5'8" / 173 cm) and select a 54"-wide silk brocade bolt,
  **Then** the calculator outputs the exact yardage requirement (e.g., "4.25 yards required, includes 0.35 yd safety margin") within 50ms.
- **Given** a directional textile requiring a one-way cut (e.g., directional jacquard or velvet nap),
  **When** calculating yardage,
  **Then** the calculator automatically flags the directional constraint and adjusts required yardage upward to prevent pattern mismatch during tailoring.
- **Given** an updated garment silhouette selection (e.g., switching from a knee-length cocktail dress to a train gown),
  **When** changed,
  **Then** the yardage recommendation updates immediately on the interface and synchronizes with the cart drawer.

**Edge Cases & Failure States:**
- Missing user measurements &rarr; Falls back to standard proportional sizing based on user height and standard size chart (US 2–24 / UK 6–28) with a clear notice advising verification with a dressmaker.
- Extreme custom dimensions beyond typical pattern blocks &rarr; Displays an alert recommending direct consultation with the Drape Atelier Concierge before cutting.

## FEAT-010: "Send to Atelier" Vetted Master Tailor Concierge

**Priority:** P1
**Driver:** Marcus Sterling
**Effort:** L
**Depends On:** FEAT-007, FEAT-008

**User Story:**
As Marcus Sterling, I want to route my purchased fabric directly to a vetted master tailor in my city with my digital pattern specs attached so that I do not have to transport heavy fabric rolls or explain specs manually.

**Description:**
A concierge service integration that links Drape's fabric fulfillment directly with a curated network of certified master tailors and couture dressmakers in major fashion capitals (London, Paris, New York, Milan, Lagos). At checkout, customers can select "Ship Directly to Atelier", choose an accredited local tailor based on reviews and specialty (e.g., Savile Row suiting, bridal corsetry, traditional embroidery), and bundle the fabric delivery with an initial bespoke consultation booking.

**Acceptance Criteria:**
- **Given** a customer checking out with cut fabric yardage,
  **When** they select "Send to Atelier",
  **Then** the interface presents a curated directory of accredited partner tailors filtered by location and garment specialty.
- **Given** a confirmed concierge booking,
  **When** the cutting room fulfills the order,
  **Then** the fabric is dispatched in white-glove archival packaging directly to the tailor's studio with the digital specification dossier pre-linked to the tailor's portal.
- **Given** a partner tailor receiving a shipment,
  **When** they scan the order QR code on the packaging,
  **Then** their atelier portal immediately displays the customer's 3D neural drape render, exact body measurements, and grainline cutting instructions.

**Edge Cases & Failure States:**
- Customer selects a partner tailor who has temporarily reached booking capacity &rarr; The interface marks the atelier as waitlisted and presents immediate alternative master ateliers with comparable credentials.

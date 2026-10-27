## FEAT-009: Digital Wardrobe & Tailor Handoff Spec Export

**Priority:** P1
**Driver:** Marcus Sterling
**Effort:** S
**Depends On:** FEAT-007, FEAT-008

**User Story:**
As Marcus Sterling, I want to export an authoritative digital technical specification sheet and PDF package of my fitting and fabric specs so that I can send it directly to my master tailor.

**Description:**
A technical export generator that compiles a comprehensive tailor handoff dossier. The generated PDF includes the high-resolution neural fitting preview render, physical textile specifications (fiber content, GSM, width, grainline orientation, recommended pressing/ironing temperature, and interlining pairing advice), exact calculated cutting layout, and order tracking details. Customers can download the PDF, generate a secure read-only web link, or directly email the dossier to their tailor's studio.

**Acceptance Criteria:**
- **Given** an order or saved fitting in the customer's account,
  **When** the user clicks "Export Tailor Spec Sheet",
  **Then** a clean, professional vector PDF is generated and downloaded within 2.0 seconds.
- **Given** the exported spec sheet,
  **When** opened by a tailor,
  **Then** it contains the mill provenance, fiber composition, bolt width, grainline alignment diagram, and care instructions formatted to international textile guild standards.
- **Given** a generated web link to a spec dossier,
  **When** accessed by an external tailor without a Drape account,
  **Then** the tailor can view the 3D rendering and cutting specs in a clean, non-editable browser view.

**Edge Cases & Failure States:**
- Browser blocks automatic PDF download popup &rarr; Displays an inline fallback button with a direct download link and an option to receive the PDF via email.

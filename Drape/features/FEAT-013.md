## FEAT-013: NFC & AR Physical Swatch Box Projection

**Priority:** P2
**Driver:** Amara Okafor
**Effort:** L
**Depends On:** FEAT-008

**User Story:**
As Amara Okafor, I want to tap my physical fabric swatch with my smartphone or scan its marker so that augmented reality projects a full-scale 3D draped dress made from that fabric right into my dressing room.

**Description:**
A connected physical-digital augmented reality integration. Physical sample swatches shipped from Drape incorporate an embedded NFC chip and a subtle visual camera anchor marker. Tapping the swatch with an NFC-enabled mobile device launches an instant browser-based WebAR session (using Apple Quick Look / Android Scene Viewer with zero app download required) that anchors a life-size, 3D animated garment draped in that exact textile onto the user's physical space or mannequin.

**Acceptance Criteria:**
- **Given** a customer who has received a physical Drape swatch box,
  **When** they tap the swatch card with an iPhone or Android phone,
  **Then** the browser opens directly to the AR viewer within 1.5 seconds without requiring an app store download.
- **Given** an active AR session pointed at a clear floor space,
  **When** the 3D dress loads,
  **Then** the garment appears at true 1:1 life-size scale with realistic ambient occlusion and environment lighting reflections.

**Edge Cases & Failure States:**
- Device lacks WebAR or LiDAR support &rarr; Gracefully falls back to high-resolution 360° interactive 3D web model viewer within the mobile browser.
- Poor room lighting preventing AR plane detection &rarr; Displays visual guidance directing the user to aim at a well-lit surface or toggle to 3D orbit mode.

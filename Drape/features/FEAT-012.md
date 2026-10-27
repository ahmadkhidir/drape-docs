## FEAT-012: Generative Dye-Lab & Pattern Scale Adjuster

**Priority:** P2
**Driver:** Julien Moreau
**Effort:** L
**Depends On:** FEAT-001

**User Story:**
As Julien Moreau, I want to customize the scale and colorway palette of textile prints using AI assistance and order the custom design printed on-demand on raw silk or linen bases so that my atelier can produce exclusive fabrics for private clients.

**Description:**
A generative print design lab where designers can modify base textile patterns. Users can interactively scale motifs (e.g., resizing a micro-floral into a bold macro print), re-colorize print layers using curated haute-couture palette swatches or natural language prompts (e.g., "shift palette to Venetian rust, olive, and ochre"), and preview the custom print draped live on garments. Custom-generated textiles are fulfilled via certified on-demand reactive digital textile printing mills on sustainable 100% natural fiber substrates.

**Model Behavior:**
- **Input:**
  - Base vector or raster pattern file (SVG/TIFF/PNG).
  - Target color palette hex array or natural language mood prompt.
  - Scale factor float (0.25x to 4.0x).
  - Selected base substrate SKU (e.g., Silk Habotai 100%, Organic Linen 220 GSM).
- **Output:** Seamless, tileable high-resolution print file (minimum 300 DPI at full bolt width) and color-matched preview renders.
- **Output contract:** Structured JSON with:
  - `print_ready_url`: Lossless 300 DPI CMYK TIFF for print production.
  - `preview_texture_url`: sRGB texture for WebGPU and Neural Tailor rendering.
  - `color_match_delta_e`: Color accuracy confidence metric (<1.5).
- **Fallback:** If generative color harmonization fails to find a safe dye formulation, the system restricts choices to pre-tested dye vat formulas and flags non-printable gamut warnings.

**Acceptance Criteria:**
- **Given** an open pattern in the Dye-Lab,
  **When** the user drags the scale slider from 1.0x to 2.5x,
  **Then** the pattern repeat rescales seamlessly without visible seam artifacts or blurriness.
- **Given** a submitted natural language colorway prompt,
  **When** processed,
  **Then** the AI adjusts the print palette to match the prompt while preserving tonal contrast and print separation.

**Edge Cases & Failure States:**
- Submitted color falls outside the physical reactive dye gamut on silk &rarr; The interface automatically snaps the color to the nearest achievable dye standard and alerts the designer with a visual gamut warning.

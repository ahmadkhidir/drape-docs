## FEAT-004: Multimodal Customer Neural Dress Fitting

**Priority:** P0
**Driver:** Amara Okafor
**Effort:** XL
**Depends On:** FEAT-001, FEAT-005

**User Story:**
As Amara Okafor, I want to upload a photo of myself and select a dress style so that the AI will tailor my chosen fabric into that dress and display it photorealistically on my body.

**Description:**
The core generative AI capability of Drape. A customer uploads a full-body photograph and selects a textile SKU from the catalog. The user then specifies their desired dress style either by choosing from an architectural silhouette library (e.g., Corseted Mermaid, Grecian Bias Gown, Asymmetric Cape Dress, Structured Tuxedo) or providing a natural language prompt with optional inspiration photos. The multimodal neural pipeline segments the user's pose and body geometry, applies 3D neural garment draping that honors the selected fabric's weight, stiffness, and luster, and renders a photorealistic preview of the custom garment tailored to the user.

**Model Behavior:**
- **Input:**
  - Customer full-body portrait image (JPEG/PNG/WebP, minimum 720x1280 resolution).
  - Selected fabric digital asset pack (PBR albedo, normal map, roughness, and measured GSM/stiffness coefficients).
  - Garment silhouette specification: curated silhouette preset ID, natural language prompt string (e.g., "strapless architectural corset gown with high slit"), and optional reference photo URL.
- **Output:** High-resolution photorealistic image (minimum 1440x2560) showing the customer wearing the custom-sewn garment with exact fabric textures, folds, shadows, and natural skin blending.
- **Output contract:** Structured JSON payload returning:
  - `render_url`: Secure ephemeral URL to the generated composite image.
  - `silhouette_id`: Validated garment silhouette classification.
  - `drape_confidence_score`: Float between 0.0 and 1.0 indicating garment geometry fit accuracy.
  - `inferred_measurements`: Approximate proportional bounding dimensions for yardage computation.
- **Fallback:** If generative rendering fails or the user photo is obscured, the system returns a stylized 3D mannequin render of the chosen dress in the selected fabric, displays an advisory message detailing the photo issue (e.g., "Full body not visible; please ensure feet to shoulders are in frame"), and refunds any computation tokens.

**Acceptance Criteria:**
- **Given** a customer who has completed biometric consent ([FEAT-005](FEAT-005.md)) and uploaded a valid full-body photo,
  **When** they select an Italian silk brocade and the "Architectural Corset Mermaid" silhouette,
  **Then** the Neural Tailor generates a photorealistic fitting image within 4.0 seconds (P95).
- **Given** a heavy, stiff fabric (e.g., 450 GSM Wool Crepe) versus a fluid fabric (e.g., 80 GSM Silk Chiffon),
  **When** simulated in the same silhouette,
  **Then** the rendered folds, flare stiffness, and fabric pooling distinctly reflect the differing physical weights and stiffness ratings.
- **Given** a custom natural language dress prompt,
  **When** submitted,
  **Then** the prompt parser maps the style into valid tailoring cut categories and renders a coherent, physically plausible dress.

**Edge Cases & Failure States:**
- Inappropriate or non-garment image upload &rarr; Automated safety classifier rejects the image prior to GPU inference, displaying a friendly prompt requesting a standard full-body portrait.
- Poor lighting or heavy occlusion (e.g., wearing heavy winter coat in upload) &rarr; Warning banner displayed prior to inference suggesting a cleaner photo for optimal draping results.
- GPU inference cluster timeout (>8.0s) &rarr; Immediate fallback to pre-rendered 3D mannequin visualization with a notification offering automatic background retry.

## FEAT-003: Micro-Weave Inspector with Dynamic Directional Lighting

**Priority:** P0
**Driver:** Julien Moreau
**Effort:** M
**Depends On:** FEAT-001

**User Story:**
As Julien Moreau, I want to zoom into the microscopic weave structure of a textile and move a virtual light source across it so that I can inspect thread count, fiber sheen, and metallic yarn reflectance.

**Description:**
A macro-inspection viewport that renders ultra-high-resolution photometric surface scans of the fabric. The inspector supports 10x optical-equivalent deep zoom down to individual warp and weft yarns. Users can drag an interactive spotlight across the 3D canvas to observe how specular highlights, subsurface scattering, and metallic thread filigree react to changing light angles.

**Acceptance Criteria:**
- **Given** a user examining a textile in the Micro-Weave Inspector,
  **When** the user activates zoom controls or pinches on mobile,
  **Then** the viewport smoothly magnifies the surface up to 1000% resolution using tiled pyramidal texture streaming without dropping frames.
- **Given** an active inspection session,
  **When** the user drags the virtual light source from left to right,
  **Then** anisotropic specular highlights shift across the weave ridges in real time, revealing yarn luster and metallic thread sparkle.
- **Given** a translucent fabric (e.g., organza, linen scrim),
  **When** backlit by the light source,
  **Then** the material exhibits authentic subsurface light transmission and silhouette pass-through.

**Edge Cases & Failure States:**
- Low bandwidth connection &rarr; Progressively streams mipmap levels, rendering low-frequency details first and displaying a subtle loading ring for ultra-high-resolution texture tiles.
- Extreme zoom beyond maximum texture resolution &rarr; Limits zoom to the native resolution threshold to prevent pixelated blurriness.

## FEAT-002: WebGPU Real-Time Cloth Physics Sandbox

**Priority:** P0
**Driver:** Julien Moreau
**Effort:** L
**Depends On:** FEAT-001

**User Story:**
As Julien Moreau, I want to interact with a real-time 3D cloth physics simulation of any selected fabric in my web browser so that I can evaluate its fluid motion, bending stiffness, and gravity response before ordering.

**Description:**
An interactive in-browser 3D canvas powered by WebGPU (with WebGL 2.0 fallback) executing a real-time particle-based Verlet integration cloth physics simulation. The cloth mesh is calibrated with laboratory physical measurements (tensile elasticity, bending resistance, and mass density derived from the fabric's GSM). Users can use mouse or touch gestures to grab, drag, flick, release, and fold the cloth, observing how heavy wool falls with sharp weight while light chiffon floats with air resistance.

**Acceptance Criteria:**
- **Given** a device with WebGPU support viewing a fabric page,
  **When** the user drags a cursor or finger across the virtual swatch,
  **Then** the cloth responds with smooth deformation at a minimum of 60 frames per second.
- **Given** a high-stiffness fabric (e.g., 400 GSM Silk Gazar),
  **When** released after being lifted,
  **Then** the cloth forms wide, architectural creases and resists limp folding, accurately reflecting its high bending rigidity.
- **Given** a low-stiffness fluid fabric (e.g., 16 Momme Silk Charmeuse),
  **When** moved through the air,
  **Then** it cascades with continuous micro-folds and fluid draping behavior.

**Edge Cases & Failure States:**
- Client browser lacks WebGPU support &rarr; Gracefully falls back to optimized WebGL 2.0 compute shader; if neither is available, renders high-resolution pre-simulated looping MP4 video clips.
- GPU crash or context loss &rarr; Automatically recovers canvas context without reloading page; falls back to static high-res editorial drape photography.

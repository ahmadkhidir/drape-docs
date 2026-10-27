## FEAT-011: Haptic & Spatial Web Audio Soundscape

**Priority:** P1
**Driver:** Julien Moreau
**Effort:** M
**Depends On:** FEAT-002

**User Story:**
As Julien Moreau, I want subtle, reactive audio feedback when interacting with fabrics online so that the digital experience evokes the rich auditory sensory atmosphere of a real physical textile cutting table.

**Description:**
A procedural, reactive sound design engine built on the Web Audio API. As users manipulate textiles in the WebGPU physics sandbox ([FEAT-002](FEAT-002.md)) or adjust cuts in the yardage calculator, the system generates subtle, dynamic audio responses: the crisp shearing sound of heavy brass tailor shears gliding across raw silk, the delicate whisper of chiffon rippling in air, or the deep, textured rustle of heavy wool crepe. Features full accessibility controls including an instant mute toggle and system sound preference detection.

**Acceptance Criteria:**
- **Given** an unmuted browser session with user audio permission granted,
  **When** the user drags a silk fabric vigorously across the physics sandbox,
  **Then** the Web Audio engine plays a synchronized, velocity-modulated cloth rustle with zero perceptible latency (<20ms).
- **Given** a user adjusting the yardage cut slider,
  **When** the slider crosses yardage notches,
  **Then** a faint, satisfying haptic scissor snip audio cue plays.
- **Given** a user who has enabled `prefers-reduced-motion` or clicks the persistent audio toggle in the header,
  **When** toggled off,
  **Then** all sound synthesis immediately ceases and the state is persisted across sessions.

**Edge Cases & Failure States:**
- Browser autoplay policy blocks unprompted audio &rarr; The audio engine initializes silently in a suspended state until the user performs their first deliberate gesture on the canvas.

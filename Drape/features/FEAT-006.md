## FEAT-006: 360° Looping Neural Motion & Garment Walk

**Priority:** P1
**Driver:** Marcus Sterling
**Effort:** L
**Depends On:** FEAT-004

**User Story:**
As Marcus Sterling, I want to view a 360-degree looping video of the tailored garment in motion so that I can see how the fabric flows, ripples, and reflects light as I step and turn.

**Description:**
An advanced neural video generation capability that transforms the static fitting render from [FEAT-004](FEAT-004.md) into a seamless 4-second looping motion clip. The model synthesizes realistic cloth dynamics as the subject performs a gentle 360-degree pivot or subtle runway step, accurately simulating the swing of skirts, the break of tailored trouser cuffs over shoes, and the shifting luster of satin or worsted wool under studio lighting.

**Model Behavior:**
- **Input:**
  - High-resolution static neural fitting image from [FEAT-004](FEAT-004.md).
  - Fabric physical parameters (GSM mass density, bending modulus, drape coefficient).
  - Motion trajectory preset: 360-degree turntable pivot or gentle walking turn.
- **Output:** Seamless 4-second looping video file (MP4/WebM, 1080x1920, 30 FPS).
- **Output contract:** Structured JSON containing:
  - `video_url`: CDN-cached streaming URL.
  - `loop_duration_ms`: Integer (4000).
  - `fps`: Integer (30).
- **Fallback:** If video inference experiences queue delays or fails, the client seamlessly maintains the interactive 2D high-res fitting image and presents a notification allowing background generation with alert delivery.

**Acceptance Criteria:**
- **Given** a successfully generated static fitting from [FEAT-004](FEAT-004.md),
  **When** the user clicks "View in Motion",
  **Then** a looping video is rendered and begins playback within 6.0 seconds.
- **Given** a flowing garment (e.g., bias-cut silk gown),
  **When** the subject pivots in the video,
  **Then** the hemline flares and billows realistically with centrifugal motion before settling with authentic cloth inertia.
- **Given** video playback on mobile,
  **When** the user drags horizontally across the video player,
  **Then** the player scrubs frame-by-frame through the 360-degree turn with zero stutter.

**Edge Cases & Failure States:**
- Low GPU server capacity &rarr; Places request in a transparent priority queue, displaying a real-time progress bar with estimated generation countdown.

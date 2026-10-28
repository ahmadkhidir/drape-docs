## Screen 5: Fitting Results View

**Route:** `/fittings/:id`
**Platform:** Web
**Presentation:** Page
**Purpose:** Showcases the photorealistic AI-tailored garment rendered onto the customer's body, provides 360° motion video playback, and launches the custom yardage calculation and ordering flow.
**Visual Focus:** High-resolution portrait render of the customer wearing the custom-draped garment with realistic fabric weight, folds, and sheen.
**Action Hierarchy:** Primary: Calculate Yardage & Order; Secondary: View in 360° Motion; Tertiary: Change Silhouette.
**Entry Points:** [Neural Fitting Screen](04-neural-fitting-screen.md), [Digital Wardrobe](09-digital-wardrobe.md).
**Exit Points:** [Atelier Checkout](06-atelier-checkout.md), [Neural Fitting Screen](04-neural-fitting-screen.md).

### Layout

**Mobile layout:**
- Full-screen high-resolution image viewer with pinch-to-zoom and compare slider toggle ("Before" vs. "After").
- Bottom floating card: garment silhouette title, selected fabric badge, and 4-second motion walk trigger button.
- Sticky primary action button at bottom of screen: "Calculate Yardage & Order".

**Web layout:**
- Centered editorial studio display:
  - Left / Main Viewport (65%): High-resolution fitting presentation. Features interactive zoom lens, lighting mode toggle ("Studio Daylight" vs. "Evening Gala"), and a toggle between the static high-res portrait and the looping 360° video walk player ([FEAT-006](../features/FEAT-006.md)).
  - Right Details Panel (35%): Fabric swatch chip, silhouette name, AI drape confidence indicator (e.g., "96% Drape Fit"), privacy ephemeral deletion countdown timer ("Original portrait deleted from servers"), and prominent action block leading to yardage calculation.

### Components

| Component | Type | Platform | Purpose | Data Source |
|---|---|---|---|---|
| Fitting Render Viewer | Container | Web | Displays high-res tailored image with zoom lens | GET `/api/v1/fittings/:id` |
| 360° Motion Player | VideoPlayer | Web | Plays 4s looping neural video walk | GET `/api/v1/fittings/:id/motion` |
| Yardage Calculator Drawer | Sheet / Drawer | Web | Computes yardage based on user dimensions ([FEAT-007](../features/FEAT-007.md)) | Local engine / API |
| Ephemeral Timer Badge | Chip | Web | Shows countdown confirming privacy photo purge | WebSocket / Timer |
| Order Button | Button | Web | Opens yardage drawer or navigates to checkout | State |

### Declared Assets
Uses the shared Loading Skeleton and Error State defined in `[screens.md](../screens.md)`.

### Overlays

| Overlay | Pattern | Trigger | Behavior | States |
|---|---|---|---|---|
| Yardage Calculator Drawer | Bottom sheet / Side drawer | Click "Calculate Yardage & Order" | Slides over screen; user enters dimensions and sees real-time yardage calculation | Default, Calculating, Result |
| Motion Render Progress Modal | Modal dialog | Click "View in 360° Motion" | Displays progress indicator while looping video synthesizes | Default, Complete |

### Data Requirements

**Data Needed:**
- Fitting record (id, status, render_url, motion_video_url, fabric_id, silhouette_id, drape_score, ephemeral_expires_at)

**Data Flow:**
1. Screen mounts &rarr; connect to WebSocket endpoint `/ws/v1/fittings/:id`
2. If `status === "PROCESSING"` &rarr; show progress animation with tailoring milestones
3. On completion &rarr; render composite image and initialize ephemeral timer countdown

### States

| State | Condition | What the User Sees |
|---|---|---|
| **Rendering** | Job in GPU queue | Elegant tailoring animation with progress bar ("Draping silk fibers...") |
| **Loaded** | Render ready | Photorealistic garment on user with active interactive zoom |
| **Video Generating** | Motion requested | Subtle pulse on motion button with percentage indicator |
| **Error** | Inference failure | Apology banner offering instant 3D parametric mannequin fallback |

**Edge Cases:**
- Fitting generation exceeds timeout threshold (>8s) &rarr; Automatically displays 3D parametric mannequin render while background worker retries.

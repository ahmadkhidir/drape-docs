## Screen 4: Neural Fitting Screen

**Route:** `/fittings/new`
**Platform:** Web
**Presentation:** Page
**Purpose:** Collects customer portrait uploads or mannequin preferences, enforces biometric privacy consent, and captures garment silhouette selections for generative neural tailoring.
**Visual Focus:** Central portrait upload dropzone with fine hairline guides, complemented by an architectural silhouette selection carousel.
**Action Hierarchy:** Primary: Render Fitting; Secondary: Switch to 3D Mannequin Mode; Tertiary: Upload Inspiration Photo.
**Entry Points:** [Fabric Detail View](03-fabric-detail-view.md).
**Exit Points:** [Fitting Results View](05-fitting-results-view.md), [Fabric Detail View](03-fabric-detail-view.md).

### Layout

**Mobile layout:**
- Top navigation with back arrow and progress step indicator: "Step 1: Your Silhouette &rarr; Step 2: Fitting".
- Upload dropzone with camera capture trigger, supported file format guidelines, and prominent privacy assurance lock.
- Mode switcher tab: "My Photo" vs. "3D Mannequin".
- Horizontal scrollable card list of curated garment silhouettes (e.g., Corseted Mermaid, Off-Shoulder Ballgown, Grecian Slip, Tailored Tuxedo).
- Optional text prompt input: "Describe custom details (e.g., high side slit, cowl neck)..."
- Sticky bottom action button: "Render Fitting".

**Web layout:**
- Two-column split studio layout:
  - Left Column (45%): Portrait upload container with drag-and-drop zone, camera integration, pose checklist ("Full body, standing upright, neutral lighting"), and plain-language privacy badge detailing 15-minute ephemeral deletion.
  - Right Column (55%): Garment silhouette selector with 8 architectural presets rendered in clean vector line art, natural language customization text input, optional dressmaker sketch upload, and selected fabric summary card.
- Floating bottom action bar with estimated inference time (<4.0s) and primary "Render Fitting" button.

### Components

| Component | Type | Platform | Purpose | Data Source |
|---|---|---|---|---|
| Photo Upload Dropzone | FileUpload | Web | Ingests user portrait with client-side validation | Local file / Camera |
| Mannequin Mode Switcher | Tabs | Web | Allows anonymous fitting on 3D body models | State |
| Silhouette Selector | Grid / Radio | Web | Captures chosen dress cut preset | Static / Preset catalogue |
| Custom Prompt Input | TextInput | Web | Natural language styling instructions | State |
| Biometric Privacy Modal | Modal | Web | Captures mandatory informed consent ([FEAT-005](../features/FEAT-005.md)) | State / Crypto API |

### Declared Assets
Uses the shared Biometric Shield Emblem defined in `[screens.md](../screens.md)`.

### Overlays

| Overlay | Pattern | Trigger | Behavior | States |
|---|---|---|---|---|
| Biometric Privacy Consent | Modal dialog | First-time upload click | Blocks upload until explicit affirmative consent is signed | Default, Submitting, Error |
| Pose Guidance Sheet | Bottom sheet | Click "Photo Tips" | Visual diagrams showing optimal standing posture and lighting | Default |

### Data Requirements

**Data Needed:**
- Selected fabric summary (id, name, thumbnail, width, gsm) — from route state
- Silhouette presets list (id, name, category, preview_svg)
- User biometric consent status — from local context / cookie

**Data Flow:**
1. Screen mounts &rarr; verify fabric `:id` in session
2. User initiates photo upload &rarr; check consent status
3. If not consented &rarr; display Biometric Privacy Consent Modal
4. On submit &rarr; dispatch multipart payload to `POST /api/v1/fittings`
5. Navigate to [Fitting Results View](05-fitting-results-view.md) with `job_id`

### States

| State | Condition | What the User Sees |
|---|---|---|
| **Default** | Initial load | Empty dropzone with standing figure outline |
| **Photo Uploaded** | Valid image selected | Preview thumbnail with green validation checkmark |
| **Validation Error** | Blurry or cropped image | Inline alert: "Full body not visible. Please include shoulders to feet" |
| **Mannequin Mode** | User toggles away from photo | Mannequin selector with 8 anatomical body silhouettes |

**Edge Cases:**
- User declines biometric consent &rarr; Drops photo file and switches automatically to 3D Mannequin Mode.

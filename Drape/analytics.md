# Analytics & Observability

## Overview

Drape telemetry exists to evaluate user engagement with tactile cloth physics, measure the conversion velocity from digital neural fitting to physical cut yardage orders, and proactively detect client-side WebGPU shader or GPU inference regressions before they impact the customer experience. Every event is captured with zero personal data, strictly consent-gated, and tied directly to product optimization decisions.

## Event Taxonomy

**Common properties on every event:** `event_id` (UUIDv4), `occurred_at` (UTC, ISO-8601), `user_id` (pseudonymous UUID or null), `anonymous_id` (cookie-backed client identifier), `session_id` (ephemeral session UUID), `platform` ("web"), `app_version` (git semantic version), `locale` (e.g., "en-US", "fr-FR").

| ID | Event | Trigger | Key properties | Feature |
|---|---|---|---|---|
| EVT-001 | `session_started` | Client web application mounts in browser | `referrer`, `landing_path`, `webgpu_supported` | — |
| EVT-002 | `textile_filtered` | Catalog filters applied or updated | `fiber_category`, `gsm_min`, `gsm_max`, `result_count` | [FEAT-001](features/FEAT-001.md) |
| EVT-003 | `physics_manipulated` | User interacts with WebGPU cloth canvas | `fabric_id`, `gesture_type`, `drag_duration_ms`, `avg_fps` | [FEAT-002](features/FEAT-002.md) |
| EVT-004 | `weave_inspected` | Micro-Weave modal opened | `fabric_id`, `zoom_level`, `light_angle_deg` | [FEAT-003](features/FEAT-003.md) |
| EVT-005 | `biometric_consent_granted` | User clicks affirmative agreement in consent modal | `regulation_standard`, `consent_version` | [FEAT-005](features/FEAT-005.md) |
| EVT-006 | `portrait_uploaded` | Full-body portrait selected and validated client-side | `file_size_kb`, `aspect_ratio`, `mannequin_fallback_flag` | [FEAT-004](features/FEAT-004.md) |
| EVT-007 | `neural_fitting_completed` | Photorealistic fitting delivered to client | `fabric_id`, `silhouette_id`, `drape_score`, `inference_latency_ms` | [FEAT-004](features/FEAT-004.md) |
| EVT-008 | `motion_video_generated` | 360-degree looping video render delivered | `fitting_id`, `duration_seconds`, `generation_latency_ms` | [FEAT-006](features/FEAT-006.md) |
| EVT-009 | `yardage_calculated` | Yardage calculation engine executed | `fabric_id`, `silhouette_id`, `recommended_yards`, `waste_safety_margin` | [FEAT-007](features/FEAT-007.md) |
| EVT-010 | `bolt_lock_acquired` | 15-minute continuous bolt reservation locked | `bolt_id`, `yards_locked`, `expires_at` | [FEAT-008](features/FEAT-008.md) |
| EVT-011 | `checkout_initiated` | Checkout form rendered with locked items | `cart_total_usd`, `is_swatch_box`, `yards_total` | [FEAT-008](features/FEAT-008.md) |
| EVT-012 | `order_placed` | Payment authorized and order committed | `order_id`, `total_amount_usd`, `payment_method_type`, `item_count` | [FEAT-008](features/FEAT-008.md) |
| EVT-013 | `spec_dossier_exported` | Technical PDF tailor spec card downloaded | `order_id`, `silhouette_id`, `export_format` | [FEAT-009](features/FEAT-009.md) |
| EVT-014 | `tailor_concierge_routed` | Order routed to partner master tailor studio | `order_id`, `tailor_studio_id`, `city` | [FEAT-010](features/FEAT-010.md) |
| EVT-015 | `cutting_ticket_completed` | Precision cut executed in cutting room | `order_id`, `bolt_id`, `measured_yards`, `cutting_operator_id` | [FEAT-008](features/FEAT-008.md) |

## Funnels & Conversion

| Funnel | Steps (event IDs) | Success event | Flow |
|---|---|---|---|
| **Discovery-to-Fitting** | EVT-002 &rarr; EVT-003 &rarr; EVT-005 &rarr; EVT-007 | `neural_fitting_completed` | [user-flow](user-flow.md) Flow 1 & 2 |
| **Fitting-to-Purchase** | EVT-007 &rarr; EVT-009 &rarr; EVT-010 &rarr; EVT-011 &rarr; EVT-012 | `order_placed` | [user-flow](user-flow.md) Flow 2 & 3 |
| **Swatch-to-Bolt** | EVT-012 (swatch) &rarr; EVT-001 &rarr; EVT-012 (yardage &ge; 3.0) | `order_placed` | [monetization](monetization.md) Swatch Credit |
| **Concierge Handoff** | EVT-012 &rarr; EVT-013 &rarr; EVT-014 | `tailor_concierge_routed` | [user-flow](user-flow.md) Flow 4 |

**Conversion definitions:**
- **Atelier Activation:** A visitor who executes at least one WebGPU cloth drag session (>3 seconds) and renders at least one custom garment fitting.
- **Commercial Conversion:** A visitor who completes a physical fabric cut purchase or sample swatch box order within the session.
- **Swatch-to-Bolt Conversion:** A customer who orders a $25 sample box and subsequently orders 3+ yards of fabric within 30 days.

## Error & Performance Monitoring

| Signal | Source | Captured fields | Purpose |
|---|---|---|---|
| WebGPU shader compilation error | Web client | `gpu_vendor`, `browser_engine`, `shader_error_log` | Detect browser WGSL compatibility issues |
| WebGPU frame drop | Web client | `screen_route`, `avg_fps`, `min_fps`, `mesh_vertices` | Monitor 60 FPS performance budget ([NFR-003](nfr.md)) |
| Serverless GPU inference timeout | Backend ML worker | `job_id`, `silhouette_id`, `elapsed_ms`, `gpu_node_id` | Track P95 <3.8s fitting latency ([NFR-004](nfr.md)) |
| Payment authorization failure | Stripe webhook | `decline_code`, `payment_method`, `amount` | Monitor checkout friction and bank declines |
| Cutting room flaw quarantine | Cutting room tablet | `bolt_id`, `linear_yard_position`, `flaw_type` | Track mill quality and defect rate ([NFR-005](nfr.md)) |

**Correlation:** Every client request injects an `X-Correlation-ID` header propagated across the API Gateway, Atelier Core Service, and Serverless GPU workers. Client error toasts log the correlation ID so customer support can immediately inspect corresponding serverless container execution logs.

**Model Quality Feedback:** When users review a neural fitting, an optional subtle thumbs-up/down feedback control emits an internal event (`output_id`, `rating`, `model_checkpoint_version`, `correlation_id`) without capturing raw image text, directly populating the golden benchmark evaluation pipeline ([NFR-030](nfr.md)).

## Business Reporting

| Report / Dashboard | Audience | Metrics & Overview KPI Mapping | Refresh |
|---|---|---|---|
| **Atelier Conversion Overview** | Executive Team, Product | Overall conversion rate, total gross merchandise value (GMV), AOV. **Maps directly to [overview](overview.md) KPI: Conversion Rate > 3.8%** | Hourly |
| **Neural Tailor Engagement Report** | ML Engineering, Product | Average fittings simulated per active session, 360° motion generation uptake. **Maps directly to [overview](overview.md) KPI: Styles per Session > 3.2** | Daily |
| **Swatch-to-Bolt Cohort Tracker** | Merchandising, Finance | 30-day repeat yardage conversion rate from sample box buyers, credit redemption rate. **Maps directly to [overview](overview.md) KPI: Swatch-to-Bolt > 22.0%** | Weekly |
| **Inference Performance & Cost Matrix** | ML Engineering, Finance | P50/P95/P99 latency per fitting, serverless GPU spend per render. **Maps directly to [overview](overview.md) KPI: Latency < 3.8s & [nfr](nfr.md) Cost <= $0.045** | Real-time |
| **Cutting Room Precision & QA Log** | Elena Rostova, Operations | Defect claim rate, continuous yardage accuracy, laser projection alignment uptime. **Maps directly to [overview](overview.md) KPI: Cut Accuracy > 95.0%** | Daily |

## Analytics Data Governance

- **Consent Gating:** Behavioral telemetry is categorized into strictly anonymous interaction pings (`session_started`, `physics_manipulated`). Any event associating a user identifier with garment silhouette choices is suppressed until the user accepts general analytical cookies.
- **Zero Personal Data Guarantee:** No personal names, street addresses, phone numbers, raw uploaded portrait images, or facial recognition embeddings are ever passed as event properties. User references use opaque UUIDs.
- **Retention & Rolling Deletion:** Raw telemetry event rows are retained for 90 days in cloud analytical partitions, after which they are rolled into daily anonymized aggregates and permanently deleted from primary storage per [nfr](nfr.md).
- **Subject-Access Deletion (GDPR/CCPA):** When an authenticated user submits a Data Subject Deletion Request, a cascading worker scrubs all corresponding `user_id` foreign keys from the analytics warehouse within 48 hours.

## Measurement & Verification

| Check | Method | When |
|---|---|---|
| Event schema validation | Automated JSON Schema CI test checking taxonomy and field constraints | Every pull request |
| PII payload scanning | Automated regex scanner inspecting outbound event batches for email/names | Continuous in staging |
| Funnel count reconciliation | Automated script comparing `order_placed` events against primary database orders | Daily at 02:00 UTC |
| Ephemeral purge verification | Verification probe ensuring fitting image URLs expire within 15 minutes | Continuous synthetic canary |

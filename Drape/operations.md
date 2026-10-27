# Support & Governance

## Overview

Drape operates a hybrid operational model combining automated digital self-service with white-glove atelier concierge support. Operational coverage spans global business hours (08:00 to 22:00 CET / EST) across European and North American fashion hubs, with specialized support leads overseeing cutting room precision, partner tailor logistics, and biometric regulatory compliance. Independent dressmaker labor disputes, custom sewing pattern drafting, and alterations beyond certified fabric specifications are strictly out of scope for support.

## Support Model & SLAs

| Tier | Who | Channel | First response | Resolution target | Escalation |
|---|---|---|---|---|---|
| **Standard** | Guest visitors, Swatch Box buyers | In-app messenger + email | &le; 1 business day | &le; 3 business days | Support Lead |
| **Atelier Client** | Verified fabric cut purchasers | Priority in-app chat + email | &le; 4 business hours | &le; 1 business day | Support Lead &rarr; Operations |
| **Couture Studio Pro** | Subscribed design studios ([Julien Moreau](user-personas.md)) | Dedicated WhatsApp Concierge + Studio Line | &le; 1 business hour | &le; 8 business hours | Head of Atelier Partnerships |

**Out of scope:**
- Sourcing non-catalog synthetic commodity textiles or deadstock not verified by Drape mill partners.
- Direct labor arbitration between clients and independent tailors regarding sewing assembly fees.
- Custom manual 2D CAD paper pattern grading adjustments beyond automated spec calculations ([FEAT-007](features/FEAT-007.md)).

**Self-serve first:**
- Order tracking, dye-lot certificate re-downloads, and swatch credit status queries are resolved via the [Digital Wardrobe](screens/09-digital-wardrobe.md) self-service portal before a ticket can be filed.

## Admin & Governance

**Roles and permissions:**
| Role | Can view | Can change | Approval required for |
|---|---|---|---|
| **Support Specialist** | Customer orders, shipping tracking, swatch credit ledger | Issue swatch credits, resend tracking | Cash refunds above $150.00 |
| **Master Cutter ([Elena Rostova](user-personas.md))** | Cutting queue, physical bolt inventory, laser guides | Update bolt status, log flaws, mark cuts complete | Discarding whole bolt (>15 yds) |
| **Tailor Concierge Lead** | Partner tailor directory, dispatch statuses, client spec dossiers | Reassign partner tailors, update studio capacity | Onboarding new atelier studio |
| **Compliance Officer ([David Chen](user-personas.md))** | Biometric consent logs, ephemeral purge verification records | Execute GDPR/BIPA erasure, issue compliance certs | External legal disclosure |
| **Super Administrator** | All system records, GPU worker telemetry, financial ledgers | Role assignments, system configuration, feature flags | Production database migrations |

**Controls:**
- **Least privilege:** Admin access is strictly role-scoped with zero shared administrative credentials.
- **No Portrait Impersonation:** Customer photographs uploaded to the Neural Tailor are processed in volatile memory and are strictly inaccessible to human support agents; support tools can inspect only stylized 3D mannequin representations.
- **Audit trail:** Every privileged action (cutting ticket override, refund issue, role elevation, data erasure) records actor, target entity, action, timestamp, and justification. Audit logs are append-only and retained for 365 days in immutable cloud storage per [nfr](nfr.md).
- **Break-glass:** Emergency elevated production access requires two-person authorization (Engineering Lead + Security Lead) and triggers real-time alerts to the executive team with post-incident review within 24 hours.

## Billing Operations

The workflows below execute the commercial policies defined in [monetization](monetization.md).

| Trigger | Detection | Action | Owner | SLA |
|---|---|---|---|---|
| **Failed Subscription Renewal** | Stripe webhook | Initiate 5-day grace period; send automated notification email to studio | Billing Ops | Immediate automated trigger |
| **Defective Yardage Claim** | Customer support ticket with photo within 7 days | Review photographic evidence against cutting room high-res table archive; approve replacement or full refund | Elena Rostova & Support Lead | &le; 2 business days |
| **Chargeback Notice** | Stripe dispute webhook | Freeze disputed user credits; assemble carrier proof of delivery, cutting ticket, and signed non-returnable checkout acknowledgement | Billing Ops | &le; 5 business days (before evidence deadline) |
| **Suspected Fraud (> $1,200)** | Risk rule anomaly or analytics velocity trigger | Place temporary 2-hour cutting hold; verify cardholder identity via 3D Secure step-up | Risk & Billing Lead | &le; 2 hours |
| **Swatch Credit Redemption Query** | Automated checkout calculation failure | Manually verify original swatch box order number and apply $25 credit balance | Support Specialist | &le; 4 business hours |

**Appeal path:** Blocked customers or contested fraud holds can submit secondary government-issued identification through an encrypted, single-use upload portal reviewed by the Risk Lead within 1 business day.

## Moderation & Abuse

| Report type | Channel | First action | Resolution | Appeal |
|---|---|---|---|---|
| **Inappropriate / NSFW Photo Upload** | Pre-inference safety classifier | Reject upload immediately; wipe image from memory; log event hash | Auto-blocked prior to GPU execution; user notified | In-app support review |
| **Generative Print Copyright Claim** | DMCA notice / rights-holder report | Suspend custom pattern SKU in Dye-Lab ([FEAT-012](features/FEAT-012.md)); pause pending print runs | Complete IP investigation within 48 hours | Legal / Email |
| **Partner Tailor Quality Violation** | Customer review &lt; 3.0 / complaint | Temporarily pause new order routing to the studio; conduct video review | Review atelier credentials within 3 business days | Head of Tailor Partnerships |

## Incident & Escalation

| Severity | Definition | Response | Communication | Containment |
|---|---|---|---|---|
| **SEV-1** | Storefront checkout completely down, or suspected biometric data leak | Page on-call immediately (&le; 15m) | Public status page updated within 15m; executive briefing | Rollback release per [release](release.md); isolate compromised worker containers |
| **SEV-2** | Serverless GPU inference cluster failing or WebGPU shader compilation broken | On-call engaged within 30m | Status page banner if user-visible; email active fitting users | Activate circuit breaker; route all fittings to 3D parametric mannequins ([NFR-011](nfr.md)) |
| **SEV-3** | Non-blocking visual glitch or catalog filter display defect | Addressed next business day | Ticket tracker update | Patch deployed in next scheduled maintenance release |

**On-call rotation:** Primary and secondary engineering rotations rotate weekly on Tuesdays at 04:00 UTC. Postmortems are blameless and published within 3 business days for all SEV-1 and SEV-2 incidents, with remediation items tracked in the issue tracker.

**Model quality degradation:** If live user feedback or automated canary runs detect neural drape fidelity dropping below the 92% threshold ([NFR-030](nfr.md)), the ML Lead rolls back the model checkpoint to the last certified baseline within 30 minutes.

## Runbooks

| Runbook | Covers | Owner |
|---|---|---|
| `RB-01: Biometric Data Erasure & BIPA Audit` | Executing user data erasure requests and certifying zero residual biometric data | Compliance Officer ([David Chen](user-personas.md)) |
| `RB-02: Serverless GPU Outage & Circuit Breaker` | Managing inference container failover and activating 3D mannequin fallback | Platform Reliability Lead |
| `RB-03: Cutting Room Flaw Quarantine` | Quarantining defective physical rolls and allocating continuous sister bolts | Master Cutting Lead ([Elena Rostova](user-personas.md)) |
| `RB-04: Fraudulent Chargeback Dispute Assembly` | Assembling signed delivery receipts and cutting ticket logs for bank contests | Billing Operations Lead |
| `RB-05: Model Checkpoint Rollback` | Reverting a degraded diffusion checkpoint to a verified golden-set model | Machine Learning Lead |
| `RB-06: Database Failover & Bolt Lock Recovery` | Failing over primary PostgreSQL to warm standby and clearing expired Redis locks | Platform Reliability Lead |

## Verification

| Check | Method | When |
|---|---|---|
| Support SLA Compliance | Customer support desk analytics report | Monthly review |
| Admin Audit Completeness | Automated audit log validation script | Monthly audit |
| Runbook Drill Execution | Simulated dry-run of GPU outage (`RB-02`) and Data Erasure (`RB-01`) | Quarterly |
| Cutting Precision Verification | Sample measurement audit on 50 finished packages | Bi-weekly |
| Dispute Win-Rate Reconciliation | Stripe dispute outcome reconciliation | Monthly |

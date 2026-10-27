# Non-Functional Requirements

## Overview

This document specifies the quantitative quality attributes, performance budgets, availability service-level objectives, security controls, model quality bars, and privacy regulations governing Drape. Quality targets are calibrated for a high-performance, WebGPU-accelerated e-commerce web platform serving luxury occasionwear buyers and couture designers across North America, Europe, and West Africa. Native mobile app metrics are deliberately waived for Phase 1 in favor of a web-first responsive architecture.

## Performance & Scalability

| ID | Operation class | Metric | Target (p50 / p95 / p99) | Load assumption | Verification |
|---|---|---|---|---|---|
| NFR-001 | Initial page load (cold) | LCP / TTI | 1.8s / 2.8s / 4.2s | 4G network, mid-tier mobile | Lighthouse CI budget |
| NFR-002 | Catalog search & swatch filter | Server response time | 80ms / 180ms / 450ms | 150 RPS sustained, 10k SKUs | k6 API load test |
| NFR-003 | WebGPU cloth physics render | Frame rate / Budget | 60 FPS / <16.6ms per frame | Active multi-touch drag | WebGPU performance profiler |
| NFR-004 | Neural Tailor static fitting | End-to-end inference | 2.2s / 3.8s / 5.5s | 25 concurrent GPU workers | Distributed inference benchmark |
| NFR-005 | 360° motion video generation | Video render latency | 4.2s / 6.0s / 8.5s | 10 concurrent video tasks | Asynchronous job monitor |
| NFR-006 | Yardage calculation & layout | Calculation execution | 15ms / 35ms / 60ms | Complex multi-panel gown | Unit benchmark suite |
| NFR-007 | High-res weave texture tile | TTFB per tile | 45ms / 95ms / 200ms | Global edge CDN, 1000 rps | Edge CDN synthetic probe |

**Throughput & capacity:**
- **Peak concurrency:** 2,500 simultaneous active visitor sessions with zero cloth physics frame drops.
- **Catalog capacity:** 10,000 digitized fabric SKUs at launch; scalable to 100,000 SKUs with zero search degradation.
- **Scaling trigger:** Auto-scale API pods when CPU/memory exceeds 70% for 3 consecutive minutes; auto-scale serverless GPU instances when inference queue depth exceeds 5 pending jobs.

## Availability & Reliability

| ID | Availability target | Monthly error budget | Measurement |
|---|---|---|---|
| NFR-010 | 99.95% monthly for core e-commerce | 21m 36s | External synthetic monitoring + status page |
| NFR-011 | 99.5% monthly for GPU inference cluster | 3h 39m | Serverless cluster health endpoint probe |
| NFR-012 | 99.99% for payment & checkout processing | 4m 19s | End-to-end checkout probe |

**Recovery objectives:**
- **RTO (Recovery Time Objective):** < 30 minutes for complete disaster recovery failover.
- **RPO (Recovery Point Objective):** < 5 minutes (zero loss of submitted orders, payments, or tailor specs).

**Degradation — what happens when a dependency fails:**
| Failure | Expected behavior | User-visible effect |
|---|---|---|
| GPU inference cluster offline | Fall back to pre-rendered 3D mannequin visualization | Banner: "Custom photo fitting temporarily busy; viewing on parametric mannequin" |
| WebGPU unsupported or context lost | Fall back to WebGL 2.0 shader or pre-recorded looping cloth motion | Seamless downgrade without crash; physics remain interactive via WebGL |
| Payment gateway (Stripe) down | Retain cart state and lock yardage inventory for 30 minutes | Notice: "Payment processing temporarily unavailable. Your yardage is reserved" |
| Web Audio API blocked or failed | Mute audio subsystem silently; disable haptic audio events | Visual feedback remains active without auditory interruption |

**Maintenance windows:** Planned zero-downtime rolling deployments occur on Tuesday/Thursday mornings at 04:00 UTC. User-facing alerts are displayed 24 hours prior to any scheduled operational database maintenance.

## Security

| ID | Control | Target / standard | Notes |
|---|---|---|---|
| NFR-020 | Authentication & Access | OWASP ASVS Level 2; mandatory MFA for atelier operators and admins | Argon2id for password hashing; WebAuthn supported |
| NFR-021 | Transport encryption | TLS 1.3 enforced (TLS 1.2 minimum); HSTS enabled with subdomains | Mixed content strictly blocked by Content Security Policy |
| NFR-022 | Data at rest | AES-256 GCM encryption for all database volumes, backups, and media buckets | Automatic customer-managed key rotation annually |
| NFR-023 | Ephemeral memory encryption | RAM-disk encryption for serverless GPU worker photo processing | Container destroyed after execution; zero swap disk writes |
| NFR-024 | Payment card compliance | PCI-DSS SAQ-A compliant | All credit card data tokenized via Stripe Elements; zero PAN on servers |
| NFR-025 | Input validation & injection | Strict schema validation; parameterized SQL queries; SVG sanitization | OWASP Top 10 automated mitigation via WAF |
| NFR-026 | Session management | Secure, HttpOnly, SameSite=Lax cookies with 14-day absolute expiry | Immediate session invalidation on password change or logout |
| NFR-027 | Vulnerability scanning | Daily automated CVE scanning; zero unresolved Critical or High vulnerabilities | Pinned lockfiles; weekly automated dependency updates |
| NFR-028 | Tamper-evident audit logging | Append-only audit logs for all administrative cut actions and privacy deletions | Retained for 365 days in immutable cloud storage |

## Model Quality & Cost

| ID | Capability | Feature | Metric | Threshold | Evaluation | Cost ceiling |
|---|---|---|---|---|---|---|
| NFR-030 | Multimodal Neural Dress Fitting | [FEAT-004](features/FEAT-004.md) | Tailoring Silhouette & Drape Fidelity | &ge; 92.0% approval score | 500-case golden benchmark evaluated by master tailors across 10 body types | &le; $0.045 per static render |
| NFR-031 | 360° Looping Neural Motion | [FEAT-006](features/FEAT-006.md) | Temporal Coherence & Mesh Integrity | SSIM &ge; 0.94; zero mesh tearing | 100-video evaluation suite verified by 3D animators | &le; $0.120 per 4-second video |
| NFR-032 | Generative Dye-Lab Color Fidelity | [FEAT-012](features/FEAT-012.md) | Color Match Accuracy (&Delta;E 2000) | &Delta;E &lt; 1.5 against physical standard | Spectrophotometer lab comparison across 50 printed silk/linen swatches | &le; $0.060 per print-ready tile |

## Privacy & Compliance

| ID | Regulation / standard | Applies because | Obligation | Evidence |
|---|---|---|---|---|
| NFR-040 | Illinois BIPA (740 ILCS 14/) | US customers uploading full-body photos | Written informed consent before upload; publicly posted retention schedule; automated destruction | Verifiable consent logs, ephemeral container destruction audit |
| NFR-041 | EU GDPR & UK GDPR | EU/UK customers; biometric and financial data | Lawful basis under Art. 6 & 9; right to erasure; DSR compliance; Data Protection Impact Assessment (DPIA) | Formal DPIA document, automated DSR workflow |
| NFR-042 | California CCPA / CPRA | California residents | Notice at collection; "Do Not Sell or Share My Personal Info"; non-discrimination | Privacy portal and deletion request log |
| NFR-043 | Texas CUBI (Bus. & Com. &sect; 503.001) | Texas residents capturing biometric identifiers | Explicit consent prior to capture; destruction within 1 year | Automated ephemeral lifecycle verification |

**Data lifecycle:**
| Data class | Retention period | Residency | Deletion mechanism |
|---|---|---|---|
| Ephemeral customer fitting photos | Maximum 15 minutes post-session | In-region volatile memory | Automatic cryptographic wipe on container termination |
| Saved customer wardrobe & measurements | Account lifetime + 30 days | US / EU multi-region | Hard-delete within 48 hours of user account closure |
| Fabric order, yardage, & cutting records | 7 years (statutory tax compliance) | Primary database | Archival cold storage with restricted audit-only access |
| Anonymized WebGPU interaction telemetry | 90 days, then aggregated | Cloud analytics warehouse | Automated rolling partition drop |

## Measurement & Verification

| ID | Verified by | When | Owner |
|---|---|---|---|
| NFR-001 | Lighthouse CI synthetic mobile test | Every pull request build | Frontend Engineering |
| NFR-002 | k6 distributed load testing suite | Pre-release staging gate | Backend Engineering |
| NFR-003 | WebGPU automated headless frame-time recorder | Weekly performance regression run | Graphics / 3D Engineering |
| NFR-004 | Distributed GPU latency and concurrency test | Continuous synthetic canary probe | Machine Learning Engineering |
| NFR-010 | Datadog uptime monitor + monthly SLO review | Continuous monitoring / monthly audit | Platform Reliability |
| NFR-020 | Third-party penetration test & OWASP audit | Annually prior to major release | Information Security |
| NFR-030 | Master Tailor Golden Benchmark Rubric | Per model checkpoint release | Machine Learning Engineering |
| NFR-040 | Biometric consent & ephemeral purge audit runbook | Quarterly compliance verification | Privacy & Legal Compliance |

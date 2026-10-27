# Risk Register

## Risk Assessment Scale

### Likelihood
| Score | Label | Definition |
|---|---|---|
| 1 | Rare | <5% probability during annual operations |
| 2 | Unlikely | 5–20% probability |
| 3 | Possible | 20–50% probability |
| 4 | Likely | 50–80% probability |
| 5 | Almost Certain | >80% probability without active intervention |

### Impact
| Score | Label | Definition |
|---|---|---|
| 1 | Negligible | Minor operational friction easily absorbed by standard workflows |
| 2 | Minor | Localized customer complaint or minor budget/timeline variance (<2 weeks) |
| 3 | Moderate | Material customer dissatisfaction, noticeable GPU cost surge, or inventory delay |
| 4 | Major | High financial loss, significant cutting room waste, or launch delay >4 weeks |
| 5 | Critical | Regulatory penalty, class-action privacy litigation, or severe brand damage |

### Risk Score
**Risk Score = Likelihood × Impact**

| Score Range | Severity | Action Required |
|---|---|---|
| 1–4 | Low | Periodic monitoring; standard operational controls |
| 5–9 | Medium | Proactive mitigation plan; monthly stakeholder review |
| 10–19 | High | Active engineering/legal mitigation; weekly executive tracking |
| 20–25 | Critical | Immediate product gating; mandatory operational tripwires |

## Risk Register

### Legal & Compliance Risks

| ID | Risk | L | I | Score | Mitigation | Contingency | Owner |
|---|---|---|---|---|---|---|---|
| R-001 | Biometric privacy regulatory enforcement or class-action litigation (Illinois BIPA / GDPR Art. 9) | 2 | 5 | 10 | Enforce affirmative informed consent before upload ([FEAT-005](features/FEAT-005.md)); process images in ephemeral encrypted RAM-disks; hard-delete photos within 15 minutes ([NFR-040](nfr.md)); retain zero facial biometric vector templates. | Instant geofenced shutdown of personal photo uploads in disputed jurisdictions; immediate automated fallback to 3D parametric mannequins; engage retained privacy counsel. | Privacy & Compliance Officer |

### Technical & Model Risks

| ID | Risk | L | I | Score | Mitigation | Contingency | Owner |
|---|---|---|---|---|---|---|---|
| R-002 | Cloud GPU inference cost runaway from high-volume non-converting visitor fitting sessions | 3 | 4 | 12 | Enforce strict quota of 3 free watermarked fittings per month on Free Tier ([monetization](monetization.md)); optimize model inference to &le; $0.045 per render ([NFR-030](nfr.md)); session IP rate-limiting. | Require phone number verification or a refundable $5 fitting deposit credited toward fabric orders after free quota exhaustion. | Machine Learning Lead |
| R-003 | WebGPU browser fragmentation or device GPU context loss causing cloth sandbox failure | 3 | 3 | 9 | Implement automated browser feature detection; provide progressive fallback to WebGL 2.0 compute shaders; recover GPU context automatically without page refresh. | Fall back seamlessly to high-resolution pre-rendered looping MP4 video clips demonstrating the fabric's movement. | 3D Graphics Lead |
| R-004 | Generative model hallucination causing anatomically implausible silhouettes or fabric clipping | 3 | 4 | 12 | Use two-stage pipeline combining strict 3D body pose estimation before neural draping; gate all model checkpoints with the 500-case Master Tailor Golden Benchmark ([NFR-030](nfr.md)). | Automated confidence threshold check (&lt;0.85 confidence triggers apology modal, prompts user for a cleaner photo, and serves a parametric 3D mannequin render). | Machine Learning Lead |

### Operational & Supply Chain Risks

| ID | Risk | L | I | Score | Mitigation | Contingency | Owner |
|---|---|---|---|---|---|---|---|
| R-005 | Cutting room measurement or grainline errors on non-returnable luxury textiles ($100–$350/yd) | 2 | 4 | 8 | Install overhead optical barcode projection cutting tables; require dual-cutter sign-off on orders &gt;3 yards; print grainline indicators directly on cutting tickets. | Maintain dedicated safety surplus on all core catalog rolls; provide 24-hour expedited replacement cut guarantee to customer with luxury gift credit. | Master Cutting Room Lead (Elena) |
| R-006 | Photometric stereo scanning bottleneck delaying seasonal fabric catalog onboarding | 3 | 3 | 9 | Establish standardized material scanning protocol; contract partner scanning labs in Milan, Paris, and London to digitize European mill collections on-site. | Launch new arrivals with high-resolution editorial photography and calibrated procedural PBR shaders while queueing high-res photometric scans. | Head of Textile Sourcing |
| R-007 | European and heritage textile mill supply chain delays leading to inventory stockouts | 3 | 4 | 12 | Enforce continuous-yardage distributed Redis locks in checkout to prevent dual-allocation; set automated reorder triggers when bolt falls below 8 yards. | White-glove concierge outreach to customer offering alternative sister mill rolls of identical GSM/fiber purity or full immediate refund. | Head of Operations |

### Market & Financial Risks

| ID | Risk | L | I | Score | Mitigation | Contingency | Owner |
|---|---|---|---|---|---|---|---|
| R-008 | Screen color and sheen expectation mismatch between display preview and physical dye lot | 3 | 3 | 9 | Heavily incentivize the $25 Swatch Presentation Box with 100% store credit; calibrate display color profiles to Delta E &lt; 1.5 ([NFR-032](nfr.md)); provide dynamic daylight/tungsten lighting toggles. | Enforce clear pre-checkout non-returnable disclaimer; contest unwarranted chargebacks using signed delivery tracking and cutting room QA proof. | Head of Customer Experience |
| R-009 | Customer hesitation to upload personal photographs due to body consciousness or privacy fear | 3 | 4 | 12 | Provide an instant, anonymous 3D mannequin option across 8 diverse anatomical body shapes; display plain-language, non-legalistic privacy guarantees directly on the dropzone. | Allow customers to upload reference garment photos or select from pre-photographed diverse human fitting models. | Product Manager |
| R-010 | Independent master tailors distrusting automated yardage calculations and demanding extra fabric | 2 | 3 | 6 | Format technical PDF specification cards ([FEAT-009](features/FEAT-009.md)) to international tailoring guild standards; display explicit pattern piece layout diagrams. | Incorporate an optional 0.5-yard "Tailor Peace-of-Mind Buffer" toggle in the automated yardage estimator ([FEAT-007](features/FEAT-007.md)). | Head of Tailor Partnerships |
| R-011 | Generalist image AI platforms releasing crude virtual try-on, degrading consumer perception | 4 | 3 | 12 | Differentiate aggressively on physical unsewn textile physics, certified mill provenance, exact yardage calculation, and direct master tailor handoff. | Double down on exclusive luxury mill partnerships, deadstock couture exclusivity, and curated white-glove atelier fulfillment. | Head of Product |

## Risk Trends

| Date | Change | Risk ID | Description |
|---|---|---|---|
| 2026-10-26 | Added | R-001 | Initialized BIPA/GDPR biometric compliance risk based on [overview.md](overview.md) regulatory exposure. |
| 2026-10-26 | Added | R-002 | Initialized GPU inference runaway cost risk based on [overview.md](overview.md) SWOT weakness. |
| 2026-10-26 | Added | R-003 | Initialized WebGPU browser fragmentation risk for client-side physics. |
| 2026-10-26 | Added | R-004 | Initialized neural drape hallucination risk for model-backed garment generation. |
| 2026-10-26 | Added | R-005 | Initialized cutting room measurement error risk on custom-cut textiles. |
| 2026-10-26 | Added | R-006 | Initialized fabric digitization bottleneck risk for catalog scaling. |
| 2026-10-26 | Added | R-007 | Initialized luxury mill supply chain lead-time volatility risk. |
| 2026-10-26 | Added | R-008 | Initialized screen-to-physical dye lot color calibration mismatch risk. |
| 2026-10-26 | Added | R-009 | Initialized user photo upload hesitation risk. |
| 2026-10-26 | Added | R-010 | Initialized tailor distrust of algorithmic yardage calculation risk. |
| 2026-10-26 | Added | R-011 | Initialized generalist try-on market commoditization risk. |

## Review Cadence

- **Weekly Standup:** Review all High risks (score &ge; 10: R-001, R-002, R-004, R-007, R-009, R-011) with engineering, design, and legal leads.
- **Monthly Operations Review:** Full risk register audit against live order claim rates, GPU inference expenditure, and supply chain lead times.
- **Milestone Gating:** Comprehensive risk re-assessment prior to exiting Phase 0 Foundation and Phase 1 Launch.

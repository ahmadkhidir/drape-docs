# Drape

**One-liner:** A sensory motion digital atelier where bespoke fashion begins with AI neural draping, interactive fabric physics, and custom yardage-to-tailor fulfillment.
**Status:** Complete (Specification)
**Interfaces:** Web

## Overview

Drape is a digital fabric atelier and e-commerce platform that allows customers to explore, simulate, and purchase luxury textiles. Users interact with physical textile simulations in real time via WebGPU and preview raw fabrics tailored onto their own bodies in bespoke dress styles using a multimodal neural draping engine. The platform bridges the divide between purchasing flat yardage and constructing bespoke occasionwear by estimating required fabric yardage and exporting production-ready specification sheets directly for tailors.

## The Problem

Purchasing luxury garment fabric online suffers from severe visualization uncertainty because buyers cannot predict how a flat, two-dimensional textile bolt will drape, reflect light, and fall across their specific body proportions in a chosen dress silhouette. Because custom-cut textiles are permanently non-returnable once severed from the bolt, consumers and designers face substantial financial risk ($150 to $1,500+ per cut) when attempting to commission bespoke occasionwear.

**How it's solved today:** Customers order small 2"x2" physical swatches by mail and wait days for delivery, attempt to drape swatches over arms in front of mirrors, consult physical garment district showrooms in select major cities, or risk purchasing yardage based purely on static, flat-lay e-commerce photography.

## The Solution

Drape solves this with a real-time, physics-based digital showroom combined with multimodal generative draping. Customers upload a full-body photograph, select any premium textile, and specify their desired dress style—either by choosing curated architectural silhouettes or entering natural language prompts and reference photos—to see the fabric rendered onto their own body with authentic physical drape, weight, and sheen. Integrated yardage calculators determine exact cuts based on garment complexity and body measurements, eliminating costly fabric waste and tailoring errors.

## Market & Competition

**Alternatives today:**
- [Mood Fabrics](https://www.moodfabrics.com) — Legacy leader in online fashion fabrics with expansive inventory, but reliant on static 2D product photos and flat swatch orders without garment visualization.
- [Tissura](https://tissura.com) — Global luxury haute couture textile supplier carrying European runway mills; high price point ($100–$800/yd) with traditional editorial photography and physical showroom consultations.
- [Britex Fabrics](https://britexfabrics.com) — Historic high-end San Francisco retailer offering online designer deadstock and woolens with conventional catalog filtering.
- [Fabrics & Fabrics](https://fabrics-fabrics.com) — Manhattan garment district specialist in designer runway deadstock and couture brocades, reliant on phone/email concierge styling.
- [DrapeAI](https://drapeai.app) — Emerging consumer virtual try-on software focusing on finished ready-to-wear apparel simulation rather than unsewn textile rolls and custom pattern cutting.

**Demand signal:** E-commerce apparel and textile return rates average 30% to 40% due to material and fit uncertainty, while high-fidelity generative virtual try-on deployments reduce returns by 20% to 40% and increase shopper conversion by up to 40% ([Marketing Tech News](https://marketingtechnews.net/news/2024/aug/06/the-role-of-virtual-try-on-technology-in-reducing-apparel-returns/); [VirtualTryOn ROI](https://virtualtryiton.com/blog/virtual-try-on-roi)).

**Platform/regulatory exposure:** User photo uploads require compliance with biometric privacy frameworks—specifically the Illinois Biometric Information Privacy Act ([740 ILCS 14/](https://www.ilga.gov/legislation/ilcs/ilcs3.asp?ActID=3004)) and EU GDPR Article 9—mandating written informed consent, transparent retention policies, and zero persistent facial template storage without user authorization.

**Verdict:** Proceed — The intersection of high-margin bespoke textiles ($50–$300+/yd) and generative neural garment draping addresses a high-stakes purchase barrier that conventional static fabric shops cannot solve.

## Target Audience

**Primary:** Bespoke occasionwear clients, gala and bridal patrons, and cultural couture enthusiasts (e.g., Aso Ebi, luxury bridal, Sari, bespoke suiting) who commission custom garments and need to visualize fabrics on themselves before purchasing expensive yardage.
**Secondary:** Independent fashion designers, couture dressmakers, and bespoke tailors seeking tactile client presentation tools and verifiable textile specifications.
**Not for:** Mass-market commodity sewing, industrial uniform manufacturers, discount synthetic craft yardage ($2–$5/yd), or shoppers looking for pre-assembled off-the-rack garments.

This customer base is selected because high-end occasionwear carries high emotional and financial stakes, making pre-purchase visualization essential while supporting unit economics that comfortably absorb GPU inference costs.

## Success Metrics & KPIs

| Metric | Definition | Baseline | Target | Timeframe | Measurement Spec |
|---|---|---|---|---|---|
| Atelier Conversion Rate | % of unique site visitors who purchase either swatches or fabric yardage | 1.2% (industry avg) | > 3.8% | 90 days post-launch | [analytics](analytics.md) |
| Neural Tailor Engagement | Average number of garment styles simulated per active visitor session | — | > 3.2 styles | 60 days post-launch | [analytics](analytics.md) |
| Swatch-to-Bolt Conversion | % of swatch sample box purchasers who subsequently order 3+ yards of fabric | 8.0% | > 22.0% | 120 days post-launch | [monetization](monetization.md) |
| Draping Inference Latency | P95 latency from style prompt/photo submission to completed neural garment render | — | < 3.8 seconds | Launch | [nfr](nfr.md) |
| Yardage Estimation Accuracy | % of tailor-completed orders reporting zero yardage shortfall or excess waste > 0.5 yd | — | > 95.0% | 180 days post-launch | [analytics](analytics.md) |

## SWOT Analysis

### Strengths *(internal, positive)*
- Proprietary multimodal neural draping pipeline that maps measured fabric physics (GSM weight, stiffness, surface reflectance) onto user body geometry.
- Real-time WebGPU tactile physics simulation providing 60 FPS interactive cloth manipulation directly in modern web browsers without plugins.
- Curated direct relationships with premium European and heritage global mills, providing verified physical textile metadata.
- End-to-end integration from digital simulation to yardage calculation and technical tailor spec export.

### Weaknesses *(internal, negative)*
- Cloud GPU inference costs for generative neural rendering create a non-zero per-session compute cost.
- Cold-start catalog constraints: high-fidelity simulation requires physical digitization (surface scanning, weight, tensile testing) for every fabric SKU.
- Dependent on user upload quality: poorly lit or occluded user photos can degrade neural try-on realism.
- Custom-cut fabric fulfillment requires high operational precision with zero tolerance for cutting errors.

### Opportunities *(external, positive)*
- Global bespoke and occasionwear market expanding across multicultural weddings, galas, and red-carpet events where personalized tailoring is mandatory.
- Browser adoption of WebGPU reaching critical mass across modern Chrome, Edge, and Safari browsers, enabling desktop-class 3D cloth physics.
- High dissatisfaction with current online fabric returns and static swatching workflows creating an eager early-adopter community.
- Expansion into vetted local tailor networks ("Send to Atelier") providing an incremental B2B service revenue stream.

### Threats *(external, negative)*
- Rapidly evolving state-level and international biometric privacy regulations increasing compliance complexity for user photo storage.
- Volatility and supply-chain lead times in luxury international textile shipping from European and Asian textile mills.
- Commoditization of generic image-to-image diffusion models by generalist platforms lacking physical textile rigor.
- Consumer skepticism regarding whether digital colors and textures on screen will accurately match physical dye lots.

## Scope

**In scope:**
- High-fidelity e-commerce catalog of premium natural, luxury, and heritage textiles (silks, wools, linens, brocades, jacquards, velvets).
- Browser-based WebGPU interactive cloth physics sandbox (drag, stretch, wave, ripple, and fold).
- Microscopic yarn-level weave inspector with dynamic directional lighting and sheen simulation.
- Multimodal Neural Tailor: User photo upload + silhouette picker / natural language prompt &rarr; neural garment drape on user body.
- Automatic yardage and pattern layout estimation based on chosen dress silhouette and body measurements.
- Technical tailor specification sheet generation (PDF export with yardage, grainline advice, and 3D preview).
- Sample swatch orders and cut-to-order yardage purchasing with luxury packaging.

**Out of scope (for now):**
- 360-degree looping motion walk animations (Phase 2).
- Reactive spatial audio and tactile soundscape (Phase 2).
- Vetted Master Tailor Concierge / "Send to Atelier" partner fulfillment network (Phase 2).
- Custom on-demand pattern printing and AI dye-lab colorway generator (Phase 3).
- Native iOS/Android mobile apps (web-first responsive architecture prioritized).

**Explicit non-goals:**
- Ready-to-wear finished apparel manufacturing or inventory holding.
- Cheap synthetic crafting supplies or mass commodity wholesale bolts.
- Fully automated algorithmic robotic sewing or garment assembly.
- Social media influencer marketplace or user-generated fast-fashion design copying.

## Assumptions & Dependencies

**Assumptions** — believed true; if wrong, the plan changes:
| # | Assumption | Risk if false | Validated? |
|---|---|---|---|
| A1 | Consumers will comfortably upload a full-body photo if guaranteed strict ephemeral privacy and immediate visual value. | Users abandon the Neural Tailor, forcing fallback to generic mannequin models. | No — requires onboarding usability validation. |
| A2 | Physical fabric suppliers will reliably provide or permit lab testing for GSM, fiber composition, and tensile metrics. | Simulation inaccuracies lead to discrepancy between digital drape and physical reality. | Partially — confirmed with initial mill partners. |
| A3 | Average order margins on luxury cut yardage ($200–$800) easily exceed cloud GPU inference costs (~$0.02–$0.05 per render). | Unit economics fail if free visitors spam the neural renderer without purchasing. | Yes — validated against cloud serverless GPU pricing. |
| A4 | Independent tailors will accept and appreciate standardized digital specification sheets and yardage calculations. | Tailors reject estimates and demand clients buy excessive safety yardage anyway. | No — requires interviews with master tailor guild members. |

**Dependencies** — external and blocking, not under the team's control:
| # | Dependency | Type | Blocks | Status |
|---|---|---|---|---|
| D1 | Serverless GPU provider with sub-second cold-start container spin-up (e.g., RunPod, Modal, or AWS Inferentia). | Infrastructure | Neural Tailor launch | Active vendor evaluation |
| D2 | WebGPU standard browser support stability across mobile WebKit and Chromium. | Platform | Real-time cloth sandbox | Supported on modern Chromium/Safari; WebGL fallback required |
| D3 | High-resolution physical textile digitization scanner access (photometric stereo / PBR material capture). | Hardware / Operations | Fabric catalog onboarding | Sourced via partner scanning lab |
| D4 | Merchant payment processor supporting custom fractional yardage billing and fraud prevention. | Vendor | E-commerce checkout | Stripe integration standard |

## Documentation

| Document | Purpose |
|---|---|
| [overview](overview.md) | Product definition, market justification, scope boundaries, and core KPIs |
| [user-personas](user-personas.md) | Researched customer personas, operator requirements, and anti-personas |
| [branding](branding.md) | Brand identity, design character, mark system, design tokens, and asset direction |
| [features](features.md) | Prioritized feature catalog, user stories, acceptance criteria, and model contracts |
| [nfr](nfr.md) | Non-functional quality targets, performance budgets, model quality bars, and privacy obligations |
| [roadmap](roadmap.md) | Phased delivery milestones, Gantt timeline, and business outcome sequencing |
| [architecture](architecture.md) | System components, WebGPU and GPU inference pipelines, data architecture, and C4 topology |
| [monetization](monetization.md) | Revenue model, pricing tiers, feature gate mapping, and billing policies |
| [risk-log](risk-log.md) | Risk register, assessment scoring, proactive mitigations, and operational tripwires |
| [user-flow](user-flow.md) | User journeys, Mermaid flowcharts, decision trees, and global navigation gates |
| [screens](screens.md) | Screen inventory, navigation map, shared UI patterns, and 10 detailed screen specifications |
| [schema](schema.md) | Authoritative relational data model, ER topology, and JSON Schema 2020-12 entities |
| [analytics](analytics.md) | Telemetry taxonomy, conversion funnels, error monitoring, and executive KPI reporting |
| [operations](operations.md) | Operational support SLAs, cutting room runbooks, and incident response governance |
| [release](release.md) | Release strategy, environment promotion pipeline, feature flags, rollback triggers, and go-live gates |

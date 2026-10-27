# Revenue Model

## Revenue Model

**Model Type:** Hybrid Direct E-Commerce + Swatch Credit Model + Professional Atelier SaaS + Marketplace Commission

**Summary:**
Drape generates primary revenue through the high-margin direct sale of physical luxury textiles cut to measure ($45 to $350+/yard) and curated luxury swatch presentation boxes ($25, fully credited toward subsequent fabric purchases). Secondary revenue streams include a professional B2B software subscription for independent couture ateliers ($89/month for client presentation tools and bulk pricing), a 12% marketplace commission on bespoke tailor bookings ("Send to Atelier"), and custom on-demand printing surcharges in the Generative Dye-Lab.

## Pricing Tiers

### Free Tier: Guest Explorer
**Price:** $0 / month
**Target:** Occasionwear buyers and first-time brides ([Amara Okafor](user-personas.md)) exploring possibilities.
**Purpose:** Acquisition channel to demonstrate the tactile physics and neural draping value proposition, eliminating purchase hesitation.
**Includes:**
- Full catalog access, fabric filtering, and composition metadata ([FEAT-001](features/FEAT-001.md))
- Unlimited real-time WebGPU cloth physics simulation and Micro-Weave inspection ([FEAT-002](features/FEAT-002.md), [FEAT-003](features/FEAT-003.md))
- Basic automated yardage and pattern calculator ([FEAT-007](features/FEAT-007.md))
- Up to 3 Neural Tailor custom dress fittings per calendar month ([FEAT-004](features/FEAT-004.md)) with subtle watermark
- Biometric consent and automated 15-minute photo deletion protection ([FEAT-005](features/FEAT-005.md))

**Limitations:**
- Neural fittings carry a translucent "Drape Atelier Preview" watermark
- No 360° motion video walk generation ([FEAT-006](features/FEAT-006.md))
- Maximum 3 fittings per month without a fabric order or swatch purchase
- Standard non-priority GPU rendering queue

### Transactional Tier: Atelier Client
**Price:** $25 per Swatch Presentation Box (100% credited toward fabric purchases) + Fabric Cut by the Yard ($45–$350/yd)
**Target:** Bespoke occasionwear clients and suiting patrons ([Amara Okafor](user-personas.md), [Marcus Sterling](user-personas.md)).
**Purpose:** Core commercial e-commerce revenue driver with high average order values ($200–$1,200).
**Includes:**
- Everything in Free Explorer, plus:
- Unlocks 60 days of unlimited, un-watermarked high-resolution Neural Tailor fittings ([FEAT-004](features/FEAT-004.md))
- Precision cut yardage to 1/8th of a yard with verified dye-lot matching ([FEAT-008](features/FEAT-008.md))
- Full technical PDF tailor specification dossier export ([FEAT-009](features/FEAT-009.md))
- Access to 360° looping neural motion walk previews ([FEAT-006](features/FEAT-006.md))
- Concierge routing to vetted local master tailors ([FEAT-010](features/FEAT-010.md))
- Archival packaging with cedar and silk ribbon presentation

### Subscription Tier: Couture Studio Pro
**Price:** $89 / month (or $890 / year with 2 months free)
**Target:** Independent fashion designers, couture ateliers, and bespoke dressmakers ([Julien Moreau](user-personas.md)).
**Purpose:** High-retention recurring revenue from professional practitioners who use Drape daily for client consultations.
**Includes:**
- Everything in Atelier Client, plus:
- Unlimited client fitting sessions with multi-client project folders
- Studio Presentation Mode (hides wholesale margins and technical debug data for live client fittings)
- Priority GPU inference queue (<2.5s P95 render latency)
- Tiered wholesale bolt pricing (15% off orders 10–24 yards; 25% off full bolts 25+ yards)
- Access to the Generative Dye-Lab for AI pattern rescaling and bespoke colorway printing ([FEAT-012](features/FEAT-012.md))
- Dedicated cutting room liaison ([Elena Rostova](user-personas.md)) and priority sample dispatch

## Feature Gate Mapping

| Feature ID | Feature | Guest Explorer | Atelier Client | Couture Studio Pro |
|---|---|---|---|---|
| [FEAT-001](features/FEAT-001.md) | Luxury Fabric Catalog & Filtering | Yes | Yes | Yes |
| [FEAT-002](features/FEAT-002.md) | WebGPU Cloth Physics Sandbox | Unlimited | Unlimited | Unlimited |
| [FEAT-003](features/FEAT-003.md) | Micro-Weave Inspector | Unlimited | Unlimited | Unlimited |
| [FEAT-004](features/FEAT-004.md) | Neural Dress Fitting | 3 / month (Watermarked) | Unlimited for 60 days | Unlimited (Priority Queue) |
| [FEAT-005](features/FEAT-005.md) | Biometric Consent & Ephemeral Purge | Yes | Yes | Yes |
| [FEAT-006](features/FEAT-006.md) | 360° Looping Neural Motion Walk | No | Yes (with fabric purchase) | Unlimited |
| [FEAT-007](features/FEAT-007.md) | Yardage & Pattern Spec Estimator | Standard | Detailed | Full atelier cutting layout |
| [FEAT-008](features/FEAT-008.md) | Cut Yardage & Swatch Checkout | Swatches only | 1/8 yard cuts | Bolt wholesale discounts |
| [FEAT-009](features/FEAT-009.md) | Digital Wardrobe & PDF Spec Export | Summary only | Full PDF Dossier | White-label studio branding |
| [FEAT-010](features/FEAT-010.md) | "Send to Atelier" Concierge | No | Yes | Partner tailor portal access |
| [FEAT-011](features/FEAT-011.md) | Haptic Spatial Audio | Yes | Yes | Yes |
| [FEAT-012](features/FEAT-012.md) | Generative Dye-Lab & Print Scaler | Preview only | No | Full production ordering |
| [FEAT-013](features/FEAT-013.md) | NFC & AR Swatch Box Projection | No | Included with swatch box | Multi-swatch studio kit |

## Payment & Billing

**Payment Processing:**
- **Primary Web Processor:** Stripe (Stripe Elements, Apple Pay, Google Pay, Credit/Debit cards).
- **Buy Now, Pay Later (BNPL):** Klarna and Afterpay integration enabled for high-value fabric orders ($250–$2,000) to smooth wedding/gala cash flow.
- **European Bank Rails:** SEPA Direct Debit and iDEAL supported for European couture atelier orders.

**Billing Cycle:**
- Fabric yardage, swatches, and concierge fees are billed as immediate one-time transactions.
- Couture Studio Pro is billed monthly ($89) or annually ($890 with a 17% discount).

**Currency Support:**
- Multi-currency native checkout: USD ($), EUR (€), GBP (£), and NGN (₦).
- Exchange rates are anchored to daily bank mid-market rates with prices rounded to luxury psychological thresholds (e.g., $125.00, €115.00, £95.00).

**Tax Handling:**
- Automated global sales tax and VAT calculation via Stripe Tax.
- US: Destination-based state sales tax collected where Drape maintains economic nexus.
- EU/UK: Destination VAT calculated; EU B2B reverse-charge mechanism validated via VIES for registered design studios with VAT IDs.

**Dunning & Studio Subscriptions:**
- Failed subscription renewals retry on days 1, 3, and 5 with automated email notification.
- Studio access remains active during a 5-day grace period; if unpaid by day 7, the account downgrades to Guest Explorer.

**Invoices & Receipts:**
- Automated PDF tax invoices containing fabric roll numbers, dye-lot batch codes, and cutting lengths dispatched immediately via email.

**Billing Events:**
- **Upgrade to Studio Pro:** Immediate charge with instant access to wholesale pricing and Dye-Lab tools.
- **Cancellation of Studio Pro:** Access persists until the end of the paid billing cycle, then reverts to Guest Explorer without loss of saved past orders.
- **Swatch Credit Redemption:** Purchasing a $25 Swatch Box issues a unique digital credit coupon applied automatically against any fabric yardage order placed within 30 days.

## Billing Operations & Fraud Policy

| Area | Policy |
|---|---|
| **Refund Window on Cut Yardage** | **Strictly Non-Returnable.** All fabric cut to measure from the bolt is final sale and non-refundable once severed. |
| **Defective Yardage Claims** | Customers have 7 calendar days from delivery to report verified cutting room errors, continuous weave snags, or dye-lot defects with photographic proof. Approved defects receive immediate full replacement cut or 100% refund. |
| **Swatch Box Returns** | Swatch sample presentation boxes are non-returnable; the $25 fee is 100% redeemable as store credit toward full yardage. |
| **Chargeback Response** | Contested aggressively with signed carrier proof of delivery, cutting room measurement audit logs, and digital order confirmation receipts. |
| **Fraud Triggers** | Orders exceeding $1,200 with mismatched shipping and billing countries trigger an automated 2-hour fraud review and require 3D Secure verification. |
| **Proration** | Upgrades between monthly and annual Studio Pro plans are prorated to the exact remaining days. |

## Key Metrics

| Metric | Definition | Target |
|---|---|---|
| **Swatch-to-Bolt Conversion** | % of swatch box buyers who purchase 3+ yards within 30 days | > 22.0% |
| **Average Order Value (AOV)** | Mean gross transaction value per completed fabric checkout | > $420.00 |
| **Fabric Gross Margin** | (Gross Fabric Revenue - Mill Cost of Goods) / Gross Fabric Revenue | > 58.0% |
| **Neural Tailor Session Conversion** | % of visitors who simulate a garment and place an order | > 6.5% |
| **Studio Pro MRR** | Monthly recurring revenue from active couture atelier subscribers | > $45,000 within 12 months |
| **Cutting Defect Claim Rate** | % of fulfilled orders reporting verified physical flaws | < 0.35% |

## Monetization Roadmap

| Phase | Roadmap Phase | Monetization Milestone |
|---|---|---|
| **Phase 1** | Launch Essentials | Direct physical fabric sales by the yard, $25 Swatch Box credit program, and Stripe multi-currency checkout. |
| **Phase 2** | Growth & Atelier Network | Launch Couture Studio Pro ($89/mo) and activate the 12% "Send to Atelier" concierge booking commission. |
| **Phase 3** | Connected Scale | Launch custom on-demand generative print fees ($28/yd surcharge) in the Dye-Lab and commercial AR swatch kits. |

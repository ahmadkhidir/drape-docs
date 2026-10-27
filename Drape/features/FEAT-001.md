## FEAT-001: Luxury Fabric Catalog & Multimodal Filtering

**Priority:** P0
**Driver:** Amara Okafor
**Effort:** M
**Depends On:** None

**User Story:**
As Amara Okafor, I want to browse and filter a curated collection of luxury textiles by fiber composition, weave structure, weight (GSM), and occasion so that I can quickly find the exact fabric suitable for my bespoke event gown.

**Description:**
A high-performance digital textile showroom presenting luxury European and heritage fabrics. Each fabric profile displays verified composition data (e.g., 100% Mulberry Silk, Super 150s Wool), certified GSM weight, physical width, origin mill, transparency rating, and physical drape classification. Users can filter by structured parameters or search via natural occasion terms (e.g., "black tie gown", "summer linen suit", "bridal veil").

**Acceptance Criteria:**
- **Given** an active visitor on the catalog page,
  **When** the user applies filters for "Silk" and "GSM > 250",
  **Then** the catalog displays only matching heavy silks (e.g., Silk Jacquard, Silk Gazar, Heavy Crepe) within 150ms.
- **Given** a user viewing an individual fabric detail view,
  **When** the page loads,
  **Then** the interface displays verified physical metrics including GSM weight, fabric width in inches/cm, fiber composition, stretch percentage, and weave category.
- **Given** a fabric SKU with low stock (<5 yards remaining on the active bolt),
  **When** viewed in the catalog,
  **Then** a `warning` badge indicates the remaining bolt length to prevent unfulfillable bespoke orders.

**Edge Cases & Failure States:**
- Network latency or search API disconnect &rarr; Displays cached top-tier textiles with a graceful retry banner; client filters cached items locally.
- Zero search results matching multi-criteria filter &rarr; Displays an editorial empty state offering adjacent fiber alternatives and an option to reset filters.

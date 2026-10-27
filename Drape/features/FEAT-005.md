## FEAT-005: Biometric Consent & Ephemeral Image Lifecycle

**Priority:** P0
**Driver:** Regulatory (Illinois BIPA / GDPR Art. 9)
**Effort:** S
**Depends On:** None

**User Story:**
As a privacy-conscious user and compliance officer, I want Drape to obtain explicit informed consent before processing my photo and automatically delete my biometric image data immediately after rendering so that my personal identity is never compromised or stored without permission.

**Description:**
A comprehensive privacy governance workflow compliant with the Illinois Biometric Information Privacy Act ([740 ILCS 14/](https://www.ilga.gov/legislation/ilcs/ilcs3.asp?ActID=3004)) and EU GDPR Article 9. Before any customer photograph is uploaded to the Neural Tailor, a modal presents clear, plain-language disclosure detailing that the photo is used exclusively for real-time garment draping simulation. Uploaded photos are processed in encrypted volatile memory and permanently purged from serverless inference containers immediately upon render completion. No persistent facial recognition templates, vector embeddings, or raw user portraits are stored unless the user explicitly opts in to save their profile to a secure digital wardrobe.

**Acceptance Criteria:**
- **Given** a user attempting to use the Neural Tailor for the first time,
  **When** they initiate a photo upload,
  **Then** a dedicated biometric consent modal appears requiring an explicit affirmative click before any file transfer occurs.
- **Given** an ephemeral fitting session,
  **When** the neural garment render is delivered to the client,
  **Then** the raw user upload is deleted from object storage within 15 minutes of session termination.
- **Given** an audit request from an authenticated user or compliance officer,
  **When** requesting data deletion,
  **Then** all associated renders and session logs are completely expunged with an automated cryptographic confirmation certificate.

**Edge Cases & Failure States:**
- User declines biometric consent &rarr; The photo upload is disabled, and the Neural Tailor seamlessly switches to a library of diverse 3D mannequin body types (petite, athletic, curvy, tall) allowing full silhouette and fabric experimentation without personal photo requirements.

# SSA HIT — Technical Integration Reference

Detailed technical specifications for architects integrating with SSA's
medical evidence collection systems.

---

## Network Protocol

SSA's current HIT protocol is **SOAP-based IHE XCA (Cross-Community Access)**
— not REST, not FHIR APIs.

**Message sequence:**
1. Patient Discovery Request (PDQ)
2. Initial Access Control Decision (SSA verifies 827 authorization)
3. Query for Documents Request (for Access Consent document)
4. Retrieve Documents Request (for Access Consent)
5. Final Access Control Decision
6. Patient Discovery Response
7. Query for Documents Request (for Clinical Document)
8. Retrieve Documents Response (clinical record returned)

Also supports **Deferred Patient Discovery (DPD)** for asynchronous responses.

**Referenced specifications (all from 2010-2011):**
- Access Consent Policies Production Spec v1.0
- Authorization Framework v3.0
- Query for Documents v3.0
- Retrieve Documents v3.0
- Patient Discovery v2.0
- Messaging Platform v3.0

Partners must be **eHealth Exchange members** to connect to SSA.
TEFCA is modernizing the directory layer but not changing the underlying
IHE XCA messaging protocol in the near term.

**SSA Security Assertion fields required:**
- Subject ID
- Subject Organization
- Subject Organization ID
- Home Community ID
- Subject Role
- Purpose of Use (government benefits determination)
- Patient Identifier
- Authorization Decision Statement

---

## Accepted Document Formats

### Structured (CCDA/CCD)

SSA accepts these 22 document types (Implementation Guide v5.0, Oct 2017):

| Document | Standard | Notes |
|----------|----------|-------|
| CCD | HL7 CCD | Base continuity of care document |
| HITSP/C32 | HITSP | Legacy format still accepted |
| CCDA R1.1 CCD | CCDA R1.1 | Preferred structured format |
| CCDA R1.1 History and Physical | CCDA R1.1 | |
| CCDA R1.1 Consultation Note | CCDA R1.1 | |
| CCDA R1.1 Diagnostic Imaging Report | CCDA R1.1 | Narrative only — no DICOM |
| CCDA R1.1 Procedure Note | CCDA R1.1 | |
| CCDA R1.1 Operative Note | CCDA R1.1 | |
| CCDA R1.1 Discharge Summary | CCDA R1.1 | |
| CCDA R1.1 Progress Note | CCDA R1.1 | |
| CCDA R2.1 Care Plan (V2) | CCDA R2.1 | |
| CCDA R2.1 Consultation Note (V3) | CCDA R2.1 | |
| CCDA R2.1 CCD (V3) | CCDA R2.1 | |
| CCDA R2.1 Diagnostic Imaging Report (V3) | CCDA R2.1 | Narrative only |
| CCDA R2.1 Discharge Summary (V3) | CCDA R2.1 | |
| CCDA R2.1 History and Physical (V3) | CCDA R2.1 | |
| CCDA R2.1 Operative Note (V3) | CCDA R2.1 | |
| CCDA R2.1 Procedure Note (V3) | CCDA R2.1 | |
| CCDA R2.1 Progress Note (V3) | CCDA R2.1 | |
| CCDA R2.1 Referral Note (V3) | CCDA R2.1 | |
| CCDA R2.1 Transfer Summary (V2) | CCDA R2.1 | |
| CCDA R2.1 Patient Generated Document (V2) | CCDA R2.1 | |

**FHIR R4 is NOT in SSA's current accepted standard.**

### Unstructured (native documents)

Accepted via ERE or as CCDA nonXMLBody wrapper:
MSWORD, PDF, Plain Text, RTF, HTML, GIF, TIF/TIFF, JPEG, PNG

**Constraints:**
- No password protection or encryption
- No hyperlinks or embedded media
- No DICOM images (DICOM narrative text accepted)
- No external file references
- Preferred scan: 200 DPI, bitonal, CCITT Group 4 compression
- Portrait orientation, US Letter (8.5" x 11")

### Content preferences
- SSA prefers data as **text** over images for dynamically generated documents
- Narrative block ordered **reverse chronologically** (most recent first)
- No HL7 2.x message delimiters — must convert to CDA elements
- Valid XML required — special characters must be encoded (&lt; etc.)

---

## Clinical Content Requirements (Form SSA-680)

Required clinical sections (from SSA's Content Checklist):

**Core clinical:**
- Problems (condition name, diagnosis code, dates, provider)
- Encounters (all healthcare encounters, dates, type, location)
- Procedures (all interventional/diagnostic/therapeutic)
- Results (labs, diagnostics — structured entries preferred)
- Medications
- Vital Signs
- Physical Exam
- Mental Status
- Functional Status
- Social History
- History of Past Illness
- Assessment and Plan

**Specialty documents assessed:**
- Audiology / Audiograms
- Cardiology (angiogram, cath, EKG, echo, stress test, Holter)
- Neurology (EEG, EMG, myelogram)
- Ophthalmology (visual acuity, visual fields)
- Radiology interpretations (CT, MRI, PET, X-ray) — NO images
- Respiratory (DLCO, PFT, spirometry)
- Surgical diagnostics (bone marrow, colonoscopy, endoscopy)
- Psychology / neuropsychological testing
- Mental status evaluations

**Sensitive content (required but complex):**
- Substance abuse records (42 CFR Part 2)
- Mental/behavioral health records
- HIV status
- Psychotherapy notes (HIPAA exclusion — additional authorization required)

SSA explicitly states: "A large portion of disability claims are mental/behavioral
in nature, which requires SSA to request information that may be marked as sensitive."

---

## CEF Structure

Records in the Certified Electronic Folder (CEF) are organized by color-coded sections:

- **Yellow section** — Medical evidence (HIT MER, HIT Extract, imaged medical records)
- **Blue section** — HIT Request and HIT Response documents (status tracking)
- Other sections — Non-medical evidence, administrative documents

When MEGAHIT fires, it places a **HIT Request** document in the blue section
containing: listed EDCS sources, HIE(s) processing, requested date range, request date.

If records received: formatted as **HIT MER** or **HIT Extract** in yellow section.
If no response: **HIT Response** document in blue section. No retry.

---

## VA-SSA Technical Pipeline

**Connection:** Federal JHIE → eHealth Exchange → MEGAHIT
**Live since:** November 11, 2016 (Veterans Day announcement)
**Authorization:** Electronic e-827 required — wet signature blocks pipeline

**Standard Health Summary content limits (POMS DI 22505.022):**

| Content Type | Limit |
|-------------|-------|
| Outpatient visits | 150 |
| Progress notes | 40 |
| Surgery reports | 10 |
| Procedures | 15 |
| Radiology/Nuclear Medicine | 10 |
| Lab results (chemistry/hematology) | 20 |
| Inpatient discharge summaries | 5 (or 4 years) |
| C&P examinations | 5 (or 4 years) |
| Coverage period | Most recent 2 years |

Note: Standard summary encompasses ALL VA sites (not just one facility).
MPRO can request modified summary tailored to DDS needs.

**DoD escalation chain (POMS DI 22505.023):**
1. MEGAHIT auto at case transfer (5-hour response window)
2. User Trigger via DCPS standalone app (5-hour response)
3. ERE eOR to DoD Central Location (10-day window)
4. Mail to MTF or NPRC (90-day follow-up for NPRC)

---

## Security and Authorization

**SSA's legal authority:** Privacy Act (not HIPAA — SSA is not a covered entity)
**Patient authorization:** Form SSA-827 (Authorization to Disclose Information to SSA)

**e-827 requirements:**
- Must be electronically signed (not wet signature) for MEGAHIT/VA/DoD
- Must be present in EDCS before automated request fires
- Valid for 12 months from signing date
- Cannot be reused across adjudicative levels
- Must be re-executed at hearing level (cannot use DDS-level 827)

**HIPAA interaction:**
SSA-827 authorizes HIPAA-covered providers to disclose PHI to SSA under
45 CFR 164.512(k) — disclosure to government agencies for their functions.
Sensitive records (42 CFR Part 2, psychotherapy notes) require additional
specific authorization beyond the standard 827.

**FedRAMP:**
Required for any cloud-hosted system integrating with SSA.
Impact level: High likely required for CEF access (disability claimant PII/PHI).
DCPS is cloud-hosted (FedRAMP posture not publicly documented).

---

## Infrastructure Notes

**SSA National Support Center (NSC):** Urbana, Maryland
Modern data center built with ~$500M Recovery Act funding; replaced old NCC
in Woodlawn, MD. Core SSA systems including MEGAHIT receiver hosted here.

**DCPS:** Cloud-hosted. FedRAMP authorized (details not public).
SSA paused DCPS modernization August 2025 due to budget/staffing.

**Government shutdown risk:**
October 2025 shutdown paused all SSA data connections.
No mechanism to maintain contractor connections during shutdown under
current appropriations law. Vendor SLAs must explicitly address this.

**$30M TMF grant:** October 2024 — Technology Modernization Fund IT upgrade
grant. Indicates active modernization budget despite Aug 2025 pause.

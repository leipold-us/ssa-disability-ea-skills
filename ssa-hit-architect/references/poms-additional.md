# Additional POMS Sections — SSA Medical Evidence Collection

Four POMS sections relevant to architects integrating with SSA's
evidence collection workflow. All fetched April 2026.

---

## DI 22505.006 — Requesting Evidence, General
**Effective: March 14, 2023 | TN 52 (01-26) | Batch run: April 3, 2026**

This is the umbrella policy governing all MER development. Most recently
touched January 2026 (TN 52), making it one of the most current sections.

### MEGAHIT automated request — period covered

For **initial-level** cases, automated request covers:
- Title II or concurrent: 12 months prior to POD (Potential Onset Date) to date of request
- Title XVI only: 12 months prior to protective filing date to date of request

For **reconsideration-level** cases:
- Period from date of last HIT request at initial level to date of new request
- **If no prior HIT request exists, HIT will NOT create an automated reconsideration request**
- DDS must manually create a User Trigger request

For **Continuing Disability Reviews (CDR):**
- 12 months prior to date of request

### User-triggered request — when to create

DDS creates User Trigger via DCPS or the MEGAHIT website when:
- No response to automated HIT request after **5 hours**
- Retrieval/conversion error occurred
- Automated response is insufficient (period not covered, document list blank)
- Automated request did not occur at reconsideration level
- Prior 827 issue has been resolved
- HIT partner identified as source *after* FO transferred the case
- Additional records needed after receipt of automated response

**Cap: 10 user-triggered requests to all HIT partners per adjudicative level**

**Note on wet-signed 827:** Valid for HIT partners for **9 months** from signature date
(not 12 months as stated in some other sources). Some partners only accept e-827.

### When to use traditional (non-HIT) requests to HIT partners

HIT is preferred. Use traditional requests only when:
- HIT response indicates claimant cannot be found (identity failure)
- HIT partner does not share sensitive records
- Policy requires **graphical evidence** (images/tracings) for abnormal testing
- MC indicates graphical evidence needed

**Graphical evidence — mandatory traditional request when testing is abnormal:**
- Visual field tests
- Audiograms
- Pulmonary function tests (PFT)
- Cardiac stress tests

**Graphical evidence — may also need traditional request:**
- Electrocardiograms (ECG) when required for cardiovascular listing
- Doppler studies or Holter monitors (when MC requests)

**Architect implication:** HIT standard documents do not include graphical tracings.
Even a perfectly connected HIT partner cannot deliver these electronically —
a traditional request is required for abnormal visual fields, PFTs, audiograms,
and cardiac stress tests. This is a structural gap in HIT coverage for the most
common disability-relevant diagnostic tests.

### Development procedure

Before requesting evidence, DDS must:
1. Review current folder for existing development
2. Check prior paper and electronic folders to avoid duplicates
3. Copy relevant evidence from prior folders

When requesting, perform all development actions concurrently (ERE, HIT, fax, mail, phone).

Do NOT make routine requests when:
- Medical source is deceased or retired (unless records transferred)
- Source is consistently uncooperative
- Evidence clearly unrelated to impairment (e.g., routine dental care)

---

## DI 81020.020 — Electronic Case Development
**Effective: September 10, 2021 | TN 24 (09-21)**

Governs case development procedures for CEF cases generally.
More recent than DI 81020.060 (2011) — updated 2021.

### Key provisions

**Correspondence for CEF cases must include:**
- DMA (Document Management Architecture) barcode with indexing information
- DDS P.O. Box of contract scanner as return address
- At DDS discretion: DMA fax number for direct-to-CEF faxing

**SSA-3369 (Work History Report):**
- Propagates automatically from EDCS SSA-3368 (Disability Report)
- DE must check CEF for existing SSA-3369 before developing
- Located in eView: Case Documents → Section E → Work History Report

**MEGAHIT reference (Section E, per cross-reference DI 81020.020E):**
This section cross-references the HIT-specific provisions including:
User Trigger procedures and MEGAHIT website access.

### Architect implication
DMA barcodes are the mechanism by which faxed documents auto-upload to CEF.
If a vendor sends fax with a properly formatted DMA barcode, it uploads
automatically without manual DDS intervention. Without barcode: manual indexing required.

---

## DI 81020.110 — Medical Evaluation
**Effective: April 17, 2025 | TN 39 (04-25)**

Most recently updated POMS section found — April 2025.
Governs how Medical Consultants (MC) and Psychological Consultants (PC)
evaluate disability cases.

### Key provisions

**Examiners must evaluate electronic cases by reviewing imaged documents
stored in the CEF** — this directly confirms the TIFF/PDF image workflow
at the examiner level. Structured data is not presented to reviewers.

**Medical assessments prepared in DCPS:**
- SSA-538 (Childhood Disability Evaluation Form)
- SSA-416 (Medical Evaluation)
- SSA-2506-BK (Psychiatric Review Technique — PRT)
- SSA-4734-F4 (Physical Residual Functional Capacity — RFC Assessment)
- SSA-4734-F4-SUP (Mental Residual Functional Capacity — MRFC Assessment)

All assessments require **electronic signature** in DCPS.
If paper version used instead: wet signature + scanned into CEF.

**Medical tracings (EKG, PFT, etc.):**
Images of tracings acceptable for medical evaluation even if image somewhat
distorts scale, as long as scale is displayed and grid lines viewable.

### Architect implication
This section (April 2025) is the most recent confirmation that:
1. Examiners work from images, not structured data
2. All formal medical assessments are created in DCPS — DCPS is the
   system of record for determinations, not just case management
3. Any AI decision support layer must output to DCPS-compatible format
   OR display alongside the imaged record in eView

RFC and PRT assessments (the actual disability determination forms) are
DCPS-native. An intelligence layer that produces structured output aligned
to RFC criteria would have the highest integration value here.

---

## DI 22505.035 — Follow-up on MER Requests
**Effective: April 15, 2024 | TN 46 (07-24)**

Governs follow-up procedures when providers don't respond. Updated 2024.

### Standard follow-up procedure

**For regular claims:**
- Initiate one follow-up request per unresponsive source
- Timing: between **10 and 20 calendar days** after initial request
- Allow at least **10 additional calendar days** for response to follow-up
- Allow more time based on experience with that source

**For Compassionate Allowances (CAL) and Quick Disability Determinations (QDD):**
(Expedited cases — likely shorter windows, consistent with priority processing)

**Follow-up methods (all constitute successful attempt):**
- Mail letter
- Fax letter
- Phone call (speaking to source)
- Phone call leaving voicemail (detailed message)

**You are NOT required to follow up** solely to obtain a medical opinion.
Recontact for functional abilities and limitations if needed to adjudicate.

### Architect implication

The 10-20 day follow-up window combined with 10-day response window means
a non-responding provider adds **20-30 days minimum** to case processing.
At scale across millions of claims, the aggregate delay from non-responders
is enormous.

A vendor solution that eliminates non-responders — or intercepts at
the follow-up point with automated escalation — addresses one of the
highest-impact latency sources in the pipeline.

The policy also clarifies that all four contact methods (mail, fax, phone, voicemail)
are equivalent — a system that automates any of these constitutes a valid follow-up.

---

## Cross-Reference Summary for Architects

| POMS Section | Last Updated | Key Constraint | Architect Relevance |
|-------------|-------------|----------------|-------------------|
| DI 22505.006 | Mar 2023 (TN Jan 2026) | 10 User Trigger cap/level; graphical evidence requires traditional request; wet 827 valid 9 months | Defines exactly when automated vs. manual requests fire |
| DI 81020.020 | Sep 2021 | DMA barcodes enable auto-CEF upload; MEGAHIT cross-ref in Section E | Fax-to-CEF automation requires barcode; work history pre-populated |
| DI 81020.110 | Apr 2025 | Examiners review images; RFC/PRT forms in DCPS | Most recent confirmation of image-based workflow; DCPS = determination system of record |
| DI 22505.035 | Apr 2024 | 10-20 day follow-up window; 10 day response window | Non-responder latency source; automated follow-up is policy-compliant |
| DI 81020.060 | Jun 2011 | PDF/TIFF conversion mandate; one request no retry | Core intake policy — oldest and most impactful |
| DI 22505.022 | Mar 2017 | VA Standard Health Summary content limits | VA pipeline constraints |
| DI 22505.023 | Mar 2017 | DoD three-level escalation; 90-day NPRC | Military record pathway |

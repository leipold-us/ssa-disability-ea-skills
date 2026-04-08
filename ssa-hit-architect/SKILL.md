---
name: ssa-hit-architect
description: >
  Deep domain knowledge of the Social Security Administration's Health Information
  Technology (HIT) program and National Medical Evidence Collection initiative.
  Use this skill whenever someone asks about: SSA disability records collection,
  MEGAHIT, SSA's RFI 28321325RI0000047, SSA HIT partnerships, electronic health
  record exchange with SSA, disability determination evidence workflows, SSA-827
  authorization, eHealth Exchange SSA connection, TEFCA and SSA, DDS evidence
  collection, SSA ERE, CEF or Certified Electronic Folder, SSA POMS evidence policy,
  or any solution/architecture targeting SSA's medical evidence program.
  Also use when an architect, vendor, or consultant is designing a solution that
  integrates with SSA systems — especially MEGAHIT, EDCS, ERE, CEF, DCPS, or eView.
  This skill supports Solution Architects and Segment Architects working within
  an Enterprise Architecture framework who need authoritative, integration-level
  knowledge of SSA's evidence collection ecosystem.
---

# SSA HIT Architect Knowledge Base

## Purpose

This skill provides authoritative domain knowledge about SSA's medical evidence
collection program for architects designing solutions that integrate with or
augment SSA's disability determination workflow. It covers the current state,
the ten core opportunities in SSA integration points, policy constraints, and
the vendor landscape as of April 2026.

**Companion skill:** `ssa-disability-ea` covers the full SSA disability
determination business process — sequential evaluation, Listings of Impairments,
RFC assessment, adjudicative levels, and quality assurance. Use that skill first
to understand the business problem. Use this skill for integration specifics.

## How to use this skill

- For system integration questions → see **SSA Systems Reference**
- For policy constraints → see **Policy and Authorization**
- For the ten opportunities and where solutions plug in → see **Opportunity and Integration Matrix**
- For the RFI and what SSA is asking → see **RFI Context**
- For acronyms → see **Acronym Guide**
- For named contacts and key organizations → see **Key Contacts**

Read the relevant section(s) before responding. For deep technical detail on
integration protocols, read `references/integration-technical.md`.
For the full ten-opportunity matrix with SSA integration points, read
`references/opportunity-matrix.md`.
For additional POMS sections (DI 22505.006, DI 81020.020, DI 81020.110,
DI 22505.035), read `references/poms-additional.md`.

---

## Program Overview

SSA administers the largest disability insurance program in the world. Each year:
- **20+ million medical records** requested from almost **500,000 providers**
- **2 million disability claims** processed annually
- **54 state DDS agencies** make initial determinations on SSA's behalf
- **219 day average processing time** as of FY2023 — up 81% since 2019
- **885,000+ claims backlogged** as of early 2026

SSA has been building electronic health record exchange capability since 2008
(MEGAHIT first pilot with Beth Israel). As of April 2026:
- **323 HIT partner organizations**, **48,886 participating providers**
- Roughly **10% coverage** of the ~500,000 provider universe SSA needs
- **TEFCA joining** via eHealth Exchange QHIN — live spring 2026
- **50% faster** claim processing when electronic records used (SSA, Feb 2026)
- **~50% of records** still arrive by mail or fax (Niskanen Center, Apr 2025)

SSA is **not a HIPAA covered entity** — it operates under the Privacy Act.
The SSA-827 authorization bridges this gap for provider disclosures.

---

## SSA Systems Reference

### Collection and Ingestion Systems

| System | Full Name | Function | Integration Relevance |
|--------|-----------|----------|----------------------|
| MEGAHIT | Medical Evidence Gathering and Analysis through Health IT | Automated record request engine. Fires at FO→DDS case transfer if HIT partner in EDCS and valid e-827 present. One request, no retry. Converts all incoming records to PDF/TIFF images. | Primary automated collection integration point. Partners connect via eHEX using SOAP/IHE XCA protocol. |
| EDCS | Electronic Disability Collect System | Case intake, routing, and facility phonebook. Routes HIT requests to correct partner via facility list. | Must contain HIT partner facility listing before MEGAHIT can fire. e-827 must be present here. |
| CEF | Certified Electronic Folder | Official claimant record folder. All evidence lands here regardless of channel. | All vendor submissions — HIT MER, ERE uploads, scanned documents — land in CEF. Yellow section = HIT records. |
| ERE | Electronic Records Express | Secure web portal for manual electronic record submissions by providers and representatives. | Alternative integration point for vendors not connected via eHEX. Supports PDF, TIF, JPEG, PNG, MSWORD, RTF, HTML. |
| Pay4HIT | Automated payment system within MEGAHIT | Pays $15 flat rate per valid HIT MER response via automated EFT to Treasury. | Part of MEGAHIT — no separate integration needed. Rate unchanged since ~2010. |

### Case Processing Systems

| System | Full Name | Function | Integration Relevance |
|--------|-----------|----------|----------------------|
| DCPS | Disability Case Processing System | Cloud-hosted case management for DDS examiners. All formal medical assessment forms are created here: RFC (SSA-4734-F4), MRFC (SSA-4734-F4-SUP), PRT (SSA-2506-BK), Medical Evaluation (SSA-416), CDEF (SSA-538). DCPS is the system of record for disability determinations — not just case management. | Ultimate integration target for AI decision support. Any intelligence output must land here to have operational value. SSA paused DCPS modernization Aug 2025. |
| eView | Electronic document viewer | Displays CEF contents to examiners and hearing staff. | AI/NLP output would need to surface here alongside raw record for examiner value. |
| CONNECT | Open source federal software | Provider-side interface that connects EHR systems to MEGAHIT via eHEX. | Providers use this to establish HIT connectivity. SSA does not maintain it. |

### Authorization

| Form/System | Function | Key Constraint |
|-------------|----------|----------------|
| SSA-827 | Patient authorization for record disclosure | Required before any HIT request fires. Expires 12 months. Cannot reuse across adjudicative levels. Hearing level requires new 827. |
| e-827 | Electronic version of SSA-827 | Required for MEGAHIT and VA/DoD. Wet signature blocks automated pipeline entirely. |

---

## Policy and Authorization

### Critical POMS Sections

**DI 81020.060** (June 2011) — Receiving Evidence in DDS
- MEGAHIT trigger conditions: HIT partner in EDCS AND valid e-827 present
- **Mandates converting all incoming electronic records to PDF or TIFF images**
- One request per provider, no retry logic
- Email evidence must be printed then scanned — cannot go directly to CEF
- Last updated 2011 — predates FHIR, TEFCA, modern standards

**DI 22505.022** (March 2017) — VA VHA Medical Evidence
- SSA-DDS Standard Health Summary content limits:
  - Progress notes: max 40
  - Lab results: max 20
  - Inpatient discharge summaries: max 5
  - Coverage: most recent 2 years only
- e-827 required — wet signature blocks pipeline
- MPRO (Medical and Professional Relations Officer) is human liaison
- Last updated 2017 — before Federal EHR modernization

**DI 22505.023** (March 2017) — Military/DoD Medical Evidence
- Three-level escalation: MEGAHIT auto → User Trigger via DCPS → ERE eOR → mail
- NPRC (St. Louis) fallback = 90-day wait
- Last updated 2017

### Technical Standards (from SSA GitHub)

SSA's accepted document formats (Implementation Guide v5.0, October 2017):
- **CCDA R1.1**, **CCDA R2.1**, **CCD**, HITSP/C32
- **FHIR is not in SSA's current accepted standard**
- 22 accepted structured document types including: CCD, H&P, Consultation Notes,
  Discharge Summaries, Progress Notes, Operative Notes, Procedure Notes, Care Plans
- Native unstructured formats accepted: PDF, TIF, JPEG, PNG, MSWORD, RTF, HTML
- **DICOM imaging not supported** — only narrative text of radiology reports
- **SSA prefers text over images** for dynamically generated documents — directly
  contradicts the POMS TIFF conversion mandate
- Preferred scan: 200 DPI, bitonal, CCITT Group 4, portrait letter

SSA's network protocol (Interoperability Guide v4.0, October 2017):
- **SOAP-based IHE XCA web services** — not REST, not FHIR APIs
- Patient Discovery → Query for Documents → Retrieve Documents sequence
- Partners must be eHealth Exchange members to connect

### Onboarding Process (Form SSA-680)

Every HIT partner must complete:
1. Form SSA-680 (23-page Clinical Content Checklist) — 5-hour burden estimate
2. Facility List (Excel) — SSA's internal phonebook for routing requests
3. Fiscal Package — EFT routing for $15 payments
4. Content Testing (Sample Document + Verification)
5. Connectivity Testing
6. Probationary Testing (~1-2 weeks in production)
7. Go-live coordination with DDS

Submit to: ssa.hit.information@ssa.gov
New Partner Committee reviews and decides on partnership.
Last major onboarding kit update: 2017-2018.
SSA GitHub repository: https://github.com/SSAgov/HealthIT (6 stars — virtually undiscovered)

---

## The Ten Opportunities

A solution architect should be aware of these ten structural opportunities.
For each opportunity's SSA integration point, read `references/opportunity-matrix.md`.

| # | Opportunity | Type | Root Cause |
|---|---------|------|-----------|
| 1 | Coverage gaps — small practices, rural, behavioral health not on TEFCA | Collection | No mandate authority; $15 rate insufficient; onboarding burden too high |
| 2 | Identity matching — 15% of electronic records undeliverable | Collection | SSN vs. MRN mismatch; no EMPI at SSA query layer |
| 3 | Structured data converted to PDF/TIFF on arrival — value destroyed | Policy | POMS DI 81020.060 mandates image conversion; policy predates modern standards |
| 4 | Unstructured clinical text unreadable at scale — no NLP layer | Intelligence | No AI processing between record receipt and examiner review |
| 5 | De-duplication — same records arrive through multiple channels | Intelligence | No record fingerprinting or longitudinal consolidation |
| 6 | Sensitive data (42 CFR Part 2, psychotherapy, HIV) excluded from exchange | Policy/Legal | Separate legal frameworks; no consent management in current HIT |
| 7 | SSA-827 expires; cannot be reused across adjudicative levels | Process | Regulatory — expiration rules set by statute |
| 8 | VA Standard Health Summary truncates records at hard limits | Intelligence | POMS DI 22505.022 caps; policy written for VistA era not Federal EHR |
| 9 | No decision support — records not mapped to disability criteria | Intelligence | MEGAHIT business rules are 2011 ICD code lookups, not AI |
| 10 | Appeals Council — no new HIT requests can be triggered | Process | Policy gap; existing record travels on CD; representatives cannot supplement |

---

## RFI Context

**RFI:** 28321325RI0000047 — National Medical Evidence Collection
**Contact:** evan.aston@ssa.gov
**Issued by:** SSA Executive Director of Clinical Medical Data Strategy
**Deadline:** October 14, 2025 (responses submitted; market assessment ongoing)

### Four Approaches SSA Is Exploring
1. **Vendor exchange / collection driven** — vendor manages national record retrieval
2. **Consumer-driven** — claimant authorizes and submits own records electronically
3. **Direct connect** — SSA connects directly to providers or networks
4. **Standards-based** — vendor drives adoption of FHIR/CCDA/IHE standards

### Eleven RFI Information Bullets (summary)
- **B1** Company profile + end-to-end collection management (non-responder elimination)
- **B2** Market size — provider network coverage across all provider types
- **B3** Timeliness — real-time to multi-day submission process
- **B4** Data formats — structured format delivery across multiple channels
- **B5** Data quality — identity reconciliation, de-duplication, completeness
- **B6** AI/ML — NLP, summarization, de-duplication, longitudinal timeline (highest value)
- **B7** Hosting — FedRAMP, cloud provider, LLM data residency (no third-party training)
- **B8** Security/827 — HIPAA (note: SSA not HIPAA entity), authorization, governance
- **B9** Disaster recovery — SLAs for national-scale service including shutdown risk
- **B10** QA/completeness — 100% completeness standard; how to address all providers
- **B11** Prior experience — federal-scale volume equivalent

### Key Insight for Architects
TEFCA going live now solves the collection problem for large health systems.
The **intelligence gap** — what happens after records arrive — is the unsolved problem.
SSA's current posture: sophisticated collection pipeline, then treat everything like a fax.
Storage cost alone of PDF/TIFF vs. structured data at 20M records/year is substantial.

---

## Key Contacts

| Name | Role | Significance |
|------|------|-------------|
| Jay Ortis | Chief of Disability Adjudication, SSA | Named in TEFCA announcement Feb 2026; program lead for modernization |
| Evan Aston | Contracting Officer | RFI contact: evan.aston@ssa.gov |
| Kitt Winter | Director, Division of HIT, SSA OCIO | Built MEGAHIT; co-authored AHIMA 2011 origin article; kitt.winter@ssa.gov |
| Bob Hastings | SSA Office of Disability Programs | Co-author of AHIMA 2011 MEGAHIT article with Kitt Winter |
| Jay Nakashima | President, eHealth Exchange | Named in TEFCA announcement; SSA's QHIN partner |
| Nihit Bajaj | Epic Technical Solutions Engineer Team Lead | Named in TechTarget Mar 2026; key Epic/SSA integration voice |
| Katie Deschaine | VP Clinical Applications, Temple Health | Temple went live Jan 20, 2026; 85% match rate on day one |

---

## Current Market Landscape (April 2026)

### Networks connected to SSA
- **eHealth Exchange (eHEX)** — primary network since 2009; now SSA's TEFCA QHIN
- **Carequality** — framework enabling cross-network queries; Epic clients use this
- **Oracle Cerner** — pursuing TEFCA QHIN status (announced Oct 2024)
- **Veradigm (Allscripts)** — direct partner, 19 states
- **CommonWell Health Alliance** — SSA general member as of 2019 (current status unconfirmed)

### Notable partners
- **OCHIN** — safety-net HIE covering 31 states; serves disability claimant population
- **VA/DoD** — via Federal JHIE; live since November 11, 2016
- **250+ health systems** via Epic EHR connecting through Carequality/eHEX

### What TEFCA changes
- Eliminates per-partner Excel facility list — directory handled automatically
- Epic transitioning all clients to TEFCA (280M patient records, ~1/3 EHR market)
- SSA in testing phase; expected live spring 2026
- Government benefits determination is a specific TEFCA use case requiring
  additional network configuration — not all networks have built it yet

---

## Architect Guidance

### Integration entry points (by solution type)

**Record collection vendor:**
Connect via eHEX (SOAP/IHE XCA) as registered HIT partner, or submit via ERE.
Complete Form SSA-680 and Facility List. Plan for months-long onboarding.
TEFCA will simplify directory management but not content standards compliance.

**Identity resolution / EMPI:**
Intercept at EDCS query layer before MEGAHIT fires.
Address SSN ↔ MRN mismatch — probabilistic matching against provider demographics.
15% failure rate at Temple Health and Sentara = quantified target.

**AI/NLP intelligence layer:**
Primary integration: MEGAHIT output → CEF → eView/DCPS examiner interface.
Records arrive as PDF/TIFF — OCR + NLP pipeline needed.
Output must surface in eView alongside raw record, or as DCPS decision support.
Map clinical concepts to SSA Listings of Impairments (Blue Book) for examiner value.
Map functional limitations to RFC exertional/nonexertional categories — this is
where most non-Listing cases are decided and where AI has the highest impact.
FedRAMP High likely required. Data must not leave security boundary for LLM training.

**Critical constraint — medical equivalence human review gate:**
Step 3 medical equivalence findings require MC/PC concurrence by statute.
AI can flag probable Listing matches for MC/PC review — it cannot make the
final finding. Design for human-in-the-loop at this specific decision point.
Any architecture that bypasses MC/PC sign-off on equivalence is non-compliant.

**CE reduction ROI:**
Better HIT coverage and record completeness directly reduces Consultative Examinations.
Each CE avoided saves SSA $200-500 in exam cost plus 2-6 weeks of processing time.
CE reduction rate is a tracked DDS efficiency metric — quantifiable and meaningful to SSA
program leadership. This is the strongest financial ROI argument for collection quality.

**VA/Federal EHR specialist:**
VA pipeline via JHIE has been live since 2016.
POMS DI 22505.022 governs what SSA receives — hard content limits apply.
Opportunity: pre-process and prioritize VA records before they leave VA firewall,
optimizing what goes into the Standard Health Summary within existing limits.
POMS was written for VistA era — Federal EHR modernization (Oracle Health) changes
what's available but not what the policy asks for.

**Consumer-driven / patient app:**
Claimant authorizes and submits own records — bypasses provider-side friction.
Requires e-827 digital lifecycle management.
Must integrate with my Social Security account for identity verification.
Addresses hearing-level gap where representatives cannot trigger new HIT requests.

### Policy constraints no technology can override
1. POMS DI 81020.060 PDF/TIFF conversion — requires policy revision, not just technology
2. 100% completeness requirement — rejects 60-80% complete records; lowering threshold requires SSA leadership decision
3. SSA-827 expiration rules — set by regulation; consumer app must work within them
4. Appeals Council new HIT requests — policy gap; requires regulatory change
5. Graphical evidence for abnormal testing — HIT standard documents do not include tracings; traditional request required for abnormal visual fields, PFTs, audiograms, cardiac stress tests regardless of HIT connectivity (DI 22505.006C.1.d)

### Questions every architect should ask SSA
- Is DCPS integration on the roadmap, or will eView remain the examiner interface?
- Has SSA updated the Implementation Guide to accept FHIR R4?
- What is the plan for POMS DI 81020.060 given TEFCA structured data delivery?
- How does the 100% completeness standard apply to TEFCA-delivered FHIR bundles?
- What FedRAMP impact level is required for access to CEF contents?

---

## Sources

All findings sourced and verified. Key sources:

- SSA HIT program: https://www.ssa.gov/hit/
- SSA GitHub HIT repository: https://github.com/SSAgov/HealthIT
- RFI: https://www.fedconnect.net/FedConnect/?doc=28321325RI0000047&agency=SSA
- POMS DI 81020.060: https://secure.ssa.gov/apps10/poms.nsf/lnx/0481020060
- POMS DI 22505.022: https://secure.ssa.gov/apps10/poms.nsf/lnx/0422505022
- POMS DI 22505.023: https://secure.ssa.gov/apps10/poms.nsf/lnx/0422505023
- SSA TEFCA announcement (Feb 11, 2026): https://www.ssa.gov/blog/en/posts/2026-02-11.html
- Niskanen Center (Apr 15, 2025): https://www.niskanencenter.org/stuck-in-the-fax-age-ssas-record-retrieval-process-needs-a-digital-overhaul/
- NOSSCR HIT update (May 2023): https://nosscr.org/article/update-on-health-it-at-ssa/
- TechTarget (Mar 2, 2026): EHR sharing speeds up disability applications
- OIG HIT audit (2022): https://oig.ssa.gov/audit-reports/2022-01-05-the-social-security-administration's-expansion-of-health-information-technology-to-obtain-and-analyze-medical-records-for-disability-claims/
- AHIMA / Kitt Winter (2011): https://pubmed.ncbi.nlm.nih.gov/21667864/
- SSA HIT partner list (Apr 6, 2026): https://www.ssa.gov/hit/materials/pdfs/HealthITPartnerOrganizations.pdf

Knowledge current as of April 2026.

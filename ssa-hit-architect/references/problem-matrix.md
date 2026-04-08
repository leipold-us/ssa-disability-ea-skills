# SSA Medical Evidence — Problem and Integration Matrix

Ten structural problems in SSA's evidence collection program, each with
the specific SSA integration point where a solution must connect.

---

## Problem 1 — Coverage gaps
**Small practices, rural clinics, behavioral health, community health centers
not reachable by TEFCA or eHEX.**

- Provider universe: ~500,000. HIT partners: 48,886 (10%)
- Non-participating providers still send fax and mail
- SSA's onboarding (Form SSA-680 + 7-step committee review) is a barrier
- $15 flat rate insufficient to cover integration costs for small practices
- No mandate authority — SSA cannot compel participation

**SSA integration point:**
Vendor delivers records to CEF via ERE upload or as a registered HIT partner
through eHEX/Carequality. SSA sees compliant HIT MER or ERE submission
regardless of how vendor retrieved the underlying record.
→ ERE → CEF / eDIB

---

## Problem 2 — Identity matching failures
**15% of electronic requests return nothing due to demographic mismatch
between SSA's SSN-based records and provider EHR demographics.**

- Documented at Temple Health (day one) and Sentara Healthcare
- Name variants, DOB errors, address changes cause mismatches
- No automated retry — failed match falls to manual follow-up
- EMPI technology exists but not applied to SSA-provider identity resolution

**SSA integration point:**
Identity resolution must occur before MEGAHIT fires. EMPI or probabilistic
matching at the EDCS query stage can intercept failures before they become
manual fallbacks. No retry means a missed match is a lost automation.
→ EDCS → MEGAHIT pre-query identity check

---

## Problem 3 — PDF/TIFF conversion destroys structured data value
**POMS DI 81020.060 mandates converting all incoming records — including
structured FHIR and CCDA — to PDF or TIFF images.**

- A FHIR R4 bundle arriving via TEFCA becomes a static image
- Keyword search impossible; machine processing impossible
- SSA's own implementation guide prefers text — contradicts POMS
- Root cause is policy, not technology — requires POMS revision
- Storage cost of TIFF/PDF vs. structured data at 20M records/year is substantial

**SSA integration point:**
OCR + NLP applied post-conversion can restore some searchability.
Parallel structured data store alongside image is possible interim approach.
Long-term fix requires SSA leadership to update POMS DI 81020.060.
→ MEGAHIT output → CEF yellow section (images) → OCR/NLP overlay

---

## Problem 4 — Unstructured clinical text unreadable at scale
**No NLP or AI layer exists between record receipt and examiner review.
20M records/year; examiners read everything manually.**

- Progress notes, ER visits, discharge summaries, handwritten annotations
- MEGAHIT business rules = ICD code lookups from 2011, not NLP
- No mapping of clinical content to SSA Listings of Impairments (Blue Book)
- DDS staffing shortages mean less examiner time per case as backlogs grow
- FY2018: cases with only HIT records processed 65% faster (approved claims)
  and 45% faster overall — demonstrating the potential

**SSA integration point:**
AI/ML layer sits between CEF image storage and examiner review in eView/DCPS.
Vendor needs read access to CEF or intercepts at MEGAHIT output.
Output must surface in eView alongside raw record or as DCPS decision support panel.
FedRAMP High likely required. Data must not leave security boundary for LLM training.
→ MEGAHIT output → CEF → eView / DCPS examiner interface

---

## Problem 5 — De-duplication
**Same records routinely arrive through multiple channels (MEGAHIT, ERE, fax,
mail) for the same claim. Manual examiner reconciliation required.**

- Single claim may trigger all four collection channels simultaneously
- No automated fingerprinting or de-duplication in current CEF
- Longitudinal timeline construction across providers and time periods
  does not exist in SSA's current workflow — explicitly requested in B6

**SSA integration point:**
Post-ingestion layer after all channels deliver to CEF.
Vendor de-duplicates before presenting to examiner — presents unified view.
Requires read access to full CEF contents.
Cannot delete from CEF (SSA system of record) — annotate or overlay instead.
→ CEF / eDIB consolidated record view

---

## Problem 6 — Sensitive data excluded from standard exchange
**Psychotherapy notes (HIPAA exclusion), substance abuse records
(42 CFR Part 2), and HIV status cannot flow through standard HIT exchange.**

- SSA explicitly states these records are required for a large portion of claims
  (especially mental/behavioral health — largest disability claim category)
- 42 CFR Part 2 (2020 update relaxed some restrictions but framework remains complex)
- No current HIT exchange solution handles all three categories in one workflow
- Domestic violence victims have additional privacy constraints

**SSA integration point:**
Supplements the 827 workflow. Vendor manages condition-specific consent forms,
tracks authorization status, triggers separate requests outside MEGAHIT.
Requires SSA OGC involvement for data use agreements.
→ EDCS authorization tracking + ERE for delivery + separate consent management

---

## Problem 7 — SSA-827 expiration and cross-level reuse
**827 expires after 12 months. Cannot be reused across adjudicative levels.
Hearing level requires new 827 even if one exists from initial claim.**

- Cases routinely span 2-3 years through appeals
- Wet signature blocks VA/DoD automated pipeline
- e-827 required for MEGAHIT — paper 827 = manual fallback
- Consumer app could make re-authorization frictionless

**SSA integration point:**
Integrates with EDCS to check 827 validity before MEGAHIT fires.
Consumer-facing app generates new e-827 and submits to EDCS.
Requires my Social Security account integration for claimant identity verification.
→ EDCS → MEGAHIT trigger logic

---

## Problem 8 — VA Standard Health Summary truncates records
**SSA-DDS Standard Health Summary has hard limits: 40 progress notes,
20 lab results, 5 discharge summaries, 2-year coverage window.**

- POMS DI 22505.022 governs what SSA receives from VA
- Policy written for VistA era — Federal EHR modernization changed what's
  available but not what the policy requests
- Critical evidence silently truncated before examiner ever sees it
- VA-SSA HIT connection live since November 11, 2016

**SSA integration point:**
Unique opportunity: intercept inside VA JHIE / Federal EHR before records
leave VA firewall. Pre-process and prioritize clinical content within the
existing hard limits — surface most disability-relevant content rather
than most-recent content.
Requires VA OIT cooperation to modify Standard Health Summary output.
→ VA JHIE → MEGAHIT input (pre-delivery, inside VA firewall)

---

## Problem 9 — No decision support
**Records arrive. Examiners read them. No system maps clinical evidence
to SSA's sequential evaluation criteria or Listings of Impairments.**

- MEGAHIT business rules engine: diagnostic code → Listings lookup (2011)
- SSA has invested in AI tools for hearing decisions and AC remand analysis
  (confirmed in SSA finance report) but not for incoming evidence processing
- SSA received $30M TMF grant Oct 2024 for IT upgrades — active budget
- RFI explicitly asks for ML algorithms aiding in "richer data"

**SSA integration point:**
Integrates into DCPS examiner workflow as decision support layer.
Could augment existing MEGAHIT business rules engine.
Must not constitute unauthorized practice of medicine.
DCPS integration is hardest technical target — SSA paused modernization Aug 2025.
→ DCPS / eView + MEGAHIT business rules engine

---

## Problem 10 — Appeals Council gap
**Cases reaching the Appeals Council carry their existing record on CD —
collected through DDS and hearing levels. Representatives cannot trigger
new HIT requests to supplement the record if evidence was missed.**

- Most complex and disputed cases have least ability to update evidence
- Policy gap, not technology gap — requires regulatory change
- Not a zero-evidence situation: existing record travels with the case
- Any vendor claiming end-to-end completeness must acknowledge this

**SSA integration point:**
Would require new integration between MEGAHIT and AC case management system.
AC operates on different docket system than OHO — separate integration pathway.
Low probability near-term without regulatory change.
→ AC case management → MEGAHIT (new connection, requires policy change)

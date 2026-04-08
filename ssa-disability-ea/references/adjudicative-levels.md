# Adjudicative Levels — Workflow and System Touchpoints

## Overview

SSA disability claims move through up to four administrative levels before
federal court. Each level is an INDEPENDENT determination — prior findings
are not binding but must be considered. New RFC required at each level.

---

## Level 1 — Initial Determination (DDS)

**Decision makers:** Disability Examiner (DE) + Medical Consultant (MC)
or Psychological Consultant (PC)

**Systems:**
- EDCS — receives case from Field Office; contains demographics, 827, facility list
- MEGAHIT — fires automatically at FO→DDS transfer if HIT partner + e-827 present
- CEF — collects all evidence from all channels
- eView — examiner views CEF contents (images)
- DCPS — examiner documents development, creates RFC/PRT forms, makes determination

**Timeline:** ~219 days average (FY2023 — up 81% since 2019)

**Evidence collection:**
- MEGAHIT automated request fires at case transfer
- Period covered: 12 months prior to POD (Title II) or protective filing date (Title XVI)
- ERE, fax, mail channels run in parallel
- CE ordered if treating source evidence insufficient

**Key workflow:**
1. FO completes intake (SSA-3368, SSA-827, SSA-3367 work history)
2. FO enters POD, transfers case to DDS via EDCS
3. MEGAHIT fires automatically to all HIT partners in EDCS
4. DDS DE reviews existing CEF contents
5. DE orders any needed supplemental development
6. MC/PC reviews medical evidence, prepares RFC/PRT forms in DCPS
7. DE makes determination, documents in DCPS
8. Notice sent to claimant

**Determination outcomes:**
- Fully favorable (disabled)
- Partially favorable (closed period)
- Unfavorable (not disabled)

---

## Level 2 — Reconsideration (DDS)

**Decision makers:** DIFFERENT DE than initial + MC/PC (independent review)

**Systems:** Same as initial — DCPS, eView, CEF

**Key difference from initial:**
MEGAHIT does NOT automatically fire at reconsideration if no HIT request
was made at initial level. DDS must create User Trigger manually.
If initial HIT request was made: auto request covers period from date of
last initial HIT request to date of new request.

**Note:** Some states use single decision-maker (SDM) process —
no formal reconsideration level before hearing.

**Evidence:** Claimant may submit new evidence; DDS develops as needed.

---

## Level 3 — Hearing (OHO / ALJ)

**Decision maker:** Administrative Law Judge — independent of DDS, independent of SSA program offices

**Systems:**
- DCPS (case management)
- CEF (evidence folder — travels from DDS)
- Separate OHO hearing scheduling and management system
- eView (ALJ reviews imaged CEF contents)

**Authorization:** NEW SSA-827 required — cannot reuse DDS-level 827.
DI 22505.006 confirmed: wet-signed 827 valid for HIT partners 9 months from signature.

**Evidence submission:**
- Claimant/representative submits new evidence via ERE
- Representative CANNOT directly trigger HIT requests
- Representative requests HIT via ERE submission; hearing office staff execute
- ALJ may subpoena records or order additional development

**Hearing process:**
- Claimant (usually with representative) appears before ALJ
- Medical expert (ME) may testify
- Vocational expert (VE) testifies on Step 5 jobs in national economy
- ALJ issues fully favorable, partially favorable, or unfavorable decision

**Timeline:** 12-24+ months backlog typical; target 270 days from request

**ALJ must consider:** DDS MC/PC RFC assessments (opinion evidence — not binding).
New independent RFC assessment created at hearing level.

---

## Level 4 — Appeals Council (AC)

**Location:** Falls Church, Virginia

**Function:** Reviews ALJ decisions for legal error, abuse of discretion,
or where ALJ decision not supported by substantial evidence.

**Evidence:** Existing record travels in CEF — NO new HIT requests can be
initiated at AC level. Representatives cannot trigger supplemental collection.

**Critical gap:** Cases reaching AC are the most complex and disputed.
They are also the least able to supplement their evidentiary record electronically.
If treating source evidence was missed at prior levels, there is no automated
mechanism to obtain it at AC.

**Outcomes:**
- Affirm ALJ decision
- Reverse (disability found or denied)
- Remand to ALJ for additional proceedings
- Dismiss (untimely or other procedural)

**Time:** Can take 12-24+ months

---

## Federal Court

Outside SSA administrative process. Record is fixed at AC level.
Remands from federal court return case to ALJ for new hearing.

---

## Cross-Level System Architecture

```
Field Office (FO)
    ↓ EDCS case transfer + POD + e-827
DDS Level 1
    ← MEGAHIT (auto, at transfer)
    ← ERE / fax / mail
    → CEF (all evidence)
    → eView (examiner reads images)
    → DCPS (RFC forms + determination)
    ↓ [if denied]
DDS Level 2 (Reconsideration)
    ← MEGAHIT (User Trigger only if no initial HIT)
    → CEF (updated)
    → DCPS (new RFC, new determination)
    ↓ [if denied]
OHO / ALJ (Hearing)
    ← ERE (representative submissions)
    ← HIT (via hearing office staff, new 827)
    → CEF (updated)
    → DCPS (new RFC, ALJ decision)
    ↓ [if unfavorable]
Appeals Council
    → CEF (fixed record — no new HIT)
    → AC decision
    ↓ [if unfavorable]
Federal Court
    → Fixed record
```

---

## Key Facts for Architects

**Evidence carries forward:** CEF accumulates evidence across levels.
Prior RFC assessments travel as opinion evidence — not binding.

**Independence at each level:** Each DE/ALJ makes fresh determination.
Cannot rubber-stamp prior level findings.

**MEGAHIT gaps by level:**
- Initial: Auto fires at transfer ✓
- Reconsideration: Auto fires only if initial HIT request exists; otherwise User Trigger required
- Hearing: No auto — User Trigger via hearing office staff after new 827
- AC: No HIT requests of any kind

**827 lifecycle:**
- FO obtains at intake
- DDS uses for initial + reconsideration (same 827 if within validity)
- Hearing level: NEW 827 required
- AC: Existing record only — no new authorization needed

**DCPS as system of record:**
All medical assessment forms (RFC, PRT, CDEF) created in DCPS at each level.
Examiners, MCs, PCs, and ALJs all use DCPS for formal determinations.
DCPS is where AI output must ultimately land to have operational value.

**eView as the evidence interface:**
All CEF contents (images) displayed to examiners, MCs, PCs, ALJs via eView.
An AI intelligence overlay would ideally surface alongside eView —
showing extracted findings, Listing matches, RFC implications
adjacent to the raw imaged record the examiner is already reading.

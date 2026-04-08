# Sequential Evaluation — Detailed Policy Reference

## Overview
**Citation:** 20 CFR 404.1520 and 416.920 | DI 22001.001 (June 2024, TN 8 Oct-24)

The five-step sequential evaluation process governs ALL adult initial disability
claims under Title II and Title XVI. Steps must be evaluated in order. Evaluation
stops the moment a determination can be made.

---

## Step 1 — Substantial Gainful Activity (SGA)

**Question:** Is the claimant engaging in SGA?
- Yes → Not disabled. STOP.
- No → Continue to Step 2.

**What counts as SGA:**
- Based on earnings thresholds (set annually by SSA)
- Nature of work also considered — not earnings alone
- Does NOT apply to Age 18 redeterminations

---

## Step 2 — Severity

**Question:** Does the claimant have a severe MDI (or combination) meeting duration?
- No → Not disabled. STOP.
- Yes → Continue to Step 3.

**Establishing a Medically Determinable Impairment (MDI) (DI 24501.020):**
- Must be established by objective medical evidence from an acceptable medical source
- Required: signs, laboratory findings, or diagnostic reports
- Claimant's statements alone CANNOT establish an MDI
- Diagnosis label alone CANNOT establish an MDI — clinical findings required

**Severity standard:**
- Impairment must significantly limit basic work activities
- "Not severe" = slight abnormality with minimal effect on ability to do basic work

**Duration requirement:**
- Must last or be expected to last at least 12 continuous months OR result in death
- Applies at every step where impairment severity is considered

---

## Step 3 — Listings of Impairments

**Question:** Does impairment meet or medically equal a Listing AND meet duration?
- Yes → Disabled. STOP.
- No → Assess RFC, then continue to Step 4.

**Key rule:** RFC assessment occurs between Steps 3 and 4 regardless of Step 3 outcome.

**Meeting a Listing (DI 24508.005):**
- Must satisfy ALL criteria in introductory text AND specific listing criteria
- Must meet duration requirement
- Diagnosis alone insufficient — all clinical findings must be present

**Medically equaling a Listing (DI 24508.010):**
Three pathways:
1. Described listing — missing one or more findings but has other findings of equal significance
2. Unlisted impairment — analogous listing; findings of equal medical significance
3. Combination — no single listing met; combination equals a closely analogous listing

**Critical constraint:** Medical equivalence REQUIRES sign-off from a Medical
Consultant (MC) or Psychological Consultant (PC). Examiner alone cannot find
medical equivalence. This is a human review gate that no AI system can bypass.

---

## RFC Assessment (Between Steps 3 and 4)

**Citation:** DI 24510.001 (August 2017, TN 63 Nov-23)

**Definition:** What a claimant can still do despite functional limitations.
An administrative determination — not a medical opinion.

**Required when:**
- Severe impairment exists AND
- Listing not met AND
- SGA determination required

**Content — what RFC describes:**

Exertional work levels:
- **Sedentary** — lifting up to 10 lbs; mostly sitting
- **Light** — lifting up to 20 lbs; standing/walking up to 6 hrs/day
- **Medium** — lifting up to 50 lbs; standing/walking up to 6 hrs/day
- **Heavy** — lifting up to 100 lbs
- **Very Heavy** — lifting over 100 lbs

Nonexertional limitations:
- **Postural** — balancing, climbing, stooping, crouching, kneeling, crawling
- **Manipulative** — reaching, handling, fingering, feeling
- **Visual** — near/far acuity, depth perception, accommodation, color vision, field of vision
- **Communicative** — hearing, speaking
- **Environmental** — cold, heat, wetness, humidity, noise, vibration, atmospheric, hazards
- **Mental** — concentration, persistence, pace; social interaction; adaptation

**Key rules:**
- Based primarily on medical evidence but may include lay evidence and claimant statements
- Must address claimant allegations, treating/examining source descriptions, all medical/nonmedical evidence
- New independent RFC required at EACH adjudicative level
- Prior RFC assessments are opinion evidence — not binding but must be considered

**Architect implication:**
RFC is the primary output that drives Steps 4 and 5 decisions.
An AI system that extracts functional limitations from clinical language
and maps them to exertional/nonexertional RFC categories addresses the
highest-value analytical gap in the determination process.

---

## Step 4 — Past Relevant Work (PRW)

**Citation:** DI 25005.001 (July 2024, TN 20 Jul-24)

**Question:** Can claimant perform any PRW as actually performed OR as generally performed in national economy?
- Yes (either) → Not disabled. STOP.
- No (both) → Continue to Step 5.

**Burden of proof:** At Step 4, claimant bears burden to show PRW is beyond RFC.

**PRW definition:** Substantial gainful activity within past 15 years, lasting long enough to learn the job.

**What adjudicators DO NOT consider at Step 4:**
- Age, education, transferability of skills
- Whether PRW exists in significant numbers nationally
- Whether PRW was in foreign country or military
- Whether employer accommodations previously existed
- Whether claimant would be hired
- Whether job openings exist

**Analysis:** Function-by-function comparison of RFC with PRW demands.

---

## Step 5 — Other Work

**Citation:** DI 25015.001 (July 2011, TN 36 Mar-25) | DI 25025.001 (August 2014, TN 14 Mar-24)

**Question:** Can claimant adjust to any other work in national economy given RFC, age, education, work experience?
- Yes → Not disabled.
- No → Disabled.

**Burden shifts to SSA at Step 5** — SSA must show other work exists in significant numbers.

**Vocational factors considered:**
- RFC (exertional and nonexertional limitations)
- Age (younger individual / closely approaching advanced age / advanced age / closely approaching retirement)
- Education (illiterate / marginal / limited / high school or more)
- Work experience (unskilled / semi-skilled / skilled; transferability of skills)

### Medical-Vocational Guidelines (Grid Rules)

Published 1979. Three tables (Grids) + Rule 204.00.

**Tables 1, 2, 3** apply when impairment-related limitations affect exertional demands:
- Each numbered rule combines: RFC level + age + education + work experience → Decision (Disabled / Not Disabled)
- Grids apply DIRECTLY when claimant fits exactly into a grid category
- Grids are used as FRAMEWORK when nonexertional limitations also present

**Rule 204.00** applies when:
- No exertional limitations but nonexertional limitations affect work ability, OR
- Exertional limitations + nonexertional limitations consistent with disabled finding without further analysis

**Nonexertional demands of work:**
- Mental, postural, manipulative, visual, communicative, environmental

**When grids don't apply directly:**
- Vocational expert (VE) testimony required
- VE identifies specific jobs claimant can perform in national economy

**Architect implication:**
Step 5 Grid Rules are a structured lookup — RFC level + age + education + work experience
produces a binary outcome. This is directly amenable to automated application once
RFC is established. The intelligence gap is in establishing the RFC, not applying the Grids.

---

## Onset and Duration

**Citation:** DI 25501.220 (October 2023, TN 50 Oct-23)

**Key dates:**
- **AOD** — Alleged Onset Date (claimant's stated disability start date)
- **POD** — Potential Onset Date (earliest possible date based on non-medical factors — set by Field Office)
- **EOD** — Established Onset Date (actual onset date determined by DDS/OHO)
- **DLI** — Date Last Insured (Title II — disability must be established before this date)

**POD purpose:** Alert DDS/OHO about work issues or non-medical factors affecting entitlement period.
DDS and OHO must consider BOTH POD and AOD when determining EOD.

**Evidence window:** Must cover from POD through date of adjudication.
Title II unfavorable cases: period ends at DLI if DLI is in the past.

**Architect implication:**
The onset date determines the evidence collection window.
A longitudinal timeline system must anchor to POD and build forward to adjudication date.
Records outside this window may not be developed unless specific exceptions apply.

---

## Continuing Disability Review (CDR)

**Citation:** DI 28005.001 (August 2022, TN 13 Nov-22)

**Legal standard:** Medical Improvement Review Standard (MIRS) — established 1984.

**To cease benefits, SSA must show:**
- Medical improvement (MI) related to ability to work AND ability to engage in SGA, OR
- Group I exception to MI (new evidence shows claimant was never disabled), OR
- Group II exception (fraud, new vocational/technical approach available, etc.)

**Distinct from initial claim:** CDR does not re-adjudicate original disability.
Compares current functioning to the "comparison point decision" — the prior favorable determination.

**Architect implication:**
CDR cases have a different evidence standard and evidence window.
A solution designed for initial claims does not automatically serve CDR cases.
The comparison point decision record is the baseline — must be available in CEF.

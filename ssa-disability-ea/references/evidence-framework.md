# Evidence Framework — Detailed Policy Reference

## Case Development Purpose and Scope
**Citation:** DI 22501.001 (October 2023, TN 31 Feb-24)

DDS develops evidence to establish:
- Whether claimant is disabled or blind
- Date disability began (if applicable)
- Date disability ended (if applicable)

Development must be complete enough to permit independent determination of:
- Nature and severity of impairment(s)
- Whether 12-month duration requirement is met
- RFC when Steps 4 and 5 apply
- How claimant functions day-to-day

**Stop development when:** Evidence is sufficient for determination — no more, no less.
Material conflicts, inconsistencies, or ambiguities must be resolved before closing.

**Sources developed:**
- Prior folders (paper and electronic — must review ALL available)
- Medical sources (treating, examining, non-examining)
- Consultative Examinations (when existing evidence insufficient)
- Nonmedical sources (claimant, family, employers, teachers)
- Vocational evidence

---

## Medical and Nonmedical Evidence Policy
**Citation:** DI 22505.001 (June 2025, TN 52 Jan-26) — most recently updated section

### Core obligation: "Every reasonable effort"
SSA must make every reasonable effort to obtain complete medical history:
1. Initial request to all identified medical sources
2. One follow-up between 10-20 days after initial request if no response
3. Minimum 10 days additional wait after follow-up

### Complete medical history
At minimum: records covering 12 months prior to whichever date is earliest —
month of filing, protective filing date, DLI, prescribed period end, or age 22.

If alleged disability began less than 12 months before filing: develop from POD.

### Categories of evidence (DI 24503.005, December 2024)

**1. Objective medical evidence**
Signs, laboratory findings from a medical source.
Does NOT include: symptoms, diagnoses, or opinions.
Required to establish an MDI — this is the threshold category.

**2. Medical opinion**
What claimant can still do despite impairments — functional abilities/limitations.
Post-March 27, 2017 rules: focused on functioning, not diagnosis or prognosis.
Physical demands: sitting, standing, walking, lifting, carrying, pushing, pulling.
Mental demands: understanding, remembering, concentration, persistence, pace,
carrying out instructions, responding to supervision/coworkers/work pressures.
Other demands: seeing, hearing, handling workplace changes.

**3. Prior administrative medical findings**
RFC assessments or findings from prior SSA adjudications.
Not binding but must be considered.

**4. Evidence from nonmedical sources**
Claimant statements, family, caregivers, employers, teachers.
Cannot establish MDI alone. Relevant to symptom evaluation and functional limitations.

**5. Other evidence**
Pain/symptom statements, educational records, work history.

### What CANNOT establish disability
- Symptoms or claimant statements alone (without objective medical corroboration)
- Diagnosis label without clinical findings
- Medical opinion alone at Step 3 (needs MC/PC sign-off for medical equivalence)

### Acceptable vs. non-acceptable medical sources
**Acceptable:** Licensed healthcare workers within scope of state/federal law;
certified speech-language pathologists; school psychologists.
**Non-acceptable:** Can provide evidence on severity and function — but CANNOT establish MDI.

---

## Consultative Examinations (CE)

### When CE is appropriate
CE ordered when existing evidence is insufficient to make determination and:
- Claimant's treating source(s) cannot or will not provide needed evidence
- Evidence is conflicting, inconsistent, or ambiguous
- Evidence is outdated

### CE is SSA's last resort
- Typically $200-500+ per exam
- Adds weeks to processing time
- CE rates are a tracked DDS efficiency metric
- SSA has documented goal to reduce CE utilization

### Architect implication — direct ROI
Every CE avoided by better treating source record completeness:
- Saves $200-500 in CE cost
- Saves 2-6 weeks of processing time
- Improves claimant experience

A HIT solution that improves completeness of treating source records
has quantifiable CE reduction ROI. This is the strongest financial
argument for collection quality improvement in the RFI context.

---

## Supplemental Development
**Citation:** DI 22505.008 (March 2016, TN 51 Sep-25)

Supplemental development = additional evidence needed when initial
development is insufficient.

DDS must contact treating sources for specific functional information
when necessary to adjudicate — not just to obtain a medical opinion.

**Architect implication:**
Supplemental development is a second-pass evidence request —
triggered when the first pass was insufficient. A system that
pre-screens incoming evidence for completeness and flags gaps
before the examiner requests development could reduce the
need for supplemental rounds, saving time on both sides.

---

## Representation of Claimants
**Citation:** DI 31001.001 (May 2025, TN 24 May-25 — very recently updated)
**Citation:** DI 31001.010 (July 2022, TN 25 Dec-25)

### Who is a representative
Individual appointed by claimant via Form SSA-1696 or e1696.
Must meet qualifications and register with SSA before recognition.

**Not a representative:** Relatives/friends providing general assistance,
representative payees, legal guardians (unless separately appointed as representative).

### Authority of appointed representative
Once recognized, can act on behalf of claimant on covered case:
- Submit evidence
- Make statements on claimant's behalf
- Request information about the claim
- Receive notices and copies of decisions

### DDS responsibilities with represented claimants
- Generally, DDS initiates all contacts THROUGH the representative
- Claimant can still contact DDS directly without permission
- If claimant requests direct contact, document in DCPS case note

### Critical limitation for HIT
Representatives CANNOT directly trigger HIT requests.
They must request via ERE submission, and hearing office staff
execute any HIT requests on their behalf at the hearing level.

Representatives can submit evidence via ERE — this is their primary
electronic channel at the hearing level.

New SSA-1696 appointment required for each claim level — cannot
reuse prior appointment across new claim filings.

### Architect implication
A consumer-facing solution that helps claimants authorize and
manage their own records bypasses the representative bottleneck.
Claimant self-authorization via my Social Security account with
e-827 generation could serve the hearing level gap directly,
without requiring representative or hearing office intermediaries.

---

## Evidence Evaluation Hierarchy

For architects designing AI/ML solutions — evidence is not all equal:

| Evidence Type | Weight | Establishes MDI? | Notes |
|--------------|--------|-----------------|-------|
| Objective medical (signs, labs) | Highest | Yes | Required for Step 2 |
| Medical opinion (treating) | High | No | Functional assessment |
| Medical opinion (examining) | Moderate | No | CE or one-time exam |
| Medical opinion (non-examining) | Lower | No | MC/PC review |
| Prior admin findings (RFC) | Opinion | No | Not binding but considered |
| Claimant statements | Context | No | Evaluated for consistency |
| Nonmedical source statements | Context | No | Lay evidence |

**AI implication:** An NLP system must distinguish between these evidence
categories as it processes records. Extracting a claimant's complaint of
pain is categorically different from extracting a lab finding — they
carry different legal weight and serve different determination purposes.

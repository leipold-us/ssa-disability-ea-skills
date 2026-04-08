# Listings of Impairments — Structure and Application

## Purpose and Location
**Citation:** DI 34001.001 (September 2000, Basic) | DI 24508.005 (April 2018)
**Location:** POMS DI 34000 series | 20 CFR Part 404, Subpart P, Appendix 1

The Listings describe impairments severe enough to prevent ANY gainful activity —
permanent or expected to last 12+ months or result in death.

Meeting a Listing = automatic disability finding at Step 3. No vocational
analysis (Steps 4 or 5) required. This is the fastest path to an approved claim.

---

## Structure

**Part A** — Adults age 18+. May also apply to children if disease process similar.
**Part B** — Children under 18 only. Applied first; Part A used if Part B doesn't apply.

Each body system section contains:
1. **Introductory text** — definitions, key concepts, required diagnostic findings
2. **Category of Impairments** — specific required findings (symptoms, signs, labs)

**Critical rule:** SSA does not find a Listing met solely because of a diagnosis label.
ALL specified clinical findings must be present.
Example: Alcoholism diagnosis alone does not establish listing — clinical findings required.

---

## Body Systems (Part A — Adults)

| Listing # | Body System | Last Major Update | Notes |
|-----------|-------------|-------------------|-------|
| 1.00 | Musculoskeletal Disorders | February 2025 | Most recently updated listing |
| 2.00 | Special Senses and Speech | — | Vision, hearing, speech |
| 3.00 | Respiratory Disorders | — | COPD, asthma, cystic fibrosis |
| 4.00 | Cardiovascular System | — | Heart disease, vascular disorders |
| 5.00 | Digestive System | — | GI disorders, liver disease |
| 6.00 | Genitourinary Disorders | — | Kidney disease, renal failure |
| 7.00 | Hematological Disorders | — | Blood disorders, sickle cell |
| 8.00 | Skin Disorders | — | Burns, dermatitis, ichthyosis |
| 9.00 | Endocrine Disorders | — | Diabetes, thyroid disorders |
| 10.00 | Congenital Disorders | — | Children primarily |
| 11.00 | Neurological Disorders | — | Epilepsy, MS, spinal cord |
| 12.00 | Mental Disorders | — | Largest claim category |
| 13.00 | Cancer | — | Malignant neoplastic diseases |
| 14.00 | Immune System Disorders | — | HIV, lupus, inflammatory arthritis |

---

## Mental Disorders (12.00) — The Critical Listing

Mental disorders are the single largest category of disability claims.
This listing directly intersects with the sensitive data problem — substance
abuse, psychotherapy notes, and behavioral health records are required
to evaluate mental disorder listings.

**12.00 subcategories include:**
- 12.02 Neurocognitive Disorders
- 12.03 Schizophrenia Spectrum and Other Psychotic Disorders
- 12.04 Depressive, Bipolar and Related Disorders
- 12.05 Intellectual Disorder
- 12.06 Anxiety and Obsessive-Compulsive Disorders
- 12.07 Somatic Symptom and Related Disorders
- 12.08 Personality and Impulse-Control Disorders
- 12.10 Autism Spectrum Disorder
- 12.11 Neurodevelopmental Disorders
- 12.13 Eating Disorders
- 12.15 Trauma- and Stressor-Related Disorders

**Paragraph B criteria** (most 12.00 listings require):
Extreme limitation of one, or marked limitation of two:
- Understanding, remembering, or applying information
- Interacting with others
- Concentrating, persisting, or maintaining pace
- Adapting or managing oneself

**Architect implication for AI/NLP:**
Mental disorder listings require extracting functional limitation ratings
(extreme / marked / moderate / mild) from psychiatric evaluations, therapy
notes, and behavioral observations. These records are also the most legally
complex to obtain (42 CFR Part 2, psychotherapy exclusion). The highest-value
clinical intelligence use case intersects directly with the hardest evidence
collection problem.

---

## Musculoskeletal Disorders (1.00) — Updated February 2025

Most recently revised listing. Key elements:
- Evaluates skeletal spine, upper/lower extremity disorders
- Includes soft tissue injuries under continuing surgical management
- Spinal disorders that cause neurological dysfunction → evaluated under 11.00
- Inflammatory arthritis → evaluated under 14.00

**Architect implication:** February 2025 update means any AI system using older
clinical criteria mappings for musculoskeletal conditions is out of date.
Listings are revised periodically — a production AI system needs a versioned
criteria update mechanism.

---

## Meeting vs. Medically Equaling a Listing

### Meeting (DI 24508.005)
Must satisfy:
- All criteria in introductory text
- All criteria in specific listing
- Duration requirement (12 months or death)

No exceptions — ALL criteria must be present simultaneously.

### Medically Equaling (DI 24508.010, October 2023)

**Pathway 1 — Described listing:**
Impairment described in Listings but missing one or more specified findings.
Other findings related to impairment are of at least equal medical significance.

**Pathway 2 — Unlisted impairment:**
Impairment not described in Listings.
Analogous listing exists.
Findings at least of equal medical significance to analogous listing.

**Pathway 3 — Combination:**
Multiple impairments, none meeting a listing individually.
Combination equals a closely analogous listing.

**Critical rule:** Can substitute symptoms for symptoms and findings for findings.
CANNOT substitute a symptom for a finding.

**MANDATORY HUMAN REVIEW:** Medical equivalence requires concurrence from
an MC or PC at every adjudicative level. This is a statutory requirement —
not an administrative preference. No AI system can make a final medical
equivalence finding. AI can flag probable equivalence for MC/PC review.

---

## Listings and the Evidence Problem

The Listings reveal exactly what clinical evidence SSA needs for Step 3:

| Body System | Key Evidence Types Required |
|-------------|---------------------------|
| 1.00 Musculoskeletal | Imaging (MRI, CT, X-ray) + functional assessment; NOT the image — the interpretation |
| 3.00 Respiratory | PFT results, DLCO, spirometry tracings (graphical — traditional request required) |
| 4.00 Cardiovascular | EKG interpretation, stress test results, echo findings; tracings for abnormal results |
| 11.00 Neurological | EEG, EMG results; imaging interpretations; neuropsychological testing |
| 12.00 Mental | Psychiatric evaluations, PRT, therapy notes, GAF scores, functional assessments |
| 2.00 Special Senses | Visual field tracings (audiograms for hearing) — traditional request required |

**The graphical evidence gap hits hardest here:** For Listings 3.00, 4.00, 2.00,
and parts of 11.00, SSA's own POMS requires traditional (non-HIT) requests for
graphical evidence even from connected HIT partners. HIT delivers the interpretation
but not the tracings — and the Listings sometimes require the tracing itself.

---

## Listings and AI — The Architecture Opportunity

The Listings are structured clinical criteria — each is essentially a set of
logical conditions (if finding A AND finding B AND duration C → disabled).

This is directly amenable to structured extraction:
1. NLP extracts clinical findings from incoming records
2. Findings are mapped to body system and listing criteria
3. System flags probable Listing meetings or close-calls for MC/PC review
4. MC/PC reviews flagged cases — confirms or rejects the finding
5. MC/PC signs medical assessment in DCPS

This workflow preserves the mandatory human review gate while dramatically
reducing the time MC/PCs spend reading raw records to identify Listing candidates.

**Current state:** MCs and PCs read every record manually, every time.
No system assists with Listing criteria matching.
MEGAHIT business rules use 2011 ICD code lookups — not Listing criteria.

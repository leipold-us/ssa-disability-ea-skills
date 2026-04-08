# SSA Disability Determination — Enterprise Architecture Skills

Two Claude AI skills providing authoritative domain knowledge for Solution Architects
and Segment Architects designing solutions that integrate with or modernize the Social
Security Administration's disability determination program.

Built from primary sources: POMS policy, SSA GitHub repository, OIG audit reports,
RFI documentation, and current market intelligence as of April 2026.

---

## The Two Skills

### `ssa-disability-ea` — Business Process and Policy

Covers the full SSA disability determination business process:

- **Sequential Evaluation** — the five-step determination framework (20 CFR 404.1520)
- **Listings of Impairments** — 14 body systems, meeting vs. medically equaling criteria
- **Residual Functional Capacity (RFC)** — exertional/nonexertional work categories
- **Medical Evidence Framework** — evidence categories, legal weight hierarchy, CE economics
- **Adjudicative Levels** — DDS → OHO/ALJ → Appeals Council workflow and system touchpoints
- **Quality Assurance** — DDS QA structure, federal oversight, design implications
- **Continuing Disability Review** — Medical Improvement Review Standard (MIRS)

**Use this skill first.** Understanding the business process is a prerequisite
for designing solutions that genuinely solve SSA's problems rather than just
delivering records faster into an unchanged workflow.

---

### `ssa-hit-architect` — Health IT Integration Layer

Covers SSA's electronic health record collection program and integration architecture:

- **SSA Systems Reference** — MEGAHIT, EDCS, CEF, ERE, DCPS, eView, Pay4HIT
- **The Ten Problems** — structural gaps with specific SSA integration points
- **Technical Standards** — CCDA R2.1, IHE XCA, 22 accepted document types, FHIR gap
- **POMS Policy** — DI 81020.060, DI 22505.006, DI 81020.110, DI 22505.035, VA/DoD pipeline
- **RFI 28321325RI0000047** — eleven information bullets analyzed with SSA integration context
- **Market Landscape** — TEFCA, eHEX, Carequality, Oracle, Veradigm, Epic as of April 2026
- **Key Contacts** — named SSA, Epic, and Temple Health personnel
- **Onboarding** — Form SSA-680, New Partner Committee, 7-step process

**Use this skill second** — after understanding the business problem from `ssa-disability-ea`.

---

## Why These Skills Exist

SSA's disability determination program is one of the largest medical records
operations in the United States — 20+ million records requested annually from
almost 500,000 providers. Despite two decades of Health IT investment, roughly
half of all records still arrive by fax or mail.

The deeper problem: when electronic records do arrive, SSA converts them to
non-searchable PDF or TIFF images before an examiner ever sees them (POMS
DI 81020.060). A sophisticated collection pipeline built on TEFCA, CCDA, and
modern EHR networks delivers its structured data directly into a process that
treats it like a fax.

Fixing this requires understanding both layers:
1. The technical integration architecture (how records get in)
2. The business process and policy (what happens to them after)

These skills encode that understanding for architects who need to work at both levels.

---

## Skill Structure

```
ssa-disability-ea/
├── SKILL.md                           # Main knowledge base (~470 lines)
└── references/
    ├── sequential-evaluation.md       # Five steps, RFC, Grid Rules, onset, CDR
    ├── evidence-framework.md          # Evidence categories, CE economics, representation
    ├── listings-structure.md          # Body systems, meeting/equaling, AI opportunity
    └── adjudicative-levels.md         # DDS/OHO/AC workflow, system touchpoints

ssa-hit-architect/
├── SKILL.md                           # Main knowledge base (~340 lines)
└── references/
    ├── problem-matrix.md              # Ten problems with SSA integration points
    ├── integration-technical.md       # IHE XCA specs, document types, CEF, VA pipeline
    └── poms-additional.md             # DI 22505.006, DI 81020.020, DI 81020.110, DI 22505.035
```

---

## Installation

Download the `.skill` files from the [Releases](../../releases) page and install
via Claude's skill management interface.

Or clone this repository and install from the local folders.

---

## Primary Sources

These skills are built from primary sources. Key references:

| Source | URL |
|--------|-----|
| SSA HIT Program | https://www.ssa.gov/hit/ |
| **SSA GitHub HIT Repository** | https://github.com/SSAgov/HealthIT |
| RFI 28321325RI0000047 | https://www.fedconnect.net/FedConnect/?doc=28321325RI0000047&agency=SSA |
| POMS DI 81020.060 (TIFF conversion) | https://secure.ssa.gov/apps10/poms.nsf/lnx/0481020060 |
| POMS DI 22505.006 (Requesting evidence) | https://secure.ssa.gov/apps10/poms.nsf/lnx/0422505006 |
| POMS DI 81020.110 (Medical evaluation) | https://secure.ssa.gov/apps10/poms.nsf/lnx/0481020110 |
| POMS DI 22001.001 (Sequential evaluation) | https://secure.ssa.gov/apps10/poms.nsf/lnx/0422001001 |
| POMS DI 34001.001 (Listings purpose) | https://secure.ssa.gov/apps10/poms.nsf/lnx/0434001001 |
| SSA TEFCA Announcement (Feb 2026) | https://www.ssa.gov/blog/en/posts/2026-02-11.html |
| Niskanen Center Analysis (Apr 2025) | https://www.niskanencenter.org/stuck-in-the-fax-age-ssas-record-retrieval-process-needs-a-digital-overhaul/ |
| OIG HIT Audit (2022) | https://oig.ssa.gov/audit-reports/2022-01-05-the-social-security-administration's-expansion-of-health-information-technology-to-obtain-and-analyze-medical-records-for-disability-claims/ |
| AHIMA / Kitt Winter (2011) | https://pubmed.ncbi.nlm.nih.gov/21667864/ |
| TechTarget (Mar 2026) | EHR sharing speeds up disability applications |
| SSA HIT Partner List (Apr 2026) | https://www.ssa.gov/hit/materials/pdfs/HealthITPartnerOrganizations.pdf |

The [SSA GitHub HIT repository](https://github.com/SSAgov/HealthIT) is SSA's
own public partner onboarding kit — virtually undiscovered (6 stars as of April 2026).
It contains Form SSA-680, the Electronic Health Document Implementation Guide (v5.0),
and the eHealth Exchange Interoperability Guide (v4.0). These documents are primary
sources for the technical integration content in `ssa-hit-architect`.

---

## Author Background

These skills were developed by a former SSA employee with direct program experience:
- Component Security Officer for OCIO systems including the eDIB Major System
- Represented SSA at ONC (Office of the National Coordinator for Health IT) in 2005
- Worked on ERE, e-827, and web services security compliance from program inception
- Access Control Utility (ACU) team supported ERE and the e-827 as early customers

---

## Knowledge Currency

Content reflects the SSA Health IT program as of **April 2026**, including:
- TEFCA joining via eHealth Exchange QHIN (announced February 11, 2026)
- Temple Health go-live (January 20, 2026)
- SSA HIT partner list as of April 6, 2026 (323 organizations, 48,886 providers)
- POMS sections current through April 2026 batch runs

---

## License

[MIT License](LICENSE) — free to use, adapt, and redistribute with attribution.

---

## Contributing

Issues and pull requests welcome. See [CONTRIBUTING.md](CONTRIBUTING.md).
Priority areas for contribution:
- Additional POMS chapter coverage (DI 110, DI 120, DI 280, DI 900)
- Updates as SSA's TEFCA integration matures
- Corrections to any policy interpretation
- Coverage of state DDS operational variations

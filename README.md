# Arterial in-house clinical adaptation package

> Status: DRAFT decision-support package, not a device file, not legal advice.
> Regulatory basis: EU MDR (Medical Device Regulation) Article 5(5) health-institution exemption, per MDCG 2023-1 (Medical Device Coordination Group guidance, January 2023).
> Intended reader: hospital QA/regulatory, clinical engineering, stroke neurology/interventional neuroradiology, IT/security, and hospital management.
> Assumption: adopting hospital already operates an appropriate QMS (Quality Management System). This package does not replace it, it maps into it.
> First-time reader: start with [terminology](docs/in-house/00-ABBREVIATIONS-AND-TERMINOLOGY.md). Every abbreviation is spelled out on first use in each document.

## What this is

Upstream `FLOWCAT-CV/arterial` (v2.1, PolyForm Noncommercial 1.0.0; models CC BY-NC 4.0, Creative Commons Attribution NonCommercial) is a research framework for automated vascular analysis from CTA (Computed Tomography Angiography): nnU-Net segmentation, VMTK (Vascular Modeling Toolkit) centerlines, landmark detection, GNN (Graph Neural Network) vessel labelling, tortuosity features, access prediction.

This package helps a hospital decide, under its own QMS, whether and how to fork, freeze, harden, and validate that research code into a narrowly scoped in-house device for internal clinical use, and to document every Article 5(5)(a)-(h) condition if it proceeds.

Narrow in-house purpose adopted here (see [Doc 03](docs/in-house/03-INTENDED-PURPOSE-AND-CLAIMS-BOUNDARY.md)):

> In-house CTA vascular visualisation aid: 3D vessel segmentation plus centerline visualisation from head-and-neck CTA, displayed alongside native CTA, to support, not drive, thrombectomy (mechanical clot removal) planning discussion. Mandatory clinician overread of source CTA. No autonomous triage, no access-probability output to clinicians in this scope.

Access prediction, tortuosity scores as decision thresholds, and intracranial-only mode are out of scope for the initial claim. Adding them later is a design change requiring re-validation and re-justification.

## How to read this package

This README is the index. Begin here; each document links back to this section.

Path 1, decide in 30 minutes. Definition first, decision second, regulation third. Read in this order:

1. [Terminology](docs/in-house/00-ABBREVIATIONS-AND-TERMINOLOGY.md), 5 minutes. The shared vocabulary.
2. [Doc 03, intended purpose](docs/in-house/03-INTENDED-PURPOSE-AND-CLAIMS-BOUNDARY.md), 5 minutes. What the device is, in plain words, before anyone justifies it.
3. [Doc 01, executive summary](docs/in-house/01-EXEC-SUMMARY.md), 10 minutes. Go or no-go.
4. [Doc 02, regulatory strategy](docs/in-house/02-REGULATORY-STRATEGY-ARTICLE-5-5.md), 10 minutes. The eight conditions plus the hidden-feature path.

Path 2, build in order. Only after Path 1 ends in GO:

5. [Doc 04, qualification and classification](docs/in-house/04-DEVICE-QUALIFICATION-AND-CLASSIFICATION.md) then [Doc 05, non-equivalence](docs/in-house/05-NON-EQUIVALENCE-JUSTIFICATION.md). No build before Doc 05 is signed.
6. [Doc 06, GSPR checklist](docs/in-house/06-GSPR-APPLICABILITY-CHECKLIST.md) (General Safety and Performance Requirements), [Doc 07, technical index](docs/in-house/07-TECHNICAL-DOCUMENTATION-INDEX-ART-5-5-f.md), [Doc 08, QMS mapping and checklist](docs/in-house/08-QMS-MAPPING-AND-ADOPTION-CHECKLIST.md).
7. [Doc 09, risk outline](docs/in-house/09-RISK-MANAGEMENT-PLAN-OUTLINE.md), [Doc 10, lifecycle outline](docs/in-house/10-SOFTWARE-LIFECYCLE-PLAN-OUTLINE.md), [Doc 11, validation plus validrig pack](docs/in-house/11-VALIDATION-PLAN-AND-VALIDRIG-PACK-SKELETON.md).
8. [Doc 12, monitoring](docs/in-house/12-CLINICAL-USE-MONITORING-AND-CAPA.md), [Doc 13, public declaration](docs/in-house/13-PUBLIC-DECLARATION-TEMPLATE-ART-5-5-e.md).
9. [Doc 14, licensing](docs/in-house/14-LICENSING-AND-SOURCE-GOVERNANCE.md) with [upstream letter](docs/in-house/14A-UPSTREAM-CONTACT-LETTER-TEMPLATE.md), [Doc 15, viability analysis](docs/in-house/15-VIABILITY-ANALYSIS.md) (HEOR, Health Economics and Outcomes Research). Pinned sources live in the [terminology doc](docs/in-house/00-ABBREVIATIONS-AND-TERMINOLOGY.md#pinned-references).

If in doubt, return here:

| Doubt | Read |
|---|---|
| Can we use Article 5(5) at all | [Doc 02](docs/in-house/02-REGULATORY-STRATEGY-ARTICLE-5-5.md), conditions (a)-(h) plus national check |
| What exactly are we claiming | [Doc 03](docs/in-house/03-INTENDED-PURPOSE-AND-CLAIMS-BOUNDARY.md), purpose plus firewall |
| Why this class and safety class | [Doc 04](docs/in-house/04-DEVICE-QUALIFICATION-AND-CLASSIFICATION.md), IIa-equivalent plus B-evaluate-C explainer |
| Why no equivalent device exists | [Doc 05](docs/in-house/05-NON-EQUIVALENCE-JUSTIFICATION.md), search method plus determination |
| What safety rules still apply | [Doc 06](docs/in-house/06-GSPR-APPLICABILITY-CHECKLIST.md), requirement by requirement |
| Where the evidence lives | [Doc 07](docs/in-house/07-TECHNICAL-DOCUMENTATION-INDEX-ART-5-5-f.md), facility, process, design, performance |
| How this fits our QMS, what to do next | [Doc 08](docs/in-house/08-QMS-MAPPING-AND-ADOPTION-CHECKLIST.md), mapping plus checklist |
| What can go wrong | [Doc 09](docs/in-house/09-RISK-MANAGEMENT-PLAN-OUTLINE.md), hazards H1-H10 |
| How we build and release safely | [Doc 10](docs/in-house/10-SOFTWARE-LIFECYCLE-PLAN-OUTLINE.md), SOUP (Software Of Unknown Provenance), SBOM (Software Bill Of Materials), hiding proof |
| How we prove it works locally | [Doc 11](docs/in-house/11-VALIDATION-PLAN-AND-VALIDRIG-PACK-SKELETON.md), retrospective plus shadow phase |
| How we watch it in use | [Doc 12](docs/in-house/12-CLINICAL-USE-MONITORING-AND-CAPA.md), relaxed cadence plus regulatory minimum |
| What we publish | [Doc 13](docs/in-house/13-PUBLIC-DECLARATION-TEMPLATE-ART-5-5-e.md), MDCG Annex A based |
| Can we legally use and share this | [Doc 14](docs/in-house/14-LICENSING-AND-SOURCE-GOVERNANCE.md), licence split plus repo rules |
| What it costs and whether it stays worth it | [Doc 15](docs/in-house/15-VIABILITY-ANALYSIS.md), viability bar plus the data that proves it |
| What an abbreviation means | [Terminology](docs/in-house/00-ABBREVIATIONS-AND-TERMINOLOGY.md) |

## Repository intent

This is now the private repository `AliakseiT/arterial-inhouse-adaptation`. It stays private until licence clearance with VHIR (Vall d'Hebron Research Institute) and UB (Universitat de Barcelona) for any hospital deployment and any future open-sourcing, plus removal of hospital-identifying, patient, or infrastructure content.

See [Doc 14](docs/in-house/14-LICENSING-AND-SOURCE-GOVERNANCE.md). Do not push upstream code verbatim to a public repo without upstream consent, PolyForm NC governs redistribution and derivative publication. Publication decisions, if any, are recorded in the hospital QMS with prior written upstream consent; this template pre-decides nothing about publication.

Related tooling, not vendored here:

- QMS content model: `AliakseiT/dearauditor-qms-baseline`, SOP/WI/record templates referenced in Doc 08, mapped not copied.
- Validation harness engine: `AliakseiT/validrig`, Doc 11 defines an arterial-visualisation pack against its engine.
- Value methods: `AliakseiT/heor-skills`, Doc 15 defines the narrow value outline.

No code in this package is a medical device. No document here asserts compliance, all `[HOSPITAL: ...]` brackets must be completed and approved inside the hospital QMS.

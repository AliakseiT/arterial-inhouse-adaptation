# Arterial In-House Clinical Adaptation Package

> **Status:** DRAFT decision-support package, not a device file, not legal advice.
> **Regulatory basis:** EU MDR Article 5(5) health-institution exemption, per MDCG 2023-1.
> **Intended reader:** hospital QA/regulatory, clinical engineering, stroke neurology/interventional neuroradiology, IT/security, and hospital management.
> **Assumption:** adopting hospital already operates an appropriate QMS. This package does not replace it — it maps into it.

## What this is

Upstream `FLOWCAT-CV/arterial` (v2.1, PolyForm Noncommercial 1.0.0; models CC BY-NC 4.0) is a **research framework** for automated vascular analysis from CTA: nnU-Net segmentation, VMTK centerlines, landmark detection, GNN vessel labelling, tortuosity features, access prediction.

This package enables a hospital to decide, under its own QMS, whether and how to **fork, freeze, harden, and validate** that research code into a narrowly-scoped **in-house device** for internal clinical use — and to document every Article 5(5)(a)–(h) condition if it proceeds.

Narrow in-house purpose adopted here (see `docs/in-house/02`):

> **In-house CTA vascular visualisation aid:** 3D vessel segmentation + centerline visualisation from head-and-neck CTA, displayed alongside native CTA, to support — not drive — thrombectomy planning discussion. Mandatory clinician overread of source CTA. No autonomous triage, no access-probability output to clinicians in this scope.

Access prediction, tortuosity scores as decision thresholds, and intracranial-only mode are **explicitly out of scope** for the initial in-house claim. Adding them later is a design change requiring re-validation and re-justification.

## Repository intent

Per owner decision: this workspace is expected to become a **private repository** under `AliakseiT`, e.g. `arterial-inhouse-adaptation`. It must stay private until:

1. Licence clearance with VHIR/UB (upstream rights holders) for any hospital deployment and for any future open-sourcing of hospital-added documentation/code, and
2. Removal/redaction of any hospital-identifying, patient, or internal-infrastructure content.

See `docs/in-house/13-LICENSING-AND-SOURCE-GOVERNANCE.md` and `15-OPEN-SOURCING-DECISION-NOTE.md`. Do not push upstream code verbatim to a public repo without upstream consent — PolyForm NC governs redistribution and derivative publication.

## Package map

| # | Document | Answers |
|---|---|---|
| 00 | `docs/in-house/00-EXEC-SUMMARY.md` | Go / no-go decision in 10 minutes |
| 01 | `01-REGULATORY-STRATEGY-ARTICLE-5-5.md` | Art 5(5)(a)–(h) + MDCG 2023-1 condition map |
| 02 | `02-INTENDED-PURPOSE-AND-CLAIMS-BOUNDARY.md` | Narrow purpose, users, out-of-scope firewall |
| 03 | `03-DEVICE-QUALIFICATION-AND-CLASSIFICATION.md` | MDSW qualification, Rule 11 reasoning, why class still matters |
| 04 | `04-NON-EQUIVALENCE-JUSTIFICATION.md` | Art 5(5)(c) method + EUDAMED search + HEOR link |
| 05 | `05-GSPR-APPLICABILITY-CHECKLIST.md` | Annex I GSPR-by-GSPR applicability and evidence pointer |
| 06 | `06-TECHNICAL-DOCUMENTATION-INDEX-ART-5-5-f.md` | Art 5(5)(f) facility/process/design/performance index |
| 07 | `07-QMS-MAPPING-AND-ADOPTION-CHECKLIST.md` | Generic-QMS mapping + hospital adoption checklist |
| 08 | `08-RISK-MANAGEMENT-PLAN-OUTLINE.md` | ISO 14971 plan outline, top hazards |
| 09 | `09-SOFTWARE-LIFECYCLE-PLAN-OUTLINE.md` | IEC 62304/82304 tailoring, SOUP/SBOM, fork governance |
| 10 | `10-VALIDATION-PLAN-AND-VALIDRIG-PACK-SKELETON.md` | Local clinical validation + validrig pack skeleton |
| 11 | `11-CLINICAL-USE-MONITORING-AND-CAPA.md` | Art 5(5)(g)(h): use review, corrective action, authority interface |
| 12 | `12-PUBLIC-DECLARATION-TEMPLATE-ART-5-5-e.md` | MDCG Annex A–based public declaration |
| 13 | `13-LICENSING-AND-SOURCE-GOVERNANCE.md` | PolyForm NC / CC BY-NC / Apache-2.0 split, private-repo rules |
| 14 | `14-HEOR-VALUE-OUTLINE.md` | heor-skills–based value outline supporting (c) without price arguments |
| 15 | `15-OPEN-SOURCING-DECISION-NOTE.md` | What can later be open-sourced and under what consent |
| A | `ANNEX-A-GLOSSARY-AND-REFERENCES.md` | Terms, sources, version pins |

Related upstream tooling (not vendored here):

- QMS content model: `AliakseiT/dearauditor-qms-baseline` — SOP/WI/record templates referenced in Doc 07 (not copied; mapped).
- Validation harness engine: `AliakseiT/validrig` — Doc 10 defines an `arterial-visualisation` pack against its engine.
- Value dossiers: `AliakseiT/heor-skills` — Doc 14 defines the narrow HEOR outline.

## How to use this package

1. Hospital management + QA read Docs 00 + 01 and confirm Art 5(5) is even plausible (same legal entity, non-industrial scale, no transfer).
2. Clinical lead owns Doc 02 — if the narrow purpose does not match local need, stop and re-scope before any engineering.
3. Regulatory function owns Docs 03 + 04 — non-equivalence (Doc 04) must precede any build work.
4. Engineering + QA own Docs 05–10 under the hospital QMS (Doc 07 checklist).
5. Only after frozen build + validation + risk acceptance: sign Doc 12 declaration, open Doc 11 monitoring.

No code in this package is a medical device. No document here asserts compliance — all `[HOSPITAL: ...]` brackets must be completed and approved inside the hospital QMS.

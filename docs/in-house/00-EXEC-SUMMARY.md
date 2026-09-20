# 00 — Executive Summary and Go/No-Go

> Read time: ~10 minutes. Owner: hospital management + QA/regulatory jointly.
> Outcome: a recorded GO / CONDITIONAL / NO-GO for pursuing an Arterial-derived in-house device.

## 1. Proposition

Adapt upstream Arterial v2.1 (research, non-commercial licence) into a **frozen, hospital-owned fork** used only inside `[HOSPITAL: legal entity name]` for **CTA vascular visualisation support** in anterior-circulation stroke planning discussion. No CE marking is sought; the legal theory is **MDR Article 5(5) in-house exemption** (MDCG 2023-1). All Annex I General Safety and Performance Requirements (GSPRs) deemed applicable must still be met, under the hospital's own QMS.

## 2. What must simultaneously be true (all eight)

| Art 5(5) | Condition | This package provides | Hospital must confirm |
|---|---|---|---|
| (a) | No transfer to another legal entity | Doc 01 §2, Doc 13 repo rules | Same-entity use incl. remote viewing; no sharing with other hospitals/vendors |
| (b) | Manufacture + use under appropriate QMS | Doc 07 mapping + checklist | QMS covers design, build, deployment, use, monitoring |
| (c) | Target-group need not met at appropriate performance by equivalent CE device | Doc 04 method + Doc 14 HEOR outline | EUDAMED/market search done, documented, periodically repeated |
| (d) | Information to competent authority on request | Doc 11 §5 authority pack | Owner + 30-day retrieval commitment |
| (e) | Public declaration (identity + GSPR statement) | Doc 12 template | Published on hospital website, kept current |
| (f) | Documentation of facility/process/design/performance sufficient for authority review | Doc 06 index + Docs 08–10 | Frozen config + evidence actually exists |
| (g) | Manufacture per (f) documentation | Doc 11 §2 + Doc 09 release gates | Build-from-source reproducibility, change control |
| (h) | Review of clinical-use experience + corrective action | Doc 11 monitoring plan | Case review cadence, complaint/CAPA linkage |

Plus overarching: **non-industrial scale** (own-patient volume only, no batch production beyond need) and **Member-State law** (some states restrict in-house types — check `[HOSPITAL: Member State]` transposition first).

Failure of any one condition collapses the exemption. Fallbacks: CE-marked device, custom-made route (not applicable to multi-patient software), investigational-device route, or research-only use with no clinical reliance.

## 3. Why narrow scope was chosen

Full Arterial (access prediction, tortuosity thresholds driving decisions) would be MDSW with higher Rule 11 class, stronger clinical-evidence burden, and a much harder Art 5(5)(c) argument (several CE planning viewers exist). The **visualisation-only** scope:

- keeps clinician judgment as the sole decision-maker (reduces GSPR clinical-evidence depth but does not remove it),
- excludes the least-validated, highest-risk model (access prediction) from clinical display,
- makes non-equivalence arguable on **workflow integration + local-population performance** rather than on novelty alone.

Widening scope later = new intended purpose = repeat Docs 02–05, 08–10.

## 4. Cost and effort signals (order of magnitude, not a quote)

- Regulatory/QA: 6–12 weeks part-time for Docs 02–07 + declaration, assuming QMS exists.
- Engineering: freeze fork, SBOM, air-gapped packaging, DICOM/NIfTI pipeline hardening, UI read-only viewer integration, logging — typically larger than regulatory work.
- Validation: retrospective CTA set with ground-truth segmentations + prospective silent/shadow phase; validrig pack (Doc 10) structures this but does not replace radiologist overread studies.
- Ongoing: per-case logging, quarterly use review, annual non-equivalence re-check, re-validation on any model/data/pipeline change.

If the hospital cannot staff a device owner, a clinical lead, and QA oversight for the device lifetime, answer is NO-GO.

## 5. Record the decision

- Decision: `[HOSPITAL: GO / CONDITIONAL-GO / NO-GO, date, signers]`
- Conditions / rationale: `[HOSPITAL: ...]`
- Linked issue/PR in hospital QMS: `[HOSPITAL: ...]`
- Next review date: `[HOSPITAL: ...]`

If GO: proceed in document order 01 → 07 before any engineering beyond a non-clinical feasibility spike on de-identified data.

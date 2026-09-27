# 01, Executive Summary and Go/No-Go

> First-time reader: terms are spelled out on first use. Full list: `00-ABBREVIATIONS-AND-TERMINOLOGY.md`.
>
> Read time: ~10 minutes. Owner: hospital management + QA/regulatory jointly.
> Outcome: a recorded GO / CONDITIONAL / NO-GO for pursuing an Arterial-derived in-house device.

## 1. Proposition

A patient arrives with a suspected stroke. The team takes a head-and-neck CTA (Computed Tomography Angiography) scan. A hospital-owned software draws the vessels as a 3D map with center lines, shows it next to the original scan, and labels which software version drew it. The physician uses the map plus the scan to discuss clot removal. The map never decides anything. If the map cannot be drawn reliably, the software says so instead of guessing.

To get there, the hospital takes upstream Arterial v2.1 (a research framework, non-commercial licence), copies it into a frozen hospital-owned version, hardens it, validates it on local scans, and runs it only inside its own legal entity. No CE marking is sought; the legal theory is the MDR (Medical Device Regulation) Article 5(5) in-house exemption (MDCG 2023-1, Medical Device Coordination Group guidance). All applicable Annex I General Safety and Performance Requirements (GSPRs) must still be met, under the hospital's own QMS (Quality Management System).

Full device definition: [Doc 03](03-INTENDED-PURPOSE-AND-CLAIMS-BOUNDARY.md). Readers unfamiliar with the device definition review Doc 03 before continuing.

## 2. What must simultaneously be true (all eight)

| Art 5(5) | Condition | This package provides | Hospital must confirm |
|---|---|---|---|
| (a) | No transfer to another legal entity | Doc 02 §2, Doc 14 repo rules | Same-entity use incl. remote viewing; no sharing with other hospitals/vendors |
| (b) | Manufacture + use under appropriate QMS | Doc 08 mapping + checklist | QMS covers design, build, deployment, use, monitoring |
| (c) | Target-group need not met at appropriate performance by equivalent CE device | Doc 05 method + evidence | EUDAMED/market search done, documented, periodically repeated |
| (d) | Information to competent authority on request | Doc 12 §5 authority pack | Owner + 30-day retrieval commitment |
| (e) | Public declaration (identity + GSPR statement) | Doc 13 template | Published on hospital website, kept current |
| (f) | Documentation of facility/process/design/performance sufficient for authority review | Doc 07 index + Docs 10-11 | Frozen config + evidence actually exists |
| (g) | Manufacture per (f) documentation | Doc 12 §2 + Doc 10 release gates | Build-from-source reproducibility, change control |
| (h) | Review of clinical-use experience + corrective action | Doc 12 monitoring plan | Case review cadence, complaint/CAPA linkage |

Plus overarching: **non-industrial scale** (own-patient volume only, no batch production beyond need) and **Member-State law** (some states restrict in-house types, check `[HOSPITAL: Member State]` transposition first).

Failure of any one condition collapses the exemption. Fallbacks: CE-marked device, custom-made route (not applicable to multi-patient software), investigational-device route, or research-only use with no clinical reliance.

## 3. Why this scope and not the full Arterial

Section 1 describes a deliberately small claim set: a map display, a version label, and an explicit failure state (Doc 03). The reasons for this scope are as follows.

Even the narrow scope is Class IIb-equivalent: stroke is a critical situation and the map is used in near-term treatment planning (Doc 04 §2). Full Arterial can do more: predict access difficulty, score tortuosity, label vessels by name. Showing those outputs would push the device toward Class III-equivalent, demand deeper clinical evidence, and collide with existing CE-marked planning viewers, which weakens the Article 5(5)(c) non-equivalence case. The small scope keeps the physician as the sole decision-maker, keeps the hardest-to-prove model (access prediction) off the clinical screen, and leaves one ground for non-equivalence: measured performance on local data against a need fixed in advance (Doc 05 §3). Where a CE-marked advanced-visualisation platform already meets that need, the right answer is NO-GO (Doc 05 §2).

Widening scope later = new intended purpose = repeat Docs 04-06, 08-10.

## 4. Cost and effort signals (order of magnitude, not a quote)

- Regulatory/QA: 6-12 weeks part-time for Docs 04-08 + declaration, assuming QMS exists.
- Engineering: freeze fork, SBOM, air-gapped packaging, DICOM/NIfTI pipeline hardening, UI read-only viewer integration, logging, typically larger than regulatory work.
- Validation: retrospective CTA set with ground-truth segmentations + prospective silent/shadow phase; validrig pack (Doc 11) structures this but does not replace radiologist overread studies.
- Ongoing: per-case logging, periodic use review (Doc 12 cadence), annual non-equivalence re-check, re-validation on any model/data/pipeline change.

If the hospital cannot staff a device owner, a clinical lead, and QA oversight for the device lifetime, answer is NO-GO.

## 5. Record the decision

- Decision: `[HOSPITAL: GO / CONDITIONAL-GO / NO-GO, date, signers]`
- Conditions / rationale: `[HOSPITAL: ...]`
- Linked issue/PR in hospital QMS: `[HOSPITAL: ...]`
- Next review date: `[HOSPITAL: ...]`

If GO: proceed in document order 01 → 07 before any engineering beyond a non-clinical feasibility spike on de-identified data.

---
> Return to the [reading index](../../README.md#how-to-read-this-package).

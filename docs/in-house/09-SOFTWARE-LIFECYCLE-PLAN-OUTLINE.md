# 09, Software Lifecycle Plan Outline (IEC 62304 / IEC 82304-1, tailored)

> First-time reader: terms are spelled out on first use. Full list: `00-ABBREVIATIONS-AND-TERMINOLOGY.md`.
>
> Owner: engineering + QA. Assumed safety class: **B minimum, evaluate C** (Doc 03 §4). If C is confirmed, add segregation, detailed design, and enhanced integration testing beyond this outline.

## 1. Lifecycle model

V-model with gated releases (plan → requirements → architecture → implementation → integration → system test → release → deployment), mapped to hospital change control (SOP-009-equiv). No clinical deployment from `main`; only from signed release tags (`hosp-vX.Y.Z`). Upstream `main` is never pulled directly into clinical builds, changes arrive via reviewed cherry-picks.

## 2. Configuration and fork governance

- Fork: `[HOSPITAL: private repo URL]` branched from upstream commit `[SHA]`; hospital diff reviewed line-by-line; `THIRD_PARTY_NOTICES.md` + `LICENSE` preserved.
- Versioning: `hosp-vX.Y.Z` (X = purpose-affecting, Y = pipeline-affecting, Z = config/docs-only); build fingerprint recorded (Doc 06 §1).
- Reproducibility: locked container (`[HOSPITAL: Dockerfile digest]`), pinned `requirements` + conda VMTK pin, weight SHA256 checks at build and at load.
- Out-of-scope hiding: build flag `[HOSPITAL: e.g. HOSP_ENABLE_ACCESS_PREDICTION=OFF]` plus UI removal for hidden modules; proof test each release (flag-state assertion + interface crawl confirming clinical users cannot reach hidden outputs). Removal is allowed but not required. What matters is the proof, filed in Doc 06, and the wider-use path in Doc 01 section 3 for uncovering.

## 3. SOUP and SBOM

| SOUP | Version pin | Licence | Risk / control |
|---|---|---|---|
| torch / torch_geometric (+ CUDA) | `[HOSPITAL]` | BSD/MIT-family | GPU determinism note; CVE watch |
| nnU-Net v2 / MONAI / torchio | `[HOSPITAL]` | Apache-2.0 | Anomaly-list review per release |
| VMTK | `[HOSPITAL: conda pin]` | BSD | Conda-only install; containerise |
| TotalSegmentator `craniofacial_structures` weights | fold-0, Apache-2.0, `LICENSE`+`NOTICE` kept | Apache-2.0 | Only skull class used; failure → H1/H3 |
| Arterial weights (extracranial seg, landmark, labelling) | `[version+SHA256]` | CC BY-NC 4.0 | Hospital-use licence clearance (Doc 13); frozen |
| Python libs (nibabel, vtk, etc.) | `[SBOM]` | various | CVE scan `[tool+date]` |

SBOM location: `[HOSPITAL: QMS ref]`; updated every release; vulnerabilities triaged before release.

## 4. Usability engineering (IEC 62366-1, summary; detail in usability file)

Use specification: time-pressured planning discussion, dim reading room, interruptions. Critical tasks: (1) recognise device output vs native CTA, (2) detect QC-failure/degraded state, (3) complete overread attestation, (4) report incident. Formative → summative with representative users on hospital workstations; acceptance includes 100% overread-attestation compliance and zero silent-misinterpretation events in test scenarios. Results feed Doc 10.

## 5. Information security and data protection

- Deployment: on-prem, `[air-gapped / VLAN-isolated]`; no telemetry; no external model endpoints during inference.
- Controls: RBAC, audit trail (who viewed which case output when), encryption at rest/in transit, DICOM cache minimisation + retention `[HOSPITAL: e.g. 30 days]` + secure deletion, logging without PHI where possible.
- DPIA: `[HOSPITAL: ref]`; patient information per local rules (in-house device use disclosure as required).
- Security testing proportionate to exposure: dependency scan each build, hardening review each release, incident playbook linked to Doc 11.

## 6. Verification strategy

Unit (geometry utils, QC gates, provenance binding) → integration (CTA→NIfTI→mask→centerlines→viewer with synthetic transforms) → system (release-candidate on held-out scans, fault injection: corrupt DICOM, missing weights, GPU OOM) → release regression suite run on every tag. Trace matrix: requirement → test → result.

## 7. Release and deployment control (Art 5(5)(g))

Release decision signed by engineering + QA + clinical lead; installation qualification on each inference node (weight hashes, smoke case, viewer integration, rollback image ready); deployment log per node; no auto-update. Any weight, code, dependency, or protocol change = new release candidate + re-validation scoping (Doc 10 §5).

---
> Doubts? Return to the [reading index](../../README.md#how-to-read-this-package).

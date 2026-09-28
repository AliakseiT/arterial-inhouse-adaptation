# Abbreviations and terminology, read this first

This package is written for a mixed audience. Clinical, engineering, and regulatory readers meet here, and each group trips over the others' shorthand. Rule used across all docs: every abbreviation is spelled out on first use in each document, then abbreviated. This page is the shared reference. If a term below conflicts with your hospital usage, record the hospital term in your QMS and use it consistently.

## Clinical and imaging terms

| Short | Full | Plain meaning |
|---|---|---|
| CTA | Computed Tomography Angiography | A CT scan timed to show blood vessels with contrast dye. The only input this in-house device accepts. |
| AIS | Acute Ischaemic Stroke | A stroke caused by a blocked brain artery. The clinical context for this device. |
| MT | Mechanical Thrombectomy | Physically removing a clot with a catheter. The procedure whose planning discussion this device supports. |
| DSA | Digital Subtraction Angiography | X-ray imaging during catheter procedures. Mentioned only as a downstream procedure, not a device function. |
| PACS | Picture Archiving and Communication System | The hospital system that stores and displays scans. The device must plug into it without replacing it. |
| DICOM | Digital Imaging and Communications in Medicine | The standard format for clinical scans. The device gates on DICOM metadata before processing. |
| NIfTI | Neuroimaging Informatics Technology Initiative (format) | A research image format. The pipeline converts DICOM to NIfTI internally. Never shown to clinicians directly. |

## Regulatory terms

| Short | Full | Plain meaning |
|---|---|---|
| MDR | Medical Device Regulation (EU) 2017/745 | The EU law. Article 5(5) is the narrow exemption this package relies on. |
| AI Act | Regulation (EU) 2024/1689 on artificial intelligence, amended by Regulation (EU) 2026/1744 | Separate EU law for AI systems. Doc 02 section 6 explains why this device is not high-risk under it. |
| IVDR | In Vitro Diagnostic Regulation (EU) 2017/746 | The sister law for lab tests. Referenced only to avoid confusion. Not used here. |
| Art 5(5)(a)-(h) | Article 5, paragraph 5, conditions (a) through (h) | Eight conditions that must all hold. Fail one, lose the exemption. Doc 02 maps each. |
| GSPR | General Safety and Performance Requirements (MDR Annex I) | The safety and performance rules that still apply even under the exemption. Doc 06 checks each one. |
| MDCG 2023-1 | Medical Device Coordination Group guidance, January 2023 | The EU guidance explaining how authorities read Article 5(5). Not law, but auditors follow it. |
| MDSW | Medical Device Software | Software that counts as a device. This package assumes the fork qualifies (Doc 04). |
| EUDAMED | European Database on Medical Devices | The EU device database. Searched in Doc 05 to prove no equivalent device exists. |
| IFU | Instructions For Use | The clinician instructions. Here called IFU-equivalent because the format is adapted for in-house use. |
| UDI | Unique Device Identification | The standard device labelling system. No CE-UDI under the exemption, but internal identification is still required for traceability. |
| QMS | Quality Management System | The hospital system for controlling design, build, deployment, and monitoring. Assumed to exist. Never replaced by this package. |
| CAPA | Corrective and Preventive Action | The process for fixing causes, not just symptoms. Linked to clinical-use review (Doc 12). |
| PMS | Post-Market Surveillance | Systematic collection of use experience. Under the exemption this appears as clinical-use review per Art 5(5)(h), not full PMS. |
| SSP | Summary of Safety and (clinical) Performance | Public summaries for higher-class devices in EUDAMED. Used as a Doc 05 source where available. |
| In-house device | No short form | A device manufactured and used only within the same EU health institution, meeting all Art 5(5) conditions (MDCG 2023-1 section 3.1). |
| Health institution | No short form | An organisation whose primary purpose is the care or treatment of patients or the promotion of public health (MDR Art 2(36)). |
| Non-industrial scale | No short form | Production limited to own-patient need. No commercial-scale manufacturing (Art 5(5) last subparagraph, MDCG 2023-1 section 3.11). |

## Engineering and AI terms

| Short | Full | Plain meaning |
|---|---|---|
| SOUP | Software Of Unknown Provenance | Third-party code or pretrained weights the hospital did not develop. Listed, versioned, and risk-assessed, never trusted blindly. |
| SBOM | Software Bill Of Materials | The versioned list of every dependency and weight. Rebuilt every release. |
| GPU | Graphics Processing Unit | The hardware that runs the models. Pinned with driver and CUDA versions. |
| CUDA | Compute Unified Device Architecture | NVIDIA software layer for GPU computing. Version mismatches break reproducibility. |
| VMTK | Vascular Modeling Toolkit | The open-source library that extracts vessel centerlines. Conda-only install. |
| GNN | Graph Neural Network | The model type used for vessel labelling upstream. Disabled from clinical display in this scope. |
| QC | Quality Control | Automated gates that reject bad inputs or suppress bad outputs instead of failing silently. |
| PHI | Protected Health Information | Patient-identifiable data. Never enters this repo. Stays in the hospital record. |
| DPIA | Data Protection Impact Assessment | The GDPR analysis for processing scan data. Filed in the hospital QMS. |
| RBAC | Role-Based Access Control | Permissions by role, so only trained users see device output. |
| CVE | Common Vulnerabilities and Exposures | Public software vulnerability entries. Checked per build (Doc 10). |

## Project-specific terms

| Term | Meaning |
|---|---|
| Upstream | The public research project FLOWCAT-CV/arterial, version 2.1, owned by VHIR and Universitat de Barcelona. |
| Fork | The hospital-owned copy of upstream code, frozen at one commit plus hospital changes. The fork, not upstream, is the candidate device. |
| Frozen build | Source commit plus pinned dependencies plus hashed weights plus config, released as one versioned unit. Only frozen builds may reach clinical use. |
| Overread | The mandatory independent clinician review of the source CTA. Device output is never standalone. Tested under time pressure in validation. |
| Phase 1 / Phase 2 | Phase 1 is the Doc 03 visualisation aid, the only claimed purpose. Phase 2 is a possible later access-difficulty decision support, outlined but not claimed (Doc 16). |
| Shadow phase | Prospective validation where the device runs in parallel with care but does not influence decisions. Doc 11 defines it. |
| validrig | The DearAuditor validation-harness engine. A pack describes one intended use. The engine stays untouched. |
| HEOR | Health Economics and Outcomes Research. Here only the viability analysis (Doc 15), not a reimbursement dossier. |
| HTA | Health Technology Assessment. Mentioned only to bound what Doc 15 is not. |

## Pinned references (verify currency at adoption)

- MDR (EU) 2017/745, Art 2(1), 2(36), 5(5), 10(9), Annex I, Annex VIII Rule 11, Annex XIII (custom-made, contrast only).
- MDCG 2023-1 (Jan 2023): health-institution exemption guidance with the Annex A declaration model.
- MDCG 2019-11 rev.1 (June 2025): Medical Device Software qualification and classification, Annex III Rule 11 table, Annex IV examples.
- IMDRF/SaMD WG/N12FINAL:2014: Software as a Medical Device risk categorisation framework (International Medical Device Regulators Forum).
- AI Act: Regulation (EU) 2024/1689, Art 3, 4, 6, 50, Annex III point 5(d); Digital Omnibus on AI, Regulation (EU) 2026/1744 (in force 2026-07-27).
- ISO 14971 (risk), IEC 62304 plus IEC 82304-1 (software lifecycle and health software), IEC 62366-1 (usability), ISO 13485 and 15189 (Quality Management System context), ISO/IEC 27001 plus 42001 (security and AI management).
- Upstream: `FLOWCAT-CV/arterial` v2.1 (PolyForm NC 1.0.0), Zenodo `10.5281/zenodo.22694951` (CC BY-NC 4.0, Creative Commons Attribution NonCommercial), TotalSegmentator Apache-2.0 sub-model; Canals 2023, Wasserthal 2023, Beyer 2026, Isensee 2021.
- Hospital-agnostic Quality Management System model: `AliakseiT/dearauditor-qms-baseline` (SOP and work-instruction record templates, mapped, not vendored).
- Validation engine: `AliakseiT/validrig` (`rig`, pack-based, on-prem, append-only runs).
- Value methods: `AliakseiT/heor-skills` (deterministic `@heor/engine`, drafts-not-submissions).

## Version pins used while drafting

- Upstream Arterial: `v2.1`, Python 3.11, torch 2.6.0 with CUDA 12.4 (Linux GPU), VMTK via conda-forge, model record `22694951`.
- This package: `v0.3.0-DRAFT`, `2026-09-28`. Hospital to re-verify upstream state at fork time. Upstream moves, the frozen fork does not.

---
> Return to the [reading index](../../README.md#how-to-read-this-package).

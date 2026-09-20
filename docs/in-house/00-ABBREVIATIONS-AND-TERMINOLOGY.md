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
| IVDR | In Vitro Diagnostic Regulation (EU) 2017/746 | The sister law for lab tests. Referenced only to avoid confusion. Not used here. |
| Art 5(5)(a)-(h) | Article 5, paragraph 5, conditions (a) through (h) | Eight conditions that must all hold. Fail one, lose the exemption. Doc 01 maps each. |
| GSPR | General Safety and Performance Requirements (MDR Annex I) | The safety and performance rules that still apply even under the exemption. Doc 05 checks each one. |
| MDCG 2023-1 | Medical Device Coordination Group guidance, January 2023 | The EU guidance explaining how authorities read Article 5(5). Not law, but auditors follow it. |
| MDSW | Medical Device Software | Software that counts as a device. This package assumes the fork qualifies (Doc 03). |
| EUDAMED | European Database on Medical Devices | The EU device database. Searched in Doc 04 to prove no equivalent device exists. |
| IFU | Instructions For Use | The clinician instructions. Here called IFU-equivalent because the format is adapted for in-house use. |
| UDI | Unique Device Identification | The standard device labelling system. No CE-UDI under the exemption, but internal identification is still required for traceability. |
| QMS | Quality Management System | The hospital system for controlling design, build, deployment, and monitoring. Assumed to exist. Never replaced by this package. |
| CAPA | Corrective and Preventive Action | The process for fixing causes, not just symptoms. Linked to clinical-use review (Doc 11). |
| PMS | Post-Market Surveillance | Systematic collection of use experience. Under the exemption this appears as clinical-use review per Art 5(5)(h), not full PMS. |
| SSP | Summary of Safety and (clinical) Performance | Public summaries for higher-class devices in EUDAMED. Used as a Doc 04 source where available. |

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
| CVE | Common Vulnerabilities and Exposures | Public software vulnerability entries. Checked per build (Doc 09). |

## Project-specific terms

| Term | Meaning |
|---|---|
| Upstream | The public research project FLOWCAT-CV/arterial, version 2.1, owned by VHIR and Universitat de Barcelona. |
| Fork | The hospital-owned copy of upstream code, frozen at one commit plus hospital changes. The fork, not upstream, is the candidate device. |
| Frozen build | Source commit plus pinned dependencies plus hashed weights plus config, released as one versioned unit. Only frozen builds may reach clinical use. |
| Overread | The mandatory independent clinician review of the source CTA. Device output is never standalone. Tested under time pressure in validation. |
| Shadow phase | Prospective validation where the device runs in parallel with care but does not influence decisions. Doc 10 defines it. |
| validrig | The DearAuditor validation-harness engine. A pack describes one intended use. The engine stays untouched. |
| HEOR | Health Economics and Outcomes Research. Here only a small workflow-value outline (Doc 14), not a reimbursement dossier. |
| HTA | Health Technology Assessment. Mentioned only to bound what Doc 14 is not. |

---
> Return to the [reading index](../../README.md#how-to-read-this-package).

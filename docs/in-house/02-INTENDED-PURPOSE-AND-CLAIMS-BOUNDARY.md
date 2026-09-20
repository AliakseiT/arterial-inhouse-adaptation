# 02 — Intended Purpose and Claims Boundary (Narrow Scope)

> Owner: clinical lead (stroke neurology / interventional neuroradiology) + QA. This is the primary design input (cf. QMS-baseline `records/mdf/intended_use.md`, SOP-008). Any widening = design change.

## 1. In-house device identity

- In-house device name: `[HOSPITAL: e.g. HOSP-ART-VIZ]`
- Version: `[HOSPITAL: frozen fork tag, e.g. 1.0.0+hosp1]`
- Upstream basis: `FLOWCAT-CV/arterial` commit `[HOSPITAL: pinned commit SHA]` + hospital diff `[HOSPITAL: fork commit SHA]`, tag `v2.1`-derived.
- Legal manufacturer/user: `[HOSPITAL: single legal entity name + address]` — same entity for manufacture and use.

## 2. Intended purpose statement (proposed narrow wording — adapt, then approve)

> `[HOSPITAL-DEVICE]` is an in-house CTA vascular visualisation aid for use inside `[HOSPITAL]` only. It renders extracranial vessel segmentation and centerlines from head-and-neck CTA alongside the native CTA to support planning discussion for adults with suspected acute ischaemic stroke considered for mechanical thrombectomy. All clinical decisions are made by the responsible physician from the source CTA and standard clinical information; the device output is adjunctive and requires mandatory overread. The device does not triage, diagnose, or recommend treatment or access route.

## 3. In-scope claims (exhaustive)

1. Display of binary vessel mask + centerlines derived from the hospital-frozen pipeline, co-registered to input CTA grid.
2. Display of pipeline provenance per case (device version, model versions, input StudyInstanceUID hash, QC flags).
3. Failure signalling: explicit "no output / degraded output" state when QC checks fail.
4. On-prem execution; no external data transfer during inference.

## 4. Out-of-scope firewall (displaying any of these to clinicians voids this scope)

- Access-difficulty probability, attention maps, tortuosity scores as thresholds, or any "difficult/easy" flag.
- Intracranial-only mode outputs, landmark-based measurements, or automated reports beyond visualisation.
- Autonomous triage, prioritisation, diagnosis, or treatment recommendation.
- Use outside `[HOSPITAL]` entity, outside adult suspected-AIS planning discussion, or on non-CTA modalities.
- Paediatric, non-stroke, or non-head-and-neck use.

Upstream modules `access_prediction`, `feature_extraction` quantitative outputs, and `vessel_labelling` names **must be disabled or hidden** in the clinical build; if retained for engineering, they are non-clinical and un-displayed. Document the disablement (build flag + verification test) in Doc 06.

## 5. Users and environment

- Intended users: `[HOSPITAL: e.g. board-certified neuroradiologists / interventionalists / stroke neurologists]` trained per Doc 07 training plan.
- Non-users: ED triage nurses, patients, external referrers (no direct output).
- Use environment: `[HOSPITAL: PACS/viewer integration description, workstation type, network zone]`; inference on `[HOSPITAL: GPU server, air-gapped/VLAN details]`.
- Input: head-and-neck CTA meeting `[HOSPITAL: acquisition spec — kVp, slice thickness, contrast phase, matrix]`; non-conforming inputs rejected with message.
- Output location: `[HOSPITAL: viewer overlay / secondary capture, never overwriting source CTA]`.

## 6. System boundary

- In-house device = frozen fork + frozen weights + deployment config + clinician-facing instructions (Docs 05/06/09).
- NOT part of device: PACS, hospital network, upstream repo, training workstations, research notebooks.
- Interfaces treated as SOUP/external: nnU-Net, MONAI, VMTK, PyTorch Geometric, TotalSegmentator mandible model (Apache-2.0), CUDA/drivers — listed in SBOM (Doc 09).

## 7. Approval

- Clinical lead: `[HOSPITAL: name/date/signature]`
- QA lead: `[HOSPITAL: name/date/signature]`
- Linked risk plan: Doc 08; linked validation: Doc 10.

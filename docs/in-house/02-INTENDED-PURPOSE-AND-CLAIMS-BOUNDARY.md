# 02, Intended Purpose and Claims Boundary (Narrow Scope)

> First-time reader: terms are spelled out on first use. Full list: `00-ABBREVIATIONS-AND-TERMINOLOGY.md`.
>
> Owner: clinical lead (stroke neurology / interventional neuroradiology) + QA. This is the primary design input (cf. QMS-baseline `records/mdf/intended_use.md`, SOP-008). Any widening = design change.

## 1. In-house device identity

- In-house device name: `[HOSPITAL: e.g. HOSP-ART-VIZ]`
- Version: `[HOSPITAL: frozen fork tag, e.g. 1.0.0+hosp1]`
- Upstream basis: `FLOWCAT-CV/arterial` commit `[HOSPITAL: pinned commit SHA]` + hospital diff `[HOSPITAL: fork commit SHA]`, tag `v2.1`-derived.
- Legal manufacturer/user: `[HOSPITAL: single legal entity name + address]`, same entity for manufacture and use.

## 2. What the device does, in plain words

A patient arrives with a suspected stroke. The team takes a head-and-neck CTA (Computed Tomography Angiography), a scan that shows the blood vessels. The device takes that scan and draws two extra pictures next to it: the vessels as a 3D shape, and the center lines running through them, like a map of the road network the catheter must travel. The physician looks at these pictures side by side with the original scan while discussing whether and how to remove the clot. The pictures add nothing the scan does not contain. They only make the vessel course easier to see and talk about.

That is the whole device. A map display, plus a label saying which software version drew it, plus an honest failure message when the map cannot be drawn. Read the formal statement below once the picture is clear.

Intended purpose statement (proposed narrow wording, adapt, then approve):

> `[HOSPITAL-DEVICE]` is an in-house CTA vascular visualisation aid for use inside `[HOSPITAL]` only. It renders extracranial vessel segmentation and centerlines from head-and-neck CTA alongside the native CTA to support planning discussion for adults with suspected acute ischaemic stroke considered for mechanical thrombectomy. All clinical decisions are made by the responsible physician from the source CTA and standard clinical information; the device output is adjunctive and requires mandatory overread. The device does not triage, diagnose, or recommend treatment or access route.

## 3. In-scope claims (exhaustive)

In plain words first, technical terms second:

1. The vessel map display: the software marks which picture elements belong to blood vessels (the vessel mask) and draws the lines through their centers (centerlines), aligned onto the original scan grid so map and scan overlap exactly.
2. The provenance label: every map carries its own identity card, device version, model versions, a hash (a fingerprint number) of the input scan identity, and the Quality Control verdict. A map can never be mistaken for another case or another software version.
3. Honest failure: when Quality Control checks fail, the device shows an explicit no-output or degraded-output state. It never shows a plausible-looking wrong map silently.
4. Local execution: the computation runs on hospital computers. Scan data leaves the hospital for no step of it.

## 4. Where the device stops (out-of-scope firewall)

The list above is everything the device does. Everything below stays a physician task, and showing any of it to clinicians voids this scope and triggers the wider-use path in Doc 01 section 3:

- Access-difficulty probability, attention maps, tortuosity scores as thresholds, or any "difficult/easy" flag.
- Intracranial-only mode outputs, landmark-based measurements, or automated reports beyond visualisation.
- Autonomous triage, prioritisation, diagnosis, or treatment recommendation.
- Use outside `[HOSPITAL]` entity, outside adult suspected-AIS planning discussion, or on non-CTA modalities.
- Paediatric, non-stroke, or non-head-and-neck use.

Upstream modules `access_prediction`, `feature_extraction` quantitative outputs, and `vessel_labelling` names are hidden from the clinical interface by configuration in this scope. The code may remain in the fork for engineering evaluation, but clinicians cannot reach it. Each release proves this with a UI crawl plus a flag-state test, recorded in Doc 06. Uncovering any of it for clinical display follows the wider-use path in Doc 01 section 3: revised purpose, fresh justification, re-validation, new declaration.

## 5. Users and environment

- Intended users: `[HOSPITAL: e.g. board-certified neuroradiologists / interventionalists / stroke neurologists]` trained per Doc 07 training plan.
- Non-users: ED triage nurses, patients, external referrers (no direct output).
- Use environment: `[HOSPITAL: PACS/viewer integration description, workstation type, network zone]`; inference on `[HOSPITAL: GPU server, air-gapped/VLAN details]`.
- Input: head-and-neck CTA meeting `[HOSPITAL: acquisition spec, kVp, slice thickness, contrast phase, matrix]`; non-conforming inputs rejected with message.
- Output location: `[HOSPITAL: viewer overlay / secondary capture, never overwriting source CTA]`.

## 6. System boundary

- In-house device = frozen fork + frozen weights + deployment config + clinician-facing instructions (Docs 05/06/09).
- NOT part of device: PACS, hospital network, upstream repo, training workstations, research notebooks.
- Interfaces treated as SOUP/external: nnU-Net, MONAI, VMTK, PyTorch Geometric, TotalSegmentator mandible model (Apache-2.0), CUDA/drivers, listed in SBOM (Doc 09).

## 7. Approval

- Clinical lead: `[HOSPITAL: name/date/signature]`
- QA lead: `[HOSPITAL: name/date/signature]`
- Linked risk plan: Doc 08; linked validation: Doc 10.

---
> Doubts? Return to the [reading index](../../README.md#how-to-read-this-package).

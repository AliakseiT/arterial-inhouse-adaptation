# 08, Risk Management Plan Outline (ISO 14971, tailored)

> First-time reader: terms are spelled out on first use. Full list: `00-ABBREVIATIONS-AND-TERMINOLOGY.md`.
>
> Owner: QA + clinical + engineering. The risk file is the backbone of the GSPR claim, keep it live from first build through retirement.

## 1. Plan essentials

- Scope: Doc 02 narrow purpose only. Out-of-scope outputs are **hazards by presence** (must remain disabled).
- Method: ISO 14971; severity × occurrence with ALARP; benefit-risk per Annex I §1/§8; traceability need→hazard→control→verification (link to QMS-baseline `records/risk/` templates).
- Team: `[HOSPITAL: clinical, engineering, QA, IT/security, human-factors]`.
- Review cadence: `[HOSPITAL: e.g. each release + quarterly use-review + post-incident]`; risk file versioned with device version.

## 2. Preliminary hazard list (expand in hospital file; non-exhaustive starter)

| # | Hazard / hazardous situation | Foreseeable harm | Controls (design / protective / information) | Verification |
|---|---|---|---|---|
| H1 | False-negative vessels / truncated centerlines relied on in discussion | Delayed or misguided access planning, prolonged procedure | QC completeness gate + fail-stop; provenance display; mandatory overread; input spec enforcement | Local validation completeness metric; usability overread test |
| H2 | False-positive vessels / artefacts presented as anatomy | Confusion, wrong-side/level discussion | Artefact抑制 via operating-point choice; visual distinction native vs derived; overread | FP review in validation; summative evaluation |
| H3 | Geometric distortion (misregistration, wrong scale/orientation) | Misjudged tortuosity/length | Registration check + orientation/scale assertion; display of source grid; automated fail on mismatch | Integration tests with synthetic transforms |
| H4 | Silent failure / stale output shown as current | Decisions on wrong patient or outdated result | Per-case provenance binding (StudyInstanceUID hash); no display without fresh QC pass; cache invalidation | Fault-injection tests |
| H5 | Automation bias under time pressure (overread skipped) | Over-reliance despite disclaimer | Workflow forcing function (overread attestation click); time-pressure summative test; training | Usability report |
| H6 | Out-of-scope output visible (access score, tortuosity flag) | Off-label reliance | Build-time disablement + verification test + UI audit each release | Disablement proof test |
| H7 | Input out-of-spec (paediatric, non-CTA, poor contrast) processed anyway | Misleading output | DICOM metadata gating + contrast/quality check + rejection message | Boundary tests |
| H8 | Model/data drift (new scanner/protocol, silent upstream weight swap) | Performance decay | Frozen weights + hash check at load; protocol-stratified monitoring; change-triggered re-validation | Monitoring chart (Doc 11) |
| H9 | Security/PHI breach (DICOM cache, logs, remote viewing) | Privacy harm, loss of trust | On-prem/air-gap, RBAC, encryption at rest/in transit, audit trail, DPIA | Security review + pentest proportionate |
| H10 | Unavailable/slow inference delaying planning discussion | Workflow delay in time-critical stroke care | Explicit non-time-critical positioning is **not** credible in stroke, instead: latency budget, fallback to native-CTA-only workflow, downtime procedure | Latency + downtime drill |

H10 note: do not claim "not for time-critical use" while deploying in stroke planning, the risk file must handle time pressure honestly.

## 3. SOUP/ML-specific risks

- Pretrained weights as SOUP: unknown training-data gaps, subgroup performance variance, version confusion. Controls: frozen version + hash, local stratified validation (age/sex/scanner/protocol), anomaly logging.
- Dependency SOUP (nnU-Net, VMTK, PyTorch stack): CVE monitoring, pin + rebuild test, anomaly process per IEC 62304 §7.1.3.
- TotalSegmentator mandible sub-model: failure affects head/neck split → propagate as H1/H3 input-qualification risk.

## 4. Residual risk and benefit-risk

- Residual risk table: `[HOSPITAL: per-hazard residual + acceptability]`.
- Benefit-risk statement: planning-discussion benefit `[HOSPITAL]` vs residual `[HOSPITAL]`; signed by clinical lead + QA. If any residual is unacceptable without a new control, no release.

## 5. Production/post-production information loop

Feeds Doc 11: discordance log, QC-failure log, complaint/incident review, periodic risk-review demos. New hazards → update file → assess re-validation → update declaration if GSPR picture changes.

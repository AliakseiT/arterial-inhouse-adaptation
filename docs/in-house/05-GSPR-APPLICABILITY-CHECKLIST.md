# 05 — GSPR Applicability Checklist (Annex I)

> Owner: QA/engineering. Instruction: for each GSPR, mark Applicable / Not applicable (with reason), state compliance method, and point to evidence (Doc 06 index). "Not applicable" needs a reasoned justification — it is itself a claim. Unmet applicable GSPRs must appear with justification in the Doc 12 public declaration.

## How to read the table

- **GSPR ref** follows MDR Annex I chapters. Only requirements relevant to a non-implantable, non-sterile, non-measuring, software-only visualisation aid are expanded; adapt if scope changes.
- Evidence pointers are to Art 5(5)(f) documentation (Doc 06), not to upstream papers alone.

| Annex I GSPR | Applicability | Compliance method (hospital fork) | Evidence (Doc 06 ref) |
|---|---|---|---|
| Ch I.1–4: Safety/performance, risk reduction ALARP, lifetime, transport/storage | Applicable | Risk management per Doc 08; lifetime defined as frozen-version service period; no transport (on-prem) | Doc 08 risk file; Doc 06 §6 lifetime |
| I.5–8: Chemical/physical/biological, infection, sterility | Not applicable — pure software, no patient/body contact | Reason: no materials, no sterility chain | N/A (record rationale) |
| I.9: Construction/environmental (EMC, power, ergonomics of hardware) | Partially applicable — deployment hardware environment | Qualified workstations/GPU server spec, UPS/thermal, display calibration for review workstations | Doc 06 §3 facility spec |
| I.10–11: Mechanical, thermal, radiation, software-specific safety | Applicable (software safety) | IEC 62304 Class B/C controls (Doc 09); defensive input validation; fail-stop on QC failure; no silent degradation | Doc 09 + V&V (Doc 10) |
| I.12: Devices with diagnostic/measuring function — accuracy/precision/stability | Applicable by analogy | Segmentation/centerline performance characterised on local data (Dice, centerline completeness, failure rate) with acceptance criteria; stability across scanner/protocol strata | Doc 10 validation report |
| I.13: Protection against radiation | Not applicable (no radiation emission; CTA acquired by separate CE scanner) | Reason recorded | N/A |
| I.14: Electronic programmable systems — repeatability, reliability, security, single-fault | Applicable (core software GSPR) | Repeatability (deterministic inference, seeded builds); single-fault analysis (fail-stop, QC gates); information security per Doc 09 §5 | Docs 09/10 |
| I.15: Active implantable — N/A | Not applicable | Reason recorded | N/A |
| I.16: Risks fromergonomics/use error (usability) | Applicable | IEC 62366-1 use engineering: overread workflow, warning design, time-pressure analysis, summative evaluation of overread compliance | Doc 09 §4 + Doc 10 usability |
| I.17: Electromagnetic — N/A beyond I.9 | See I.9 | — | — |
| I.18: Performance + benefit-risk | Applicable | Performance spec (Doc 02/06 §4) + benefit-risk statement in risk file; residual risk vs planning-discussion benefit | Doc 08 benefit-risk |
| Ch II (design/manufacture specifics 10–22): mostly N/A for pure software except software lifecycle | Applicable subset | Documented per Doc 09; no CMR/phthalates/nanomaterials claims (record N/A with reason) | Doc 09, SBOM |
| Ch III.23: Labelling + information supplied (IFU-equivalent) | Applicable — adapted | Clinician-facing instructions: purpose, limits, overread duty, input requirements, failure states, version/provenance, support route; in `[HOSPITAL: language(s)]`; versioned with device | Doc 06 §7 (IFU-equivalent) |
| Ch III: UDI | Not applicable as CE-UDI, but **internal identification required** for (e)(h) | Internal device ID + version + per-case provenance (StudyInstanceUID link, model versions) enabling traceability and corrective action | Doc 11 traceability |
| Post-market (Annex I §3 risk + Art 5(5)(h)) | Applicable via (h) | Use-review plan, discordance log, incident/CAPA linkage (Doc 11) | Doc 11 |

## Benefit-risk conclusion (to be completed)

> Residual risks `[HOSPITAL: summarise from Doc 08]` are / are not acceptable against the planning-discussion benefit `[HOSPITAL: ...]` because `[HOSPITAL: ...]`. Signed `[QA + clinical lead + date]`.

## Unmet-GSPR register (must mirror Doc 12)

| GSPR | Why not fully met | Justification / mitigation | Authority-communication status |
|---|---|---|---|
| `[HOSPITAL: none expected at GO]` | | | |

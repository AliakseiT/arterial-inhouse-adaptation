# 06, GSPR Applicability Checklist (Annex I)

> First-time reader: terms are spelled out on first use. Full list: `00-ABBREVIATIONS-AND-TERMINOLOGY.md`.
>
> Owner: QA/engineering. Instruction: for each GSPR, mark Applicable / Not applicable (with reason), state compliance method, and point to evidence (Doc 07 index). "Not applicable" needs a reasoned justification, it is itself a claim. Unmet applicable GSPRs must appear with justification in the Doc 13 public declaration.

## How to read the table

- **GSPR ref** follows MDR Annex I chapters. Only requirements relevant to a non-implantable, non-sterile, non-measuring, software-only visualisation aid are expanded; adapt if scope changes.
- Evidence pointers are to Art 5(5)(f) documentation (Doc 07), not to upstream papers alone.

| Annex I GSPR | Applicability | Compliance method (hospital fork) | Evidence (Doc 07 ref) |
|---|---|---|---|
| Ch I.1-4: Safety/performance, risk reduction ALARP, lifetime, transport/storage | Applicable | Risk management per Doc 09; lifetime defined as frozen-version service period; no transport (on-prem) | Doc 09 risk file; Doc 07 §6 lifetime |
| I.5-8: Chemical/physical/biological, infection, sterility | Not applicable, pure software, no patient/body contact | Reason: no materials, no sterility chain | N/A (record rationale) |
| I.9: Construction/environmental (EMC, power, ergonomics of hardware) | Partially applicable, deployment hardware environment | Qualified workstations/GPU server spec, UPS/thermal, display calibration for review workstations | Doc 07 §3 facility spec |
| I.10-11: Mechanical, thermal, radiation, software-specific safety | Applicable (software safety) | IEC 62304 Class B/C controls (Doc 10); defensive input validation; fail-stop on QC failure; no silent degradation | Doc 10 + V&V (Doc 11) |
| I.12: Devices with diagnostic/measuring function, accuracy/precision/stability | Applicable by analogy | Segmentation/centerline performance characterised on local data (Dice, centerline completeness, failure rate) with acceptance criteria; stability across scanner/protocol strata | Doc 11 validation report |
| I.13: Protection against radiation | Not applicable (no radiation emission; CTA acquired by separate CE scanner) | Reason recorded | N/A |
| I.14: Electronic programmable systems, repeatability, reliability, security, single-fault | Applicable (core software GSPR) | Repeatability (deterministic inference, seeded builds); single-fault analysis (fail-stop, QC gates); information security per Doc 10 §5 | Docs 10/10 |
| I.15: Active implantable, N/A | Not applicable | Reason recorded | N/A |
| I.16: Risks fromergonomics/use error (usability) | Applicable | IEC 62366-1 use engineering: overread workflow, warning design, time-pressure analysis, summative evaluation of overread compliance | Doc 10 §4 + Doc 11 usability |
| I.17: Electromagnetic, N/A beyond I.9 | See I.9 |, |, |
| I.18: Performance + benefit-risk | Applicable | Performance spec (Doc 04/07 §4) + benefit-risk statement in risk file; residual risk vs planning-discussion benefit | Doc 09 benefit-risk |
| Ch II (design/manufacture specifics 10-22): mostly N/A for pure software except software lifecycle | Applicable subset | Documented per Doc 10; no CMR/phthalates/nanomaterials claims (record N/A with reason) | Doc 10, SBOM |
| Ch III.23: Labelling + information supplied (IFU-equivalent) | Applicable, adapted | Clinician-facing instructions: purpose, limits, overread duty, input requirements, failure states, version/provenance, support route; in `[HOSPITAL: language(s)]`; versioned with device | Doc 07 §7 (IFU-equivalent) |
| Ch III: UDI | Not applicable as CE-UDI, but **internal identification required** for (e)(h) | Internal device ID + version + per-case provenance (StudyInstanceUID link, model versions) enabling traceability and corrective action | Doc 12 traceability |
| Post-market (Annex I §3 risk + Art 5(5)(h)) | Applicable via (h) | Use-review plan, discordance log, incident/CAPA linkage (Doc 12) | Doc 12 |

## Benefit-risk conclusion (to be completed)

> Residual risks `[HOSPITAL: summarise from Doc 09]` are / are not acceptable against the planning-discussion benefit `[HOSPITAL: ...]` because `[HOSPITAL: ...]`. Signed `[QA + clinical lead + date]`.

## Unmet-GSPR register (must mirror Doc 13)

| GSPR | Why not fully met | Justification / mitigation | Authority-communication status |
|---|---|---|---|
| `[HOSPITAL: none expected at GO]` | | | |

---
> Return to the [reading index](../../README.md#how-to-read-this-package).

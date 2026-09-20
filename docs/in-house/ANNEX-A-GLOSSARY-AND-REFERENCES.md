# Annex A, Glossary and References

## Glossary

| Term | Meaning in this package |
|---|---|
| In-house device | Device manufactured and used only within the same EU health institution meeting all Art 5(5) conditions (MDCG 2023-1 §3.1). |
| Health institution | Organisation whose primary purpose is care/treatment of patients or promotion of public health (MDR Art 2(36)). |
| Non-industrial scale | Production limited to own-patient need; no commercial-scale manufacturing (Art 5(5) last subparagraph; MDCG §3.9). |
| MDSW | Medical Device Software (MDCG 2019-11). |
| GSPR | General Safety and Performance Requirements, MDR Annex I. |
| SOUP | Software of Unknown Provenance (IEC 62304), includes pretrained weights and third-party libs. |
| SBOM | Software Bill of Materials. |
| Overread | Mandatory independent clinician review of source CTA; device output never standalone. |
| Frozen build | Source commit + dependency pins + weight hashes + config released as a single versioned unit. |

## Pinned references (verify currency at adoption)

- MDR (EU) 2017/745, Art 2(1), 2(36), 5(5), 10(9), Annex I, Annex VIII Rule 11, Annex XIII (custom-made, contrast only).
- MDCG 2023-1 (Jan 2023): health-institution exemption guidance + Annex A declaration model.
- MDCG 2019-11: MDSW qualification/classification.
- ISO 14971 (risk), IEC 62304 + IEC 82304-1 (software lifecycle/health software), IEC 62366-1 (usability), ISO 13485/15189 (QMS context), ISO/IEC 27001 + 42001 (security/AI management).
- Upstream: `FLOWCAT-CV/arterial` v2.1 (PolyForm NC 1.0.0), Zenodo `10.5281/zenodo.22694951` (CC BY-NC 4.0), TotalSegmentator Apache-2.0 sub-model; Canals 2023, Wasserthal 2023, Beyer 2026, Isensee 2021.
- Hospital-agnostic QMS model: `AliakseiT/dearauditor-qms-baseline` (SOP/WI/record templates, mapped, not vendored).
- Validation engine: `AliakseiT/validrig` (`rig`, pack-based, on-prem, append-only runs).
- Value methods: `AliakseiT/heor-skills` (deterministic `@heor/engine`, drafts-not-submissions).

## Version pins used while drafting

- Upstream Arterial: `v2.1`, Python 3.11, torch 2.6.0/cu124 (Linux GPU), VMTK via conda-forge, model record `22694951`.
- This package: `v0.1.0-DRAFT`, `2026-09-20`. Hospital to re-verify upstream state at fork time, upstream moves, the frozen fork does not.

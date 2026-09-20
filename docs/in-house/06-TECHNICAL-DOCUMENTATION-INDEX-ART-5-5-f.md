# 06, Technical Documentation Index, Art 5(5)(f)

> First-time reader: terms are spelled out on first use. Full list: `00-ABBREVIATIONS-AND-TERMINOLOGY.md`.
>
> Owner: engineering + QA. Purpose: the single index an authority uses to understand facility, process, design, and performance. Every row must resolve to a controlled hospital-QMS record, not to upstream URLs.

## 1. Device identification

| Item | Value |
|---|---|
| In-house device ID | `[HOSPITAL: HOSP-ART-VIZ + version]` |
| Upstream basis | `FLOWCAT-CV/arterial` commit `[SHA]`, tag `v2.1`-derived; hospital fork commit `[SHA]` |
| Model weights | `[per-model version + SHA256 + source (Zenodo DOI 10.5281/zenodo.22694951 or hospital-retrained) + licence]` |
| Build fingerprint | `[HOSPITAL: reproducible-build hash, builder identity, date]` |
| Status | `[DRAFT / FROZEN / DEPLOYED / RETIRED]` |

## 2. Manufacturing facility (software)

- Build environment: `[HOSPITAL: locked container/VM spec, OS, CUDA/cuDNN, Python 3.11, pinned requirements, VMTK source]`
- Build site / operator roles: `[HOSPITAL: ...]`; segregation of build vs clinical environments.
- Deployment facility: `[HOSPITAL: server room, network zone, air-gap/VLAN, GPU nodes, PACS integration point]`
- Records: `[HOSPITAL: QMS refs for facility qualification, backup/restore]`

## 3. Manufacturing process

1. Fork + freeze (Doc 13) → 2. Dependency pin + SBOM (Doc 09) → 3. Hospital hardening diff (DICOM intake, QC gates, viewer integration, access-prediction disablement) → 4. Verification (unit/integration, build reproducibility) → 5. Validation on local data (Doc 10) → 6. Risk/usability sign-off (Docs 08/09) → 7. Release decision → 8. Controlled deployment + installation qualification → 9. Training → 10. Clinical-use monitoring (Doc 11).
- Process records: `[HOSPITAL: QMS change/build/release record refs]`
- Nonconforming builds: quarantine procedure `[HOSPITAL: SOP ref]`; no clinical deployment of unreleased builds.

## 4. Design and performance data (incl. intended purpose per Doc 02)

| Artifact | Hospital record | Notes |
|---|---|---|
| Intended purpose + claims boundary | Doc 02 (approved) | Primary input |
| System/software requirements | `[HOSPITAL: SRS ref]`, input conformance, QC thresholds, fail-stop, provenance, performance floors | Testable, traced |
| Architecture | `[HOSPITAL: arch ref]`, pipeline stages enabled/disabled, data flow CTA→NIfTI→mask→centerlines→viewer, SOUP boundaries | Upstream `processor` orchestration adapted |
| SOUP/SBOM | `[HOSPITAL: SBOM ref]`, torch 2.6.0/cu124 (or hosp. pin), torch_geometric, MONAI, nnU-Net v2, VMTK, TotalSegmentator mandible (Apache-2.0) | CVE review filed |
| Risk file | Doc 08 | Hazards incl. automation bias, silent failure |
| Usability file | `[HOSPITAL: usability ref]`, overread workflow validation | IEC 62366-1 |
| Verification report | `[HOSPITAL: V&V ref]`, integration + regression, disablement proof | |
| Validation report | Doc 10, local retrospective + shadow-phase results vs acceptance criteria | No validation, no use |
| IFU-equivalent + on-screen warnings | §7 below | Versioned with device |
| Provenance/QC spec | Per-case: device/model versions, input hash, QC flags, failure codes | |

Upstream-only evidence (papers, Zenodo metrics) is **context**, never performance proof for the hospital build.

## 5. Performance summary (completed post-validation)

- Acceptance criteria: `[HOSPITAL: e.g. Dice ≥ X on local test set, centerline completeness ≥ Y, QC-failure rate ≤ Z, overread-compliance 100% in summative]`
- Results: `[HOSPITAL: summary + report ref]`
- Limitations: `[HOSPITAL: known failure anatomies/protocols, out-of-scope inputs]`

## 6. Scale and lifetime

- Expected volume: `[HOSPITAL: cases/year, sites, concurrency]`, proportionate to own need (non-industrial scale rationale).
- Service lifetime: `[HOSPITAL: version support window, re-validation triggers, retirement plan ref]`.

## 7. Information supplied with the device (IFU-equivalent contents)

Purpose, target users, mandatory overread statement, input requirements, step-by-step use, interpretation limits, failure/degraded states with screenshots, version/provenance reading guide, incident-reporting route, support contact, language `[HOSPITAL]`, document version tied to device version.

## 8. Authority-retrieval drill

- Pack location: `[HOSPITAL: QMS path]`
- Owner: `[HOSPITAL: name/role]`
- Last drill date/result: `[HOSPITAL: ...]` (target: complete pack retrievable ≤ `[HOSPITAL: e.g. 10 working days]`).

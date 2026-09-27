# 11, Local Clinical Validation Plan + validrig Pack Skeleton

> First-time reader: terms are spelled out on first use. Full list: `00-ABBREVIATIONS-AND-TERMINOLOGY.md`.
>
> Owner: clinical lead + QA + engineering. Principle: upstream metrics (papers, Zenodo) do not validate the hospital build on hospital data. Validation happens on **frozen hospital build + local CTA**, with pre-registered acceptance criteria. Engine: `AliakseiT/validrig` (`rig`), pack name `arterial-visualisation`.

## 1. Acceptance criteria (set before data is touched)

| Dimension | Metric (example, hospital to approve) | Floor |
|---|---|---|
| Segmentation (local test set, ground truth) | Dice (vessel mask), 95HD | `[HOSPITAL: e.g. Dice ≥ 0.80 mean, ≥ 0.70 p5]` |
| Centerline completeness | % clinically-relevant segments visualised without gap > `[X]` mm | `[HOSPITAL: ≥ 95%]` |
| Failure behaviour | QC-gate sensitivity to corrupt/out-of-spec inputs (no silent wrong output) | `[HOSPITAL: 100% fail-stop on fault suite]` |
| Robustness strata | Performance by scanner/protocol/contrast-phase/age-band | `[HOSPITAL: no stratum > Δ below floor without documented limitation]` |
| Human factors | Overread-attestation compliance; misinterpretation events | `[HOSPITAL: 100% / zero]` |
| Latency | CTA-to-display p95 on production node | `[HOSPITAL: e.g. ≤ 15 min, with fallback procedure]` |
| Automation | Manual interaction steps (seeds, edits) per case to reach a usable map | `[HOSPITAL: e.g. 0]` |

Floors for completeness, latency, and automation are the performance characteristics of the Doc 05 §3 need, with the same values. The in-house build must meet them here, and the CE candidates are measured against them in §3A.

If any floor is missed: no clinical use; either improve (new release candidate) or narrow purpose further.

## 2. Retrospective study (ground-truth)

- Dataset: `[HOSPITAL: N CTA, consecutive eligible cases over DATES, inclusion/exclusion, de-identification, ethics/DPIA ref]`; split dev/validation/test with test locked before tuning operating point. The test set comes from a later acquisition period than the development data (temporal separation), as the IIb-equivalent depth in Doc 04 §3 requires.
- Ground truth: `[HOSPITAL: e.g. two-reader vessel segmentation + adjudication protocol, annotation tool, reader credentials]`.
- Execution: frozen build only; provenance logged per case; failures analysed by anatomy/protocol stratum; limitations encoded into IFU-equivalent (Doc 07 §7).
- Report: methods, CONSORT-style flow, per-stratum results, failure gallery, trace to requirements/risks.

## 3. Silent / shadow phase (prospective, non-influencing)

- `[HOSPITAL: N consecutive cases, duration]` run in parallel with standard care; output visible only to the study team, **never** to the treating team. A watermarked output shown to treating clinicians would influence care and is not a shadow phase. Ethics approval: `[HOSPITAL: ethics ref]`.
- Endpoints: technical success rate, QC-flag rate, discordance between device visualisation and final radiology read, time impact, incident count.
- Stop rules: `[HOSPITAL: e.g. >X% technical failure, any silent wrong-output event, any safety signal → halt + CAPA]`.

## 3A. CE comparator arm (required where Doc 05 claims a performance gap)

Purpose: evidence for Art 5(5)(c). It shows whether available CE-marked candidates meet the Doc 05 §3 need on local data. It can run before the in-house device is built.

- Candidates: each CE device dispositioned in Doc 05 §6 as closest, `[HOSPITAL: name, version, EUDAMED ID]`, used within its IFU (Instructions For Use), by operators trained per the vendor. Access via existing licence, vendor evaluation licence, or vendor-run processing under a DPA (Data Processing Agreement) on de-identified data.
- Data: the §2 locked test set, or a pre-specified subset sized `[HOSPITAL: N, with rationale]`. Same ground truth, same readers.
- Measures: the §1 completeness, latency, and automation metrics, recorded per characteristic. Readers blinded to which system produced the map where the display allows.
- Decision rule, fixed before measurement: a candidate that meets every Doc 05 §3 characteristic is equivalent. (c) fails and the hospital uses or procures that device.
- Report: per candidate, per characteristic, met or missed with value and confidence interval. Filed as Doc 05 evidence. Vendors may be offered the report for factual correction before filing.

## 4. validrig pack skeleton (`packs/arterial-visualisation/`)

The hospital authors a pack; the engine stays untouched (validrig principle: new intended use = new pack).

```
packs/arterial-visualisation/
  pack.yaml            # id: arterial-visualisation, version, intended-use ref (Doc 03), frozen device version
  cases/               # casebank: local CTA descriptors + ground-truth refs (PHI never in repo; pointers only)
  batteries.yaml       # smoke (offline, fake judge) / regression / validation (locked test set)
  tasks.yaml           # visualisation-fidelity tasks: completeness, artefact rate, QC-gate behaviour
  perturbations.yaml   # acquisition axes: dose/noise, contrast phase, slice thickness, scanner shift
  judge.yaml           # default: expert-read adjudication protocol (human); offline: deterministic fake for CI
  acceptance.yaml      # floors from §1, machine-checked
  publish.yaml         # prose + {{fact}} placeholders for the validation report (rig publish)
```

- `rig run packs/arterial-visualisation --battery validation --out ./runs --seed 1` produces the pinned run; `rig diff --baseline <old> --candidate <new>` gates every release candidate (§5).
- Judge swaps, pack edits, or weight changes alter `pack_hash`/`run_id` → revalidation event by construction. Never substitute judges from scripts.
- PHI discipline: pack holds pointers + hashes; pixels stay on-prem in `[HOSPITAL: data enclave path]`; runs store metrics + provenance, never images.

## 5. Re-validation triggers (any one → new candidate + scoped re-run)

New upstream cherry-pick, weight change, dependency/CUDA change, new scanner/protocol, PACS/viewer change, drift signal (Doc 12), or 12-month expiry without review. Scope: `rig diff` regression minimum; full validation if pipeline or operating point changed.

## 6. Validation report and release linkage

Report location: `[HOSPITAL: QMS ref]`; includes acceptance verdict per criterion, subgroup analysis, failure gallery, usability summative, benefit-risk input to Docs 06/09, and explicit release recommendation (approve / approve-with-limitations / reject). No report → no release → no declaration.

---
> Return to the [reading index](../../README.md#how-to-read-this-package).

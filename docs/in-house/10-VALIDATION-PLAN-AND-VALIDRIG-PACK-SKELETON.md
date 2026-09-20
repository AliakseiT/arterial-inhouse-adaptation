# 10 — Local Clinical Validation Plan + validrig Pack Skeleton

> Owner: clinical lead + QA + engineering. Principle: upstream metrics (papers, Zenodo) do not validate the hospital build on hospital data. Validation happens on **frozen hospital build + local CTA**, with pre-registered acceptance criteria. Engine: `AliakseiT/validrig` (`rig`), pack name `arterial-visualisation`.

## 1. Acceptance criteria (set before data is touched)

| Dimension | Metric (example — hospital to approve) | Floor |
|---|---|---|
| Segmentation (local test set, ground truth) | Dice (vessel mask), 95HD | `[HOSPITAL: e.g. Dice ≥ 0.80 mean, ≥ 0.70 p5]` |
| Centerline completeness | % clinically-relevant segments visualised without gap > `[X]` mm | `[HOSPITAL: ≥ 95%]` |
| Failure behaviour | QC-gate sensitivity to corrupt/out-of-spec inputs (no silent wrong output) | `[HOSPITAL: 100% fail-stop on fault suite]` |
| Robustness strata | Performance by scanner/protocol/contrast-phase/age-band | `[HOSPITAL: no stratum > Δ below floor without documented limitation]` |
| Human factors | Overread-attestation compliance; misinterpretation events | `[HOSPITAL: 100% / zero]` |
| Latency | CTA-to-display p95 on production node | `[HOSPITAL: e.g. ≤ 15 min, with fallback procedure]` |

If any floor is missed: no clinical use; either improve (new release candidate) or narrow purpose further.

## 2. Retrospective study (ground-truth)

- Dataset: `[HOSPITAL: N CTA, consecutive eligible cases over DATES, inclusion/exclusion, de-identification, ethics/DPIA ref]`; split dev/validation/test with test locked before tuning operating point.
- Ground truth: `[HOSPITAL: e.g. two-reader vessel segmentation + adjudication protocol, annotation tool, reader credentials]`.
- Execution: frozen build only; provenance logged per case; failures analysed by anatomy/protocol stratum; limitations encoded into IFU-equivalent (Doc 06 §7).
- Report: methods, CONSORT-style flow, per-stratum results, failure gallery, trace to requirements/risks.

## 3. Silent / shadow phase (prospective, non-influencing)

- `[HOSPITAL: N consecutive cases, duration]` run in parallel with standard care; output visible only to study team, **never** to treating team, or visible with explicit "validation — do not use" watermark per ethics approval `[HOSPITAL: ethics ref]`.
- Endpoints: technical success rate, QC-flag rate, discordance between device visualisation and final radiology read, time impact, incident count.
- Stop rules: `[HOSPITAL: e.g. >X% technical failure, any silent wrong-output event, any safety signal → halt + CAPA]`.

## 4. validrig pack skeleton (`packs/arterial-visualisation/`)

The hospital authors a pack; the engine stays untouched (validrig principle: new intended use = new pack).

```
packs/arterial-visualisation/
  pack.yaml            # id: arterial-visualisation, version, intended-use ref (Doc 02), frozen device version
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

New upstream cherry-pick, weight change, dependency/CUDA change, new scanner/protocol, PACS/viewer change, drift signal (Doc 11), or 12-month expiry without review. Scope: `rig diff` regression minimum; full validation if pipeline or operating point changed.

## 6. Validation report and release linkage

Report location: `[HOSPITAL: QMS ref]`; includes acceptance verdict per criterion, subgroup analysis, failure gallery, usability summative, benefit-risk input to Docs 05/08, and explicit release recommendation (approve / approve-with-limitations / reject). No report → no release → no declaration.

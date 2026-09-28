# 16, Phase 2 Outline: Access-Difficulty Decision Support (not claimed)

> First-time reader: terms are spelled out on first use. Full list: `00-ABBREVIATIONS-AND-TERMINOLOGY.md`.
>
> Owner: clinical lead + regulatory + QA. Status: outline of a possible later intended purpose. Nothing here is claimed, declared, or shown to clinicians. The Phase 1 device is the Doc 03 visualisation aid, and Doc 13 declares only that. This document sets out how the hospital decides whether Phase 2 is worth building, using published evidence and data gathered while Phase 1 is in use. It fixes the decision rule before any of that data is looked at.

## 1. Why a second phase exists

Upstream Arterial's distinctive output is not the vessel map. CE-marked advanced-visualisation platforms already draw vessel maps (Doc 05 §2). Its distinctive output is the access prediction module: a probability that catheter navigation along a pathway (femoral or radial, left or right) will be difficult, with attention maps marking the segments that drive the estimate.

Phase 1 keeps that output away from clinicians on purpose (Doc 03 §4, Doc 01 §3). The reason is not that it lacks value. It needs Class III-equivalent evidence the hospital does not yet have. Phase 1 is where the hospital gathers that evidence without exposing patients to an unvalidated prediction.

## 2. Candidate Phase 2 intended purpose (draft, for scoping only)

> `[HOSPITAL-DEVICE]` Phase 2 adds, for adults with suspected acute ischaemic stroke considered for mechanical thrombectomy at `[HOSPITAL]`, an estimate of catheter-access difficulty per pathway from head-and-neck CTA, with the vessel segments that contribute most to the estimate highlighted on the Phase 1 map. The responsible physician chooses the access route. `[HOSPITAL: final wording after the §5 gate]`

Consequences that follow from any wording close to this:

- **Class III-equivalent.** The estimate is used for an immediate choice, the access route, in a critical situation. That is "treat or diagnose" in the IMDRF table (Doc 04 §2.1). Leaving out recommendation wording does not change what the information is used for. Upstream's own interpretation table says "consider alternative access" at high values. Evidence depth follows the III row of Doc 04 §3.
- **IEC 62304 Class C.** A wrong estimate at the moment of route choice can delay reperfusion, and overread of the source CTA does not check a probability.
- **Member-State check.** Confirm that `[HOSPITAL: Member State]` does not restrict in-house manufacture of Class III-equivalent software before any build (Doc 02 national check).
- **EU AI Act.** The Doc 02 §6 reading does not depend on class and stays the same. Route choice is not emergency patient triage under Annex III 5(d). Re-confirm with counsel when the purpose is written.
- **Art 5(5)(c).** A fresh non-equivalence case for this purpose (§6).

## 3. Evidence that informs the decision

Two sources. Neither validates the hospital build on its own; only Doc 11-style validation of a frozen Phase 2 build does that.

### 3.1 Published data

- Upstream publications and the ArterialGNet repository (`perecanals/arterial_gnet`): model design, training cohort, reported performance. `[HOSPITAL: list the papers and figures relied on, with DOI]`.
- The training target. Upstream documentation describes the output as "0 = easy, 1 = difficult" but does not define difficult access. `[VERIFY with upstream: definition of the difficult-access label, e.g. failed route, conversion, catheterisation time threshold, operator rating; cohort size and site]`. Local ground truth (§4.2) must measure the same thing, or the hospital must state how the two differ.
- Independent literature on access difficulty and route conversion in thrombectomy, to set a realistic local event rate and a clinically meaningful performance bar. `[HOSPITAL]`.
- The upstream uncertainty band is the spread across five cross-validation folds. It is not a calibrated probability interval. Calibration is established locally (§4.3).

Published figures set expectations. They do not replace the local measurements in §4.

### 3.2 Phase 1 internal data

Phase 1 produces three things Phase 2 needs:

- A consecutive local CTA archive, processed by a frozen and validated segmentation and centerline pipeline, with QC (Quality Control) outcomes logged (Doc 12 §1).
- A measured safety and reliability record for that pipeline, on which the access model depends (Doc 12, Doc 11 §3).
- Procedure outcomes for the same patients, collected under §4.

## 4. Offline outcome study during Phase 1

### 4.1 Where the model runs

The access model runs **offline, retrospectively, on closed cases, in a research environment outside the device boundary**. It does not run in the clinical build. Consequences:

- The Phase 1 device is unchanged. Hazard H6 (Doc 09) and the release proof that hidden outputs are unreachable (Doc 10) stay as they are.
- Nobody treating the patient can see a prediction, because none exists until after the procedure.
- Outcomes are only known after the procedure anyway, so nothing is lost by running later.

Inputs are the Phase 1 segmentation and centerline outputs, or a re-run of the same frozen pipeline on archived CTA, in `[HOSPITAL: research enclave]`. Access model version and weight hashes are pinned and logged per run, as for the device.

### 4.2 Outcome fields (per eligible case)

| # | Field | Definition | Source |
|---|---|---|---|
| P1 | Planned access route | Route in the documented procedure plan | Procedure plan (Doc 15 D1 endpoint) |
| P2 | Access route used | Route through which the target vessel was catheterised | Procedure report |
| P3 | Route conversion | Change of access site or approach after arterial puncture, yes/no plus reason | Procedure report |
| P4 | Access time | Minutes from arterial puncture to target-vessel catheterisation `[HOSPITAL: choose the local timestamp]` | Procedure report / registry |
| P5 | Access failure | Target vessel not reached | Procedure report |
| P6 | Difficult-access label | Local definition matching the upstream label (§3.1) | Derived from P3-P5 by a rule fixed in advance |
| P7 | Model output | Probability per pathway, attention map reference, model version | Offline run log |

Readers who derive P6 are blinded to P7.

### 4.3 What gets measured

Discrimination (e.g. AUC with confidence interval), calibration (calibration slope and intercept, reliability plot), performance at the operating points the Phase 2 display would use, and performance by stratum (age band, arch type, scanner, protocol). The number of outcome events decides how precise these can be. Small event counts are the most likely reason for a "keep collecting" verdict.

### 4.4 Legal basis

This is a new purpose for the data. The Doc 12 case log exists for Art 5(5)(h), not for research. Linking procedure outcomes to model outputs is processing of health data for research under GDPR (General Data Protection Regulation). Required before the first offline run: `[HOSPITAL: ethics committee ref]`, `[HOSPITAL: DPIA (Data Protection Impact Assessment) ref]`, legal basis and patient-information route per local rules. Pixels and identifiers stay on-prem. Only aggregates leave the research environment.

## 5. Phase 2 decision gate (fix before looking at any §4 result)

Signed by clinical lead, regulatory, and QA before the first offline run. Values are the hospital's; examples in brackets.

| Criterion | Evidence | Threshold |
|---|---|---|
| Enough outcome events | §4 event count | `[HOSPITAL: e.g. ≥ N difficult-access events, from a sample-size calculation for the precision needed]` |
| Discrimination | §4.3 | `[HOSPITAL: e.g. lower 95% CI bound of AUC ≥ X]` |
| Calibration | §4.3 | `[HOSPITAL: e.g. slope within [a, b]; recalibration allowed only on development data, never on the test set]` |
| Clinical need | Local rate of P3/P5 and P4 distribution | `[HOSPITAL: e.g. conversion rate ≥ Y% or access time p90 ≥ Z min]`. No need, no Phase 2. |
| Phase 1 track record | Doc 12 reviews, Doc 11 shadow results | No open safety CAPA; QC suppression rate within `[HOSPITAL]` |
| Published support | §3.1 | Label definition confirmed; no published signal contradicting local results |
| Market check for (c) | Fresh Doc 05 search for access-prediction and route-planning devices | Search completed and filed. A CE device that meets the need ends Phase 2. |
| Resourcing | Doc 01 §4 at III depth | Named owner, clinical lead, QA, and budget for an external or temporally separated validation cohort |

Verdicts:

- **Proceed:** every criterion met. Open Phase 2 as a new intended purpose: revise Docs 03-13, run Doc 11 at III depth with a prospective component, publish a new declaration. The offline study is development evidence, not the validation.
- **Keep collecting:** clinical need shown, but events or precision are short. Set the next review date.
- **Stop:** no clinical need, performance below the bar, a CE equivalent exists, or Phase 1 safety is not stable. Record and close. Phase 1 continues on its own merits.

## 6. Non-equivalence for Phase 2

The Phase 2 (c) case is written fresh, per Doc 05. It is likely to be stronger than the Phase 1 case, because access-difficulty prediction is not a standard feature of advanced-visualisation platforms. That is an expectation to test, not a finding. The search in §5 is required, and a CE device that meets the need ends Phase 2 however good the in-house model is.

## 7. Why the open-source basis supports the in-house path

This is an argument for the route the hospital takes. It is **not** an Art 5(5)(c) ground. Doc 05 §3 lists open-source status among the grounds that do not hold, and that stays true. If a CE device meets the need, the answer is NO-GO whatever the licence.

Where it matters is in making the evidence above obtainable and checkable:

- **Inspection.** Code, architecture, and weights are available. The hospital can see what features drive a prediction, read the attention maps, and trace a failure to a segment, a feature, or a model. A closed product usually offers none of that.
- **Local re-running.** The model runs on the hospital's own archive, offline, with no vendor involvement, as often as needed. §4 depends on this.
- **Reproducibility.** Pinned code, pinned weights, and hashed inputs let an authority, an auditor, or another site re-run the analysis and get the same numbers (Doc 07, Doc 11 §4).
- **Shared evidence.** Methods and aggregate results can be published and compared with upstream and with other sites that run the same open model. Evidence can grow across institutions without any device moving between them (Doc 14 §4).
- **Continuity.** The model does not disappear when a vendor changes roadmap, although the hospital then carries maintenance itself (Doc 12 §6).

Limits to state alongside:

- The code and weights are open. The upstream training data and the difficult-access label are not fully documented (§3.1). Transparency of the model is not transparency of its training.
- The licence is noncommercial (Doc 14 §1).
- Openness does not lower any evidence bar. It makes the bar reachable for a single hospital.

## 8. Sign-off

- Gate criteria fixed: `[HOSPITAL: clinical lead, regulatory, QA, date]`
- Gate verdict: `[HOSPITAL: proceed / keep collecting / stop, date, next review]`
- Linked: Doc 01 §3 (phased path), Doc 02 §3 (wider-use path), Doc 03 §4 (hidden modules), Doc 04 §3 (III row), Doc 05 (fresh search), Doc 12 §3 (review input), Doc 14 (publication).

---
> Return to the [reading index](../../README.md#how-to-read-this-package).

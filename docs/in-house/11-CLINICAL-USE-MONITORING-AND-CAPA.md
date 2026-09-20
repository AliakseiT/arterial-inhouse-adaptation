# 11 — Clinical-Use Monitoring, Corrective Action, Authority Interface

> Owner: device owner + QA. Covers Art 5(5)(g) manufacture-per-doc and (h) use-review + corrective action, plus national vigilance.

## 1. Per-case traceability (enables (h))

Every clinical use logs: device version + weight hashes, input StudyInstanceUID (hashed patient link via hospital record, not in device log), QC flags, output status (displayed / degraded / suppressed), viewing user + overread attestation, timestamp. Log location: `[HOSPITAL: ...]`; retention `[HOSPITAL: ...]`; linkable to patient record for corrective action without duplicating PHI.

## 2. Manufacture-per-doc (g) in operation

Only released tags deployed; installation qualification per node; deployment log; rollback image; no hot-patching. Deviations (e.g. emergency rollback) recorded as nonconformities with QA disposition before resuming use.

## 3. Routine review cadence

| Review | Frequency | Inputs | Owner | Output |
|---|---|---|---|---|
| Case-log triage | `[e.g. weekly]` | QC failures, discordances, complaints | Device owner | Triage to CAPA/change or close |
| Clinical-use review | `[e.g. quarterly]` | Discordance rate, stratum drift, latency, training compliance | Clinical lead + QA | Review minute; risk-file update decision |
| Non-equivalence re-check | `≤12 months` + ad-hoc | EUDAMED/market scan (Doc 04) | Regulatory | Re-affirmation or transition plan |
| Management review input | per QMS cycle | All above + audit findings | Management | Resource/continue/retire decision |

## 4. Discordance and incident handling

- Discordance definition: `[HOSPITAL: e.g. device visualisation materially disagrees with final radiology read, or QC flag disputed]`. Log all; sample-review even when overread "caught" the issue — near-misses count.
- Incident: any use that caused or could cause harm → hospital incident system + national in-house reporting route `[HOSPITAL: authority + timeline]` + risk-file update + CAPA. Do not wait for quarterly review.
- Corrective action scale: advisory notice to users → temporary suspension → version recall/rollback → purpose narrowing → retirement. Each has a pre-assigned decision-maker `[HOSPITAL: names/roles]`.

## 5. Authority pack (Art 5(5)(d) readiness)

Maintained at `[HOSPITAL: QMS path]`: Docs 01–12 current versions, frozen source access procedure, build reproducibility statement, validation report, risk file, deployment list, case-volume summary, declaration copy, non-equivalence evidence. Owner `[HOSPITAL]`; retrieval drill `[HOSPITAL: frequency, last result]`. Cooperate with inspections; respect Member-State notification duties `[HOSPITAL: citation or N/A]`.

## 6. Change control (all changes via QMS)

Upstream monitoring `[HOSPITAL: owner + frequency]`; every hospital change assessed for purpose/safety/performance impact → re-validation scoping (Doc 10 §5) → updated Docs 02/05/06/08/12 as affected → new release tag → re-training if workflow changed. Unassessed auto-updates are forbidden.

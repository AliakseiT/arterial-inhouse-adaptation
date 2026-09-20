# 11, Clinical-Use Monitoring, Corrective Action, Authority Interface

> First-time reader: terms are spelled out on first use. Full list: `00-ABBREVIATIONS-AND-TERMINOLOGY.md`.
>
> Owner: device owner + QA. Covers Art 5(5)(g) manufacture-per-doc and (h) use-review + corrective action, plus national vigilance.

## 1. Per-case traceability (enables (h))

Every clinical use logs: device version + weight hashes, input StudyInstanceUID (hashed patient link via hospital record, not in device log), QC flags, output status (displayed / degraded / suppressed), viewing user + overread attestation, timestamp. Log location: `[HOSPITAL: ...]`; retention `[HOSPITAL: ...]`; linkable to patient record for corrective action without duplicating PHI.

## 2. Manufacture-per-doc (g) in operation

Only released tags deployed; installation qualification per node; deployment log; rollback image; no hot-patching. Deviations (e.g. emergency rollback) recorded as nonconformities with QA disposition before resuming use.

## 3. Routine review cadence

What the law actually demands here is thin but firm. Article 5(5)(g) requires manufacture per the filed documentation. Article 5(5)(h) requires review of experience from clinical use plus all necessary corrective actions. Annex I section 3 requires risk management as a continuous process with systematic updating. MDCG 2023-1 adds that the Quality Management System must cover vigilance, corrective and preventive action (CAPA), and change control. None of these set a calendar. No quarterly or annual frequency appears in the text. The hospital sets a proportionate cadence and defends it. The named roles are required in substance, a device-responsible person, clinical oversight, QA oversight, because without them (g) and (h) cannot be performed. Titles may follow hospital usage.

Relaxed minimum for pathfinder adoption:

| Review | Minimum frequency | Inputs | Owner | Output |
|---|---|---|---|---|
| Case-log triage | Per case cluster, at least monthly, zero-case months logged as such | Quality Control (QC) failures, discordances, complaints | Device owner | Triage to CAPA/change or close |
| Clinical-use review | Twice yearly until case volume exceeds `[HOSPITAL: e.g. 100 cases]`, then quarterly | Discordance rate, stratum drift, latency, training compliance | Clinical lead + QA | Review minute; risk-file update decision |
| Non-equivalence re-check | `12 months` maximum + ad-hoc on new market entrants | European Database on Medical Devices (EUDAMED)/market scan (Doc 04) | Regulatory | Re-affirmation or transition plan |
| Management review input | per existing hospital QMS cycle, no extra cycle | All above + audit findings | Management | Resource/continue/retire decision |

## 4. Discordance and incident handling

- Discordance definition: `[HOSPITAL: e.g. device visualisation materially disagrees with final radiology read, or QC flag disputed]`. Log all; sample-review even when overread "caught" the issue, near-misses count.
- Incident: any use that caused or could cause harm → hospital incident system + national in-house reporting route `[HOSPITAL: authority + timeline]` + risk-file update + CAPA. Do not wait for quarterly review.
- Corrective action scale: advisory notice to users → temporary suspension → version recall/rollback → purpose narrowing → retirement. Each has a pre-assigned decision-maker `[HOSPITAL: names/roles]`.

## 5. Authority pack (Art 5(5)(d) readiness)

Maintained at `[HOSPITAL: QMS path]`: Docs 01-12 current versions, frozen source access procedure, build reproducibility statement, validation report, risk file, deployment list, case-volume summary, declaration copy, non-equivalence evidence. Owner `[HOSPITAL]`; retrieval drill `[HOSPITAL: frequency, last result]`. Cooperate with inspections; respect Member-State notification duties `[HOSPITAL: citation or N/A]`.

## 6. Change control (all changes via QMS)

Upstream monitoring `[HOSPITAL: owner + frequency]`; every hospital change assessed for purpose/safety/performance impact → re-validation scoping (Doc 10 §5) → updated Docs 02/05/06/08/12 as affected → new release tag → re-training if workflow changed. Unassessed auto-updates are forbidden.

---
> Return to the [reading index](../../README.md#how-to-read-this-package).

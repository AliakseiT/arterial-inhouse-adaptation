# 15, Viability Analysis (does continued operation pay off)

> First-time reader: terms are spelled out on first use. Full list: `00-ABBREVIATIONS-AND-TERMINOLOGY.md`.
>
> Owner: clinical lead + hospital finance liaison + QA. Engine: `AliakseiT/heor-skills` (Health Economics and Outcomes Research skills), deterministic `@heor/engine` for all arithmetic. This analysis never supports the Article 5(5)(c) non-equivalence case in Doc 05. Cost arguments cannot establish non-equivalence, and MDCG 2023-1 §3.2.3 excludes in-house manufacture for purely economic motives. Its sole regulatory-adjacent role is informing the Doc 12 continue-or-retire decision and the Doc 01 resourcing picture.

## 1. Objective and viability bar

Objective: determine, from measured local data, whether continued operation of the Doc 03 device stays economically viable for the hospital over `[HOSPITAL: horizon, e.g. 3 years]`.

Viability bar, set before data collection and approved by management:

- The device remains viable if, at observed case volume, the mean net annual cost (operating cost minus monetised planning-time savings minus avoided repeat-imaging cost) is at or below `[HOSPITAL: budget threshold, EUR amount]` AND no safety signal from Doc 12 monitoring contradicts continued use.
- If the bar is missed, management reviews continuation: narrow further, reduce operating cost, or retire per the Doc 12 change process. Missing the bar never triggers scope widening on economic grounds.

Out of scope: QALY (Quality-Adjusted Life Year) or ICER (Incremental Cost-Effectiveness Ratio) claims, payer reimbursement, cross-hospital generalisation. Those require a full HTA (Health Technology Assessment) dossier, not this analysis.

## 2. Data dictionary (what gets collected, where, by whom)

Collection starts in the Doc 11 shadow phase so that a native-only baseline exists before the device influences care. Every field below is recorded per eligible case; aggregates only leave the hospital record.

| # | Field | Definition | Source | Recorded by |
|---|---|---|---|---|
| D1 | Planning duration | Minutes from CTA (Computed Tomography Angiography) availability in PACS (Picture Archiving and Communication System) to the documented procedure plan (access route and approach). `[HOSPITAL: if the plan is not timestamped, use arterial puncture time instead; choose one endpoint and keep it fixed]` | Planning log / EHR (Electronic Health Record) timestamp | Study team, shadow phase; treating team, live phase |
| D2 | Repeat CTA | Repeat head-and-neck CTA ordered for the same presentation, yes/no plus reason | Radiology order record | Study team |
| D3 | Device QC (Quality Control) outcome | Pass, degraded, or suppressed, per Doc 07 provenance spec | Device case log (Doc 12) | Automatic |
| D4 | Overread discordance | Device visualisation materially disagrees with final radiology read, yes/no | Discordance log (Doc 12) | Reviewing radiologist |
| D5 | Device downtime minutes | Minutes the device was unavailable during the planning window | Deployment log (Doc 12) | Clinical engineering |
| D6 | Staff minutes by role | Attending, resident, radiographer minutes attributable to the planning step | Time-motion observation sheet | Study team |
| D7 | Operating cost ledger | Annualised build, validation amortisation, GPU (Graphics Processing Unit) hosting, maintenance, QA review time, training | Finance + QA records | Finance liaison |

Baseline (native-only) values for D1, D2, and D6 come from `[HOSPITAL: consecutive eligible cases before deployment, N and date range]` extracted from the same sources by the same definitions. Without this baseline the comparison in section 3 cannot be computed, and viability cannot be claimed.

## 3. Model structure

Decision tree with two arms, native-only versus native-plus-aid, evaluated per eligible case and scaled by observed annual volume:

- Arm A (native-only): planning cost = D6 costed at hospital role rates + probability of repeat CTA (D2 baseline rate) times repeat-imaging unit cost.
- Arm B (native-plus-aid): planning cost = D6 costed at observed aided minutes + device QC branch: pass (D6 aided + share of D7 per case), degraded or suppressed (fallback to Arm A cost for that case plus D5 downtime share), plus discordance review cost (D4 rate times review minutes).
- Parameters, each with source and uncertainty range: D1 mean and distribution by arm, D2 rate by arm, D4 rate, D3 branch probabilities, D7 annual total, role rates from `[HOSPITAL: cost accounting reference, year]`, annual volume from Doc 05 target-group count.

Analysis outputs: mean net annual cost with uncertainty interval, break-even table (minimum cases per year and minimum minutes saved per case at which net crosses the section 1 bar), tornado ranking of cost drivers. Sensitivity method: Monte-Carlo over D1, D2, and D4 distributions; scenario with and without downtime. Arithmetic runs in `@heor/engine`; prose references results as placeholders resolved from run artefacts, never hand-typed.

## 4. Allowed versus forbidden uses

| Allowed | Forbidden |
|---|---|
| Continue-or-retire input for Doc 12 management review | Any input to Doc 05 non-equivalence |
| Resourcing transparency for Doc 01 | Price-based comparison against CE devices |
| Monitoring indicators for Doc 12 (D1 trend, D4 rate) | Efficacy or safety claims beyond Doc 11 validation |
| Internal budget planning | Payer or HTA submission language |

## 5. Deliverable and review

Deliverable: 2-4 page viability note plus engine run archive, reviewed by `[HOSPITAL: clinician + QA + finance]`, filed with Doc 12 monitoring records. First edition after shadow-phase data cut; refresh at each clinical-use review until the viability verdict is stable across two consecutive reviews. Every page carries: "Draft, requires review by qualified professionals. Not regulatory, clinical, or reimbursement advice."

---
> Return to the [reading index](../../README.md#how-to-read-this-package).

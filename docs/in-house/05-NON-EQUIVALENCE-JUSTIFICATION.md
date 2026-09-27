# 05, Non-Equivalence Justification, Art 5(5)(c)

> First-time reader: terms are spelled out on first use. Full list: `00-ABBREVIATIONS-AND-TERMINOLOGY.md`.
>
> Owner: regulatory + clinical lead, before any build. This is the condition most authorities probe first, and the one most likely to end the project. Economic arguments (price, licence cost) are inadmissible, use technical/clinical grounds only (MDCG 2023-1 §3.2.3, §3.6.2). Read Doc 02 section 1A first: the adaptation from research code to a narrow clinical purpose is part of this justification, not background.

## 1. Target patient group (precise)

`[HOSPITAL: e.g. adults presenting to HOSPITAL ED with suspected anterior-circulation large-vessel occlusion, undergoing head-and-neck CTA per local stroke protocol, annual volume ≈ N]`. Link to Doc 03. Vague groups ("stroke patients") are rejected, define presentation, anatomy (extracranial pathway), and workflow step.

## 2. The likely equivalent, stated up front

3D vessel segmentation with centerlines from head-and-neck CTA is not new. CE-marked advanced-visualisation platforms from the CT vendors and from independent software makers offer CTA vessel analysis: vessel extraction, centerlines, curved planar reformats. Many run on-prem. Stroke AI platforms are a second category; they mostly target occlusion detection, perfusion, and triage, which is a different intended purpose.

A hospital that already owns or can procure an advanced-visualisation platform that produces usable head-and-neck centerlines on its own CTA protocol, within the time the planning discussion allows, has an equivalent device. The answer is then NO-GO: use or procure the CE device. The package expects this outcome at many hospitals and treats it as a correct result, not a failure.

## 3. Specific need claimed

MDCG 2023-1 §3.6.1 accepts two kinds of need: a need for a specific device, or a need for "a specified level of performance of a device for certain performance characteristics". The Doc 03 device can only claim the second kind. The hidden upstream outputs (access prediction, tortuosity scores) are not part of the device and cannot support (c).

Need statement: `[HOSPITAL: e.g. an extracranial vessel map from aortic arch to intracranial ICA, produced without manual seeding or editing, on the local stroke CTA protocol, available within N minutes of image arrival, with centerline completeness ≥ Y% in elongated or tortuous anatomy, and an explicit failure state]`. Each number is a performance characteristic the hospital fixes before looking at any candidate's results.

Grounds that can hold, each with evidence:

| Ground | Characteristic (Annex XIV.3 aspect) | Evidence that carries it |
|---|---|---|
| Performance on local data | Completeness, automation (manual steps), time to usable map in the stroke window (technical: critical performance characteristics) | Comparator arm, Doc 11 §3A: the CE candidate run on the locked local test set as its IFU (Instructions For Use) allows, measured against the fixed need |
| Conditions of use | Deployment or data-flow constraint the candidate cannot meet (technical: used under similar conditions) | Vendor written confirmation + the hospital rule it conflicts with. Thin where on-prem options exist |
| Availability | Candidate not CE-marked or not accessible in the Member State under EU, national, or local rules (MDCG 2023-1 §3.6.4) | Vendor or distributor statement, procurement record |

Grounds that do not hold: price, licence cost, open-source status, preference for own software, familiarity, workflow convenience with no measured performance consequence, novelty of outputs the device does not show. Explicit QC (Quality Control) failure signalling and provenance labelling support the case but do not carry it alone; CE platforms have their own error handling.

## 4. Timing: justify before manufacture

MDCG 2023-1 §3.6.3 places the search and justification before first manufacture. The in-house device does not need to exist for that. The need is a set of fixed performance characteristics (§3). The pre-manufacture justification shows that the available CE candidates miss them on local data. Doc 11 later shows that the in-house build meets them. A non-clinical feasibility spike on de-identified data (Doc 01 §5) may inform where the numbers are set, but the numbers are fixed and signed before any candidate is measured against them.

## 5. Search method (describe in QMS, execute, file evidence)

| Step | Source | Query / scope | Date | Reviewer | Result |
|---|---|---|---|---|---|
| 1 | EUDAMED (device + SSP where available) | `[HOSPITAL: search terms, e.g. CTA vessel analysis, centerline, advanced visualisation, thrombectomy planning]` | `[date]` | `[name]` | `[HOSPITAL: N candidates, disposition]` |
| 2 | Competent-authority / notified-body lists | `[HOSPITAL: ...]` | | | |
| 3 | Vendor enquiry (IFU + intended purpose + performance data requested) | `[HOSPITAL: vendors contacted]` | | | |
| 4 | Literature / guidelines (stroke planning viewers) | `[HOSPITAL: ...]` | | | |
| 5 | Internal formulary / prior evaluations | `[HOSPITAL: ...]` | | | |

File IFUs, datasheets, correspondence, and search exports with the justification. One-off Googling is not a method.

## 6. Equivalence assessment per candidate

For each closest CE candidate, complete:

- Candidate: `[name, manufacturer, EUDAMED ID, version]`
- Intended purpose delta: `[why it does not cover the Doc 03 purpose]`
- Performance delta: `[e.g. failure modes on local-type data, lack of QC/provenance signalling, deployment incompatibility with air-gap requirement, each with evidence or clearly-labelled gap analysis]`
- Conclusion: `[not equivalent at appropriate performance / equivalent → STOP and procure instead]`

Template row (copy per candidate):

| Candidate | Purpose gap | Comparator result vs §3 need (Doc 11 §3A) | Evidence ref | Disposition |
|---|---|---|---|---|
| `[HOSPITAL]` | `[HOSPITAL]` | `[HOSPITAL: per characteristic, met / missed + value]` | `[HOSPITAL]` | `[HOSPITAL]` |

## 7. Determination statement (sign before manufacture)

> On `[date]`, `[HOSPITAL legal entity]` determined that no equivalent CE-marked device available on the market meets the §3 need of the §1 target group at the specified level of performance for the Doc 03 purpose, on the evidence filed at `[HOSPITAL: QMS ref]`. Next scheduled re-check: `[date, ≤12 months]`. New CE entrants trigger ad-hoc re-check per Doc 12.

Signers: `[clinical lead + regulatory/QA + date]`.

## 8. Maintenance

- Re-check cadence: `[HOSPITAL: annual minimum]` + trigger on new EUDAMED entries, vendor launches, guideline changes.
- If an equivalent appears: review and update this justification. A later market entrant does not invalidate the justification made at the start of manufacture, but if a CE-marked device turns out at least equivalent and meets the need at appropriate performance, start a transition to it (MDCG 2023-1 §3.6.3). Record in CAPA/change (Doc 12). The hospital may pause new clinical use during the review; the guidance does not require it.
- Doc 15 (viability analysis) plays no part in this justification. Economic evidence is inadmissible for (c).

---
> Return to the [reading index](../../README.md#how-to-read-this-package).

# 05, Non-Equivalence Justification, Art 5(5)(c)

> First-time reader: terms are spelled out on first use. Full list: `00-ABBREVIATIONS-AND-TERMINOLOGY.md`.
>
> Owner: regulatory + clinical lead, before any build. This is the condition most authorities probe first. Economic arguments (price, licence cost) are inadmissible, use technical/clinical grounds only. Read Doc 02 section 1A first: the adaptation from research code to a narrow clinical purpose is part of this justification, not background.

## 1. Target patient group (precise)

`[HOSPITAL: e.g. adults presenting to HOSPITAL ED with suspected anterior-circulation large-vessel occlusion, undergoing head-and-neck CTA per local stroke protocol, annual volume ≈ N]`. Link to Doc 03. Vague groups ("stroke patients") are rejected, define presentation, anatomy (extracranial pathway), and workflow step.

## 2. Specific need claimed

The in-house device addresses `[HOSPITAL: e.g. integrated extracranial centerline visualisation inside the local planning-discussion workflow with provenance/QC signalling tuned to local scanners/protocols]`, which available CE devices do not provide at appropriate performance because `[HOSPITAL: complete, e.g. no CE viewer validated on local CTA acquisition mix produces equivalent centerline completeness on tortuous arches; or workflow requires on-prem air-gapped execution incompatible with available cloud devices; each limb needs evidence, not assertion]`.

## 3. Search method (describe in QMS, execute, file evidence)

| Step | Source | Query / scope | Date | Reviewer | Result |
|---|---|---|---|---|---|
| 1 | EUDAMED (device + SSP where available) | `[HOSPITAL: search terms, e.g. CTA vascular visualisation, thrombectomy planning]` | `[date]` | `[name]` | `[HOSPITAL: N candidates, disposition]` |
| 2 | Competent-authority / notified-body lists | `[HOSPITAL: ...]` | | | |
| 3 | Vendor enquiry (IFU + intended purpose + performance data requested) | `[HOSPITAL: vendors contacted]` | | | |
| 4 | Literature / guidelines (stroke planning viewers) | `[HOSPITAL: ...]` | | | |
| 5 | Internal formulary / prior evaluations | `[HOSPITAL: ...]` | | | |

File IFUs, datasheets, correspondence, and search exports with the justification. One-off Googling is not a method.

## 4. Equivalence assessment per candidate

For each closest CE candidate, complete:

- Candidate: `[name, manufacturer, EUDAMED ID, version]`
- Intended purpose delta: `[why it does not cover the Doc 03 purpose]`
- Performance delta: `[e.g. failure modes on local-type data, lack of QC/provenance signalling, deployment incompatibility with air-gap requirement, each with evidence or clearly-labelled gap analysis]`
- Conclusion: `[not equivalent at appropriate performance / equivalent → STOP and procure instead]`

Template row (copy per candidate):

| Candidate | Purpose gap | Performance gap | Evidence ref | Disposition |
|---|---|---|---|---|
| `[HOSPITAL]` | `[HOSPITAL]` | `[HOSPITAL]` | `[HOSPITAL]` | `[HOSPITAL]` |

## 5. Determination statement (sign before manufacture)

> On `[date]`, `[HOSPITAL legal entity]` determined that no equivalent CE-marked device available on the market meets the §1 target-group need at appropriate performance for the Doc 03 purpose, on the evidence filed at `[HOSPITAL: QMS ref]`. Next scheduled re-check: `[date, ≤12 months]`. New CE entrants trigger ad-hoc re-check per Doc 12.

Signers: `[clinical lead + regulatory/QA + date]`.

## 6. Maintenance

- Re-check cadence: `[HOSPITAL: annual minimum]` + trigger on new EUDAMED entries, vendor launches, guideline changes.
- If an equivalent appears: review and update this justification. A later market entrant does not invalidate the justification made at the start of manufacture, but if a CE-marked device turns out at least equivalent and meets the need at appropriate performance, start a transition to it (MDCG 2023-1 §3.6.3). Record in CAPA/change (Doc 12). The hospital may pause new clinical use during the review; the guidance does not require it.
- Doc 15 (viability analysis) plays no part in this justification. Economic evidence is inadmissible for (c).

---
> Return to the [reading index](../../README.md#how-to-read-this-package).

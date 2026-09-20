# 14, HEOR / Value Outline (supports Doc 04, never substitutes for it)

> First-time reader: terms are spelled out on first use. Full list: `00-ABBREVIATIONS-AND-TERMINOLOGY.md`.
>
> Owner: clinical + finance/HTA liaison. Engine: `AliakseiT/heor-skills`. Scope discipline: this outline frames **workflow/performance value** of the narrow visualisation aid. It must not argue price, and Art 5(5)(c) cannot be won on cost.

## 1. Question and perspective

- Decision question: does the Doc 02 visualisation aid, integrated into local thrombectomy planning discussion, reduce planning friction and failure-demand (repeat reads, delayed decisions, avoidable DSA runs) for the Doc 04 target group, from the **hospital perspective** over `[HOSPITAL: horizon, e.g. 3 years]`?
- Out of scope: QALY/ICER claims, payer reimbursement, cross-hospital generalisation. Those need a full HTA dossier, not this outline.

## 2. Minimal dossier skeleton (`dossier.yaml` + `documents/`)

Per heor-skills pipeline (regulation-navigator → tariff-scout → prisma-review → economic-modeling → hta-quality-check; no submission drafting needed in-house):

```
value/
  dossier.yaml        # product (HOSP-ART-VIZ narrow scope), setting, horizon, perspective
  documents/          # local SOP excerpts, validation summary (Doc 10), time-motion observations
  literature/         # PRISMA-2020 screen on planning-viewer performance (prisma-review skill)
  model/              # @heor/engine run: decision-tree/time-cost model, NOT an LLM calculation
  report/             # hta-quality-check score + consistency review + human-review disclaimer
```

## 3. Model discipline (deterministic engine does the math)

- Model type: simple decision-tree / budget-impact shell (planning time, repeat-imaging rate, staffing), parameters from Doc 10/11 observations and hospital cost accounting, each with source + uncertainty range.
- PSA: Monte-Carlo over planning-time and discordance-rate distributions; tornado on drivers; scenario: native-CTA-only vs native+visualisation-aid.
- Rule: every number traceable to `model/runs/*.json` + Excel export with live formulas; no hand-typed results in prose (use `{{fact}}`-style placeholders per heor conventions).

## 4. Allowed vs forbidden uses

| Allowed (feeds Doc 04 context) | Forbidden |
|---|---|
| Time-motion / workflow-integration description | Cost-based non-equivalence ("CE device too expensive") |
| Local-performance gap narrative (with Doc 10 data) | Efficacy/safety claims beyond validation |
| Implementation-cost transparency for management (Doc 00 resourcing) | Payer/HTA submission language |
| Monitoring KPIs for Doc 11 (planning-discussion duration, discordance) | Publication as comparative-effectiveness evidence without protocol |

## 5. Deliverable and review

- Deliverable: 2-4 page value note + engine run archive, reviewed by `[HOSPITAL: clinician + QA + finance]`, filed alongside Doc 04 as **context only**. Every page carries: "Draft, requires review by qualified professionals. Not regulatory, clinical, or reimbursement advice."

---
> Return to the [reading index](../../README.md#how-to-read-this-package).

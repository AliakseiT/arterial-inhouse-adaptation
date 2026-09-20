# 03 — Device Qualification and Classification Reasoning

> Owner: regulatory function. Purpose: explain why Art 5(5)(f) documentation depth is what it is, even though no CE class certificate is issued.

## 1. Qualification as MDSW (medical device software)

Apply MDCG 2019-11 logic to the Doc 02 purpose:

1. **Software** acting on CTA data beyond mere storage/communication (segmentation, centerline computation, rendering that influences planning discussion) → qualifies as MDSW under MDR Art 2(1).
2. **Intended purpose** (Doc 02) has a medical purpose (supporting intervention planning) → device, not accessory, not non-device viewer.
3. Research-only or pure visualisation of anatomy **without** a medical purpose would not qualify — but Doc 02 explicitly claims planning-discussion support, so qualification as a device is the conservative and correct assumption.

Record: `[HOSPITAL: qualification decision QUALIFIED AS DEVICE / rationale / sign-off]`. If the hospital instead claims non-device status, it must evidence that no medical-purpose action occurs — inconsistent with clinical use described here, and not recommended.

## 2. MDR classification reasoning (Rule 11, Annex VIII)

MDR Rule 11 (software): Class I if it does not drive decisions; **Class IIa** if it provides information used to take decisions with diagnostic/therapeutic purposes; **Class IIb/III** if decisions may cause serious deterioration or surgical invasiveness implications.

- Under Doc 02's narrow scope (adjunctive visualisation, mandatory overread, no thresholds/flags), the most defensible reading is **Class IIa-equivalent** (information supporting a therapeutic decision in stroke).
- If access prediction or tortuosity-driven triage were shown, classification-equivalent rises to **Class IIb** (decisions with potential for serious deterioration / invasive procedure gating). This is a primary reason Doc 02 excludes those outputs.
- Informative vs driving matters less than the hospital admits: the authority will assess worst-case foreseeable reliance, not the disclaimer alone.

Record: `[HOSPITAL: classification-equivalent decision, rule cited, rationale, reviewer]`. There is no notified body under Art 5(5); the class-equivalent sets **documentation depth** (risk, validation, clinical-evidence expectations) — IIa-equivalent still demands real validation (Doc 10), not a paperwork exercise.

## 3. Consequences for this package

| If class-equivalent is… | Then… |
|---|---|
| IIa-equiv (narrow scope) | Docs 05/08/10 as written are proportionate. Proceed. |
| IIb-equiv (or scope creep) | Stop. Re-scope to Doc 02 or rebuild Docs 04/05/08/10 at IIb depth (independent validation cohorts, tighter residual-risk bar, deeper clinical evidence). Re-sign Doc 00. |
| Claimed Class I / non-device | Provide standalone rationale; authority is unlikely to accept for planning-support CTA software. Do not use to reduce validation. |

## 4. IEC 62304 safety class (distinct from MDR class)

Preliminary software safety classification per IEC 62304 (Doc 09): **Class B minimum, evaluate Class C** — a hazardous failure (false/missing vessels, distorted geometry, silent failure) can contribute to a hazardous situation in thrombectomy planning even with overread, given time pressure and automation bias. Final class after risk analysis (Doc 08): `[HOSPITAL: B / C + rationale]`. Class C would tighten architecture, segregation, and verification obligations.

## 5. Sign-off

- `[HOSPITAL: regulatory reviewer, date]`
- Linked: Doc 02 (purpose), Doc 04 (equivalence search scoped by this classification), Doc 08 (hazards assume IIa-equiv harm model).

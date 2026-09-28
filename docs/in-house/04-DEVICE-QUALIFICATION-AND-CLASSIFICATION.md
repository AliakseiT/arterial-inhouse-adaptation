# 04, Device Qualification and Classification Reasoning

> First-time reader: terms are spelled out on first use. Full list: `00-ABBREVIATIONS-AND-TERMINOLOGY.md`.
>
> Owner: regulatory function. Purpose: explain why Art 5(5)(f) documentation depth is what it is, even though no CE class certificate is issued.

## 1. Qualification as MDSW (medical device software)

Apply MDCG 2019-11 rev.1 (June 2025) logic to the Doc 03 purpose:

1. **Software** acting on CTA data beyond mere storage/communication (segmentation, centerline computation, rendering that influences planning discussion) → qualifies as MDSW under MDR Art 2(1). MDCG 2019-11 rev.1 Annex I (image management systems) draws the same line: systems "only used for viewing, archiving and transmitting images are not considered medical devices", while those with "image processing functions which alter image data or complex quantitative functions to aid in diagnosis, are qualified as MDSW". Segmentation and centerline extraction create new image data.
2. **Intended purpose** (Doc 03) has a medical purpose (supporting intervention planning) → device, not accessory, not non-device viewer.
3. Research-only or pure visualisation of anatomy **without** a medical purpose would not qualify, but Doc 03 explicitly claims planning-discussion support, so qualification as a device is the conservative and correct assumption.

Record: `[HOSPITAL: qualification decision QUALIFIED AS DEVICE / rationale / sign-off]`. If the hospital instead claims non-device status, it must evidence that no medical-purpose action occurs, inconsistent with clinical use described here, and not recommended.

## 2. MDR classification reasoning (Rule 11, Annex VIII)

### 2.1 The rule

Rule 11, first three paragraphs (sub-rule 11a in MDCG 2019-11 rev.1 §4.2.1):

> Software intended to provide information which is used to take decisions with diagnosis or therapeutic purposes is classified as class IIa, except if such decisions have an impact that may cause: death or an irreversible deterioration of a person's state of health, in which case it is in class III; or a serious deterioration of a person's state of health or a surgical intervention, in which case it is classified as class IIb.

MDCG 2019-11 rev.1 reads sub-rule 11a as "generally applicable to all MDSW (excluding those MDSW that have no medical purpose)". Class I under sub-rule 11c covers only software outside 11a and 11b. A device with the Doc 03 purpose therefore starts at IIa. The question is only whether an exception lifts it to IIb or III. The exceptions apply where decisions "if based on incorrect information from the MDSW, are reasonably likely to have an impact" of the listed severity.

MDCG 2019-11 rev.1 Annex III maps Rule 11a onto the IMDRF (International Medical Device Regulators Forum) risk framework (IMDRF/SaMD WG/N12FINAL:2014). Two axes decide the class:

| State of healthcare situation | Treat or diagnose | Drives clinical management | Informs clinical management |
|---|---|---|---|
| Critical | Class III (IV.i) | Class IIb (III.i) | Class IIa (II.i) |
| Serious | Class IIb (III.ii) | Class IIa (II.ii) | Class IIa (I.ii) |
| Non-serious | Class IIa (II.iii) | Class IIa (I.iii) | Class IIa (I.i) |

Definitions (IMDRF N12 §5, as reproduced in Health Canada's guidance "Software as a Medical Device (SaMD): Definition and Classification", §2.3.1):

- Treat or diagnose: the information "will be used to take an immediate or near-term action".
- Drive clinical management: the information "will be used to: triage or identify early signs of a disease or condition that will be used to guide next diagnostics or treatment interventions; aid in diagnosis; aid in treatment". Aid in treatment is "providing enhanced support to safe and effective use of medicinal products or a medical device".
- Inform clinical management: the information "will not trigger an immediate or near-term action".
- Critical situation: accurate or timely action "is vital to avoid death, long-term disability or other serious deterioration of health". The listed criteria include "Life threatening state of health", "Requires major therapeutic interventions", and "Sometimes time critical". Acute stroke meets all three.

### 2.2 Position for the Doc 03 purpose: Class IIb-equivalent

Healthcare situation: critical. Acute ischaemic stroke is life-threatening, and MDCG 2019-11 rev.1 Annex IV calls stroke critical in its own example.

Significance: drives clinical management. The vessel map aids treatment. It is looked at during the planning of a thrombectomy that follows within minutes. "Inform" cannot hold, because by definition inform-level information does not trigger near-term action, and the planning discussion is near-term action.

Critical plus drives gives Class IIb (IMDRF III.i). Rule 11's own text leads to the same place independently: a wrong map can mislead the planning of an endovascular intervention, and "surgical intervention" is a IIb trigger.

### 2.3 Why not Class III

MDCG 2019-11 rev.1 Annex IV gives the nearest example: "MDSW intended to perform diagnosis by means of image analysis for making treatment decisions in patients with acute stroke should be classified as class III", because the situation is critical and the significance is "treat or diagnose".

The Doc 03 device differs on the significance axis, not on severity. It does not detect or diagnose the occlusion. It does not select patients for thrombectomy. It does not recommend an access route or device. The decision to treat is taken from the source CTA and clinical assessment before the map matters. The treatment itself is also planned and carried out on the source CTA, angiography, and clinical judgement. The map aids that action, which is the drive-level "aid in treatment"; it is not the information the action is taken on. The map is a display of anatomy already present in the CTA, under mandatory overread.

This package does not argue that incorrect output is harmless. Doc 04 §4 and Doc 09 H1, H5, and H10 assume a wrong display can contribute to serious harm under time pressure. The case against III rests only on what the information is used for.

An authority may still read the planning step as "treat" and assign III-equivalent. The hospital records its answer to that reading. Showing any hidden upstream output (access-difficulty probability, tortuosity flags) moves the significance toward "treat or diagnose" and makes III the likely reading. This is a primary reason Doc 03 excludes those outputs.

### 2.4 Record

Record: `[HOSPITAL: classification-equivalent decision, rule and MDCG 2019-11 rev.1 table cell cited, rationale, reviewer]`. There is no notified body under Art 5(5); the class-equivalent sets **documentation depth** (risk, validation, clinical-evidence expectations), not a certificate.

## 3. Consequences for this package

| If class-equivalent is… | Then… |
|---|---|
| IIb-equiv (base case for Doc 03 scope) | Docs 06-12 target this depth. Validation uses a locked test set temporally separated from development data, two-reader ground truth, and a prospective shadow phase (Doc 11). Proceed. |
| III-equiv (authority reading, or any hidden output shown) | Stop. Either restore the Doc 03 scope or rebuild Docs 05, 09, 10, 11 at III depth: external validation cohort from another site or period, independent readers, prospective clinical-performance evidence, tighter residual-risk bar. Re-sign Doc 01. |
| IIa-equiv claimed | Needs a standalone argument that the information only informs and triggers no near-term action. Hard to sustain for use in acute stroke planning. Never use it to reduce validation. |
| Class I / non-device claimed | Not available: sub-rule 11a covers all MDSW with a medical purpose. Do not use. |

## 4. IEC 62304 safety class (distinct from MDR class)

IEC 62304 is the software lifecycle standard. It assigns its own safety class based on what harm the software can contribute to, not the MDR device class. Class A means no injury is possible. Class B means a failure can contribute to non-serious injury. Class C means a failure can contribute to death or serious injury.

"B minimum, C expected" means this: never go below Class B, and plan for Class C. Only the risk analysis in Doc 09 can bring it back to B. A wrong or missing vessel display in thrombectomy (mechanical clot removal) planning can contribute to a serious harm even with overread, because stroke care runs under time pressure and reviewers trust displays. That pushes toward C. The IIb-equivalent position in §2 already assumes serious deterioration is possible, so C is the expected outcome unless the Doc 09 analysis shows that risk controls outside the software (overread, native-CTA fallback) reduce the software's contribution.

Preliminary position (Doc 10): Class B minimum, Class C expected. Final class after risk analysis (Doc 09): `[HOSPITAL: B / C + rationale]`. At C, the hospital adds stronger architecture segregation, detailed design records, and deeper integration verification. The class does not change the narrow purpose. It changes how much proof is needed.

## 5. Sign-off

- `[HOSPITAL: regulatory reviewer, date]`
- Linked: Doc 03 (purpose), Doc 05 (equivalence search scoped by this classification), Doc 09 (hazards assume the IIb-equiv harm model: serious deterioration possible).

---
> Return to the [reading index](../../README.md#how-to-read-this-package).

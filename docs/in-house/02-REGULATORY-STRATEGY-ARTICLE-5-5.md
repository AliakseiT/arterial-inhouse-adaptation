# 02, Regulatory Strategy: Article 5(5) Conditions and MDCG 2023-1 Map

> First-time reader: terms are spelled out on first use. Full list: `00-ABBREVIATIONS-AND-TERMINOLOGY.md`.
>
> Owner: hospital regulatory/QA function. Sources: MDR Art 5(5)(a)-(h), MDCG 2023-1 §§3-4 + Annex A.
> This is a strategy note, not advice. Confirm against `[HOSPITAL: Member State]` national implementation.

## 1. Legal theory in one paragraph

With the exception of the relevant Annex I GSPRs (General Safety and Performance Requirements), the MDR (Medical Device Regulation) does not apply to a device manufactured and used only within the same EU health institution, on a non-industrial scale, meeting all Art 5(5)(a)-(h) conditions. Upstream Arterial is not a device placed on the market; the hospital's frozen, renamed fork (`[HOSPITAL: in-house device identifier, e.g. HOSP-ART-VIZ-1.0]`) is the candidate in-house device. Software use counts as "use within" when the clinical act occurs inside the legal entity, including remote viewing by its staff on its systems, provided nothing is made available to another legal entity (MDCG 2023-1 §3.2.2, §3.4).

## 1A. Adaptation as manufacture

> Prerequisite: Doc 03 defines the device. Readers unfamiliar with the device definition review Doc 03 before this section.

The hospital does not transfer open-source code into a product. It manufactures a distinct device by adapting research code to a different intended purpose, and that adaptation forms part of the Article 5(5) case in three respects, each filed as evidence.

First, upstream purpose versus in-house purpose. Upstream Arterial is a research framework with a broad, unvalidated claim set: segmentation, centerlines, labelling, tortuosity features, access prediction. The in-house device claims one narrow thing: visualisation support with mandatory overread (Doc 03). Different purpose means different device. Upstream is therefore not an equivalent device for Doc 05 purposes, and no one can argue the hospital simply relabelled research software.

Second, the adaptation record is manufacturing evidence. The fork log shows the manufacturing steps: pinning, hardening the DICOM (Digital Imaging and Communications in Medicine) intake, adding Quality Control gates and fail-stop behaviour, adding provenance logging, hiding predictive outputs, locking the deployment. Each change links to a requirement, a risk control, and a test (Docs 07, 08, 09). An authority reading the (f) file sees manufacture happening, not copying.

Third, local validation closes the loop. Upstream metrics describe other data. Hospital validation (Doc 11) characterises the adapted build on local scanners and protocols. That is the performance data (f) demands and the reason (c) holds: the need is met at appropriate performance only after hospital-specific adaptation, which no off-the-shelf device underwent for this site.

Limits. Adaptation does not excuse any condition. It supports (c), (f), and (g) only where the record is complete: dated fork diffs, reviewed changes, validation on the frozen build. An adaptation without local evidence carries no weight.

## 2. Condition-by-condition map

### (a) No transfer to another legal entity
- **Means:** binary, model weights, outputs, documentation-as-device, and remote access stay inside `[HOSPITAL: legal entity]`. No sale, loan, cloud processing by a separate controller/processor outside the entity unless that processing is strictly internal provision (seek local counsel; joint-entity hospital groups need entity analysis).
- **Evidence:** Doc 14 repo access rules; deployment architecture (Doc 07 §3) showing on-prem/air-gapped inference; user-access list; no-transfer attestation in Doc 13.
- **Trap:** teleradiology via an external legal entity, multi-site groups with separate entities, or sharing the fork with another hospital breaks (a).

### (b) Appropriate QMS
- **Means:** manufacture + use under a QMS compliant with Art 5(5), relevant Annex I, national law, and applicable ISO standards if certified. MDCG points to MDR Art 10(9) elements as guidance: management responsibility, resource management, design/development, document/record control, traceability, change control, risk, vigilance/CAPA, PMS-like use review.
- **Evidence:** Doc 08 mapping table from each element to `[HOSPITAL: SOP reference]`; gaps become CAPAs before clinical use.
- **Note:** ISO 13485 certification is **not** legally required for (b), but the QMS must be real, documented, and followed. ISO 15189 alone is insufficient for a software device.

### (c) Non-equivalence to CE devices
- **Means:** documented justification, **before first manufacture**, that the target group's specific needs cannot be met, or not at appropriate performance, by an equivalent CE device. Technical, biological, or clinical grounds, not price or convenience.
- **Evidence:** Doc 05 (search method, EUDAMED + vendor + literature, dated results, reviewer, re-check cadence) + Doc 15 (workflow/performance framing).
- **Trap:** "Arterial is open-source and free" is not a (c) argument. General-purpose CE viewers with adequate performance defeat (c) unless a specific, evidenced gap is shown.

### (d) Information to competent authority on request
- **Means:** provide manufacture/use info including justification of manufacturing, modification, and use; accept inspections; respect Member-State restrictions/notifications.
- **Evidence:** Doc 12 §5 authority pack + named owner + retrieval drill.

### (e) Public declaration
- **Means:** draw up and publish (e.g. hospital website): institution name/address, device identification, GSPR compliance statement with reasoned justification for any unmet requirement.
- **Evidence:** Doc 13 (MDCG Annex A-based). Keep versioned; update on every change affecting identity or GSPR claim.

### (f) Technical documentation (facility / process / design / performance)
- **Means:** documentation detailed enough for the authority to ascertain GSPR compliance, covering manufacturing facility, process, design and performance data including intended purpose. For software: frozen source commit, build environment, SOUP/SBOM, data pipeline, verification/validation, risk, usability, security.
- **Evidence:** Doc 07 index; Docs 06, 08-10 supply content. "Upstream README" is not (f).

### (g) Manufacture per (f)
- **Means:** management ensures every deployed instance matches (f); controlled builds, releases, installation, configuration.
- **Evidence:** Doc 10 release gates + Doc 12 §2 deployment controls.

### (h) Clinical-use review + corrective action
- **Means:** systematic review of experience from clinical use; all necessary corrective actions.
- **Evidence:** Doc 12 monitoring plan (case log, overread discordance, incidents, CAPA linkage).

### Non-industrial scale (last subparagraph)
- Produce only what own-patient need requires; no stockpiling, no commercial-scale operation. Deployment count, case volume, and build frequency must be proportionate. Document the volume rationale in Doc 07 §6.

## 3. Hidden features and the wider-use path (transparency rule)

> Prerequisite: Doc 03 defines the device as a vessel map, a version label, and an explicit failure state. This section builds on that definition.

The fork contains more than the defined device, because upstream Arterial ships extra modules: access prediction, tortuosity scoring, vessel labelling names, attention maps. For the initial claim these extras are hidden from the clinical interface by configuration, not removed from the repository. The hospital declares this openly in Docs 03, 06, and 12: what is hidden, where the flag lives, and the release proof test that confirms clinicians cannot reach it.

Uncovering any hidden output for clinical display is a new intended purpose. It requires a Doc 03 revision, fresh non-equivalence analysis, risk and validation updates, and a new declaration before use. Enabling outside this process is not permitted.

## 4. What (5)(5) does NOT waive

- Relevant Annex I GSPRs (safety, performance, risk, usability, labelling/IFU-equivalent, security).
- National law (device-type restrictions, notification duties, language rules for information supplied with the device).
- Data protection (GDPR), information security, medical professional duties, procurement rules.
- IP/licence compliance (Doc 14).

## 5. National check (complete first)

- `[HOSPITAL: Member State + competent authority + contact]`
- `[HOSPITAL: national in-house restrictions/notifications applicable? Y/N + citation]`
- `[HOSPITAL: language requirements for clinician-facing information]`
- `[HOSPITAL: incident-reporting route for in-house devices]`
- Reviewed with: `[HOSPITAL: regulatory function sign-off, date]`

---
> Return to the [reading index](../../README.md#how-to-read-this-package).

# 01, Regulatory Strategy: Article 5(5) Conditions and MDCG 2023-1 Map

> First-time reader: terms are spelled out on first use. Full list: `00-ABBREVIATIONS-AND-TERMINOLOGY.md`.
>
> Owner: hospital regulatory/QA function. Sources: MDR Art 5(5)(a)-(h), MDCG 2023-1 §§3-4 + Annex A.
> This is a strategy note, not advice. Confirm against `[HOSPITAL: Member State]` national implementation.

## 1. Legal theory in one paragraph

With the exception of the relevant Annex I GSPRs, the MDR does not apply to a device manufactured and used **only within the same EU health institution**, on a **non-industrial scale**, meeting **all** Art 5(5)(a)-(h) conditions. Upstream Arterial is not a device placed on the market; the hospital's **frozen, renamed fork** (`[HOSPITAL: in-house device identifier, e.g. HOSP-ART-VIZ-1.0]`) is the candidate in-house device. Software use counts as "use within" when the clinical act occurs inside the legal entity, including remote viewing by its staff on its systems, provided nothing is made available to another legal entity (MDCG 2023-1 §3.2.2, §3.4).

## 2. Condition-by-condition map

### (a) No transfer to another legal entity
- **Means:** binary, model weights, outputs, documentation-as-device, and remote access stay inside `[HOSPITAL: legal entity]`. No sale, loan, cloud processing by a separate controller/processor outside the entity unless that processing is strictly internal provision (seek local counsel; joint-entity hospital groups need entity analysis).
- **Evidence:** Doc 13 repo access rules; deployment architecture (Doc 06 §3) showing on-prem/air-gapped inference; user-access list; no-transfer attestation in Doc 12.
- **Trap:** teleradiology via an external legal entity, multi-site groups with separate entities, or sharing the fork with another hospital breaks (a).

### (b) Appropriate QMS
- **Means:** manufacture + use under a QMS compliant with Art 5(5), relevant Annex I, national law, and applicable ISO standards if certified. MDCG points to MDR Art 10(9) elements as guidance: management responsibility, resource management, design/development, document/record control, traceability, change control, risk, vigilance/CAPA, PMS-like use review.
- **Evidence:** Doc 07 mapping table from each element to `[HOSPITAL: SOP reference]`; gaps become CAPAs before clinical use.
- **Note:** ISO 13485 certification is **not** legally required for (b), but the QMS must be real, documented, and followed. ISO 15189 alone is insufficient for a software device.

### (c) Non-equivalence to CE devices
- **Means:** documented justification, **before first manufacture**, that the target group's specific needs cannot be met, or not at appropriate performance, by an equivalent CE device. Technical, biological, or clinical grounds, not price or convenience.
- **Evidence:** Doc 04 (search method, EUDAMED + vendor + literature, dated results, reviewer, re-check cadence) + Doc 14 (workflow/performance framing).
- **Trap:** "Arterial is open-source and free" is not a (c) argument. General-purpose CE viewers with adequate performance defeat (c) unless a specific, evidenced gap is shown.

### (d) Information to competent authority on request
- **Means:** provide manufacture/use info including justification of manufacturing, modification, and use; accept inspections; respect Member-State restrictions/notifications.
- **Evidence:** Doc 11 §5 authority pack + named owner + retrieval drill.

### (e) Public declaration
- **Means:** draw up and publish (e.g. hospital website): institution name/address, device identification, GSPR compliance statement with reasoned justification for any unmet requirement.
- **Evidence:** Doc 12 (MDCG Annex A-based). Keep versioned; update on every change affecting identity or GSPR claim.

### (f) Technical documentation (facility / process / design / performance)
- **Means:** documentation detailed enough for the authority to ascertain GSPR compliance, covering manufacturing facility, process, design and performance data including intended purpose. For software: frozen source commit, build environment, SOUP/SBOM, data pipeline, verification/validation, risk, usability, security.
- **Evidence:** Doc 06 index; Docs 05, 08-10 supply content. "Upstream README" is not (f).

### (g) Manufacture per (f)
- **Means:** management ensures every deployed instance matches (f); controlled builds, releases, installation, configuration.
- **Evidence:** Doc 09 release gates + Doc 11 §2 deployment controls.

### (h) Clinical-use review + corrective action
- **Means:** systematic review of experience from clinical use; all necessary corrective actions.
- **Evidence:** Doc 11 monitoring plan (case log, overread discordance, incidents, CAPA linkage).

### Non-industrial scale (last subparagraph)
- Produce only what own-patient need requires; no stockpiling, no commercial-scale operation. Deployment count, case volume, and build frequency must be proportionate. Document the volume rationale in Doc 06 §6.

## 3. Hidden features and the wider-use path (transparency rule)

The fork contains upstream modules outside the narrow purpose: access prediction, tortuosity scoring, vessel labelling names, attention maps. For the initial claim these are hidden from the clinical interface by configuration, not removed from the repository. The hospital declares this openly in Docs 02, 06, and 12: what is hidden, where the flag lives, and the release proof test that confirms clinicians cannot reach it.

Uncovering any hidden output for clinical display is a new intended purpose. It requires a Doc 02 revision, fresh non-equivalence analysis, risk and validation updates, and a new declaration before use. No silent enabling. The pathfinder scope stays credible because the wider scope has a defined door, not a backdoor.

## 4. What (5)(5) does NOT waive

- Relevant Annex I GSPRs (safety, performance, risk, usability, labelling/IFU-equivalent, security).
- National law (device-type restrictions, notification duties, language rules for information supplied with the device).
- Data protection (GDPR), information security, medical professional duties, procurement rules.
- IP/licence compliance (Doc 13).

## 4. National check (complete first)

- `[HOSPITAL: Member State + competent authority + contact]`
- `[HOSPITAL: national in-house restrictions/notifications applicable? Y/N + citation]`
- `[HOSPITAL: language requirements for clinician-facing information]`
- `[HOSPITAL: incident-reporting route for in-house devices]`
- Reviewed with: `[HOSPITAL: regulatory function sign-off, date]`

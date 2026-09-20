# 07 — QMS Mapping and Hospital Adoption Checklist

> Owner: QA. Principle: the hospital's QMS stays the system of record. This doc maps Art 5(5)/Annex I needs onto it and gives the adoption checklist. QMS-baseline SOP numbers below are a reference model (`AliakseiT/dearauditor-qms-baseline`); replace with `[HOSPITAL: SOP]` equivalents.

## 1. Element mapping (MDCG 2023-1 Table 1 style)

| Required element (Art 5(5)/Annex I/MDCG) | Reference-model SOP | Hospital equivalent | Gap / action |
|---|---|---|---|
| Management responsibility, resources, (g) manufacture-per-doc | SOP-005 Governance, SOP-004 Mgmt review, SOP-017 Infrastructure | `[HOSPITAL]` | `[HOSPITAL]` |
| Document/record control, (f) technical documentation | SOP-001 Doc control; MDF templates (`intended_use`, `device_description`, `classification_decision`, `in_house_justification`) | `[HOSPITAL]` | `[HOSPITAL]` |
| Design & development control | SOP-008 Design control | `[HOSPITAL]` | `[HOSPITAL]` |
| Risk management (Annex I §3) | SOP-018 (ISO 14971) | `[HOSPITAL]` | `[HOSPITAL]` |
| Software lifecycle / config / release | SOP-020 (IEC 62304) + WI-002 | `[HOSPITAL]` | `[HOSPITAL]` |
| Verification & validation execution | WI-001 | `[HOSPITAL]` | `[HOSPITAL]` |
| Usability engineering | SOP-019 (IEC 62366-1) | `[HOSPITAL]` | `[HOSPITAL]` |
| Change management | SOP-009 | `[HOSPITAL]` | `[HOSPITAL]` |
| Traceability / identification (e)(h) | SOP-007 MDF control | `[HOSPITAL]` | `[HOSPITAL]` |
| Feedback/complaints, PMS-like use review (h) | SOP-012, SOP-014 | `[HOSPITAL]` | `[HOSPITAL]` |
| Incident reporting / vigilance | SOP-013 | `[HOSPITAL: national route]` | `[HOSPITAL]` |
| Nonconforming product, CAPA | SOP-015, SOP-002 | `[HOSPITAL]` | `[HOSPITAL]` |
| Internal audit | SOP-003 | `[HOSPITAL]` | `[HOSPITAL]` |
| Training/competence | SOP-011 + training matrix | `[HOSPITAL]` | `[HOSPITAL]` |
| Information security | SOP-021 (ISO 27001) | `[HOSPITAL]` | `[HOSPITAL]` |
| Data protection (DICOM/PHI) | SOP-023 (GDPR/nFADP) | `[HOSPITAL: DPIA ref]` | `[HOSPITAL]` |
| AI management (where adopted) | SOP-022 (ISO 42001) | `[HOSPITAL: if applicable]` | `[HOSPITAL]` |
| Supplier control (GPU/IT, annotation services) | SOP-010 | `[HOSPITAL: supplier list]` | `[HOSPITAL]` |
| QMS software validation (if QMS tooling used) | SOP-006 | `[HOSPITAL]` | `[HOSPITAL]` |

All gaps → actions with owners/dates before clinical use. Uncertified QMS is acceptable only if every row above is genuinely operated, not aspirational.

## 2. Hospital adoption checklist (complete in order; record evidence ref + date + signer per line)

### Phase A — Decide (no engineering beyond de-identified feasibility)
- [ ] A1. National law check (Doc 01 §4) signed. `[ref/date/signer]`
- [ ] A2. Same-legal-entity + non-industrial-scale confirmation signed. `[…]`
- [ ] A3. Doc 02 narrow purpose approved by clinical lead + QA. `[…]`
- [ ] A4. Doc 03 qualification/classification-equivalent recorded. `[…]`
- [ ] A5. Doc 04 non-equivalence search + determination signed **before build**. `[…]`
- [ ] A6. Licence clearance to fork/deploy internally (Doc 13) + private-repo created. `[…]`
- [ ] A7. Device owner, clinical lead, QA oversight named; resourcing for lifetime committed. `[…]`
- [ ] A8. GO decision (Doc 00 §5) recorded. `[…]`

### Phase B — Build under QMS
- [ ] B1. Upstream commit pinned; fork frozen; build env locked (Docs 06/09). `[…]`
- [ ] B2. SBOM + SOUP risk + CVE review filed. `[…]`
- [ ] B3. Access-prediction/quantitative outputs disabled + verified (Doc 02 §4 proof test). `[…]`
- [ ] B4. DICOM→NIfTI intake, QC gates, fail-stop, provenance logging implemented. `[…]`
- [ ] B5. Risk file drafted (Doc 08); architecture + requirements traced. `[…]`
- [ ] B6. IFU-equivalent + on-screen warnings drafted in required language(s). `[…]`
- [ ] B7. Verification (incl. build reproducibility) complete. `[…]`

### Phase C — Validate, approve, declare
- [ ] C1. Local validation per Doc 10 executed; acceptance criteria met; report approved. `[…]`
- [ ] C2. Usability summative (overread compliance under time pressure) passed. `[…]`
- [ ] C3. Residual benefit-risk accepted (Docs 05/08). `[…]`
- [ ] C4. Release decision + installation qualification signed. `[…]`
- [ ] C5. Training completed and recorded (role matrix). `[…]`
- [ ] C6. Public declaration published (Doc 12) + version linked to frozen build. `[…]`
- [ ] C7. Monitoring plan live (Doc 11): case log, discordance review, CAPA route. `[…]`

### Phase D — Operate
- [ ] D1. Quarterly use review held; annual non-equivalence re-check scheduled. `[…]`
- [ ] D2. Authority-pack drill passed (Doc 06 §8). `[…]`
- [ ] D3. Any change → change control + re-validation assessment before deployment. `[…]`
- [ ] D4. Retirement/decommissioning plan on file. `[…]`

## 3. Training roles (minimum)

| Role | Needs device training | Content |
|---|---|---|
| Interventionalists / neuroradiologists / stroke neurologists (users) | Yes | Purpose/limits, overread duty, failure states, incident reporting |
| Radiographers / PACS operators | Yes (handling) | Input spec, rejection handling, provenance check |
| Clinical engineering / IT | Yes | Deployment, monitoring, rollback, backup |
| QA/regulatory | Yes | Docs 01–12, authority interface |
| Management | Awareness | Doc 00 + (g)(h) duties |

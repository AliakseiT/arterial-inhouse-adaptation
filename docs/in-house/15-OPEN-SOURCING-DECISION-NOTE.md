# 15, Open-Sourcing Decision Note (future, gated)

> First-time reader: terms are spelled out on first use. Full list: `00-ABBREVIATIONS-AND-TERMINOLOGY.md`.
>
> Owner: repo owner + hospital legal + upstream rights holders. Default: this adaptation stays private. Publication is a separate decision with separate consent.

## 1. What could eventually be published (after sanitisation + consent)

- Hospital-authored **method** docs (this package's structure, checklists, validrig pack skeleton, HEOR outline), containing no hospital-identifying, patient, infrastructure, or authority-correspondence content.
- Hospital-authored **hardening patches** (QC gates, provenance logging, disablement flags), only if upstream accepts the contribution model and NC terms permit the publication channel.
- Validation **methods and aggregate metrics**, never images, never per-case data, only with ethics approval for the aggregate disclosure.

## 2. What stays private permanently

Upstream code/weights beyond fair-use excerpts (NC redistribution bar), hospital instance records (Docs 02/04/06/10-12 as completed), SBOM with internal hostnames, deployment configs, logs, training records, authority correspondence, any PHI-adjacent material.

## 3. Gate checklist for any publication step

- [ ] Written consent from VHIR/UB for the exact material + licence (NC-compatible channel).
- [ ] Hospital management + legal + QA sign-off; de-identification review passed.
- [ ] Upstream `LICENSE`/`Required Notice`/`THIRD_PARTY_NOTICES` + model `LICENSE`/`NOTICE` bundled correctly.
- [ ] No PHI, no internal infrastructure, no authority docs in the published set (two-reviewer check).
- [ ] Publication version frozen and recorded; issues channel designated (public issues ≠ incident reporting, Doc 11 route stays internal).

Without all five: do not publish. A private repo with good hygiene is the compliant steady state.

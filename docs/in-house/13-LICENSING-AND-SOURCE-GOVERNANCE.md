# 13, Licensing and Source Governance

> First-time reader: terms are spelled out on first use. Full list: `00-ABBREVIATIONS-AND-TERMINOLOGY.md`.
>
> Owner: hospital legal + engineering. Upstream rights: VHIR + Universitat de Barcelona (2022-2026). This note prevents the most common failure mode: treating open-source visibility as freedom to deploy clinically or republish.

## 1. Licence split (verify against pinned upstream commit before relying)

| Layer | Licence | What it means for the hospital |
|---|---|---|
| Arterial **source code** (`FLOWCAT-CV/arterial`) | PolyForm Noncommercial 1.0.0 (`LICENSE`, with `Required Notice` preservation) | Internal non-commercial hospital use including in-house clinical deployment is within the permitted non-commercial scope **provided** the hospital qualifies (public-health organisation use is expressly permitted regardless of funding). Redistribution, public forks, hosted offering, or commercial use require a separate licence from VHIR/UB. |
| Arterial **trained weights** (Zenodo `10.5281/zenodo.22694951`) | CC BY-NC 4.0 (non-commercial, attribution) | Same posture as code: internal clinical use allowed; sharing outside the legal entity, commercial use, or public redistribution requires rights-holder consent. |
| TotalSegmentator `craniofacial_structures` sub-model | Apache-2.0 (per `THIRD_PARTY_NOTICES.md` + in-model `LICENSE`/`NOTICE`) | Permits commercial use **of that sub-model alone**; keep `LICENSE`+`NOTICE` with every copy. Does not lift NC terms on surrounding Arterial code/weights. |
| Dependencies (nnU-Net/MONAI Apache-2.0, VMTK BSD, PyG MIT, + transitive) | As labelled | Comply independently; preserve attributions; SBOM records obligations (Doc 09 §3). |

PolyForm NC § "Changes and New Works" governs hospital modifications: internal use is fine; **publishing** the modified work (including a public GitHub repo) is distribution-like and needs upstream consent. When in doubt, ask before pushing.

## 2. Repository rules for this private adaptation repo

1. **Private from creation.** `AliakseiT/arterial-inhouse-adaptation` (or hospital-owned private repo), no public visibility until Doc 15 clearance.
2. **Upstream hygiene.** Pin upstream commit SHA; never force-push upstream history; keep `LICENSE`, `Required Notice`, `THIRD_PARTY_NOTICES.md`, model `LICENSE`/`NOTICE` intact in every copy (build artefacts, weight mirrors, air-gap media).
3. **Attribution.** Preserve VHIR/UB copyright notices + cite Canals 2023, Wasserthal 2023, Beyer 2026, Isensee 2021 (upstream README §Citation) in internal docs and any publication.
4. **No weight leakage.** Weights live in controlled storage (`ARTERIAL_MODELS_DIR` equivalent), never in git; access-logged; hashed at build/load.
5. **Hospital-confidential separation.** Patient data, internal network maps, and authority correspondence stay in the hospital QMS, never in this repo, even private. This repo holds the *method*; the hospital record holds the *instance*.
6. **Contributor terms.** Hospital contributors act under employment/QMS; external contributors require a written IP/licence assignment compatible with upstream NC terms before merge.

## 3. Required upstream discussion (before clinical use and before any open-sourcing)

Contact the Arterial research team (via upstream GitHub issues/contact) to cover: (a) awareness of intended in-house clinical adaptation, (b) confirmation of NC-scope interpretation for the specific hospital deployment, (c) defect-reporting channel (upstream issues are public, never include PHI), (d) back-porting safety fixes without pulling unvalidated features, (e) terms for publishing any hospital-added validation/tooling. Record outcome at `[HOSPITAL: QMS ref]`; Doc 15 gates publication on written consent.

## 4. Red lines

- No public repo/weights mirror, no multi-hospital sharing, no vendor hand-off, no commercial service built on the fork, each breaks Art 5(5)(a) and/or the NC licences simultaneously.
- No removal of licence/notice files to "clean" the repo. No re-licensing of upstream code under MIT/Apache by the hospital.
- Procurement of GPU/cloud services does not transfer device responsibility; DPAs and processor terms must keep processing inside the (a)-boundary per counsel.

---
> Return to the [reading index](../../README.md#how-to-read-this-package).

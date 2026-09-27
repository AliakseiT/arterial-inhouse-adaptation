# 14, Licensing and Source Governance

> First-time reader: terms are spelled out on first use. Full list: `00-ABBREVIATIONS-AND-TERMINOLOGY.md`.
>
> Owner: hospital legal + engineering. Upstream rights: VHIR (Vall d'Hebron Research Institute) + UB (Universitat de Barcelona), 2022-2026. Two questions are kept apart here. The licences decide what the hospital may do with the code and weights. Article 5(5)(a) decides where the device may go. The most common failure mode is to answer one and assume the other.

## 1. Licence split (verify against pinned upstream commit before relying)

| Layer | Licence | What it means for the hospital |
|---|---|---|
| Arterial **source code** (`FLOWCAT-CV/arterial`) | PolyForm Noncommercial 1.0.0 (`LICENSE`, first line is the `Required Notice`) | Use, changes, and distribution are licensed for any noncommercial purpose. The licence names public health organisations and public research organisations as permitted users regardless of funding. A privately owned or for-profit hospital is not named; it confirms with VHIR/UB that its clinical use is noncommercial, or obtains a commercial licence. Commercial use, including a paid hosted service, needs a separate licence. |
| Arterial **trained weights** (Zenodo `10.5281/zenodo.22694951`) | CC BY-NC 4.0 (Creative Commons Attribution NonCommercial) | Noncommercial use, sharing, and adaptation are licensed with attribution. Commercial use needs rights-holder consent. |
| TotalSegmentator `craniofacial_structures` sub-model | Apache-2.0 (per `THIRD_PARTY_NOTICES.md` + in-model `LICENSE`/`NOTICE`) | Permits commercial use **of that sub-model alone**; keep `LICENSE`+`NOTICE` with every copy. Does not lift NC terms on surrounding Arterial code/weights. |
| Dependencies (nnU-Net/MONAI Apache-2.0, VMTK BSD, PyG MIT, + transitive) | As labelled | Comply independently; preserve attributions; SBOM records obligations (Doc 10 §3). |

PolyForm NC grants a Changes and New Works License and a Distribution License that covers changed software. Noncommercial publication of a modified fork is therefore licensed, on one condition from the Notices clause: every recipient gets the licence terms (or their URL) and the `Required Notice` line. Upstream consent is not a licence precondition for noncommercial use by a qualifying organisation. Section 3 explains why the hospital contacts upstream anyway.

## 2. Rules for the hospital's fork repository

The hospital's fork and its filled-in records are a different thing from this public method package. This package holds templates and no upstream code. The fork holds the candidate device.

1. **Private, for Article 5(5) reasons.** The fork lives in a private, hospital-controlled repository. The licence does not require this. Article 5(5)(a) and confidentiality do: the fork is the hospital's device, and its records carry hospital-identifying and infrastructure detail.
2. **Upstream hygiene.** Pin upstream commit SHA; never force-push upstream history; keep `LICENSE`, `Required Notice`, `THIRD_PARTY_NOTICES.md`, model `LICENSE`/`NOTICE` intact in every copy (build artefacts, weight mirrors, air-gap media).
3. **Attribution.** Preserve VHIR/UB copyright notices + cite Canals 2023, Wasserthal 2023, Beyer 2026, Isensee 2021 (upstream README §Citation) in internal docs and any publication.
4. **No weight leakage.** Weights live in controlled storage (`ARTERIAL_MODELS_DIR` equivalent), never in git; access-logged; hashed at build/load.
5. **Hospital-confidential separation.** Patient data, internal network maps, and authority correspondence stay in the hospital QMS, never in the fork repository. The fork holds code and build configuration; the QMS holds the records.
6. **Contributor terms.** Hospital contributors act under employment/QMS; external contributors require a written IP/licence assignment compatible with upstream NC terms before merge.

## 3. Upstream contact (before clinical use)

Contact the Arterial research team (via upstream GitHub issues/contact, template in Doc 14A). The purpose is safety and coordination, not permission:

- (a) awareness of the intended in-house clinical adaptation;
- (b) confirmation of noncommercial scope for this hospital, mandatory for a privately owned or for-profit hospital;
- (c) a defect-reporting channel (upstream issues are public, never include PHI, Protected Health Information);
- (d) back-porting safety fixes without pulling unvalidated features;
- (e) advance notice before the hospital publishes its own additions, such as validation methods, so safety-relevant findings reach upstream first.

Record the outcome in the hospital QMS.

## 4. Red lines

Article 5(5)(a), no transfer to another legal entity:

- The released device (frozen build, deployed weights, deployment configuration) never goes to another legal entity. This includes another hospital in the same group if it is a separate entity, and a vendor running it outside strict internal provision.
- Procurement of GPU/cloud services does not transfer device responsibility; DPAs (Data Processing Agreements) and processor terms must keep processing inside the (a)-boundary per counsel.

Publishing source code or methods is a separate act. It supplies source, not a device. Any institution that deploys published code manufactures its own in-house device and carries every Article 5(5) duty itself. MDCG 2023-1 does not address this case directly, so the hospital takes counsel advice before publishing and states in the publication that no device is supplied.

Licence:

- No commercial service or sale built on the fork without a commercial licence from VHIR/UB.
- No removal of licence/notice files to "clean" the repo. No re-licensing of upstream code under MIT/Apache by the hospital.
- No public mirror of the weights. Point to the Zenodo record, so every user gets the published, hashed version.

---
> Return to the [reading index](../../README.md#how-to-read-this-package).

# Upstream contact letter template (hospital legal review required)

> File with Doc 14. Send before clinical use. Keep the reply in the hospital QMS. Never include patient data, internal network detail, or authority correspondence.

Subject: In-house clinical adaptation of Arterial, licence confirmation request

Dear Arterial team,

`[HOSPITAL: legal entity name, address]` is evaluating an in-house adaptation of Arterial (`FLOWCAT-CV/arterial`, pinned commit `[SHA]`, version 2.1-derived) for internal use only, under the EU Medical Device Regulation Article 5(5) health-institution exemption. Scope is narrow: Computed Tomography Angiography vessel segmentation plus centerline visualisation to support thrombectomy planning discussion, with mandatory clinician overread. Predictive outputs remain hidden from clinicians.

We confirm the following understanding and ask you to correct us where wrong:

1. Our internal, non-commercial deployment inside a single health institution falls within the permitted non-commercial scope of the PolyForm Noncommercial 1.0.0 code licence and the CC BY-NC 4.0 (Creative Commons Attribution NonCommercial) weight licence. `[HOSPITAL: if privately owned or for-profit, state the ownership and ask explicitly whether this clinical use counts as noncommercial]`
2. We keep all copyright notices, the Required Notice, THIRD_PARTY_NOTICES.md, and the TotalSegmentator Apache-2.0 LICENSE plus NOTICE with every copy.
3. The device build and weights stay inside our legal entity, as Article 5(5)(a) requires. If we publish our own additions, such as validation methods, we do so on noncommercial terms with your notices, and we tell you beforehand.
4. We report defects without patient data through this channel: `[HOSPITAL: chosen channel]`. We pull only reviewed safety fixes, never unvalidated upstream changes, into clinical builds.
5. `[HOSPITAL: include only if adopting Doc 16]` We may evaluate the access prediction module offline on closed local cases, never shown to clinicians. Could you share how the difficult-access training label was defined and on which cohort the model was trained?

Please confirm or correct, and tell us your preferred channel for safety-relevant defect reports.

Authorised for `[HOSPITAL]`: `[name, role, date]`

---
> Return to the [reading index](../../README.md#how-to-read-this-package).

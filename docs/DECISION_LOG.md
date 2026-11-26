# AIVX Decision Log

**Document ID:** AIVX-ADR-INDEX-001 · **Version:** 1.0 · **Date:** 2026-11-26

Status terms: APPROVED = explicit user decision; PROPOSAL = recommended but not accepted; OPEN = must decide; DEFERRED = later gate.

| ADR | Topic | Decision / position | Status | Evidence / next step |
|---|---|---|---|---|
| ADR-001 | Product ownership | Private app for owner and a few invited friends; no public business/marketing scope | APPROVED | User project instructions |
| ADR-002 | Platform | Genuine native Android application; Kotlin + Jetpack Compose preferred; no silent web/React/WebView substitute | APPROVED | User decision; verify AI Studio Build mode in account |
| ADR-003 | Processing model | All user workflows online/cloud; Android is a client, media/AI/rendering server-side | APPROVED | User explicitly selected online-only; vendor is OPEN |
| ADR-004 | Canonical project | One versioned editable project and command API is required | PROPOSAL | Must select schema/engine after FilmCraft feasibility spike |
| ADR-005 | NLE engine | `storytold/filmcraft` is primary candidate | PROPOSAL | Build/test cloud spike; not yet integrated |
| ADR-006 | Visual feedback | Point/circle/lasso/time-range annotations with saved independent comments and one batch Run | APPROVED REQUIREMENT | FEAT-15 detailed spec |
| ADR-007 | BYOK | Support configured providers/protocol adapters; no promise that arbitrary unknown APIs auto-work | APPROVED REQUIREMENT | Provider capability and adapter design |
| ADR-008 | Provider secrets | Store server-side encrypted; never in APK | REQUIRED SECURITY DESIGN | Must test before production |
| ADR-009 | Heavy AI | Optional remote workers, invoked by capability and user choice | PROPOSAL | Model/GPU selection and budget OPEN |
| ADR-010 | Billing | No assumption that user can pay; no paid cloud/GPU resources until explicit approval | APPROVED CONSTRAINT | Verify billing/card/access and price before creating resources |
| ADR-011 | Repository use | All unique catalogue entries receive a classification/allocation; not all are installed or bundled | APPROVED INTERPRETATION | 264 unique GitHub rows + source occurrence ledger |
| ADR-012 | External editor interoperability | Must be proven by import/round-trip tests per target; no universal compatibility claim | REQUIRED ACCEPTANCE RULE | CapCut/Alight Motion/Node Video/Premiere/Resolve matrix |
| ADR-013 | Google AI Studio first task | Inspect workspace/docs/native Build availability before implementing; no paid resources or full editor generation | PROPOSAL | Use master prompt file |
| ADR-014 | User media retention | Retention and provider-side copy policy not yet selected | OPEN | Must decide before upload to external AI provider |
| ADR-015 | Cloud vendor/region | Google Cloud plausible, not selected | OPEN | Compare cost, region, storage, GPU, free tier and phone usability |
| ADR-016 | Friend roles | Owner/editor/commenter/viewer role proposal | PROPOSAL | User approval needed before invite implementation |
| ADR-017 | 3D and VFX integration | Separate specialist workers with editable project references | PROPOSAL | Define GLB/OBJ/FBX import and render contract |
| ADR-018 | Offline support | Offline AI/edit mode excluded by online-only decision; cached read-only view may be considered | APPROVED DIRECTION | Detailed cache behavior OPEN |

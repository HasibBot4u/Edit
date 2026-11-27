# PROJECT_STATUS

**Project ID:** AIVX  
**Date:** 2026-11-27 (Asia/Dhaka, UTC+6)  
**Current phase:** B — Requirements Analysis and Documentation Integrity (`IN PROGRESS / NOT EXITED`: `AIVX-A0-INSPECT-001` completed; `AIVX-B0-ANALYSIS-RECONCILE-001` archived with errata; `AIVX-B1-DOC-CORRECTIONS-001` applied; Tier 1–3 user decisions and under-specified feature FRs/tests remain `OPEN`)  
**Overall status:** Authoritative specifications, ID ranges, canonical entity mappings, cross-document test register (`docs/TEST_REGISTER.md`), traceability matrix (`docs/TRACEABILITY.md`), decision register (`docs/DECISION_LOG.md`), and repository unique audit ledger (`docs/REPOSITORY_UNIQUE_AUDIT.csv`) are reconciled under `docs/`; Phase B is **NOT EXITED** pending explicit user approval of open decisions; AIVX app feature implementation is `NOT STARTED` (`0` app source/Gradle/manifest/resource/metadata changes).

---

## 1. Approved User Requirements

- [`APPROVED`] Native Android application; Kotlin + Jetpack Compose preferred (`ADR-002`).
- [`APPROVED`] Online-only processing and editing workflow (`ADR-003`).
- [`APPROVED`] Private use by owner and a few invited friends; no public business/monetization scope (`ADR-001`).
- [`APPROVED`] User-configured AI providers and endpoints (BYOK) subject to adapter/capability validation, with secrets stored server-side only (`ADR-007`, `ADR-008`).
- [`APPROVED`] Prompt-based AI generation/editing and manual professional editing (15 approved feature scopes `FEAT-01..15`).
- [`APPROVED`] Visual point/circle/lasso/range selection, independent comments, and one Run action to batch approved changes (`FEAT-15`, `ADR-006`).
- [`APPROVED CONSTRAINT`] No paid cloud/storage/GPU/API resources created without explicit user approval, free-tier/billing verification, and cost disclosure (`ADR-010`).

---

## 2. Completed Documentation & Inspection Work

- [`PASS`] Read `docs/ORIGINAL_REPOSITORY_CATALOGUE.txt` verbatim (412 numbered occurrences): reconciled 411 GitHub URLs, 1 GitLab URL (`#025` Pitivi), 410 well-formed GitHub owner/repo paths, 1 malformed GitHub URL (`#315` `https://github.com/cavalry`), 264 unique valid GitHub identities, 108 repeated identities, and 146 extra duplicate occurrences.
- [`PASS`] Preserved original 412 occurrences, order, duplicates, and URLs verbatim in `docs/REPOSITORY_OCCURRENCES_412.csv`.
- [`PASS`] Reconciled 264-row `docs/REPOSITORY_UNIQUE_AUDIT.csv` (keyed by `first_catalogue_number`): flagged 7 suspect copy-paste/contradictory entries (`#014`, `#043`, `#047`, `#140`, `#290`, `#362`, `#367`) as `BLOCKED / NEEDS SOURCE RECHECK` (`Not directly verified`), aligned `#137 pitivi/pitivi` (`Not directly verified`), reconciled legacy 2-digit and semantically mismatched module IDs against `docs/TRACEABILITY.md`, and separated non-catalogue external references (`openreelio/openreelio`, `filmcraft-desktop/filmcraft`) in `docs/REPOSITORY_AUDIT.md` as `NOT VERIFIED`.
- [`PASS`] Executed `AIVX-A0-INSPECT-001` in Google AI Studio Build mode (`FACT`): verified native Android Kotlin + Jetpack Compose template workspace (`AGP 9.1.1`, `Gradle 9.3.1`, `Kotlin 2.4.21`, `KSP 2.3.5`, `Compose BOM 2024.09.00`, `compileSdk = 36` `minorApiLevel = 1`, `targetSdk = 36`, `minSdk = 24`, Java `11`, `namespace = "com.example"`, `applicationId = "com.example"`). Baseline A0 checks: standalone `compile_applet` = `PASS`; `gradle :app:testDebugUnitTest` = `1 PASS / 1 FAIL` (`ExampleUnitTest.addition_isCorrect` = `PASS`; `ExampleRobolectricTest` SDK 36 = `FAIL` due to `MavenArtifactFetcher` `HttpURLConnection` `IOException`); `lint_applet` = `NOT TESTED`; `androidTest`/emulator/`adb` = `BLOCKED`. Full verbatim `docs/reports/AIVX-A0-INSPECT-001.md` is `NOT AVAILABLE` (not reconstructed).
- [`PASS`] Executed `AIVX-B0-ANALYSIS-RECONCILE-001` and archived verbatim at `docs/reports/AIVX-B0-ANALYSIS-RECONCILE-001.md` (`AIVX-B0-REPORT-ARCHIVE-001`).
- [`PASS`] Executed `AIVX-B1-DOC-CORRECTIONS-001` (documentation-only): corrected all spec header ID ceilings (`41` defined FRs, `NFR-001..015`, `DATA-001..024`, `API-001..045`, `SEC-001..030`, `RISK-001..032`, `ADR-001..018`, `TEST-001..088`, `TEST-ARCH-001..007`), mapped `docs/CANONICAL_PROJECT_MODEL.md` entities to `DATA-001..024` with `OPEN` companion relationships, created `docs/TEST_REGISTER.md`, fixed `docs/TRACEABILITY.md`, created `docs/reports/AIVX-B0-REPORT-ERRATA-001.md`, expanded `docs/DECISION_LOG.md` with Tier 1–4 Open User Decision Register, reconciled `docs/README.md` / `docs/PROJECT_MANIFEST.md` / `docs/CHANGELOG.md`, and archived `docs/reports/AIVX-B1-DOC-CORRECTIONS-001.md`.

---

## 3. Important Audit & Verification Limitations — Do Not Overclaim

- [`NOT TESTED`] All source files in all 264 unique repositories were not read line-by-line; no repository was cloned, built, or runtime-tested (`NO — not executed`; `NOT INTEGRATED`).
- [`NOT VERIFIED`] Per-repository license review is `OUTSTANDING / NOT VERIFIED`; the repeated CSV `license_policy` text is a policy reminder, not a license audit.
- [`NOT VERIFIED`] External non-catalogue references (`openreelio/openreelio`, `filmcraft-desktop/filmcraft`) are not counted in 412/264 and have not been source-audited.
- [`FACT`] Only the initial untouched Android template exists in this workspace; zero AIVX app feature code, release APK/AAB, cloud API, storage bucket, Firebase/Cloud Run project, GPU worker, provider key, or paid service has been created.
- [`NOT TESTED`] Zero acceptance tests in `docs/TEST_REGISTER.md` (`TEST-001..088`, `TEST-ARCH-001..007`) have been executed; no target-app export round-trip has been tested.
- [`NOT TESTED`] No application build or unit/UI test was executed for documentation-only tasks `AIVX-B0-REPORT-ARCHIVE-001` or `AIVX-B1-DOC-CORRECTIONS-001`.

---

## 4. Current Technical Recommendations (`PROPOSAL`)

- [`PROPOSAL`] Native Android client in Kotlin + Compose; separate authenticated cloud control plane and media/AI/render workers.
- [`PROPOSAL`] `#004 storytold/filmcraft` as primary headless NLE candidate; requires bounded Linux cloud feasibility spike before adoption (`ADR-005`).
- [`PROPOSAL`] `#037 FFmpeg/FFmpeg` as media probe/decode/encode foundation, not canonical project store.
- [`PROPOSAL`] Canonical versioned project model + typed, validated, undoable command/batch API.
- [`PROPOSAL`] `#003 openfilm/openfilm` point/circle/time-range UX pattern for `FEAT-15`, retaining AIVX's native project schema.
- [`PROPOSAL`] AI Agent workflow: inspect → plan → validate → dry-run → user approval → atomic apply → visual QC → per-comment report.
- [`PROPOSAL`] Optional isolated specialist workers invoked by capability and explicit user approval.
- [`FACT`] Google AI Studio Android Build builds the native Android client only, not a private backend/worker server.

---

## 5. Open Decisions & Phase B Blockers (`OPEN`)

All user decisions remain explicitly `OPEN` in `docs/DECISION_LOG.md` (none selected on the user's behalf):

- [`OPEN` — Tier 1, blocks Phase C UX] `DEC-UX-01` (P0 vs P1/P2 staging), `DEC-UX-02` (`minSdk` / device matrix / portrait+landscape), `DEC-UX-03` (`ADR-016` friend roles & BYOK isolation), `DEC-UX-04` (`ADR-006` FEAT-15 confidence thresholds), `DEC-UX-05` (`ADR-018` offline/weak-network UX).
- [`OPEN` — Tier 2, blocks Phase D Architecture] `ADR-004`/`ADR-005` (canonical schema & FilmCraft spike vs custom FFmpeg engine), `DEC-ARCH-01` (preview streaming transport), `DEC-ARCH-02` (`ADR-007` initial BYOK adapters), `DEC-ARCH-03` (authentication method).
- [`OPEN` — Tier 3, blocks Cloud/Backend] `ADR-010` (billing/card & cost ceilings), `ADR-015` (cloud vendor, region, DB, storage, queue), `ADR-009` (GPU worker policy), `ADR-014` (media retention & external-provider consent), `ADR-008` (BYOK secret vault).
- [`OPEN` — Account/Tooling] Account-level UI confirmation of streaming emulator preview, APK/AAB export, and physical-device install controls; resolution of container Robolectric SDK 36 HTTP fetch failure.
- [`OPEN` — Requirements] Under-specified feature FRs and acceptance tests for `PLATFORM-CORE (TEST-001..019)`, `FEAT-04 (TEST-039)`, `FEAT-05 (TEST-040)`, `FEAT-06`, `FEAT-07` (mixing/DSP), `FEAT-08` (shaping/animation), `FEAT-09`, `FEAT-10`, and `FEAT-11`.
- [`DEFERRED` — Tier 4] `ADR-012` (third-party editor export priority beyond MP4/OTIO), `ADR-017` (3D/Natron workers), `DEC-DEF-01` (tablet multi-pane), `DEC-DEF-02` (ComfyUI/Diffusion/TTS workers).

---

## 6. Verification Matrix

| Area | Status | Evidence / Next Gate |
|---|---|---|
| Catalogue reconciliation (412 / 264) | `PASS` | `docs/REPOSITORY_OCCURRENCES_412.csv` (412 rows verbatim) & `docs/REPOSITORY_UNIQUE_AUDIT.csv` (264 unique rows reconciled) |
| README / selected docs audit | `PARTIAL` | 7 suspect entries + `#137` marked `BLOCKED / NEEDS SOURCE RECHECK` (`Not directly verified`); license audit `OUTSTANDING / NOT VERIFIED` |
| Full repository source & build audit | `NOT TESTED` | Requires pinned-commit clone, source/security/license review, and isolated build per candidate |
| A0 workspace & toolchain check (`AIVX-A0-INSPECT-001`) | `PASS` *(Robolectric `FAIL`; emulator `BLOCKED`)* | Native Kotlin/Compose template verified; `compile_applet` = `PASS`; `ExampleUnitTest` = `PASS`; `ExampleRobolectricTest` (SDK 36) = `FAIL`; `lint_applet` = `NOT TESTED`; `androidTest`/`adb` = `BLOCKED`; full verbatim report `NOT AVAILABLE` |
| B0 reconciliation audit & archive (`AIVX-B0-ANALYSIS-RECONCILE-001`) | `PASS (archived + errata)` | Archived verbatim at `docs/reports/AIVX-B0-ANALYSIS-RECONCILE-001.md`; errata at `docs/reports/AIVX-B0-REPORT-ERRATA-001.md` |
| B1 documentation reconciliation (`AIVX-B1-DOC-CORRECTIONS-001`) | `PASS (docs-only; app build NOT TESTED)` | Reconciled headers, canonical model, `docs/TEST_REGISTER.md`, `docs/TRACEABILITY.md`, `docs/DECISION_LOG.md`, CSV & manifest; archived at `docs/reports/AIVX-B1-DOC-CORRECTIONS-001.md` |
| Phase B exit gate | `OPEN / NOT EXITED` | Blocked on explicit user approval of Tier 1–3 decisions (`docs/DECISION_LOG.md`) and `OPEN` feature FRs/tests |
| FilmCraft build/test spike | `NOT TESTED` | Pin commit; run isolated Linux cloud build/render spike |
| Android AIVX implementation | `NOT STARTED` | Waiting for Phase B exit and Phase C approval |
| Cloud backend & provider gateway | `NOT STARTED` | Requires architecture, auth, and billing/cost approval (`ADR-010`, `ADR-015`) |
| `FEAT-15` visual feedback | `SPECIFIED / NOT TESTED` | `TEST-041..052` defined (`NOT TESTED`); thresholds `OPEN` (`DEC-UX-04`) |
| External project export | `NOT TESTED` | `TEST-070..080` defined (`NOT TESTED`); target-app import round-trips required |
| Security QA | `DESIGNED / NOT TESTED` | `SEC-001..030` specified; zero security tests executed |

---

## 7. Next Allowed Action

Review `docs/reports/AIVX-B1-DOC-CORRECTIONS-001.md` and submit explicit user decisions on **Tier 1 UX Decisions (`DEC-UX-01..05`)** (and optionally Tier 2/3 decisions in `docs/DECISION_LOG.md`) via a bounded **Phase B2 Decision Sign-Off** task (`AIVX-B2-DECISION-SIGNOFF-001`). Do not begin Phase C UI coding, Android source edits, or cloud/billing provisioning until approved.

---

## 8. Current Official Platform Facts Checked (2026-11-26)

- [`FACT`] Google AI Studio Build mode documentation describes native Android projects using Kotlin + Jetpack Compose, a browser-based Android emulator, physical-device installation, and GitHub import. Verify actual account UI controls before relying on them: https://ai.google.dev/gemini-api/docs/aistudio-build-mode
- [`FACT`] Firebase Cloud Storage requires Blaze billing; no-cost allowances may apply under Blaze, while Spark projects cannot access Cloud Storage buckets: https://firebase.google.com/docs/storage/faqs-storage-changes-announced-sept-2024
- [`FACT`] Cloud Run GPU docs describe NVIDIA L4 (min 4 CPU / 16 GiB) and RTX PRO 6000 (20 CPU / 80 GiB), requiring billing/quota and instance-based billing with scale-to-zero: https://docs.cloud.google.com/run/docs/configuring/services/gpu
- [`OPEN`] No Firebase/Cloud Run project or billing account has been created; no user payment card or budget is assumed.

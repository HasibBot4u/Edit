# PROJECT_STATUS

**Project ID:** AIVX  
**Date:** 2026-11-25 (baseline spec dated 2026-11-26)  
**Current phase:** B — Requirements Analysis and Documentation Integrity (`AIVX-A0-INSPECT-001` completed; `AIVX-B0-ANALYSIS-RECONCILE-001` archived; doc corrections pending review)  
**Overall status:** 21 verbatim baseline docs stored under `docs/`; `AIVX-A0-INSPECT-001` readiness check completed; `AIVX-B0-ANALYSIS-RECONCILE-001` report archived at `docs/reports/AIVX-B0-ANALYSIS-RECONCILE-001.md`; proposed documentation corrections remain `PROPOSAL` (pending user review); AIVX app feature implementation `NOT STARTED`.

## 1. Approved user requirements

- [APPROVED] Native Android application; Kotlin + Jetpack Compose preferred.
- [APPROVED] Online-only processing and editing workflow.
- [APPROVED] Private use by owner and a few invited friends; no public business/monetization scope.
- [APPROVED] User-configured AI providers and endpoints (BYOK) subject to adapter/capability validation.
- [APPROVED] Prompt-based AI generation/editing and manual professional editing.
- [APPROVED] Visual point/circle/lasso/range selection, independent comments and one Run action to batch approved changes (FEAT-15).
- [APPROVED] All assistant recommendations accepted as features to consider, but cloud cost, engine and operational decisions still need evidence/approval.

## 2. Completed documentation/inventory work

- [PASS] Read uploaded `docs/ORIGINAL_REPOSITORY_CATALOGUE.txt` from first to last numbered row (412 links).
- [PASS] Reconciled 411 GitHub-hosted URLs, 410 well-formed owner/repository paths, 264 unique GitHub repositories, 108 repeated identities and 146 extra duplicate occurrences.
- [PASS] Identified GitLab Pitivi (#025) and malformed owner-only GitHub URL `https://github.com/cavalry` (#315).
- [PASS] Preserved original 412 occurrences and duplicates in `docs/REPOSITORY_OCCURRENCES_412.csv`.
- [PASS] Created 264-row `docs/REPOSITORY_UNIQUE_AUDIT.csv`; corrected 53 vague specialty allocations with evidence-based categories and explicit block reasons.
- [PASS] Reviewed accessible README/primary docs and selected technical docs for priority repositories; selected FilmCraft architecture/testing/project files, OpenFilm spec, OpenReel agent spec/limits, OpenReelio agent/API/model docs, MCP Video tools, Clypra NLE skill, Shotcut architecture, Natron and other worker references.
- [PASS] Prepared PRD/SRS, architecture, canonical project model, FEAT-15, provider gateway, agent edit protocol, export/interchange, security, repository audit, risks, decisions and traceability, and stored all 21 verbatim baseline documents under `docs/`.
- [PASS] Prepared separate Google AI Studio custom instructions (`docs/GOOGLE_AI_STUDIO_CUSTOM_INSTRUCTIONS.txt`) and a bounded master prompt in `.txt` formats.
- [PASS] Prepared consolidated Markdown and HTML reference strategy so AI Studio does not need ZIP upload.
- [PASS] Executed `AIVX-A0-INSPECT-001` in Google AI Studio Build mode (`FACT`): verified native Android Kotlin + Jetpack Compose template workspace (`AGP 9.1.1`, `Gradle 9.3.1`, `Kotlin 2.4.21`, `KSP 2.3.5`, `Compose BOM 2024.09.00`, `compileSdk = 36` `minorApiLevel = 1`, `targetSdk = 36`, `minSdk = 24`, Java `11`, `namespace = "com.example"`, `applicationId = "com.example"`). Baseline checks recorded during A0: `compile_applet` (standalone) = `PASS`; `gradle :app:testDebugUnitTest` = `1 PASS / 1 FAIL` (`ExampleUnitTest.addition_isCorrect` = `PASS`; `ExampleRobolectricTest` on SDK 36 = `FAIL` due to `MavenArtifactFetcher` `HttpURLConnection` `IOException`); `lint_applet` = `NOT TESTED`; `androidTest`/emulator/`adb` = `BLOCKED` (no `adb`/emulator in agent container). Zero app source files modified.
- [PASS] Executed `AIVX-B0-ANALYSIS-RECONCILE-001` and archived the complete verbatim reconciliation report at `docs/reports/AIVX-B0-ANALYSIS-RECONCILE-001.md` (`AIVX-B0-REPORT-ARCHIVE-001`).
- [OPEN] Proposed documentation/ID/repository-audit corrections in Section E of `docs/reports/AIVX-B0-ANALYSIS-RECONCILE-001.md` remain `PROPOSAL` and pending user review/approval; no requirement-ID edits or repository classification changes have been applied yet.

## 3. Important audit limitation — do not overclaim

- [NOT TESTED] All source files in all 264 unique repositories were not read line-by-line.
- [NOT TESTED] No complete clone/build/test of all repositories was performed.
- [NOT TESTED] No repository was built or run in this environment; all integrations remain `NOT INTEGRATED`.
- [NOT TESTED] Some original URLs were inaccessible, moved, renamed, malformed or returned 404; see `docs/REPOSITORY_UNIQUE_AUDIT.csv` and `docs/REPOSITORY_AUDIT.md`.
- [FACT] Only the initial untouched Android template exists in this workspace; no AIVX app feature code, release APK/AAB, cloud API, storage bucket, Firebase/Cloud Run project, GPU worker, provider key or paid service was created.
- [NOT TESTED] No target-app editable project round-trip was tested (CapCut, Alight Motion, Node Video, Premiere Pro, Resolve).
- [NOT TESTED] No build or test was executed for documentation-only archiving task `AIVX-B0-REPORT-ARCHIVE-001`.

The defensible outcome is: full catalogue inventory and per-repo allocation, broad README/selected technical-document review, detailed design docs stored under `docs/`, completed A0 workspace readiness inspection, and archived B0 reconciliation audit report; not a full repository source-code audit or implemented app.

## 4. Current technical recommendations

- [PROPOSAL] Android client in Kotlin + Compose; cloud control plane and media/AI/render workers.
- [PROPOSAL] FilmCraft (`storytold/filmcraft`) as primary headless NLE candidate; test on cloud Linux before adoption.
- [PROPOSAL] FFmpeg as media probe/decode/encode foundation, not canonical project store.
- [PROPOSAL] Canonical versioned project + typed command/undo system.
- [PROPOSAL] OpenFilm point/circle/time-range UX pattern for FEAT-15, but retain AIVX native project schema.
- [PROPOSAL] AI Agent workflow: inspect → plan → validate → dry-run → approval → atomic apply → visual QC → report.
- [PROPOSAL] Remote optional specialist workers for ASR, OCR, VLM, tracking, segmentation, inpainting, upscaling, interpolation, stabilization, 3D, VFX, audio and video generation.
- [FACT] Google AI Studio Build is an Android client build surface, not the assumed private server runtime. Native Kotlin/Compose workspace and `compile_applet` build were verified in `AIVX-A0-INSPECT-001`; UI export/device-install options remain user-side to verify.
- [FACT] Firebase Cloud Storage currently requires Blaze; GPU worker usage may incur significant charges. No paid resources are approved.

## 5. Open decisions/blockers

- [OPEN] User review and approval of B0 documentation correction proposals in `docs/reports/AIVX-B0-ANALYSIS-RECONCILE-001.md` (Section E) and Tier 1 UX decisions (`DEC-UX-01..05`).
- [OPEN] Account-level UI confirmation of streaming emulator preview, APK/AAB export and physical-device install controls (workspace native Kotlin/Compose build confirmed in `AIVX-A0-INSPECT-001`).
- [OPEN] Cloud vendor/region, database, object storage, queue, worker runtime (`ADR-015`).
- [OPEN] Billing/card access and monthly/per-job cost ceilings (`ADR-010`).
- [OPEN] Authentication/invitation/friend-role policy (`ADR-016` / `DEC-ARCH-03`).
- [OPEN] Media retention and third-party provider upload/retention policy (`ADR-014`).
- [OPEN] FilmCraft as final engine; project model alignment (`ADR-004`, `ADR-005`).
- [OPEN] Provider protocol adapters, model routing and default/fallback policy (`ADR-007` / `DEC-ARCH-02`).
- [OPEN] Preview streaming approach and device test matrix (`DEC-ARCH-01`, `DEC-UX-02`).
- [OPEN] First external editor format to support (`ADR-012` — `DEFERRED`).
- [OPEN] Which advanced features are P0 vs later releases (`DEC-UX-01`).

## 6. Verification matrix

| Area | Status | Evidence / next gate |
|---|---|---|
| Catalogue reconciliation | PASS | 412 and 264 CSV row checks (`docs/REPOSITORY_OCCURRENCES_412.csv`, `docs/REPOSITORY_UNIQUE_AUDIT.csv`) |
| README/selected docs audit | PARTIAL | See per-repo evidence status; suspect CSV entries flagged in `docs/reports/AIVX-B0-ANALYSIS-RECONCILE-001.md` |
| Full source audit | NOT TESTED | Needs clone/file-by-file inspection for selected repos |
| A0 workspace & toolchain check (`AIVX-A0-INSPECT-001`) | PASS (with Robolectric FAIL / emulator BLOCKED) | Native Kotlin/Compose template verified; `compile_applet` = `PASS`; `ExampleUnitTest` = `PASS`; `ExampleRobolectricTest` (SDK 36) = `FAIL` (container HTTP fetch blocked); `lint_applet` = `NOT TESTED`; `androidTest`/`adb` = `BLOCKED` |
| B0 reconciliation audit & archive (`AIVX-B0-ANALYSIS-RECONCILE-001`) | PASS (archived) | Complete report archived at `docs/reports/AIVX-B0-ANALYSIS-RECONCILE-001.md`; no build/test run for doc-only change (`NOT TESTED`) |
| B1 documentation corrections | OPEN (pending review) | Proposals listed in Section E of `docs/reports/AIVX-B0-ANALYSIS-RECONCILE-001.md`; not yet applied |
| FilmCraft build/test | NOT TESTED | Pin commit; run CI/headless render spike |
| Android AIVX implementation | NOT STARTED | Waiting for Phase B completion and Phase C approval |
| Cloud backend | NOT STARTED | Requires architecture and billing approval |
| Provider gateway | NOT STARTED | Requires backend, vault, adapter contracts |
| FEAT-15 | SPECIFIED | Requires annotation prototype and acceptance tests |
| External project export | NOT TESTED | Per-app import/round-trip tests |
| Security | DESIGNED, NOT TESTED | Threat model and test matrix before release |

## 7. Next allowed action

Review the archived B0 reconciliation report at `docs/reports/AIVX-B0-ANALYSIS-RECONCILE-001.md` and explicitly approve (or adjust) the bounded Phase B1 documentation correction task (`AIVX-B1-DOC-CORRECTIONS-001`) along with Tier 1 UX decisions (`DEC-UX-01..05`). Do not begin Phase C, application feature implementation, or cloud/billing provisioning until approved.


## 8. Current official platform facts checked (2026-11-26)

- [FACT] Google AI Studio Build mode documentation currently describes native Android projects using Kotlin + Jetpack Compose, a browser-based Android emulator, physical-device installation and GitHub import. Verify the actual UI/account before relying on these controls: https://ai.google.dev/gemini-api/docs/aistudio-build-mode
- [FACT] Firebase Cloud Storage requires Blaze billing; Google notes that no-cost usage may still apply under Blaze, while Spark projects cannot access Cloud Storage buckets: https://firebase.google.com/docs/storage/faqs-storage-changes-announced-sept-2024
- [FACT] Current Cloud Run GPU docs describe L4 (minimum 4 CPU/16 GiB) and full RTX PRO 6000 (20 CPU/80 GiB), require billing/quota and instance-based billing, and allow scale-to-zero: https://docs.cloud.google.com/run/docs/configuring/services/gpu
- [OPEN] No Firebase/Cloud Run project or billing has been created. No user billing/card availability is assumed.

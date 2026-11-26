# PROJECT_STATUS

**Project ID:** AIVX  
**Date:** 2026-11-26  
**Current phase:** A — Foundation / Analysis / Pre-build readiness  
**Overall status:** Documentation package ready; repository inventory complete; deep source audit partial; app implementation NOT STARTED.

## 1. Approved user requirements

- [APPROVED] Native Android application; Kotlin + Jetpack Compose preferred.
- [APPROVED] Online-only processing and editing workflow.
- [APPROVED] Private use by owner and a few invited friends; no public business/monetization scope.
- [APPROVED] User-configured AI providers and endpoints (BYOK) subject to adapter/capability validation.
- [APPROVED] Prompt-based AI generation/editing and manual professional editing.
- [APPROVED] Visual point/circle/lasso/range selection, independent comments and one Run action to batch approved changes (FEAT-15).
- [APPROVED] All assistant recommendations accepted as features to consider, but cloud cost, engine and operational decisions still need evidence/approval.

## 2. Completed documentation/inventory work

- [PASS] Read uploaded `ORIGINAL_REPOSITORY_CATALOGUE.txt` from first to last numbered row (412 links).
- [PASS] Reconciled 411 GitHub-hosted URLs, 410 well-formed owner/repository paths, 264 unique GitHub repositories, 108 repeated identities and 146 extra duplicate occurrences.
- [PASS] Identified GitLab Pitivi (#025) and malformed owner-only GitHub URL `https://github.com/cavalry` (#315).
- [PASS] Preserved original 412 occurrences and duplicates in `REPOSITORY_OCCURRENCES_412.csv`.
- [PASS] Created 264-row `REPOSITORY_UNIQUE_AUDIT.csv`; corrected 53 vague specialty allocations with evidence-based categories and explicit block reasons.
- [PASS] Reviewed accessible README/primary docs and selected technical docs for priority repositories; selected FilmCraft architecture/testing/project files, OpenFilm spec, OpenReel agent spec/limits, OpenReelio agent/API/model docs, MCP Video tools, Clypra NLE skill, Shotcut architecture, Natron and other worker references.
- [PASS] Prepared PRD/SRS, architecture, canonical project model, FEAT-15, provider gateway, agent edit protocol, export/interchange, security, repository audit, risks, decisions and traceability.
- [PASS] Prepared separate Google AI Studio custom instructions and a bounded master prompt in `.txt` formats.
- [PASS] Prepared consolidated Markdown and HTML reference strategy so AI Studio does not need ZIP upload.

## 3. Important audit limitation — do not overclaim

- [NOT TESTED] All source files in all 264 unique repositories were not read line-by-line.
- [NOT TESTED] No complete clone/build/test of all repositories was performed.
- [NOT TESTED] No repository was built or run in this environment; all integrations remain `NOT INTEGRATED`.
- [NOT TESTED] Some original URLs were inaccessible, moved, renamed, malformed or returned 404; see unique CSV and repository report.
- [NOT TESTED] No Android project, APK/AAB, cloud API, storage bucket, Firebase/Cloud Run project, GPU worker, provider key or paid service was created.
- [NOT TESTED] No target-app editable project round-trip was tested (CapCut, Alight Motion, Node Video, Premiere Pro, Resolve).

The defensible outcome is: full catalogue inventory and per-repo allocation, broad README/selected technical-document review, and detailed design docs; not a full repository source-code audit.

## 4. Current technical recommendations

- [PROPOSAL] Android client in Kotlin + Compose; cloud control plane and media/AI/render workers.
- [PROPOSAL] FilmCraft (`storytold/filmcraft`) as primary headless NLE candidate; test on cloud Linux before adoption.
- [PROPOSAL] FFmpeg as media probe/decode/encode foundation, not canonical project store.
- [PROPOSAL] Canonical versioned project + typed command/undo system.
- [PROPOSAL] OpenFilm point/circle/time-range UX pattern for FEAT-15, but retain AIVX native project schema.
- [PROPOSAL] AI Agent workflow: inspect → plan → validate → dry-run → approval → atomic apply → visual QC → report.
- [PROPOSAL] Remote optional specialist workers for ASR, OCR, VLM, tracking, segmentation, inpainting, upscaling, interpolation, stabilization, 3D, VFX, audio and video generation.
- [FACT] Google AI Studio Build is an Android client build surface, not the assumed private server runtime. Verify account-level native features before building.
- [FACT] Firebase Cloud Storage currently requires Blaze; GPU worker usage may incur significant charges. No paid resources are approved.

## 5. Open decisions/blockers

- [OPEN] Google AI Studio account-level native Android Build availability/export/build path.
- [OPEN] Cloud vendor/region, database, object storage, queue, worker runtime.
- [OPEN] Billing/card access and monthly/per-job cost ceilings.
- [OPEN] Authentication/invitation/friend-role policy.
- [OPEN] Media retention and third-party provider upload/retention policy.
- [OPEN] FilmCraft as final engine; project model alignment.
- [OPEN] Provider protocol adapters, model routing and default/fallback policy.
- [OPEN] Preview streaming approach and device test matrix.
- [OPEN] First external editor format to support.
- [OPEN] Which advanced features are P0 vs later releases.

## 6. Verification matrix

| Area | Status | Evidence / next gate |
|---|---|---|
| Catalogue reconciliation | PASS | 412 and 264 CSV row checks |
| README/selected docs audit | PARTIAL | See per-repo evidence status |
| Full source audit | NOT TESTED | Needs clone/file-by-file inspection for selected repos |
| FilmCraft build/test | NOT TESTED | Pin commit; run CI/headless render spike |
| Android project | NOT STARTED | AI Studio A0 capability inspection |
| Cloud backend | NOT STARTED | Requires architecture and billing approval |
| Provider gateway | NOT STARTED | Requires backend, vault, adapter contracts |
| FEAT-15 | SPECIFIED | Requires annotation prototype and acceptance tests |
| External project export | NOT TESTED | Per-app import/round-trip tests |
| Security | DESIGNED, NOT TESTED | Threat model and test matrix before release |

## 7. Next allowed action

Run `GOOGLE_AI_STUDIO_MASTER_BUILD_PROMPT.txt` task `AIVX-A0-INSPECT-001` in Google AI Studio Build mode. It is inspect/verify/report only. Confirm native Android availability in the current account and list workspace/document gaps. Do not implement code or create any paid cloud resource in that first task.

After the report, approve one bounded Phase A implementation task and separately approve cloud vendor/billing before provisioning services.


## 8. Current official platform facts checked (2026-11-26)

- [FACT] Google AI Studio Build mode documentation currently describes native Android projects using Kotlin + Jetpack Compose, a browser-based Android emulator, physical-device installation and GitHub import. Verify the actual UI/account before relying on these controls: https://ai.google.dev/gemini-api/docs/aistudio-build-mode
- [FACT] Firebase Cloud Storage requires Blaze billing; Google notes that no-cost usage may still apply under Blaze, while Spark projects cannot access Cloud Storage buckets: https://firebase.google.com/docs/storage/faqs-storage-changes-announced-sept-2024
- [FACT] Current Cloud Run GPU docs describe L4 (minimum 4 CPU/16 GiB) and full RTX PRO 6000 (20 CPU/80 GiB), require billing/quota and instance-based billing, and allow scale-to-zero: https://docs.cloud.google.com/run/docs/configuring/services/gpu
- [OPEN] No Firebase/Cloud Run project or billing has been created. No user billing/card availability is assumed.

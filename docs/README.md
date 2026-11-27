# AIVX — AI Video Editor: Pre-Build Documentation and Repository Audit

**Document ID:** AIVX-README-001 · **Version:** 1.3 · **Date:** 2026-11-27 (Asia/Dhaka)  
**Product:** private online-only native Android AI video editor  
**Current phase:** B — Requirements Analysis and Documentation Integrity (`IN PROGRESS / NOT EXITED` — A0 completed, B0 archived + errata, B1 & B1.1 traceability/gate repairs completed; Phase C entry blocked on Tier 1 `DEC-UX-01..05`, while Tier 2/3 belong to Phase D and Cloud gates)  
**Implementation status:** `NOT STARTED` (only the untouched Android template exists; zero app feature code or cloud/billing resources created)

---

## 1. Repository Layout vs External Upload Artefacts (`FACT`)

Authoritative project documentation now lives inside this GitHub-synced repository under `docs/`:

1. **Authoritative repository documents (`docs/`):** All 21 baseline specifications, CSV ledgers, `docs/TEST_REGISTER.md`, and archived task reports under `docs/reports/`. Edit and reference files under `docs/`.
2. **Immutable AI Studio upload snapshots (`public/assets/aistudio/`):** Original session upload snapshots (`AI_STUDIO_UPLOAD_MASTER_2a4612b0.html`, `REPOSITORY_OCCURRENCES_412_a17f05e9.csv`, `REPOSITORY_UNIQUE_AUDIT_616fcf9d.csv`). Retained intact as archival upload evidence — do **not** delete or treat as the mutable source of truth.
3. **Historical external upload-bundle artefacts (outside `docs/`):** Files created before GitHub sync (`GOOGLE_AI_STUDIO_MASTER_BUILD_PROMPT.txt`, `REPOSITORY_REGISTER_SUMMARY.md`, `ALL_PROJECT_DOCS.md`, `AI_STUDIO_UPLOAD_MASTER.html`, `UPLOAD_GUIDE.txt`, `PACKAGE_VERIFICATION.json`). Not stored inside `docs/`; see `docs/PROJECT_MANIFEST.md` for status.

### Google AI Studio attachment note (if attaching files manually in a new session)

Google AI Studio's supported attachment formats include `.txt`, `.md`, `.html`, and `.csv`, not `.zip`. When working directly inside this GitHub-synced workspace, read the authoritative files under `docs/` directly rather than re-uploading ZIP backups.

Official Google AI Studio Build docs: https://ai.google.dev/gemini-api/docs/aistudio-build-mode (always verify actual account-level UI controls such as streaming emulator, APK/AAB export, and device install inside the active session).

---

## 2. Original Catalogue Reconciliation (`FACT`)

The user-provided `docs/ORIGINAL_REPOSITORY_CATALOGUE.txt` contains **412** numbered link occurrences. `docs/REPOSITORY_OCCURRENCES_412.csv` preserves all 412 rows in original order verbatim, including duplicates and original URLs. `docs/REPOSITORY_UNIQUE_AUDIT.csv` contains **264** unique, well-formed GitHub owner/repository identities keyed by `first_catalogue_number` (`001..403`).

- 411 GitHub-hosted URLs, one GitLab URL (`#025` Pitivi).
- 410 well-formed GitHub owner/repository paths; one malformed owner-only GitHub URL (`#315` `https://github.com/cavalry`).
- 264 unique GitHub repository identities.
- 108 identities are repeated; 146 additional duplicate occurrences.

---

## 3. Evidence Limitation — Critical (`FACT`)

The original catalogue has been fully inventoried and every unique valid GitHub identity has an allocation/status row in `docs/REPOSITORY_UNIQUE_AUDIT.csv`. A broad set of public README and selected architecture/API/spec/test documents was fetched in the baseline review. **This is not a full source-code audit of every file in all 264 repositories.** Repositories were not cloned, built, installed, benchmarked, or runtime-tested. All integrations remain `NOT INTEGRATED`; all build/runtime columns remain `NO — not executed`; per-repository license review remains `OUTSTANDING / NOT VERIFIED` (the CSV `license_policy` text is a policy reminder, not a license audit).

---

## 4. Product Decisions Summary

- **`APPROVED`:** Private use (owner + a few invited friends), genuine native Android (Kotlin + Jetpack Compose preferred), online-only cloud processing, BYOK provider support (server-side secrets only), prompt editing/generation, FEAT-15 visual region comments + batch Run, manual professional editing, no public marketing/monetization.
- **`PROPOSAL`:** Cloud control plane; server-authoritative canonical project model; `#004 storytold/filmcraft` as primary NLE candidate (requires bounded cloud feasibility spike); FFmpeg media foundation; OpenFilm annotation UX pattern; specialist isolated workers.
- **`OPEN` (User Decision Required — see `docs/DECISION_LOG.md`):** P0 vs P1/P2 priority (`DEC-UX-01`), `minSdk`/orientation (`DEC-UX-02`), friend roles (`DEC-UX-03`), FEAT-15 thresholds (`DEC-UX-04`), offline UX (`DEC-UX-05`), final NLE engine (`ADR-004/005`), preview transport (`DEC-ARCH-01`), initial BYOK adapters (`DEC-ARCH-02`), auth method (`DEC-ARCH-03`), billing/cost ceilings (`ADR-010`), cloud vendor/region (`ADR-015`), GPU policy (`ADR-009`), media retention/consent (`ADR-014`), vault implementation (`ADR-008`), and first external export target (`ADR-012` — `DEFERRED`).

---

## 5. Architecture Summary

Android is a native client for workspace/projects, timeline UI, preview playback, FEAT-15 annotation, comment queue, plan approval, job tracking, and export download. It is **not** a server runtime. Separate authenticated cloud services own canonical project state, object storage, encrypted BYOK secrets, AI orchestration, media processing, final rendering, interchange, and QC. No cloud service or paid resource may be created without explicit user approval and cost disclosure.

---

## 6. Priority Repository Allocations (Catalogue vs Non-Catalogue)

### In-catalogue priority candidates (part of the 412 / 264 ledger)
- `#004 storytold/filmcraft`: primary headless NLE engine candidate; requires isolated build/test/API/render feasibility gate (`NOT TESTED`).
- `#037 FFmpeg/FFmpeg`: probe/decode/encode/media filter foundation (`NOT INTEGRATED`).
- `#003 openfilm/openfilm`: point/circle/time-range annotation UX reference for FEAT-15.
- `#193 JuneYaooo/rea-video`: shot-level reverse-analysis worker candidate.
- `#008 FireRedTeam/FireRed-OpenStoryline`: optional script/storyboard/creative planning worker.
- `#142 inematds/mcp-video`: selected media/QC tool patterns (sandboxed subset only).
- `#141 Augani/openreel-video`: agent dry-run/transaction/undo architecture reference.
- `#046 AcademySoftwareFoundation/OpenTimelineIO`: interchange adapter with feature-loss reports.
- `#139 AIEraDev/Clypra`: timeline/timebase/performance engineering reference.
- `#023 Natron`, `#021 Blender`, `#226 SAM2`, `#304 RAFT`, `#301 ProPainter`, `#071 RIFE`, `#303 Gyroflow`, ASR/TTS/music, and ComfyUI tools: isolated optional cloud workers, never Android APK payloads.

### Non-catalogue external research references (NOT counted in 412 or 264; `NOT VERIFIED`)
- `openreelio/openreelio`: external command/event-sourcing and plugin-permission reference (`NOT VERIFIED`).
- `filmcraft-desktop/filmcraft`: external disambiguation target noted solely to distinguish from `#004 storytold/filmcraft` (`NOT VERIFIED`).

See `docs/REPOSITORY_AUDIT.md` and `docs/REPOSITORY_UNIQUE_AUDIT.csv` for full details and caveats.

---

## 7. Authoritative Document Map (`docs/`)

| File | Purpose | Status |
|---|---|---|
| `docs/README.md` | Product context, repository layout, document index, next step | `ACTIVE` |
| `docs/PROJECT_STATUS.md` | Current phase, A0/B0/B1 evidence, blockers, verification matrix | `ACTIVE` |
| `docs/PROJECT_MANIFEST.md` | Authoritative index of all repo docs, reports, and snapshots | `ACTIVE` |
| `docs/AI_INSTRUCTIONS.md` | Persistent AI Build instructions | `ACTIVE` |
| `docs/GOOGLE_AI_STUDIO_CUSTOM_INSTRUCTIONS.txt` | Copy-ready AI Studio persistent custom instructions | `READY` |
| `docs/PRD_SRS.md` | Product vision, scope, journeys, 41 defined FRs, 15 NFRs | `BASELINE` |
| `docs/ARCHITECTURE.md` | Client/cloud/services architecture & `TEST-ARCH-001..007` | `PROPOSAL` |
| `docs/CANONICAL_PROJECT_MODEL.md` | Canonical project entities (`DATA-001..024`), timebase & commands | `PROPOSAL` |
| `docs/FEAT15_VISUAL_FEEDBACK.md` | Visual annotations, comments, batch Run & `TEST-041..052` | `APPROVED REQUIREMENT / PROPOSAL DESIGN` |
| `docs/PROVIDER_GATEWAY.md` | BYOK capability manifest, SSRF/vault rules & `TEST-060..069` | `PROPOSAL` |
| `docs/AI_AGENT_EDIT_PROTOCOL.md` | Typed tools, plan/approval/apply/QC loop & `TEST-053..059` | `PROPOSAL` |
| `docs/EXPORT_INTERCHANGE.md` | Rendered outputs, interchange loss reports & `TEST-070..080` | `PROPOSAL` |
| `docs/SECURITY_THREAT_MODEL.md` | Threat model, `SEC-001..030` & security QA requirements | `REQUIRED BEFORE RELEASE` |
| `docs/REPOSITORY_AUDIT.md` | Repository specialty allocations, non-catalogue refs & caveats | `PARTIAL SOURCE AUDIT` |
| `docs/REPOSITORY_UNIQUE_AUDIT.csv` | 264 unique GitHub repos keyed by `first_catalogue_number` | `PARTIAL SOURCE AUDIT / 264 rows` |
| `docs/REPOSITORY_OCCURRENCES_412.csv` | Original 412 catalogue occurrences preserved verbatim | `PASS / 412 rows` |
| `docs/ORIGINAL_REPOSITORY_CATALOGUE.txt` | Original user-supplied 412-link source catalogue | `SOURCE (IMMUTABLE)` |
| `docs/RISK_REGISTER.md` | Risk register (`RISK-001..032`) | `OPEN` |
| `docs/DECISION_LOG.md` | `ADR-001..018` + Tier 1–4 Open User Decision Register | `ACTIVE` |
| `docs/TRACEABILITY.md` | Repaired feature/platform & cross-cutting `NFR-001..015` traceability (v1.2) | `BASELINE` |
| `docs/TEST_REGISTER.md` | Cross-document test register with primary/secondary ownership (`TEST-001..088`, `TEST-ARCH-001..007`) | `BASELINE / NOT TESTED` |
| `docs/CHANGELOG.md` | Chronological project documentation & decision history | `ACTIVE` |
| `docs/reports/AIVX-A0-INSPECT-001.md` | Original full A0 readiness report | `NOT AVAILABLE` *(verified summary logged in `docs/PROJECT_STATUS.md`)* |
| `docs/reports/AIVX-B0-ANALYSIS-RECONCILE-001.md` | Archived Phase B0 requirements & audit report (verbatim) | `ARCHIVED REPORT` |
| `docs/reports/AIVX-B0-REPORT-ERRATA-001.md` | Post-archive errata & B1 reconciliation tracker for B0 | `ARCHIVED SUPPLEMENT` |
| `docs/reports/AIVX-B1-DOC-CORRECTIONS-001.md` | Phase B1 documentation reconciliation completion report | `ARCHIVED REPORT` |
| `docs/reports/AIVX-B1.1-TRACEABILITY-REPAIR-001.md` | Phase B1.1 traceability, test-ownership, NFR & phase-gate repair report | `ARCHIVED REPORT` |

---

## 8. Current Phase B Workflow & Phase-Specific Approval Sequence

1. **`AIVX-A0-INSPECT-001` (`COMPLETED`):** Native Kotlin/Compose workspace verified (`compile_applet` = `PASS`; `ExampleUnitTest` = `PASS`; `ExampleRobolectricTest` SDK 36 = `FAIL` due to container network fetch; `androidTest`/`adb` = `BLOCKED`). Full verbatim A0 report file is `NOT AVAILABLE`.
2. **`AIVX-B0-ANALYSIS-RECONCILE-001` (`ARCHIVED` + `ERRATA`):** Archived at `docs/reports/AIVX-B0-ANALYSIS-RECONCILE-001.md` with errata at `docs/reports/AIVX-B0-REPORT-ERRATA-001.md`.
3. **`AIVX-B1-DOC-CORRECTIONS-001` (`COMPLETED` — Docs Only):** Reconciled spec headers, canonical model mappings, `docs/TEST_REGISTER.md`, `docs/TRACEABILITY.md`, `docs/DECISION_LOG.md`, and 264-row unique CSV.
4. **`AIVX-B1.1-TRACEABILITY-REPAIR-001` (`COMPLETED` — Docs Only):** Repaired `FEAT-06`/`FEAT-08` FR/SCR/DATA/API ownership, eliminated numeric-adjacency mapping leaks, separated primary (`FEAT-13`) vs secondary (`FEAT-14`) ownership of `FR-045..046` / `TEST-087..088`, added Cross-Cutting `NFR-001..015` traceability, and clarified phase-specific approval gates.
5. **Phase-specific approval gates (next allowed action):**
   - **Before Phase C (UX/UI Design) begins:** Approve **Tier 1 (`DEC-UX-01..05`)** in `docs/DECISION_LOG.md` and confirm minimum FR readiness for any feature chosen into P0/P1 UX scope (`AIVX-B2-DECISION-SIGNOFF-001`).
   - **Before Phase D (Technical Architecture) is finalized:** Approve **Tier 2 (`ADR-004/005`, `DEC-ARCH-01..03`)** *(not mandatory to start Phase C unless an exact UX dependency is shown)*.
   - **Before Backend / Cloud / Storage / GPU provisioning:** Approve **Tier 3 (`ADR-008/009/010/014/015`)** *(not mandatory to start Phase C)*.
   - **Deferred (`Tier 4`):** `ADR-012`, `ADR-017`, `DEC-DEF-01`, `DEC-DEF-02`.

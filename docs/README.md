# AIVX — AI Video Editor: Pre-Build Documentation and Repository Audit

**Document ID:** AIVX-README-001 · **Version:** 1.1 · **Date:** 26 November 2026  
**Product:** private online-only native Android AI video editor  
**Current phase:** A — Foundation / analysis documentation  
**Implementation status:** NOT STARTED

## Google AI Studio ZIP upload workaround

Google AI Studio's supported input formats listed by the user include `.txt`, `.md`, `.html` and `.csv`, but not `.zip`. Therefore:

- Upload `GOOGLE_AI_STUDIO_CUSTOM_INSTRUCTIONS.txt` as the custom instruction reference or copy its text into the Build project's instruction field if available.
- Upload `GOOGLE_AI_STUDIO_MASTER_BUILD_PROMPT.txt` and paste its contents into the Build prompt.
- Upload `AI_STUDIO_UPLOAD_MASTER.html` as the main consolidated reference file. It contains the documentation set in one searchable file.
- Upload `ALL_PROJECT_DOCS.md` as an alternative combined reference if HTML rendering is inconvenient.
- Attach `REPOSITORY_UNIQUE_AUDIT.csv` and `REPOSITORY_OCCURRENCES_412.csv` separately when the agent needs the full repository table.
- Upload individual `.md` files only when a task needs a focused specification.
- The ZIP package is optional backup only. **Do not upload the ZIP to Google AI Studio.**

The user should confirm which file types and file-size limits are currently accepted in their actual AI Studio session. Do not assume the interface supports unlimited attachments. Current Google documentation describes Kotlin + Jetpack Compose native Android Build, browser-based emulator, physical-device install and GitHub import, but the active account/session must be checked. Official docs: https://ai.google.dev/gemini-api/docs/aistudio-build-mode

## Original catalogue reconciliation

The user-provided `ORIGINAL_REPOSITORY_CATALOGUE.txt` contains 412 numbered link occurrences. The occurrence CSV preserves all 412 rows in original order, including duplicates. The unique register contains 264 unique, well-formed GitHub owner/repository identities.

- 411 GitHub-hosted URLs, one GitLab URL.
- 410 well-formed GitHub owner/repository paths.
- 264 unique GitHub repository identities.
- 108 identities are repeated; 146 additional duplicate occurrences.
- Catalogue #025 is Pitivi on GitLab.
- Catalogue #315 is malformed owner-only `https://github.com/cavalry`.

## Evidence limitation — critical

The original catalogue has been fully inventoried and every unique valid GitHub identity has an allocation/status row. A broad set of public README and selected architecture/API/spec/test documents was fetched. **This is not a full source-code audit of every file in all 264 repositories.** Repositories were not all cloned, built, installed, benchmarked or runtime-tested. The CSV distinguishes README evidence, selected deeper docs, incomplete source review and blocked/moved paths. All integrations are `NOT INTEGRATED`; all build/runtime evidence is `NO — not executed`.

Do not describe the work as “every source file has been deeply audited”. The defensible status is: complete catalogue inventory + unique allocation; partial documentation/source evidence review; source-level and runtime audit outstanding.

## Product decisions

- **APPROVED:** private use, native Android, Kotlin + Compose preferred, online-only processing, BYOK provider support, prompt editing, visual region comments and batch Run, manual professional editing, no public business/monetization.
- **PROPOSAL:** cloud control plane; server-authoritative canonical project model; FilmCraft as NLE candidate; FFmpeg media foundation; OpenFilm annotation UX pattern; specialist model/render workers.
- **OPEN:** cloud vendor/region, budget and payment ability, backend/database/storage/queue, identity/friend roles, project retention, final engine, GPU availability, export priorities, device support and exact external AI providers.

## Architecture summary

Android is a native client for projects, timeline, preview, annotation and job controls. It must not be the private server runtime. Cloud services handle canonical project state, storage, provider secrets, analysis, AI generation, media processing, final rendering, interchange and quality checks. All paid resources require explicit approval.

## Priority repository allocations

- `storytold/filmcraft`: primary headless NLE engine candidate; requires isolated build/test/API/render feasibility gate.
- `FFmpeg/FFmpeg`: probe/decode/encode/media filter foundation.
- `openfilm/openfilm`: point/circle/time-range annotation UX reference for FEAT-15.
- `JuneYaooo/rea-video`: shot-level reverse-analysis worker candidate.
- `FireRedTeam/FireRed-OpenStoryline`: optional script/storyboard/creative planning worker.
- `inematds/mcp-video`: selected media/QC tool patterns.
- `Augani/openreel-video` / `openreelio/openreelio`: agent transaction/event sourcing patterns.
- `AcademySoftwareFoundation/OpenTimelineIO`: interchange adapter, with feature-loss reports.
- `AIEraDev/Clypra`: timeline/timebase/performance engineering reference.
- `Natron`, `Blender`, SAM2, RAFT, ProPainter, RIFE, Gyroflow, ASR/TTS/music and ComfyUI tools: isolated optional workers, not Android APK payload.

See `REPOSITORY_AUDIT.md` and `REPOSITORY_UNIQUE_AUDIT.csv` for detailed allocations and caveats.

## Document map

| File | Purpose | Status |
|---|---|---|
| `PROJECT_STATUS.md` | Current phase, verified evidence, blockers, next step | ACTIVE |
| `PROJECT_MANIFEST.md` | Authoritative document index | ACTIVE |
| `AI_INSTRUCTIONS.md` | Persistent agent instructions | ACTIVE |
| `GOOGLE_AI_STUDIO_CUSTOM_INSTRUCTIONS.txt` | Copy/upload-ready AI Studio instructions | READY |
| `GOOGLE_AI_STUDIO_MASTER_BUILD_PROMPT.txt` | Bounded first Build task: inspect/verify/report only | READY |
| `PRD_SRS.md` | Product and functional/non-functional requirements | BASELINE |
| `ARCHITECTURE.md` | Client/cloud/service architecture | PROPOSAL |
| `CANONICAL_PROJECT_MODEL.md` | Canonical editable project data and command contract | PROPOSAL |
| `FEAT15_VISUAL_FEEDBACK.md` | Circle/point/time comments and batch Run specification | APPROVED REQUIREMENT / PROPOSAL DESIGN |
| `PROVIDER_GATEWAY.md` | BYOK capability and secret model | PROPOSAL |
| `AI_AGENT_EDIT_PROTOCOL.md` | Tool permissions, plan, approval, apply and verify loop | PROPOSAL |
| `EXPORT_INTERCHANGE.md` | Rendered output and editable export compatibility | PROPOSAL |
| `SECURITY_THREAT_MODEL.md` | Threats and controls | REQUIRED BEFORE RELEASE |
| `REPOSITORY_AUDIT.md` | Repository specialty and allocation report | PARTIAL SOURCE AUDIT |
| `REPOSITORY_UNIQUE_AUDIT.csv` | One row per unique GitHub repository | 264 rows |
| `REPOSITORY_OCCURRENCES_412.csv` | Original 412 catalogue occurrences, duplicates intact | 412 rows |
| `REPOSITORY_REGISTER_SUMMARY.md` | Exact counts and next audit method | ACTIVE |
| `RISK_REGISTER.md` | Risk inventory | OPEN |
| `DECISION_LOG.md` | Approved/proposed/open decisions | ACTIVE |
| `TRACEABILITY.md` | Feature/requirement/screen/data/API/security/test mapping | BASELINE |
| `CHANGELOG.md` | Change history | ACTIVE |
| `ALL_PROJECT_DOCS.md` | Combined Markdown reference | READY |
| `AI_STUDIO_UPLOAD_MASTER.html` | Combined searchable HTML reference for AI Studio | READY |

## Upload workflow

1. Open Google AI Studio Build mode in the browser.
2. Verify that the active session visibly offers native Android/Kotlin/Compose Build mode. If not, stop; do not accept a web substitute.
3. Attach the Custom Instructions `.txt`, Master Build Prompt `.txt`, and `AI_STUDIO_UPLOAD_MASTER.html`.
4. Attach the two CSV files if the UI permits. If it enforces a small attachment count, use the HTML master first and add the CSVs in a second message.
5. Paste the Master Build Prompt exactly. It asks for inspection and a gap report, not code edits.
6. Review the capability report and approve the next bounded task before implementation.

## Current next action

Run the `AIVX-A0-INSPECT-001` master prompt in Build mode. Do not create paid cloud resources or generate the complete editor yet. First verify native Build availability, inspect workspace/docs, and list gaps/open decisions.

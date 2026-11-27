# AIVX Decision Log

**Document ID:** AIVX-ADR-INDEX-001 · **Version:** 1.1 · **Date:** 2026-11-27 (Asia/Dhaka)

Status terms: `APPROVED` = explicit user decision; `PROPOSAL` = recommended but not accepted; `OPEN` = user decision required before proceeding to dependent phase; `DEFERRED` = intentionally postponed to a later gate.

> **Decision Governance Rule (`APPROVED`):** Existing `ADR-001..018` identifiers are preserved without renumbering. No open user decision (feature priority, `minSdk`/device matrix, portrait/landscape policy, friend permissions, FEAT-15 thresholds, authentication method, cloud vendor/region, billing/card & cost ceilings, GPU policy, media retention, external provider media consent, or final NLE engine) is chosen on the user's behalf.

---

## 1. Architecture Decision Records (`ADR-001..018`)

| ADR | Topic | Decision / position | Status | Evidence / next step |
|---|---|---|---|---|
| `ADR-001` | Product ownership | Private app for owner and a few invited friends; no public business/marketing scope | `APPROVED` | User project instructions |
| `ADR-002` | Platform | Genuine native Android application; Kotlin + Jetpack Compose preferred; no silent web/React/WebView substitute | `APPROVED` | User decision; native workspace verified in A0 (`FACT`); UI emulator/export/device-install confirmation remains `OPEN` |
| `ADR-003` | Processing model | All user workflows online/cloud; Android is a client, media/AI/rendering server-side | `APPROVED` | User explicitly selected online-only; cloud vendor is `OPEN` (`ADR-015`) |
| `ADR-004` | Canonical project | One versioned editable project and command API is required | `PROPOSAL` / `OPEN` | Must select schema/engine alignment after FilmCraft feasibility spike; user approval required |
| `ADR-005` | NLE engine | `storytold/filmcraft` is primary candidate | `PROPOSAL` / `OPEN` | Build/test cloud spike required; not yet integrated; fallback selection remains `OPEN` |
| `ADR-006` | Visual feedback | Point/circle/lasso/time-range annotations with saved independent comments and one batch Run | `APPROVED REQUIREMENT` | FEAT-15 detailed spec (`docs/FEAT15_VISUAL_FEEDBACK.md`); confidence thresholds `OPEN` (`DEC-UX-04`) |
| `ADR-007` | BYOK | Support configured providers/protocol adapters; no promise that arbitrary unknown APIs auto-work | `APPROVED REQUIREMENT` | Provider capability & adapter design (`docs/PROVIDER_GATEWAY.md`); initial adapter set `OPEN` (`DEC-ARCH-02`) |
| `ADR-008` | Provider secrets | Store server-side encrypted; never in APK | `REQUIRED SECURITY DESIGN` / `OPEN` *(vault impl)* | Must test before production; vault implementation choice tied to `ADR-015` |
| `ADR-009` | Heavy AI | Optional remote workers, invoked by capability and user choice | `PROPOSAL` / `OPEN` | Model/GPU activation policy and budget `OPEN` (depends on `ADR-010`, `ADR-015`) |
| `ADR-010` | Billing | No assumption that user can pay; no paid cloud/GPU resources until explicit approval | `APPROVED CONSTRAINT` / `OPEN` *(ceiling)* | Verify free-tier limits, billing/card requirement, region, and user budget cap before creating resources |
| `ADR-011` | Repository use | All unique catalogue entries receive a classification/allocation; not all are installed or bundled | `APPROVED INTERPRETATION` | 264 unique GitHub rows (`first_catalogue_number` key) + 412-row occurrence ledger |
| `ADR-012` | External editor interoperability | Must be proven by import/round-trip tests per target; no universal compatibility claim | `REQUIRED ACCEPTANCE RULE` / `DEFERRED` *(priority)* | CapCut/Alight Motion/Node Video/Premiere/Resolve target priority `DEFERRED` to P1/P2 |
| `ADR-013` | Google AI Studio first task | Inspect workspace/docs/native Build availability before implementing; no paid resources or full editor generation | `EXECUTED` (`AIVX-A0-INSPECT-001`) | Completed in A0; results logged in `docs/PROJECT_STATUS.md` |
| `ADR-014` | User media retention | Retention, deletion schedule, and external-provider media-upload consent policy not yet selected | `OPEN` | Must be decided by user before uploading private media to cloud or external AI providers |
| `ADR-015` | Cloud vendor/region | Google Cloud plausible, not selected | `OPEN` | Compare cost, region, storage, GPU, free tier, card requirement, and phone usability before user choice |
| `ADR-016` | Friend roles | Owner/editor/commenter/viewer role proposal | `OPEN` (`PROPOSAL` documented) | User approval needed on roles, invite policy, and BYOK key isolation (`DEC-UX-03`, `DEC-ARCH-03`) |
| `ADR-017` | 3D and VFX integration | Separate specialist workers with editable project references | `PROPOSAL` / `DEFERRED` *(P2 candidate)* | Define GLB/OBJ/FBX import and render contract when prioritized |
| `ADR-018` | Offline support | Offline AI/edit mode excluded by online-only decision; cached read-only view may be considered | `APPROVED DIRECTION` / `OPEN` *(cache UX)* | Detailed offline/weak-network behavior remains `OPEN` (`DEC-UX-05`) |

---

## 2. Open User Decision Register (Tier 1–4 — Requires Explicit User Approval)

No item below is decided yet. Each entry records options, dependencies, and the gate it blocks.

### Tier 1 — Required Before Phase C (UX / UI Design)

| Decision ID | Linked ADR | Topic | Options Under Consideration | Dependencies | Status |
|---|---|---|---|---|---|
| `DEC-UX-01` | — | P0 vs P1/P2 vertical-slice feature prioritization (preserving all 15 approved features) | **Option A (`PROPOSAL`):** P0 = Auth (`SCR-01`), Workspace/Project (`SCR-02..03`), Upload/Proxy (`SCR-04`), Preview + Basic Timeline (`SCR-05..06`), FEAT-15 Visual Feedback + Comment Queue (`SCR-08..09`), BYOK Settings (`SCR-12`), Basic MP4 Export (`SCR-10..11`); remaining features staged in P1/P2. **Option B:** Design all 15 `FEAT` panels simultaneously up front. | `docs/PRD_SRS.md`, `SCR-01..14` | `OPEN` — User Decision Required |
| `DEC-UX-02` | `ADR-002` | Android target device matrix, `minSdk`, and portrait/landscape policy | **Option A (`PROPOSAL`):** Phone-first Portrait + Landscape support (Landscape rotation for Timeline & FEAT-15 Canvas); user specifies `minSdk` (current template = `24`; `26+` optional). **Option B:** Portrait-only mobile layout. | `NFR-014`, `app/build.gradle.kts` | `OPEN` — User Decision Required |
| `DEC-UX-03` | `ADR-016` | Invited friend roles, invite flow, and BYOK key isolation | **Option A (`PROPOSAL`):** Least-privilege roles (`OWNER`, `EDITOR`, `COMMENTER`, `VIEWER`); friends cannot spend Owner's BYOK key without explicit policy. **Option B:** Equal editor permissions for all invited friends. | `FR-053`, `SEC-002`, `SEC-026`, `DATA-023` | `OPEN` — User Decision Required |
| `DEC-UX-04` | `ADR-006` | FEAT-15 annotation UX & target-resolution confidence thresholds | **Option A (`PROPOSAL`):** Confidence `>= 0.85` pre-selected (editable), `< 0.85` mandatory disambiguation picker, `RASTERIZED` always shows reconstruction risk badge & opt-in inpaint+new-layer choice. **Option B:** Manual target confirmation on every comment regardless of confidence. | `docs/FEAT15_VISUAL_FEEDBACK.md`, `FR-020..029` | `OPEN` — User Decision Required |
| `DEC-UX-05` | `ADR-018` | Offline / weak-network client behavior | **Option A (`PROPOSAL` for P0):** Strict online-only status banner + resumable upload/job auto-resume, zero local edits. **Option B (`PROPOSAL` for P1):** Read-only cached project list and past comments while blocking all mutations/AI/renders. | `ADR-003`, `ADR-018`, `RISK-031` | `OPEN` — User Decision Required |

### Tier 2 — Required Before Phase D (Technical Architecture Approval)

| Decision ID | Linked ADR | Topic | Options Under Consideration | Dependencies | Status |
|---|---|---|---|---|---|
| `ADR-004` / `ADR-005` | `ADR-004`, `ADR-005` | Canonical project schema & final headless NLE engine | **Option A (`PROPOSAL`):** Run bounded cloud Linux feasibility spike on `storytold/filmcraft`; adopt if gates pass, else fall back to FFmpeg + custom canonical timeline engine. **Option B:** Build custom FFmpeg-backed canonical timeline engine from start. | `docs/CANONICAL_PROJECT_MODEL.md`, `RISK-004`, `RISK-005` | `OPEN` — User Decision Required |
| `DEC-ARCH-01` | `ADR-003` | Android preview streaming & paused-frame accuracy transport | **Option A (`PROPOSAL`):** Server-side FFmpeg proxy MP4/HLS streamed in Android Media3/ExoPlayer + server-side exact paused-frame reference/crop. **Option B:** Real-time WebRTC / server-rendered frame stream. | `docs/ARCHITECTURE.md` §5–6, `FEAT-15`, `NFR-008` | `OPEN` — User Decision Required |
| `DEC-ARCH-02` | `ADR-007` | Initial BYOK provider protocol adapters | **Option A (`PROPOSAL`):** P0 supports 3 standard families (`OpenAI-compatible`, `Anthropic-compatible`, `Google Gemini-compatible`) + strict allow-listed `Custom HTTP` JSON adapter with SSRF blocks. **Option B:** Start with a single provider family. | `docs/PROVIDER_GATEWAY.md`, `SEC-004`, `SEC-019` | `OPEN` — User Decision Required |
| `DEC-ARCH-03` | `ADR-016` | Authentication method & private invite allowlist | **Option A:** Google Sign-In (`CredentialManager`) + server-side invite allowlist. **Option B:** Email/Password or Passkey custom auth backend + invite token. | `SCR-01`, `SEC-001..003`, `NFR-001..002` | `OPEN` — User Decision Required |

### Tier 3 — Required Before Any Backend / Cloud / Paid Provisioning

| Decision ID | Linked ADR | Topic | Options Under Consideration | Dependencies | Status |
|---|---|---|---|---|---|
| `ADR-010` | `ADR-010` | Billing / payment card availability & monthly/per-job cost ceiling | **Option A:** Zero-cost / free-tier control plane only (no cloud GPU workers; user BYOK API only). **Option B:** Paid cloud/GPU with strict monthly hard cap and per-job approval ceiling. | `RISK-001`, `RISK-025`, `NFR-013` | `OPEN` — User Decision Required |
| `ADR-015` | `ADR-015` | Cloud vendor, region, database, object storage, and job queue | **Option A:** Google Cloud (Cloud Run + Cloud Storage + Firestore/Cloud SQL) in user-chosen region (note: Firebase Storage requires Blaze billing). **Option B:** Alternative cloud / VPS + S3-compatible object storage (e.g., R2/B2) + Postgres/Redis. | `ADR-010`, `docs/ARCHITECTURE.md` §7, `RISK-022`, `RISK-032` | `OPEN` — User Decision Required |
| `ADR-009` | `ADR-009` | Heavy AI / GPU worker policy (ASR, SAM2, ProPainter, Upscale, Diffusion) | **Option A:** P0 uses BYOK external APIs + CPU FFmpeg only; self-hosted GPU workers `DEFERRED`. **Option B:** On-demand scale-to-zero serverless GPU workers (requires billing & quota). | `ADR-010`, `ADR-015`, `RISK-017` | `OPEN` — User Decision Required |
| `ADR-014` | `ADR-014` | Media retention, deletion schedule, and external-provider media-upload consent | **Option A (`PROPOSAL`):** User-configurable retention (e.g., proxy/export expiry + manual original delete) + explicit per-provider "Allow private media upload" consent toggle. **Option B:** Permanent storage with manual deletion only. | `SEC-010`, `SEC-016`, `RISK-014`, `RISK-028` | `OPEN` — User Decision Required |
| `ADR-008` | `ADR-008` | Server-side BYOK secret vault implementation | **Option A:** Managed Secret Manager / KMS envelope encryption. **Option B:** Application-level AES-GCM encryption with server-managed master key. | `ADR-015`, `SEC-004`, `SEC-017` | `OPEN` — User Decision Required |

### Tier 4 — Safely `DEFERRED` Candidates (Confirm When Reached)

| Decision ID | Linked ADR | Topic | Why Safe to Defer Now | Dependencies | Status |
|---|---|---|---|---|---|
| `ADR-012` | `ADR-012` | First external third-party editor export beyond MP4/OTIO (`CapCut`, `Alight Motion`, `Node Video`, `Premiere`, `DaVinci Resolve`) | Canonical model, MP4/WAV export, and OTIO round-trip must be verified first; each target app requires version-specific import tests. | `FEAT-12`, `docs/EXPORT_INTERCHANGE.md` | `DEFERRED` (P1/P2) |
| `ADR-017` | `ADR-017` | 3D (`Blender`) and Node VFX (`Natron` / `OpenFX`) specialist workers | Heavy Linux/GPU container workers best added after core timeline, FEAT-15, and safe agent protocol are stable. | `FEAT-04`, `FEAT-10`, `ADR-009` | `DEFERRED` (P2) |
| `DEC-DEF-01` | `ADR-002` | Advanced tablet/foldable multi-pane layouts | Phone-first UX takes priority; standard adaptive foundations can be added without blocking P0. | `DEC-UX-02` | `DEFERRED` (P2) |
| `DEC-DEF-02` | `ADR-009` | Optional ComfyUI / Diffusion / Lip-Sync / Restoration / TTS workers | High VRAM, model-version, security, and cost overhead; evaluate and add individually on demand. | `ADR-009`, `ADR-010`, `docs/REPOSITORY_AUDIT.md` | `DEFERRED` (P2+) |

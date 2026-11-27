# AIVX Cross-Document Test Definition Register

**Document ID:** AIVX-TEST-REG-001 · **Version:** 1.0 · **Date:** 2026-11-27 (Asia/Dhaka)  
**Status:** BASELINE REGISTER — ALL EXECUTION STATES ARE `NOT TESTED`  
**Related:** `docs/PRD_SRS.md`, `docs/TRACEABILITY.md`, `docs/ARCHITECTURE.md`, `docs/CANONICAL_PROJECT_MODEL.md`, `docs/FEAT15_VISUAL_FEEDBACK.md`, `docs/AI_AGENT_EDIT_PROTOCOL.md`, `docs/PROVIDER_GATEWAY.md`, `docs/EXPORT_INTERCHANGE.md`, `docs/SECURITY_THREAT_MODEL.md`

> **Verification & Scope Rules (`FACT`):**
> - **Zero tests in this register have been executed (`NOT TESTED`).** Defining a test specification is not proof of implementation or pass status.
> - Existing IDs are never renumbered.
> - Tests are defined **only** where an existing approved requirement (`FR-*` / `NFR-*` / approved spec section) provides a clear, testable basis. Where a feature is too broadly specified to write reliable acceptance tests without inventing product scope, its slot is explicitly marked **`OPEN`** or **`RESERVED`**.

---

## 1. Summary of Test ID Ranges

| Test ID Range | Count | Owner Scope | Source / Definition Location | Definition Status | Execution Status |
|---|---|---|---|---|---|
| `TEST-001..019` | 19 | `PLATFORM-CORE` (Auth, Project, Upload, Sharing, Offline) | This register (§2) | `RESERVED / OPEN` | `NOT TESTED` |
| `TEST-020..029` | 10 | `FEAT-01` Timeline & Core Editing | This register (§3.1) — grounded in `FR-010..017`, `FR-006`, `NFR-006` | `DEFINED (PROPOSAL)` | `NOT TESTED` |
| `TEST-030..033` | 4 | `FEAT-02` Keyframe & Motion Curve | This register (§3.2) — grounded in `FR-013..017` | `DEFINED (PROPOSAL)` | `NOT TESTED` |
| `TEST-034..038` | 5 | `FEAT-03` Layering & Compositing | This register (§3.3) — grounded in `FR-011..014`, `FR-017` | `DEFINED (PROPOSAL)` | `NOT TESTED` |
| `TEST-039` | 1 | `FEAT-04` 3D Scene / Camera / Assets | This register (§3.4) | `OPEN` (under-specified FR) | `NOT TESTED` |
| `TEST-040` | 1 | `FEAT-05` Vector / Drawing / Motion Graphics | This register (§3.4) | `OPEN` (under-specified FR) | `NOT TESTED` |
| `TEST-041..052` | 12 | `FEAT-15` Visual Feedback & Batch Comments | `docs/FEAT15_VISUAL_FEEDBACK.md` §9 (indexed in §4) | `DEFINED` | `NOT TESTED` |
| `TEST-053..059` | 7 | `FEAT-13` / `FEAT-15` AI Agent Edit Protocol | `docs/AI_AGENT_EDIT_PROTOCOL.md` §10 (indexed in §5) | `DEFINED` | `NOT TESTED` |
| `TEST-060..069` | 10 | `FEAT-13` BYOK Provider Gateway | `docs/PROVIDER_GATEWAY.md` §8 (indexed in §6) | `DEFINED` | `NOT TESTED` |
| `TEST-070..080` | 11 | `FEAT-12` Export & Interchange | `docs/EXPORT_INTERCHANGE.md` §7 (indexed in §7) | `DEFINED` | `NOT TESTED` |
| `TEST-081..088` | 8 | `FEAT-14` Video Reverse Engineering | This register (§8) — grounded in `FR-040..046` | `DEFINED (PROPOSAL)` | `NOT TESTED` |
| `TEST-ARCH-001..007` | 7 | System Architecture Acceptance Gates | `docs/ARCHITECTURE.md` §10 (indexed in §9) | `DEFINED` | `NOT TESTED` |

---

## 2. `TEST-001..019` — Platform Core Foundation (`RESERVED / OPEN`)

**Status:** `RESERVED / OPEN` · **Execution:** `NOT TESTED`  
**Related Requirements:** `FR-001..006`, `FR-053`, `NFR-001..005`, `SEC-001..003`, `SEC-006`, `SEC-007`, `SEC-026`, `SCR-01..04`, `SCR-14`

**Why `RESERVED / OPEN`:** While high-level requirements exist for private project CRUD (`FR-001`), resumable upload/probe/proxy (`FR-002..005`), and friend sharing (`FR-053`), exact testable boundaries — authentication provider (`DEC-ARCH-03`), friend role permission matrix (`DEC-UX-03` / `ADR-016`), offline read-only cache policy (`DEC-UX-05` / `ADR-018`), upload size/duration caps (`SEC-007`), and media retention/deletion rules (`ADR-014`) — remain `OPEN` user decisions. No acceptance tests are invented here ahead of those decisions.

---

## 3. `TEST-020..040` — Canonical Timeline, Keyframes, Compositing, 3D & Graphics

### 3.1 `FEAT-01` Timeline & Core Editing (`TEST-020..029`) — `DEFINED (PROPOSAL)` / `NOT TESTED`

| Test ID | Grounded In | Verifiable Acceptance Criterion | Execution Status |
|---|---|---|---|
| `TEST-020` | `FR-010`, `DATA-002` | Creating a sequence stores explicit canvas width/height, aspect ratio, rational frame rate (`numerator/denominator`), audio sample rate, and color settings without floating-point FPS rounding drift. | `NOT TESTED` |
| `TEST-021` | `FR-011`, `DATA-006..008`, `DATA-013` | Adding supported clip/layer kinds (video, audio, image, text, shape, vector, adjustment, mask) assigns stable IDs, valid track bindings, and explicit editability categories (`NATIVE_EDITABLE`, `RECONSTRUCTED_EDITABLE`, `RASTERIZED`, `GENERATED_MEDIA`, `EXTERNAL_REFERENCE`). | `NOT TESTED` |
| `TEST-022` | `FR-012`, `DATA-007`, `NFR-007` | Trim, split, move, and ripple-delete operations compute exact integer/rational timeline coordinates while keeping source media PTS/timebase separate from timeline coordinates. | `NOT TESTED` |
| `TEST-023` | `FR-012`, `FR-017` | Duplicate, reorder, group, lock, hide, mute, and link actions persist in canonical state; attempting to mutate a locked track or clip is rejected with an actionable validation error. | `NOT TESTED` |
| `TEST-024` | `FR-013`, `API-018` | Setting supported crop, anchor, position, scale, rotation, opacity, playback speed, reverse, and freeze-frame parameters passes through typed commands (`API-018`) and survives project reload. | `NOT TESTED` |
| `TEST-025` | `FR-015`, `CANONICAL_PROJECT_MODEL.md` §3 | Timeline snapping, markers, guides, safe-area coordinates, and frame-accurate seek resolve consistently to exact sequence frame indices on both CFR and VFR source media. | `NOT TESTED` |
| `TEST-026` | `FR-016`, `DATA-019`, `API-019`, `SEC-013` | Every committed edit increments `project.revision`, writes a `DATA-019 Operation` audit record with `operationId` and authenticated `actor`, and supports exact undo/redo round-trip. | `NOT TESTED` |
| `TEST-027` | `FR-017` | Invalid time ranges (e.g., negative duration, `sourceOut <= sourceIn`), illegal clip overlaps, unknown target IDs, and unsupported command combinations are rejected with actionable errors and zero state mutation. | `NOT TESTED` |
| `TEST-028` | `FR-006`, `NFR-006`, `API-018` | Submitting a command against a stale `baseRevision` is rejected by server-side optimistic concurrency control; no concurrent change is silently overwritten. | `NOT TESTED` |
| `TEST-029` | `FR-006`, `SEC-015` | Loading an older supported `schemaVersion` runs a deterministic tested migration; loading an unsupported newer `schemaVersion` is refused with a clear message and without destructive rewrite. | `NOT TESTED` |

### 3.2 `FEAT-02` Keyframe & Motion Curve (`TEST-030..033`) — `DEFINED (PROPOSAL)` / `NOT TESTED`

| Test ID | Grounded In | Verifiable Acceptance Criterion | Execution Status |
|---|---|---|---|
| `TEST-030` | `FR-014`, `DATA-010` | Adding, updating, and deleting keyframes on supported clip/effect properties stores exact rational timestamps and evaluates linear and hold interpolation accurately. | `NOT TESTED` |
| `TEST-031` | `FR-014`, `DATA-010`, `NFR-007` | Bezier and approved easing curve keyframes evaluate deterministically at sequence frame boundaries and round-trip identically after project save/reopen. | `NOT TESTED` |
| `TEST-032` | `FR-014`, `FR-016`, `API-018`, `API-019` | Keyframe creation, editing, and removal execute via typed commands with inverse payloads and undo/redo back to the exact prior curve state. | `NOT TESTED` |
| `TEST-033` | `FR-014`, `FR-017` | Out-of-bounds parameter values, malformed Bezier control points, or invalid keyframe timestamps are rejected with actionable errors and no partial track corruption. | `NOT TESTED` |

### 3.3 `FEAT-03` Layering & Compositing (`TEST-034..038`) — `DEFINED (PROPOSAL)` / `NOT TESTED`

| Test ID | Grounded In | Verifiable Acceptance Criterion | Execution Status |
|---|---|---|---|
| `TEST-034` | `FR-011`, `FR-012`, `DATA-006` | Track `zOrder` deterministically governs visual stacking from bottom to top across both preview proxy and render outputs. | `NOT TESTED` |
| `TEST-035` | `FR-013`, `DATA-006`, `DATA-007`, `API-018` | Layer opacity and supported blend modes update via typed commands and preserve exact canonical parameter values. | `NOT TESTED` |
| `TEST-036` | `FR-011`, `FR-012`, `FR-013` | Adjustment layers apply only to tracks below their `zOrder` and stop affecting output immediately when hidden/muted. | `NOT TESTED` |
| `TEST-037` | `FR-011`, `FR-013`, `DATA-008` | Alpha-bearing image, text, and shape layers composite cleanly over underlying video layers without corrupting underlying track pixels or opacity. | `NOT TESTED` |
| `TEST-038` | `FR-017`, `SEC-020` | Requesting an unsupported blend mode, cyclic/invalid layer grouping, or invalid compositing target is rejected with an actionable error. | `NOT TESTED` |

### 3.4 `TEST-039` (`FEAT-04` 3D) & `TEST-040` (`FEAT-05` Graphics) — `OPEN` / `NOT TESTED`

| Test ID | Feature | Status | Reason `OPEN` (No Invented Scope) |
|---|---|---|---|
| `TEST-039` | `FEAT-04` 3D Scene / Camera / Assets | `OPEN` | Current baseline lacks feature-specific FRs for 3D asset formats (`GLB`/`OBJ`/`FBX`), polygon/memory caps, camera rig contract, and headless 3D worker timeout (`ADR-017` is `PROPOSAL` / `DEFERRED` candidate). |
| `TEST-040` | `FEAT-05` Vector / Drawing / Motion Graphics | `OPEN` | Current baseline lacks feature-specific FRs for editable SVG/Lottie/code-renderer contracts, sandbox timeouts, and raster-fallback rules. |

---

## 4. `TEST-041..052` — `FEAT-15` Visual Feedback & Batch Comments (`DEFINED` / `NOT TESTED`)

Authoritative source: `docs/FEAT15_VISUAL_FEEDBACK.md` §9. These tests verify **`FEAT-15` visual annotation, target resolution, and batch Run** (they are **not** general `FEAT-06` tracking tests or `FEAT-07` audio mixing tests).

| Test ID | Summary (from `docs/FEAT15_VISUAL_FEEDBACK.md` §9) | Grounded In | Execution Status |
|---|---|---|---|
| `TEST-041` | Circle on known native text layer at a fixed frame resolves to correct layer ID and time within one sequence frame. | `FR-020`, `FR-022`, `FR-023` | `NOT TESTED` |
| `TEST-042` | Rectangle/lasso geometry remains correct under preview scaling, letterboxing, rotation, and device DPI. | `FR-020`, `FR-021` | `NOT TESTED` |
| `TEST-043` | User can add at least 20 independent comments without screenshot upload or losing captured timestamps. | `FR-022`, `FR-024`, `FR-025` | `NOT TESTED` |
| `TEST-044` | Comment context stores project revision and asset/layer IDs, not only natural-language text. | `FR-022`, `DATA-011`, `DATA-012` | `NOT TESTED` |
| `TEST-045` | A text-target comment changes only the selected text layer and keeps its track/timing intact. | `FR-023`, `FR-028`, `FEAT-08` (text-target subset) | `NOT TESTED` |
| `TEST-046` | Raster-only text is not misrepresented as editable text; offers reconstructed-layer workflow with warning. | `FR-023`, `FR-027`, `FEAT-08` (raster-warning subset) | `NOT TESTED` |
| `TEST-047` | Conflicting comments are surfaced before approval. | `FR-026`, `FR-027` | `NOT TESTED` |
| `TEST-048` | User declines plan; no project revision or provider job is created. | `FR-026`, `SEC-014` | `NOT TESTED` |
| `TEST-049` | Approved batch applies as one undoable operation group. | `FR-028`, `FR-016`, `DATA-020` | `NOT TESTED` |
| `TEST-050` | Worker failure during pre-commit causes no partial project mutation. | `FR-028`, `NFR-006`, `NFR-015` | `NOT TESTED` |
| `TEST-051` | Project revision changes between annotation and Run; stale anchors are revalidated and conflicts displayed. | `FR-022`, `FR-027` | `NOT TESTED` |
| `TEST-052` | Post-batch visual comparison inspects the marked time/range and returns evidence-backed verification (`PASS`/`FAIL`/`NEEDS REVIEW`). | `FR-029` | `NOT TESTED` |

---

## 5. `TEST-053..059` — AI Agent Edit Protocol (`DEFINED` / `NOT TESTED`)

Authoritative source: `docs/AI_AGENT_EDIT_PROTOCOL.md` §10 (`FEAT-13` / `FEAT-15` safe agent execution).

| Test ID | Summary (from `docs/AI_AGENT_EDIT_PROTOCOL.md` §10) | Grounded In | Execution Status |
|---|---|---|---|
| `TEST-053` | Invalid command type rejected by Project Service. | `FR-033`, `FR-034`, `SEC-009` | `NOT TESTED` |
| `TEST-054` | Operation against stale project revision rejected. | `FR-006`, `NFR-006`, `FR-027` | `NOT TESTED` |
| `TEST-055` | Agent cannot access a different project by guessing project/object ID. | `NFR-002`, `SEC-003` | `NOT TESTED` |
| `TEST-056` | Read-only agent turn does not create a project revision. | `FR-034`, `SEC-009` | `NOT TESTED` |
| `TEST-057` | Explicit user approval required before mutation. | `FR-026`, `FR-035`, `SEC-014` | `NOT TESTED` |
| `TEST-058` | Tool permission revocation takes effect immediately. | `FR-034`, `NFR-002`, `SEC-026` | `NOT TESTED` |
| `TEST-059` | Failed batch restores previous project revision and produces failure receipt. | `FR-028`, `SEC-014`, `NFR-006` | `NOT TESTED` |

---

## 6. `TEST-060..069` — BYOK Provider Gateway (`DEFINED` / `NOT TESTED`)

Authoritative source: `docs/PROVIDER_GATEWAY.md` §8 (`FEAT-13` BYOK provider security & routing).

| Test ID | Summary (from `docs/PROVIDER_GATEWAY.md` §8) | Grounded In | Execution Status |
|---|---|---|---|
| `TEST-060` | Secret never appears in Android traffic response or project export. | `FR-031`, `NFR-003`, `SEC-004` | `NOT TESTED` |
| `TEST-061` | Provider key is redacted from logs and error payloads. | `FR-031`, `NFR-011`, `SEC-005` | `NOT TESTED` |
| `TEST-062` | Mismatched provider capability blocks task before file upload. | `FR-032`, `NFR-004`, `SEC-010` | `NOT TESTED` |
| `TEST-063` | Unknown custom response schema is marked unsupported, not silently guessed. | `FR-032`, `SEC-028` | `NOT TESTED` |
| `TEST-064` | Retry after ambiguous timeout does not duplicate a billed task without recovery check. | `FR-046`, `SEC-012` | `NOT TESTED` |
| `TEST-065` | Disabled provider profile cannot be selected by router. | `FR-030` | `NOT TESTED` |
| `TEST-066` | SSRF / private IP / loopback / link-local / cloud metadata target is blocked. | `SEC-019` | `NOT TESTED` |
| `TEST-067` | Owner A cannot read Owner B's provider profile or secret. | `NFR-002`, `SEC-003` | `NOT TESTED` |
| `TEST-068` | Provider deletion clears vault reference and scheduled metadata. | `FR-030`, `SEC-017` | `NOT TESTED` |
| `TEST-069` | Cost limit blocks new jobs and returns clear reason. | `FR-035`, `NFR-013`, `SEC-011` | `NOT TESTED` |

---

## 7. `TEST-070..080` — `FEAT-12` Export & Interchange (`DEFINED` / `NOT TESTED`)

Authoritative source: `docs/EXPORT_INTERCHANGE.md` §7. These tests verify **`FEAT-12` rendered export and interchange** (not `FEAT-09` Color grading, `FEAT-10` VFX filters, or `FEAT-11` Stabilization).

| Test ID | Summary (from `docs/EXPORT_INTERCHANGE.md` §7) | Grounded In | Execution Status |
|---|---|---|---|
| `TEST-070` | Rendered MP4 probe and playback pass (including audio stream integrity). | `FR-050`, `FR-051` | `NOT TESTED` |
| `TEST-071` | Rendered A/V sync stays within agreed tolerance. | `FR-050`, `FEAT-07` (export-stage sync subset only) | `NOT TESTED` |
| `TEST-072` | Alpha channel export verified with checkerboard where format supports alpha. | `FR-050` | `NOT TESTED` |
| `TEST-073` | 30 / 60 / 120 fps rendered frame counts verified accurately. | `FR-050`, `NFR-007` | `NOT TESTED` |
| `TEST-074` | OpenTimelineIO (OTIO) import/export round-trip preserves supported clips and timing. | `FR-052`, `API-041`, `API-042` | `NOT TESTED` |
| `TEST-075` | Unsupported effects/objects appear in the export feature-loss report. | `FR-052`, `API-043` | `NOT TESTED` |
| `TEST-076` | Adobe Premiere Pro import verification test on documented version. | `FR-052`, `ADR-012` | `NOT TESTED` |
| `TEST-077` | DaVinci Resolve import verification test on documented version. | `FR-052`, `ADR-012` | `NOT TESTED` |
| `TEST-078` | CapCut import verification test on selected app version (`DEFERRED` until `ADR-012`). | `FR-052`, `ADR-012` | `NOT TESTED` |
| `TEST-079` | Alight Motion package import verification test (`DEFERRED` until `ADR-012`). | `FR-052`, `ADR-012` | `NOT TESTED` |
| `TEST-080` | Node Video project import verification test (`DEFERRED` until `ADR-012`). | `FR-052`, `ADR-012` | `NOT TESTED` |

---

## 8. `TEST-081..088` — `FEAT-14` Video Reverse Engineering (`DEFINED (PROPOSAL)` / `NOT TESTED`)

Grounded strictly in existing approved `FR-040..046` and `docs/PRD_SRS.md` Journey B.

| Test ID | Grounded In | Verifiable Acceptance Criterion | Execution Status |
|---|---|---|---|
| `TEST-081` | `FR-040`, `DATA-016` | Reverse analysis produces timestamped shot records where every finding is labeled `OBSERVED`, `INFERRED`, or `UNKNOWN` with linked timestamp evidence. | `NOT TESTED` |
| `TEST-082` | `FR-041`, `API-032` | Scene/shot boundary detection generates proposed cut timestamps that the user can inspect and accept/adjust before applying any edit. | `NOT TESTED` |
| `TEST-083` | `FR-042`, `DATA-014`, `API-033` | Transcript generation stores word-level start/end timestamps, confidence, speaker, and language fields whenever provided by the selected ASR worker/provider. | `NOT TESTED` |
| `TEST-084` | `FR-043`, `DATA-015`, `API-017` | OCR extraction stores text strings, normalized bounding-box geometry, timestamps, and confidence values linked to source frames. | `NOT TESTED` |
| `TEST-085` | `FR-044`, `API-034`, `SEC-028` | VLM shot analysis describes visual events, framing, objects, camera motion, and visible text while preserving explicit uncertainty/confidence metadata and never upgrading guesses to `OBSERVED`. | `NOT TESTED` |
| `TEST-086` | `FR-040`, `FR-044`, `CANONICAL_PROJECT_MODEL.md` §8 | Reconstruction plans classify every proposed element (`NATIVE_EDITABLE`, `RECONSTRUCTED_EDITABLE`, `RASTERIZED`, `GENERATED_MEDIA`) and do not claim exact source font/layer recovery from flattened pixels. | `NOT TESTED` |
| `TEST-087` | `FR-045`, `DATA-004`, `API-038` | Generated media is persisted as an immutable `DATA-004 Asset` recording model, provider, prompt, seed, parameters, task ID, and provenance metadata. | `NOT TESTED` |
| `TEST-088` | `FR-046`, `SEC-012`, `API-038` | Generation and reverse-analysis worker retries enforce retry bounds and deduplicate via provider/job task IDs to avoid unintended duplicate billing or duplicate assets. | `NOT TESTED` |

---

## 9. `TEST-ARCH-001..007` — Architecture Acceptance Gates (`DEFINED` / `NOT TESTED`)

Authoritative source: `docs/ARCHITECTURE.md` §10.

| Test ID | Gate Description (from `docs/ARCHITECTURE.md` §10) | Related IDs | Execution Status |
|---|---|---|---|
| `TEST-ARCH-001` | Native Kotlin/Compose project successfully created in the actual AI Studio account. | `ADR-002`, `RISK-002` | `NOT TESTED` *(A0 verified template workspace & standalone `compile_applet`; full account UI/emulator/device-install confirmation remains `OPEN`)* |
| `TEST-ARCH-002` | Android client authenticates and calls a non-paid health endpoint. | `NFR-001`, `API-001` | `NOT TESTED` |
| `TEST-ARCH-003` | Resumable upload to private bucket works with authorization; storage billing approval is recorded. | `FR-002`, `ADR-010`, `SEC-006` | `NOT TESTED` |
| `TEST-ARCH-004` | Worker probes a sample video and reports codec/size/duration/FPS/VFR/audio/color metadata. | `FR-003`, `API-011`, `DATA-005` | `NOT TESTED` |
| `TEST-ARCH-005` | Canonical project revision increments atomically under concurrent edits. | `FR-006`, `NFR-006`, `API-018` | `NOT TESTED` |
| `TEST-ARCH-006` | API keys never appear in APK, network response to client, logs, or crash reports. | `FR-031`, `NFR-003`, `SEC-004`, `SEC-005`, `SEC-022` | `NOT TESTED` |
| `TEST-ARCH-007` | Render job can be cancelled and retried without duplicate project mutations. | `FR-051`, `SEC-012`, `API-045` | `NOT TESTED` |

---

## 10. Features with `OPEN` Acceptance Criteria (Do Not Invent Scope)

The following approved feature areas do **not** yet have sufficient feature-specific FRs or boundary/failure rules to define complete acceptance tests without inventing unapproved requirements. They are tracked explicitly as **`OPEN`** in `docs/TRACEABILITY.md`:

- **`PLATFORM-CORE` (`TEST-001..019`):** Upload size/duration limits, invite expiry, role permission matrix (`DEC-UX-03`), auth method (`DEC-ARCH-03`), offline UX (`DEC-UX-05`), retention/deletion verification (`ADR-014`).
- **`FEAT-04` (3D — `TEST-039`):** Supported 3D formats (`GLB`/`OBJ`/`FBX`), polygon/memory caps, camera contract, sandbox timeout (`ADR-017`).
- **`FEAT-05` (Graphics — `TEST-040`):** Editable SVG/Lottie/code-renderer boundaries, sandbox limits, fallback behavior.
- **`FEAT-06` (Masks, Tracking & Rotoscoping):** Mask path editing, tracking drift/occlusion failure rules, segmentation worker (`SAM2`/`ProPainter`) acceptance tests.
- **`FEAT-07` (Multitrack Audio Studio):** Audio mixing, EQ/ducking/LUFS loudness targets, sample-rate mismatch handling, Bangla ASR accuracy (`TEST-070..071` cover export-stage audio/sync only, not audio mixing).
- **`FEAT-08` (Typography & Text Animation):** Font fallback reporting, Bangla/Unicode text shaping, RTL/kerning boundaries, text animation presets (`TEST-045..046` cover FEAT-15 text-target mutation and raster warning only).
- **`FEAT-09` (Color Management & Grading):** Color space/OCIO transform accuracy, SDR/HDR tone mapping, invalid `.cube` LUT rejection.
- **`FEAT-10` (VFX & Filters):** Effect chain limits, parameter range validation, unsupported OpenFX/plugin fallback.
- **`FEAT-11` (Stabilization & Restoration):** Missing gyro metadata fallback, GPU upscale/interpolation artifact/scene-cut protection, cost/timeout gates.
- **Security QA Matrix (`docs/SECURITY_THREAT_MODEL.md` §6):** Cross-account isolation, role downgrade, expired signed URL, malformed media/decompression bomb, prompt injection in on-screen text, APK/log secret scan, backup/restore/deletion drill — formal `TEST-SEC-*` or reserved `TEST-*` assignment remains `OPEN`.

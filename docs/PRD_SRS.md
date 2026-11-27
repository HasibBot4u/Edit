# AIVX — Product Requirements and Software Requirements Specification

**Document ID:** AIVX-PRD-001 / AIVX-SRS-001  
**Version:** 1.1 · **Date:** 2026-11-27 (Asia/Dhaka)  
**Status:** PRE-BUILD BASELINE — scope largely accepted; detailed prioritization remains OPEN  
**Audience:** user, Android Build agent, backend architect, QA  
**Related:** FEAT-01..15, FR-001..053 (41 defined; grouped with reserved gaps), NFR-001..015, SCR-01..14, DATA-001..024, API-001..045, SEC-001..030, TEST-001..088 (see `docs/TEST_REGISTER.md`), TEST-ARCH-001..007

## 1. Product vision

A private online video creation and professional editing workspace on Android. The user can create or import footage, ask an AI to analyze/reference-reconstruct or generate video content, receive a truly editable timeline where output elements are represented as layers when possible, manually refine every supported property, select exact visual elements with on-frame gestures, collect multiple comments, and execute all approved changes together through a verified AI editing pipeline.

It is not a one-shot generator whose output cannot be changed. It is also not a promise to reconstruct hidden source files, proprietary fonts, 3D geometry or exact animation from a flattened MP4. Reconstruction quality depends on available source/project data, visual evidence, provider model capability, and whether the original element is editable or rasterized.

## 2. User and environment

- Primary role: owner/editor.
- Additional roles: invited friend/editor/commenter/viewer — final permissions OPEN.
- Target platform: Android phones; tablet adaptation is desirable but not yet prioritized.
- Network assumption: app requires internet to sign in, access projects, upload, request AI work, preview cloud jobs and export. Clear connectivity errors are required.
- Device: Android version/minimum API level OPEN; screen sizes and GPU capability vary.
- App distribution: private APK/AAB path; public Play Store launch N/A unless requested.

## 3. Scope

### In scope

- Native Android project UI and navigation.
- Cloud-authenticated private workspace and projects.
- Media upload/import to cloud, proxy and metadata generation.
- Canonical editable timeline/layers and project persistence.
- Natural-language generation and edit planning.
- Visual region/point/time annotation and batch comment execution.
- Manual editor tools for approved timeline/effect capabilities.
- Provider profile management for user-supplied APIs.
- Background jobs with progress, retry/cancel and QC.
- Project export, supported interchange adapters and limitation reports.
- Security, access control, retention and private sharing with friends.

### Out of scope unless later approved

- Public social network, public creator profiles, monetization, ads, SEO, marketing and public launch.
- Local/offline AI or local editing engines on the phone.
- Full desktop editor replacement, desktop app or cross-platform app suite.
- Silent arbitrary shell execution by the AI.
- Universal import compatibility for every third-party editor without a format adapter and round-trip tests.

## 4. User journeys

### Journey A — create from prompt
1. User creates a project and chooses aspect ratio/resolution/frame rate.
2. User describes intended video; may attach reference media.
3. AI proposes brief, style plan, shots, asset plan, timeline structure and expected job/cost.
4. User reviews/approves the plan and any paid generation operation.
5. Cloud jobs generate/find assets and build editable sequence/layers.
6. User previews and edits manually or with AI.
7. User exports or asks for a supported interchange format.

### Journey B — analyze and reconstruct an existing video
1. User uploads video.
2. Probe service stores metadata and creates review proxy.
3. Scene detector creates cuts; ASR provides timestamped words; OCR identifies on-screen text; VLM describes shots/actions/camera/layout; audio model identifies speech/music/SFX and timing; tracking/segmentation may identify objects/layers.
4. A timeline-oriented report separates `OBSERVED`, `INFERRED`, `UNKNOWN` and `LOW CONFIDENCE` facts.
5. Reconstruction planner proposes editable text/shape/vector/2.5D/3D elements where evidence supports it and video/raster proxies where not.
6. User approves; worker builds a draft project and renders review frames.
7. User visually reviews, adds comments, and reruns selected parts.

### Journey C — select one visual target and request a change
1. User pauses at a frame or selects a time range.
2. User circles/lassos/points to a visible object.
3. Client writes normalized geometry in display space and captures current sequence timestamp and project revision.
4. Backend creates target context by intersecting geometry/time with layers, OCR/text objects, masks, clip IDs and assets.
5. User enters a short request such as “change this font”.
6. The agent resolves the target to the editable text entity or marks the item raster-only/ambiguous.
7. It stores a structured comment and shows target chips (time, target, layer, confidence).

### Journey D — collect many comments and execute together
1. User watches and adds comments at 2s, 5s, 8s, etc.
2. Comments stay independent, each with their own revision/context and target references.
3. User selects Run.
4. Planner groups compatible changes, detects conflicts, checks project revision and computes operation ordering/dependencies.
5. User sees a dry-run list, affected layers/times, preview thumbnails, confidence, estimated cost and any destructive/raster fallback steps.
6. User approves all or a subset.
7. System applies the batch as one atomic undoable action, then renders validation previews/QC.
8. User accepts, adjusts, or undoes the batch.

### Journey E — BYOK provider management
1. User creates provider profile and chooses protocol (OpenAI-style, Anthropic-style, custom adapter).
2. User enters endpoint, model identifier, secret and supported capabilities.
3. Server validates endpoint and runs a minimal non-destructive connection test.
4. Profile lists supported text/image/audio/video/function-calling/streaming/context features and pricing configuration.
5. AI router selects only compatible profiles; user can set priority/fallback manually.

## 5. Feature catalogue

| Feature ID | Feature | Baseline status | Main dependencies |
|---|---|---|---|
| FEAT-01 | NLE Timeline & Core Editing | APPROVED SCOPE; implementation OPEN | Canonical model, render engine |
| FEAT-02 | Keyframe & Motion Curve Editor | APPROVED SCOPE; implementation OPEN | Timeline, timebase |
| FEAT-03 | Layering & Compositing | APPROVED SCOPE; 2D baseline first | Render graph |
| FEAT-04 | 3D Scene / Camera / Assets | APPROVED SCOPE; phased/worker-based | Blender or other 3D worker, interchange |
| FEAT-05 | Vector, Drawing & Motion Graphics | APPROVED SCOPE | SVG/shape model, code renderer |
| FEAT-06 | Masks, Tracking, Rotoscoping | APPROVED SCOPE; optional workers | SAM2, RAFT, Track-Anything |
| FEAT-07 | Multitrack Audio Studio | APPROVED SCOPE | Audio graph/DSP, ASR/music workers |
| FEAT-08 | Typography & Text Animation | APPROVED SCOPE | Text shaping/font metrics, layer model |
| FEAT-09 | Color Management & Grading | APPROVED SCOPE | OCIO/LUT/color pipeline |
| FEAT-10 | VFX & Filters | APPROVED SCOPE; catalog phased | Render graph, OpenFX-style contracts |
| FEAT-11 | Stabilization & Restoration | APPROVED SCOPE; job based | Gyroflow/RAFT/RIFE/SR models |
| FEAT-12 | Export & Interchange | APPROVED SCOPE; format-by-format validation | FFmpeg/OTIO/FilmCraft adapters |
| FEAT-13 | AI Creation & Editing Assistant | APPROVED SCOPE | Provider gateway, agent tools |
| FEAT-14 | Video Reverse Engineering | APPROVED SCOPE | Probe, scene, OCR, ASR, VLM, tracking |
| FEAT-15 | Visual Feedback & Batch Revision | APPROVED SCOPE; core differentiator | Annotation anchors, comments, planner, atomic command batch |

## 6. Functional requirements (FR)

> **ID numbering note (`FACT`):** Exactly **41** functional requirements are defined across 6 grouped ranges: `FR-001..006` (6), `FR-010..017` (8), `FR-020..029` (10), `FR-030..035` (6), `FR-040..046` (7), and `FR-050..053` (4). Unused slots (`FR-007..009`, `FR-018..019`, `FR-036..039`, `FR-047..049`) are **reserved for future expansion within each group**; existing IDs are never renumbered. Detailed feature-level FRs and boundary/failure acceptance criteria for `FEAT-04` (3D), `FEAT-05` (Graphics), `FEAT-06` (Masks/Tracking), `FEAT-07` (Audio mixing/DSP), `FEAT-08` (Typography animation/Bangla shaping), `FEAT-09` (Color/LUT), `FEAT-10` (VFX/OpenFX), and `FEAT-11` (Stabilization/Restoration) remain `OPEN`.

### Project and media
- FR-001: User can create, rename, duplicate and delete private projects. Delete requires confirmation and retention policy execution.
- FR-002: User can upload supported video/audio/image assets with resumable progress, cancellation and checksum verification.
- FR-003: System probes each asset and stores codec, container, resolution, frame rate, VFR/CFR, duration, timebase, rotation, color metadata, audio streams and file checksum.
- FR-004: System creates a proxy/thumbnail/waveform where permitted and links every derivative to the original asset.
- FR-005: Missing/unavailable media produces an explicit offline state, not silent blank output.
- FR-006: Project saves use revision numbers and schema versions; older schemas migrate deterministically; newer unsupported schema is refused rather than destructively rewritten.

### Timeline and edit
- FR-010: User can create sequences with explicit canvas size, aspect ratio, frame rate, audio rate and color settings.
- FR-011: User can add video, audio, image, text, shape, vector, adjustment, mask and supported generated layers.
- FR-012: User can trim, split, move, ripple delete, duplicate, reorder, group, lock, hide, mute and link clips.
- FR-013: User can set crop, anchor, position, scale, rotation, opacity, blend mode, playback speed, reverse and freeze frame where engine supports it.
- FR-014: User can keyframe supported clip/effect parameters with linear, hold, Bezier and approved easing curves.
- FR-015: Timeline snapping, markers, guides, safe areas and frame-accurate seek are supported.
- FR-016: Every successful edit is undoable/redoable and associated with an operation ID.
- FR-017: Invalid ranges, overlaps, invalid keyframe values and unsupported operation combinations are rejected with actionable messages.

### Visual feedback / comments
- FR-020: User can draw a circle, freehand lasso, rectangle, point marker, arrow or time-range selection on the preview.
- FR-021: Gesture coordinates are transformed from screen coordinates to normalized stage coordinates and preserve preview scaling/letterboxing offsets.
- FR-022: The annotation records sequence time and frame index/timebase, source-media time where applicable, selected range, project revision, selected object IDs and geometry.
- FR-023: The server resolves candidate editable entities by time intersection, bounding boxes/masks and semantic recognition; the agent must report ambiguity.
- FR-024: User can attach text instruction and optional priority to a comment.
- FR-025: Comments remain separately stored and can be edited, resolved, ignored, reordered or grouped.
- FR-026: Run creates a batch proposal; no edit is applied until the user approves.
- FR-027: Planner reports conflicts, missing layers, stale project revision and raster-only targets before execution.
- FR-028: Approved batch is atomic and undoable as one group; failure rolls back the project mutation.
- FR-029: Post-batch verification inspects the changed timestamps/regions and returns PASS/FAIL/NEEDS REVIEW per comment.

### AI/provider
- FR-030: User can create/edit/disable/delete provider profiles.
- FR-031: Secret is submitted directly to the secure server endpoint and thereafter represented by a secret reference, never echoed to the client.
- FR-032: Provider adapter declares supported modalities/features and a connection test result.
- FR-033: AI output is an `EditPlan` with validated typed operations, target IDs, time ranges, confidence, evidence and unresolved questions.
- FR-034: Agent only uses allowlisted tools with scoped project/job permissions.
- FR-035: Paid or costly AI/generation/GPU tasks show estimated spend and require policy-defined approval.

### Analysis and generation
- FR-040: Reverse analysis produces timestamped shot records and evidence labels OBSERVED/INFERRED/UNKNOWN.
- FR-041: Scene/shot boundaries may be proposed by scene detection and must be reviewable.
- FR-042: Transcript supports word-level start/end, confidence, speaker and language where model provides it.
- FR-043: OCR stores text box geometry, timestamps and confidence.
- FR-044: VLM can describe visual events, framing, objects, camera motion and text but must preserve uncertainty.
- FR-045: Generated media is stored as an asset with model/provider/prompt/seed/parameters/task ID and editable provenance where exposed.
- FR-046: Generation task retries are bounded and deduplicated where provider supports task IDs.

### Export and collaboration
- FR-050: Export settings include format/container, codec, resolution, frame rate, quality/bitrate, audio settings, color and alpha where supported.
- FR-051: Export job includes progress, cancellation and final technical report.
- FR-052: Interchange exports include a feature-loss report and list unsupported objects/effects.
- FR-053: User can share a project with invited friends using role-scoped access; public link is off by default.

## 7. Non-functional requirements (NFR)

- NFR-001 Security: all API endpoints require authentication except health/readiness endpoints with no private data.
- NFR-002 Authorization: project, asset, provider and job access is checked server-side on every operation.
- NFR-003 Secrets: external provider keys never ship in APK, database plaintext, logs or analytics.
- NFR-004 Privacy: media is private by default; uploads disclose which AI provider receives which media and for what task.
- NFR-005 Reliability: uploads and long jobs resume after process/app restart where supported.
- NFR-006 Consistency: command application is atomic; revision conflicts do not silently overwrite changes.
- NFR-007 Determinism: same project revision + same settings + same engine/version should produce reproducible frame output within documented codec/GPU tolerance.
- NFR-008 Performance: interaction commands return quickly; expensive operations are asynchronous jobs with progress.
- NFR-009 Scalability: workers have per-job CPU/RAM/GPU/time quotas and queue limits.
- NFR-010 Accessibility: controls have labels, touch targets, keyboard/assistive navigation and contrast review.
- NFR-011 Observability: logs redact secrets/media contents and expose job IDs, timing, engine versions and failure reason.
- NFR-012 Recovery: snapshots, backups, restore tests and retention deletion are specified before friend sharing.
- NFR-013 Cost: configurable monthly/per-job ceilings and job-level estimated/actual cost.
- NFR-014 Compatibility: supported Android versions/devices and codecs are published in-app.
- NFR-015 Graceful degradation: unavailable provider or worker never destroys editable project state.

## 8. Scope staging — proposed priority

**P0 (architecture/build spike):** Native project shell, identity choice, cloud API contract, project revision/command shell, asset upload/probe, one preview, one basic clip edit, one render job.  
**P1 (editing foundation):** tracks/clips, transform/crop, trims/splits, undo/redo, text layers, captions/audio, autosave/recovery.  
**P2 (AI workflow):** provider gateway, transcript/VLM analysis, prompt plan, FEAT-15 comment collection and atomic batch.  
**P3 (advanced):** masks/tracking, color, VFX, 3D, stabilization/restoration, advanced audio and more exporters.  
This staging is a PROPOSAL; user requested high scope but approved implementation order is not yet established beyond docs-first.

## 9. Acceptance and traceability

Every FR must link to a FEAT (or `PLATFORM-CORE`), one or more SCR screens, DATA/API entities, SEC requirements and TEST cases. See `docs/TRACEABILITY.md` and `docs/TEST_REGISTER.md`. Every item remains `PLANNED` / `NOT TESTED` until implementation and verification evidence are recorded. No repository README claim makes an FR PASS.

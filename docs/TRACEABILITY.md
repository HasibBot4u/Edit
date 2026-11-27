# AIVX Requirement and Test Traceability

**Document ID:** AIVX-TRACE-001 · **Version:** 1.1 · **Date:** 2026-11-27 (Asia/Dhaka)  
**Status:** Reconciled baseline mapping; all implementation and verification states are `PLANNED` / `NOT TESTED`.  
**Related:** `docs/PRD_SRS.md`, `docs/TEST_REGISTER.md`, `docs/ARCHITECTURE.md`, `docs/CANONICAL_PROJECT_MODEL.md`, `docs/SECURITY_THREAT_MODEL.md`

## 1. Feature and Platform Traceability Matrix

| Feature / Scope | Requirement group | Screens | Data / API | Security | Acceptance tests (`docs/TEST_REGISTER.md`) |
|---|---|---|---|---|---|
| `PLATFORM-CORE` *(Foundation: Auth, Workspace, Media Upload/Probe, Friend Sharing, Offline)* | `FR-001..006`, `FR-053`, `NFR-001..015` | `SCR-01..04`, `SCR-14` | `DATA-001`, `DATA-004`, `DATA-005`, `DATA-023`, `DATA-024`; `API-001..004`, `API-009`, `API-011`, `API-044`, `API-045` | `SEC-001..003`, `SEC-006`, `SEC-007`, `SEC-015`, `SEC-016`, `SEC-022..026`, `SEC-030` | `TEST-001..019` (`RESERVED / OPEN` — pending `DEC-UX-03`, `DEC-UX-05`, `DEC-ARCH-03`, `ADR-014`) |
| `FEAT-01` Timeline / Core | `FR-010..017` | `SCR-05`, `SCR-06` | `DATA-002..012`, `DATA-019`; `API-010..020` | `SEC-002`, `SEC-003`, `SEC-013` | `TEST-020..029` (`DEFINED (PROPOSAL)` / `NOT TESTED`) |
| `FEAT-02` Keyframe / Motion | `FR-013..015`, `FR-016`, `FR-017` | `SCR-06`, `SCR-07` | `DATA-008..010`; `API-018`, `API-019` | `SEC-013` | `TEST-030..033` (`DEFINED (PROPOSAL)` / `NOT TESTED`) |
| `FEAT-03` Compositing | `FR-011..014`, `FR-017` | `SCR-06`, `SCR-07` | `DATA-006..013`; `API-018..020` | `SEC-008`, `SEC-020` | `TEST-034..038` (`DEFINED (PROPOSAL)` / `NOT TESTED`) |
| `FEAT-04` 3D | `FR-011`, `FR-033`, `FR-050` *(under-specified — `OPEN`)* | `SCR-06`, `SCR-10` | `DATA-006`, `DATA-007`, `DATA-009`; `API-037` | `SEC-008`, `SEC-020` | `TEST-039` (`OPEN` — feature FRs/criteria needed) |
| `FEAT-05` Graphics | `FR-011..015` *(under-specified — `OPEN`)* | `SCR-06`, `SCR-07` | `DATA-007..010`; `API-018`, `API-037` | `SEC-020` | `TEST-040` (`OPEN` — feature FRs/criteria needed) |
| `FEAT-06` Masks / Tracking | `FR-011`, `FR-022..029`, `FR-044` *(tracking FRs `OPEN`)* | `SCR-05..09` | `DATA-009`, `DATA-013`; `API-035`, `API-036`, `API-037` | `SEC-007`, `SEC-008`, `SEC-010` | `OPEN` *(dedicated mask/tracking/occlusion tests not yet defined; `TEST-041..052` belong to `FEAT-15`)* |
| `FEAT-07` Audio | `FR-003`, `FR-011`, `FR-042` *(audio mixing/DSP FRs `OPEN`)* | `SCR-05..07` | `DATA-004`, `DATA-006`, `DATA-009`, `DATA-014`; `API-011`, `API-033`, `API-037` | `SEC-007`, `SEC-010` | `OPEN` *(audio studio mixing/DSP tests not yet defined; export-stage audio/sync subset only: `TEST-070`, `TEST-071`)* |
| `FEAT-08` Typography | `FR-011..014`, `FR-023..029` *(shaping/animation FRs `OPEN`)* | `SCR-06..09` | `DATA-008`, `DATA-011`, `DATA-012`; `API-018`, `API-023..030` | `SEC-013`, `SEC-028` | `TEST-045`, `TEST-046` *(FEAT-15 text-target/raster subset only)*; font fallback, Bangla/Unicode shaping & text-animation tests `OPEN` |
| `FEAT-09` Color | `FR-010`, `FR-013`, `FR-050` *(color/LUT/OCIO FRs `OPEN`)* | `SCR-07`, `SCR-10` | `DATA-003`, `DATA-009`; `API-018`, `API-037` | `SEC-020` | `OPEN` *(dedicated color/LUT/HDR tests not yet defined)* |
| `FEAT-10` VFX | `FR-013`, `FR-033` *(VFX/OpenFX FRs `OPEN`)* | `SCR-07`, `SCR-10` | `DATA-009`; `API-018`, `API-037` | `SEC-008`, `SEC-020` | `OPEN` *(dedicated VFX/plugin fallback tests not yet defined)* |
| `FEAT-11` Stabilization / Restoration | `FR-003`, `FR-033`, `FR-050` *(stabilization/SR FRs `OPEN`)* | `SCR-05`, `SCR-10` | `DATA-004`, `DATA-006`, `DATA-021`; `API-037`, `API-039` | `SEC-007`, `SEC-008`, `SEC-011` | `OPEN` *(dedicated stabilization/upscale/interpolation tests not yet defined)* |
| `FEAT-12` Export / Interchange | `FR-050..052` | `SCR-10`, `SCR-11` | `DATA-001..013`, `DATA-021`, `DATA-022`; `API-012`, `API-013`, `API-040..045` | `SEC-027` | `TEST-070..080` (`DEFINED` in `docs/EXPORT_INTERCHANGE.md` §7 / `NOT TESTED`) |
| `FEAT-13` AI Assistant & BYOK Gateway | `FR-030..035`, `FR-045..046` | `SCR-07..09`, `SCR-12` | `DATA-017..021`, `DATA-024`; `API-007`, `API-008`, `API-014`, `API-015`, `API-018..020`, `API-025..031`, `API-038`, `API-039` | `SEC-004`, `SEC-005`, `SEC-009..012`, `SEC-017..019`, `SEC-028`, `SEC-029` | `TEST-053..059` (`docs/AI_AGENT_EDIT_PROTOCOL.md` §10); `TEST-060..069` (`docs/PROVIDER_GATEWAY.md` §8) — all `NOT TESTED` |
| `FEAT-14` Reverse Engineering | `FR-040..046` | `SCR-12`, `SCR-13` | `DATA-004`, `DATA-011`, `DATA-014..016`, `DATA-018`; `API-016`, `API-017`, `API-032..038` | `SEC-010`, `SEC-028` | `TEST-081..088` (`DEFINED (PROPOSAL)` in `docs/TEST_REGISTER.md` §8 / `NOT TESTED`) |
| `FEAT-15` Visual Feedback & Batch Comments | `FR-020..029` | `SCR-08`, `SCR-09` | `DATA-011`, `DATA-012`, `DATA-014..016`, `DATA-018..022`; `API-005..008`, `API-021..030` | `SEC-009`, `SEC-010`, `SEC-013`, `SEC-014`, `SEC-028` | `TEST-041..052` (`docs/FEAT15_VISUAL_FEEDBACK.md` §9); agent batch protocol: `TEST-053..059` (`docs/AI_AGENT_EDIT_PROTOCOL.md` §10) — all `NOT TESTED` |
| `ARCHITECTURE-GATES` *(Cross-cutting system verification)* | `ADR-001..018`, `NFR-001..015` | All applicable | Control plane, storage, probe, command journal, vault, jobs | `SEC-001..030` | `TEST-ARCH-001..007` (`DEFINED` in `docs/ARCHITECTURE.md` §10 / `NOT TESTED`) |

## 2. Screen ID map (`SCR-01..14`)

- `SCR-01`: Sign-in / account recovery.
- `SCR-02`: Private workspace/project list.
- `SCR-03`: Create project / sequence settings.
- `SCR-04`: Asset upload / media bin / import status.
- `SCR-05`: Preview/player and source inspection.
- `SCR-06`: Multitrack timeline.
- `SCR-07`: Inspector/effect/keyframe panels.
- `SCR-08`: Visual feedback canvas/annotation palette.
- `SCR-09`: Comment queue, plan diff, batch approval and verification report.
- `SCR-10`: Export/interchange settings and compatibility report.
- `SCR-11`: Render/job queue and downloads.
- `SCR-12`: AI assistant/provider profiles.
- `SCR-13`: Reverse-engineering report / shot evidence.
- `SCR-14`: Settings, privacy, membership and cost limits.

## 3. Data ID map (`DATA-001..024`)

`DATA-001` Project, `DATA-002` Sequence, `DATA-003` SequenceSettings, `DATA-004` Asset, `DATA-005` AssetProbe, `DATA-006` Track, `DATA-007` Clip, `DATA-008` LayerObject, `DATA-009` Effect, `DATA-010` KeyframeTrack, `DATA-011` Annotation, `DATA-012` Comment, `DATA-013` Mask, `DATA-014` Transcript, `DATA-015` OCRRecord, `DATA-016` AnalysisReport, `DATA-017` ProviderProfile, `DATA-018` EditPlan, `DATA-019` Operation, `DATA-020` OperationBatch, `DATA-021` Job, `DATA-022` RenderOutput, `DATA-023` Membership, `DATA-024` AuditEvent.

*(See `docs/CANONICAL_PROJECT_MODEL.md` §2 for core entity mappings and `OPEN` companion-entity relationships, including unassigned `Marker`.)*

## 4. API ID map (`API-001..045`, proposed logical groups)

`API-001` Auth; `API-002` Workspace; `API-003` Project; `API-004` Asset upload; `API-005` Annotation; `API-006` Comment; `API-007` Plan; `API-008` Batch approval; `API-009` Jobs; `API-010` Timeline read; `API-011` Probe; `API-012` Render; `API-013` Export; `API-014` Provider profile; `API-015` Connection test; `API-016` Analysis; `API-017` Transcript/OCR; `API-018` Command execution; `API-019` Undo/redo; `API-020` Project snapshot; `API-021` Annotation create; `API-022` Anchor resolve; `API-023` Comment create; `API-024` Comment update; `API-025` Plan from comments; `API-026` Plan validate; `API-027` Dry run; `API-028` Batch approve; `API-029` Batch apply; `API-030` Batch verify; `API-031` Capability manifest; `API-032` Scene detection; `API-033` ASR; `API-034` VLM; `API-035` Tracking; `API-036` Segmentation; `API-037` Specialist worker; `API-038` Generation task; `API-039` Cost estimate; `API-040` Export job; `API-041` Interchange import; `API-042` Interchange export; `API-043` Export loss report; `API-044` Media download; `API-045` Job cancel/resume.

**Traceability status:** mapped at design level only. Implementation links, commits, and test evidence are to be added per vertical slice. No requirement or test is marked implemented or verified (`NOT TESTED`).

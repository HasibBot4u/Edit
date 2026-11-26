# AIVX Requirement and Test Traceability

**Document ID:** AIVX-TRACE-001 · **Version:** 1.0 · **Date:** 2026-11-26  
**Status:** Baseline mapping; all implementation states are PLANNED / NOT TESTED.

| Feature | Requirement group | Screens | Data/API | Security | Acceptance tests |
|---|---|---|---|---|---|
| FEAT-01 Timeline/Core | FR-010..017 | SCR-05, SCR-06 | DATA-002..012; API-010..020 | SEC-002, 003, 013 | TEST-020..029 |
| FEAT-02 Keyframe/Motion | FR-013..015 | SCR-06, SCR-07 | DATA-008..010; API-018 | SEC-013 | TEST-030..033 |
| FEAT-03 Compositing | FR-011..014 | SCR-06, SCR-07 | DATA-006..013; API-018..020 | SEC-008, 020 | TEST-034..038 |
| FEAT-04 3D | FR-011, 033, 050 | SCR-06, SCR-10 | DATA-006, 007, 009; API-037 | SEC-008, 020 | TEST-039 |
| FEAT-05 Graphics | FR-011..015 | SCR-06, SCR-07 | DATA-007..010; API-018 | SEC-020 | TEST-040 |
| FEAT-06 Masks/Tracking | FR-011, 022..029, 044 | SCR-05..09 | DATA-009, 011, 012; API-022..029 | SEC-007, 008, 010 | TEST-041..052 |
| FEAT-07 Audio | FR-003, 011, 042 | SCR-05..07 | DATA-004, 006, 009; API-011, 033 | SEC-007, 010 | TEST-043, 070..072 |
| FEAT-08 Typography | FR-011..014, 023..029 | SCR-06..09 | DATA-008, 011, 012; API-023..030 | SEC-013, 028 | TEST-045, 046 |
| FEAT-09 Color | FR-010, 013, 050 | SCR-07, SCR-10 | DATA-003, 009; API-018, 041 | SEC-020 | TEST-073 |
| FEAT-10 VFX | FR-013, 033 | SCR-07, SCR-10 | DATA-009; API-018, 037 | SEC-008, 020 | TEST-039, 073 |
| FEAT-11 Stabilization/Restoration | FR-003, 033, 050 | SCR-05, SCR-10 | DATA-004, 006; API-034..038 | SEC-007, 008, 011 | TEST-074 |
| FEAT-12 Export/Interchange | FR-050..052 | SCR-10, SCR-11 | DATA-001..013; API-040..045 | SEC-027 | TEST-070..080 |
| FEAT-13 AI Assistant | FR-030..046 | SCR-07..09, SCR-12 | DATA-018..024; API-020..039 | SEC-004, 009..012, 028 | TEST-053..069 |
| FEAT-14 Reverse Engineering | FR-040..046 | SCR-12, SCR-13 | DATA-004, 011, 018; API-032..038 | SEC-010, 028 | TEST-081..088 (to define) |
| FEAT-15 Visual Feedback | FR-020..029 | SCR-08, SCR-09 | DATA-011, 012, 018..022; API-021..030 | SEC-009, 010, 013, 014, 028 | TEST-041..059 |

## Screen ID map

- SCR-01 Sign-in / account recovery.
- SCR-02 Private workspace/project list.
- SCR-03 Create project / sequence settings.
- SCR-04 Asset upload / media bin / import status.
- SCR-05 Preview/player and source inspection.
- SCR-06 Multitrack timeline.
- SCR-07 Inspector/effect/keyframe panels.
- SCR-08 Visual feedback canvas/annotation palette.
- SCR-09 Comment queue, plan diff, batch approval and verification report.
- SCR-10 Export/interchange settings and compatibility report.
- SCR-11 Render/job queue and downloads.
- SCR-12 AI assistant/provider profiles.
- SCR-13 Reverse-engineering report / shot evidence.
- SCR-14 Settings, privacy, membership and cost limits.

## Data ID map

DATA-001 Project, DATA-002 Sequence, DATA-003 SequenceSettings, DATA-004 Asset, DATA-005 AssetProbe, DATA-006 Track, DATA-007 Clip, DATA-008 LayerObject, DATA-009 Effect, DATA-010 KeyframeTrack, DATA-011 Annotation, DATA-012 Comment, DATA-013 Mask, DATA-014 Transcript, DATA-015 OCRRecord, DATA-016 AnalysisReport, DATA-017 ProviderProfile, DATA-018 EditPlan, DATA-019 Operation, DATA-020 OperationBatch, DATA-021 Job, DATA-022 RenderOutput, DATA-023 Membership, DATA-024 AuditEvent.

## API ID map (proposed logical groups)

API-001 Auth; API-002 Workspace; API-003 Project; API-004 Asset upload; API-005 Annotation; API-006 Comment; API-007 Plan; API-008 Batch approval; API-009 Jobs; API-010 Timeline read; API-011 Probe; API-012 Render; API-013 Export; API-014 Provider profile; API-015 Connection test; API-016 Analysis; API-017 Transcript/OCR; API-018 Command execution; API-019 Undo/redo; API-020 Project snapshot; API-021 Annotation create; API-022 Anchor resolve; API-023 Comment create; API-024 Comment update; API-025 Plan from comments; API-026 Plan validate; API-027 Dry run; API-028 Batch approve; API-029 Batch apply; API-030 Batch verify; API-031 Capability manifest; API-032 Scene detection; API-033 ASR; API-034 VLM; API-035 Tracking; API-036 Segmentation; API-037 Specialist worker; API-038 Generation task; API-039 Cost estimate; API-040 Export job; API-041 Interchange import; API-042 Interchange export; API-043 Export loss report; API-044 Media download; API-045 Job cancel/resume.

**Traceability status:** mapped at design level only. Implementation links, commits and test evidence are to be added per vertical slice. No requirement is marked implemented or verified.

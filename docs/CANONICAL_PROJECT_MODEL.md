# AIVX — Canonical Editable Project Model

**Document ID:** AIVX-DATA-001 · **Version:** 1.1 · **Date:** 2026-11-27 (Asia/Dhaka)  
**Status:** PROPOSAL; no engine or DB schema is final.  
**Related:** FEAT-01..15, DATA-001..024, API-001..045, ADR-003..005, TEST-020..039 (see `docs/TEST_REGISTER.md`)

## 1. Source-of-truth rules

1. The server stores the canonical project document and operation history.
2. The Android client may cache a snapshot for responsiveness but cannot authoritatively commit a new revision locally.
3. AI workers may read an immutable snapshot and return a typed `EditPlan`; they may not directly patch raw project JSON.
4. All edits pass through the Project Command API, validate against current revision, are recorded, and are undoable.
5. Assets are immutable objects referenced by IDs. Replaced assets create new versions or derivative references; do not silently overwrite original source.
6. A render job pins `project_revision`, renderer/worker version, export settings and input asset versions.
7. Every time-based item carries source and timeline domains separately. Frame time is represented exactly at sequence boundaries.

## 2. Core entities

| Entity | Data ID | Key fields | Notes |
|---|---|---|---|
| Project | `DATA-001` | `projectId`, `ownerId`, `memberIds`, `schemaVersion`, `revision`, `settings`, `sequenceIds`, `assetIds` | One private editing workspace |
| Sequence | `DATA-002` | `sequenceId`, `projectId`, `frameRate`, `width`, `height`, `pixelAspect`, `colorConfig`, `audioSampleRate`, `trackIds`, `duration` | Timebase and output settings; companion `DATA-003 SequenceSettings` nesting/normalization is `OPEN` |
| Track | `DATA-006` | `trackId`, `sequenceId`, `kind`, `zOrder`, `visible`, `locked`, `muted`, `solo`, `blendMode`, `trackEffects` | A layer lane |
| Clip | `DATA-007` | `clipId`, `trackId`, `assetId`, `kind`, `timelineStart`, `timelineDuration`, `sourceIn`, `sourceOut`, `speed`, `transform`, `opacity`, `effects`, `keyframeTracks` | Clip instance, not source asset |
| Asset | `DATA-004` | `assetId`, `objectKey`, `sha256`, `mediaKind`, `probe`, `duration`, `streams`, `derivatives`, `provenance` | Immutable input/derived media; companion `DATA-005 AssetProbe` storage relation is `OPEN` |
| TextLayer | `DATA-008` *(subtype)* | `textLayerId`, `clipId`, `text`, `fontRef`, `fontSize`, `fontWeight`, `tracking`, `leading`, `fill`, `stroke`, `shadow`, `alignment`, `animation` | Native editable text subtype of `DATA-008 LayerObject` where supported |
| ShapeLayer | `DATA-008` *(subtype)* | `shapeId`, `geometry`, `fill`, `stroke`, `transform`, `keyframes` | Shape/vector subtype of `DATA-008 LayerObject` |
| Effect | `DATA-009` | `effectId`, `effectType`, `params`, `enabled`, `maskIds`, `keyframeTracks`, `engineId`, `version` | Typed effect instance |
| Mask | `DATA-013` | `maskId`, `path`, `feather`, `expansion`, `opacity`, `inverted`, `mode`, `trackingBinding` | Path geometry and temporal data |
| KeyframeTrack | `DATA-010` | `targetId`, `propertyPath`, `interpolation`, `keyframes[]` | Per-property animation curve |
| Marker | `OPEN` *(unassigned)* | `markerId`, `time`, `label`, `color`, `notes` | Sequence marker; no standalone `DATA-*` ID assigned yet (candidate sub-entity of `DATA-002 Sequence` — `OPEN`) |
| Annotation | `DATA-011` | `annotationId`, `revision`, `sequenceId`, `timeAnchor`, `rangeAnchor`, `geometry`, `candidateTargets`, `commentId` | Exact visual feedback anchor |
| Comment | `DATA-012` | `commentId`, `text`, `status`, `priority`, `annotationId`, `createdBy`, `createdAt` | User intent tied to evidence |
| Operation | `DATA-019` | `operationId`, `commandType`, `targetIds`, `payload`, `baseRevision`, `resultRevision`, `inversePayload`, `actor`, `source` | Manual or AI operation audit record; grouped by `DATA-020 OperationBatch` (`OPEN` schema relation) |
| EditPlan | `DATA-018` | `planId`, `basedOnRevision`, `operations[]`, `conflicts[]`, `confidence`, `costEstimate`, `evidenceRefs`, `approvalState` | AI proposal before applying |
| Job | `DATA-021` | `jobId`, `jobType`, `status`, `progress`, `inputRevision`, `workerVersion`, `costEstimate`, `actualCost`, `resultAssetIds`, `error` | Async operation lifecycle |

### 2.1 Companion `DATA-001..024` entities and unresolved relationships (`OPEN`)

The following entities are defined in the `docs/TRACEABILITY.md` Data ID map (`DATA-001..024`) and are referenced across feature/security specifications, but their exact relational/document embedding and foreign-key schema with the core entities above remain **`OPEN`** until Phase D technical schema approval (no production DB schema or migration is defined yet):

- `DATA-003` (`SequenceSettings`): whether embedded inside `DATA-002 Sequence` or stored as a versioned preset reference (`OPEN`).
- `DATA-005` (`AssetProbe`): whether embedded inside `DATA-004 Asset` or stored as a separate immutable probe record (`OPEN`).
- `DATA-008` (`LayerObject`): exact discriminator contract across `TextLayer`, `ShapeLayer`, vector, adjustment, and future 3D/generated overlay subtypes (`OPEN`).
- `Marker`: no standalone `DATA-*` ID exists in `DATA-001..024`; whether `Marker` lives as a sub-entity of `DATA-002 Sequence` or receives a future `DATA-*` ID is `OPEN`.
- `DATA-014` (`Transcript`), `DATA-015` (`OCRRecord`), `DATA-016` (`AnalysisReport`): analysis artefacts linked to `DATA-004 Asset`, `DATA-002 Sequence`, and `DATA-011 Annotation` (`OPEN`).
- `DATA-017` (`ProviderProfile`): server-side BYOK configuration owned by user, referenced by `DATA-018 EditPlan` and `DATA-021 Job` (see `docs/PROVIDER_GATEWAY.md`).
- `DATA-020` (`OperationBatch`): atomic grouping of `DATA-019 Operation` records for batch apply/undo (`OPEN`).
- `DATA-022` (`RenderOutput`), `DATA-023` (`Membership`), `DATA-024` (`AuditEvent`): output manifest, project sharing roles, and security audit log entities (`OPEN`).

## 3. Time representation

Represent time internally with integer ticks or rational time. The canonical model must hold:
- `timelineTime`: sequence-relative timeline coordinate.
- `sourceTime`: media presentation coordinate (PTS/timebase) in the asset.
- `frameIndex`: integer sequence frame index where an operation is frame-bound.
- `sampleIndex`: integer audio sample index where audio edit is sample-bound.
- `frameRate`: numerator/denominator pair; do not store a floating-point FPS as the only value.
- `sourceTimebase`: media stream timebase numerator/denominator.

Conversion is explicit, tested and performed at system boundaries. Variable-frame-rate video uses timestamps from the source media. Display strings such as `00:00:02:15` are presentation-only. For a 29.97 drop-frame sequence, the timecode format is metadata and not a direct integer-seconds conversion.

FilmCraft uses a very fine fixed integer tick rate internally; this is one possible implementation. If adopted, AIVX must use a tested adapter and not assume its time ticks are identical to other sources.

## 4. Example project JSON envelope (illustrative, not an approved production schema)

```json
{
  "schemaVersion": 1,
  "projectId": "prj_example",
  "revision": 12,
  "sequenceIds": ["seq_main"],
  "assets": [],
  "sequences": [],
  "operationHead": "op_000012",
  "updatedAt": "2026-11-26T00:00:00Z"
}
```

Do not create production DB tables from this sketch without design approval and migration tests.

## 5. Command contract

All edits must use a command envelope:

```json
{
  "commandId": "cmd_opaque_id",
  "idempotencyKey": "job-or-user-generated-stable-key",
  "projectId": "prj_example",
  "baseRevision": 12,
  "commandType": "text.updateStyle",
  "targetIds": ["txt_3"],
  "payload": {"fontFamilyRef": "font_roboto", "fontWeight": 700},
  "actor": {"type": "user", "id": "usr_owner"},
  "source": {"type": "ai_batch", "planId": "plan_42", "commentIds": ["com_2"]}
}
```

Server response returns committed revision, operation ID, resulting target summaries and validation warnings. If `baseRevision` is stale, reject or run a conflict resolver; never silently overwrite.

## 6. Project schema evolution

- Every document has `schemaVersion`.
- Every migration has a deterministic unit test with old fixture and expected new fixture.
- Never edit a migration already shipped; add a new migration.
- Unsupported newer schemas are refused with clear message.
- Keep migrations reversible where feasible; when not reversible, document the loss and back up the original.
- Project export includes canonical JSON, media manifest, fonts/asset references, effect definitions/version IDs and any external resources needed.

## 7. Effect and renderer abstraction

An effect declares: stable ID; schema version; input/output domains; parameter schema/ranges/defaults; color-space requirements; whether it needs source frames, neighboring frames, audio, other tracks or a tracking model; preview quality; render resource class; alpha handling; GPU/CPU fallback; deterministic behavior; unsupported interchange behavior. The Project Service does not know vendor-specific worker implementation details.

## 8. Native editability categories

Every imported/generated object is assigned one of:
- `NATIVE_EDITABLE`: actual text/vector/shape/clip/layer/effect with parameters preserved.
- `RECONSTRUCTED_EDITABLE`: AI-derived approximation represented as layers but not source-identical.
- `RASTERIZED`: flattened video/image/object without underlying typography/geometry data.
- `GENERATED_MEDIA`: model output video/image/audio whose internal latent structure is not editable.
- `EXTERNAL_REFERENCE`: object stored in another editor/project format; not yet imported into canonical model.

UI must never describe a rasterized caption as editable text before OCR/reconstruction succeeds.

## 9. Retention and deletion

Project delete must schedule removal of source, proxies, previews, analysis files, embeddings, comments, export files and backups in accordance with the selected retention policy. A tombstone and deletion job track completion. Provider copies cannot always be purged by our system; disclose each provider’s retention controls and record user choice.

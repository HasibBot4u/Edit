# AI Agent Editing Protocol — Inspect, Plan, Approve, Apply, Verify

**Document ID:** AIVX-API-002 · **Version:** 1.0 · **Status:** PROPOSAL  
**Related:** FEAT-13/14/15, API-020..030, DATA-018..024, SEC-009..020, TEST-041..059

## 1. Core rule

The agent is a planner/operator that invokes typed project tools. It is not a free-form code executor with unrestricted access to storage or the project database. All changes are generated as structured operations and committed by the Project Service. The user remains in control of the approved edit scope.

## 2. Tool capability tiers

### Read-only tools

`project.inspect`, `project.getRevision`, `sequence.inspect`, `timeline.getRange`, `layer.inspect`, `asset.inspect`, `media.probe`, `media.getProxy`, `frame.get`, `frame.crop`, `annotation.list`, `comment.list`, `transcript.get`, `ocr.get`, `scene.list`, `analysis.report`, `effects.catalog`, `fonts.catalog`, `providers.capabilities`, `jobs.list`, `export.inspectSupport`.

### Proposal tools

`analysis.createPlan`, `feedback.resolveTargets`, `edit.planFromPrompt`, `edit.planFromComments`, `edit.validatePlan`, `edit.estimateCost`, `edit.previewPlan`, `export.plan`.

### Mutation tools (approval-gated)

`project.command.apply`, `project.batch.apply`, `project.undo`, `project.redo`, `media.asset.attach`, `export.start`, `generation.start`, `worker.start`.

### Restricted/destructive tools

`project.delete`, `asset.delete`, `provider.delete`, `comment.purge`, `project.restore` require separate confirmation and strict permission checks. These are never available implicitly to the AI planning loop.

## 3. Standard operation envelope

```json
{
  "operationId": "op_01H...",
  "commandType": "text.updateStyle",
  "targetIds": ["txt_03"],
  "timeRange": {"sequenceStart": "120/30", "sequenceEnd": "150/30"},
  "payload": {"fontFamilyRef": "font_inter", "fontWeight": 700},
  "preconditions": {"targetRevision": 5, "expectedTextHash": "sha256:..."},
  "evidenceRefs": ["ann_42", "frame_4_0"],
  "confidence": 0.96,
  "risk": "LOW",
  "estimatedCost": {"currency": "USD", "amount": 0.00}
}
```

The JSON schema is a design sketch. Production schemas must be versioned and validated at the server boundary. `timeRange` should use canonical time units/rationals, not lossy strings; the example is illustrative.

## 4. Required plan lifecycle

`DRAFT → VALIDATING → READY_FOR_REVIEW → APPROVED → APPLYING → VERIFYING → COMMITTED`.
Alternative terminal states: `REJECTED`, `CANCELLED`, `CONFLICTED`, `FAILED`, `ROLLED_BACK`, `NEEDS_CLARIFICATION`.

A plan record captures: user prompt; source comments; project revision; context references; resolved targets; planned operations; tool versions; provider/model route; costs; uncertainty; conflicts; unsupported features; risk; preview render references; approval identity/time; execution result; verification checks; inverse/undo group.

## 5. Safe edit loop

1. Inspect only relevant project context and user-provided assets.
2. Parse natural-language intent into target/property/time/action slots.
3. Resolve targets from IDs and visual anchors; request clarification if ambiguity affects the result.
4. Build operation plan and dependencies.
5. Validate ranges/schema/capabilities/permissions and detect unsupported features.
6. Run dry-run previews and estimates; no irreversible mutation yet.
7. Present concise summary and detailed expandable diff.
8. Receive explicit approval for the plan or selected subset.
9. Re-check base revision and permissions immediately before mutation.
10. Apply atomic batch; store operation history.
11. Render the affected interval; compare with expected target and run QC.
12. Return a result for every user comment and an undo action.

## 6. Conflict rules

- Two comments modify the same property at overlapping time spans: mark `CONFLICTED`; do not guess.
- A comment refers to a removed/moved layer: attempt re-resolution with IDs + geometry + time; ask user if confidence below threshold.
- Two operations are compatible and target different layers: may batch.
- A proposed change affects unmarked parts of the film: show scope expansion and ask permission.
- Project revision advanced after plan creation: revalidate all preconditions and create a new plan revision if changed.

## 7. Evidence and explanation

AI can show a short decision summary: “I found the selected region at 00:04.00–00:04.83 and matched it to Text Layer 3 (confidence 0.96). It is a native text layer, so font can be changed directly.” It must not expose hidden chain-of-thought. The user receives evidence, target, confidence, affected time, operation summary, limitations and rollback path.

## 8. Agent tool permissions

Every call includes user ID, project role, project ID, job ID if applicable, allowed resource scope and operation class. Read-only and mutation permissions are different. A tool call is rejected if its declared permission exceeds the user role or the current approval state. Workers receive scoped object references, not broad bucket credentials.

## 9. Required security constraints

- Never execute arbitrary shell commands derived from a prompt.
- Never accept absolute filesystem paths from a client as trusted worker paths.
- Never allow external tools to write raw canonical project files.
- Never put provider keys or signed URLs in prompts, tool traces or model responses.
- Treat retrieved files and model output as untrusted input.
- Validate file type/content, decode safely, limit decompressed size and processing time.
- Keep user confirmation for paid provider calls, video generation, inpainting, large render and destructive operations.

## 10. Acceptance tests

TEST-053 invalid command type rejected; TEST-054 operation against stale revision rejected; TEST-055 agent cannot access a different project by guessing ID; TEST-056 read-only agent turn does not create project revision; TEST-057 approval required before mutation; TEST-058 tool permission revocation takes effect immediately; TEST-059 failed batch restores previous project revision and produces failure receipt.

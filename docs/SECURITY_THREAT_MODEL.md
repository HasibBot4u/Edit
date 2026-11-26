# Security, Privacy and Abuse-Resistance Threat Model

**Document ID:** AIVX-SEC-001 · **Version:** 1.0 · **Status:** PROPOSAL / REQUIRED BEFORE CLOUD RELEASE  
**Related:** SEC-001..030, NFR-001..015, DATA-001..030, RISK-001..040

## 1. Assets to protect

Source videos/photos/audio; generated media; comments and annotations; project structure; transcripts and OCR; user identities and friend access; BYOK provider secrets; signed storage URLs; cloud worker credentials; model prompts/results; billing identifiers and job usage; logs and backups.

## 2. Trust boundaries

1. Android device ↔ API gateway.
2. API gateway ↔ identity/auth service.
3. API ↔ project DB and object storage.
4. Orchestrator ↔ external provider APIs.
5. Queue ↔ untrusted job input and isolated workers.
6. Worker ↔ object storage and rendered output.
7. Plugin/skill/third-party executable ↔ project data.
8. Export package ↔ target application/user file system.

## 3. Threats and controls

### Credential theft / provider secret exposure
Threat: keys accidentally enter APK, client logs, prompts, crash reports or public object metadata. Controls: server vault, secret references, KMS envelope encryption, strict redaction, no client retrieval endpoint, key rotation, per-provider access scope, test with APK/static artifact scanning.

### Cross-project data exposure
Threat: user guesses another project/asset/job ID. Controls: server-side ownership/role authorization on every API and object read; non-sequential opaque IDs do not replace authorization; object keys must be tenant-scoped; negative tests across two accounts.

### Malicious uploads / parser vulnerabilities
Threat: malformed media, decompression bombs, codec/parser exploit, huge dimensions, pathological duration, oversized manifests. Controls: quarantine upload, type sniffing, malware/file checks where available, resource caps, sandboxed decode workers, patched dependencies, no privileged service account inside worker, per-job timeout and memory limit.

### SSRF / provider endpoint abuse
Threat: user-configured endpoint hits cloud metadata, internal IP, loopback or private network. Controls: scheme allowlist; resolve/recheck DNS; block private/reserved/link-local/metadata ranges; egress proxy; redirect validation; request/response size limits; TLS policy; no access to internal service endpoints.

### Prompt injection / untrusted media instructions
Threat: on-screen text/audio/metadata tells the AI to exfiltrate data or perform unapproved operations. Controls: treat media/OCR/transcript/document content as untrusted evidence, never as system instructions; tool allowlists; project-scoped data access; no arbitrary code execution; approval gates.

### Destructive or unintended AI edits
Threat: wrong target, scope expansion, accidental deletion or conflicting comments. Controls: typed EditPlan, confidence, dry-run, affected-time list, atomic transactions, undo, stale revision detection, explicit approval for destructive operations.

### Cost abuse / repeated generation
Threat: runaway GPU loops, provider retries, large uploads, repeated expensive exports. Controls: user/project/job quota, budget ceiling, rate limits, idempotency keys, bounded retries, cost estimates, circuit breakers, admin/user alerts.

### Signed URL leakage
Threat: private media URL leaked in logs, screenshots or chat. Controls: short TTL, single object/action scope, no logging query string, use backend proxy where required, revoke ability where store supports it.

### Friend permission abuse
Threat: commenter changes timeline or sees keys. Controls: least privilege; COMMENTER can comment but cannot execute edits unless assigned EDITOR; no provider secret access for friends unless explicit account ownership transfer model is approved.

### Backup and deletion gaps
Threat: project delete leaves derived files/backups/provider retained copies. Controls: data inventory, object tags/manifest, deletion job receipt, backup expiry policy, provider-specific retention notice, restoration/deletion tests.

## 4. Security requirements

- SEC-001: TLS for all network transport.
- SEC-002: authentication required for private resources.
- SEC-003: object-level authorization enforced by backend.
- SEC-004: BYOK keys never delivered to Android after save.
- SEC-005: logs and error reports redact secrets and signed URLs.
- SEC-006: storage objects private by default.
- SEC-007: upload size, duration, resolution and decode resource limits.
- SEC-008: isolated worker process/container, least privilege and ephemeral workspace.
- SEC-009: AI operations use typed schema and allowlisted tools.
- SEC-010: external-provider upload requires explicit media-sharing consent.
- SEC-011: per-user/job cost and rate limits.
- SEC-012: idempotency for external and internal jobs.
- SEC-013: every edit carries authenticated actor and audit record.
- SEC-014: batch edit has approval and rollback path.
- SEC-015: project schema migrations are backed up and tested.
- SEC-016: secure deletion/retention policy.
- SEC-017: secrets rotation and revocation.
- SEC-018: no arbitrary shell execution from user prompt.
- SEC-019: prevent SSRF and path traversal.
- SEC-020: plugin/workflow execution is sandboxed and permission-scoped.
- SEC-021: dependency and container images are pinned/scanned.
- SEC-022: no service-account credentials in source repository, Android app or logs.
- SEC-023: incident response and credential revocation process documented.
- SEC-024: Android network security config avoids cleartext traffic.
- SEC-025: crash analytics do not capture frame images, raw transcripts or keys.
- SEC-026: friend roles are tested with a deny-by-default permission matrix.
- SEC-027: export/import packages are checked for zip-slip, path traversal and unsafe XML/JSON expansion.
- SEC-028: model output is validated and treated as untrusted.
- SEC-029: moderation/safety policies are applied to user media and generated content as required by chosen provider.
- SEC-030: backup restore and deletion test evidence stored before release.

## 5. Privacy notice content required

Before upload or external AI call, show: what data is sent (full video, extracted frames, audio, transcript, selected region), which service receives it, region if known, purpose, retention information from that provider, estimated job cost, and how to cancel/delete. Do not claim provider-side deletion unless provider API confirms it.

## 6. Tests

Security QA must include: two-account object isolation; role downgrade; expired URL; revoked provider key; SSRF private IP; file traversal; malformed media; oversize upload; prompt injection in on-screen text; repeated job requests; timeout after provider accepted task; batch conflict; deletion of all derivatives; log scanning for secrets; APK scan for secrets/native libraries; restore from backup; friend invite revocation.

# AIVX Risk Register

**Document ID:** AIVX-RISK-001 · **Version:** 1.1 · **Date:** 2026-11-27 (Asia/Dhaka) · **Status:** OPEN / PRE-BUILD  
**Related:** RISK-001..032 (32 defined risks)

Scales: Probability and Impact are Low/Medium/High. No risk is marked closed until evidence exists.

| Risk ID | Risk | Probability | Impact | Mitigation / control | Owner | Status |
|---|---|---|---|---|---|---|
| RISK-001 | Cloud-only design incurs ongoing storage/egress/CPU/GPU bills | High | High | No paid resources until billing approval; job-level budgets; proxy tiers; monthly cap | Owner + cloud architect | OPEN |
| RISK-002 | Google AI Studio Build account may not expose complete native Kotlin/Compose flow or code export | Medium | High | Verify in-product; no React/WebView fallback; bounded native spike | Owner + Build agent | OPEN |
| RISK-003 | AI Studio Android build produces client only; server must be designed/deployed separately | High | High | Separate control plane and workers; no backend secret in APK | Architecture | OPEN |
| RISK-004 | FilmCraft does not compile or lacks required Android/cloud integration | Medium | High | Server-side Linux build spike; API adapter; retain fallback selection OPEN | Engine spike | OPEN |
| RISK-005 | Multi-renderer strategy causes inconsistent preview/export | High | High | One canonical project model; renderer parity tests; define supported effect subset | Rendering | OPEN |
| RISK-006 | User assumes every generated visual component is editable | High | High | Editability categories; raster detection; reconstruction confidence and explicit limitations | AI/product | OPEN |
| RISK-007 | AI misidentifies selected target/time | Medium | High | Exact IDs/anchors/timebase, candidate list, confidence threshold, user confirmation | FEAT-15 | OPEN |
| RISK-008 | Multiple comments conflict or stale anchors | Medium | High | Project revision anchors, conflict detection, dry-run, atomic batch/undo | Project service | OPEN |
| RISK-009 | Custom provider endpoint causes SSRF or internal network access | Medium | Critical | Egress restrictions, private IP rejection, URL validation, proxy, no direct arbitrary fetch | Security | OPEN |
| RISK-010 | Provider API is labelled compatible but lacks video/tools/streaming | High | Medium | Capability manifests and actual connection tests; adapters per protocol | Provider gateway | OPEN |
| RISK-011 | Provider keys leak into Android app or logs | Medium | Critical | Server vault; key references; secret redaction; APK and logs scanning | Security | OPEN |
| RISK-012 | Upload or decoder accepts malicious/hostile media | Medium | High | Quarantine, sandbox, size/duration caps, patched codec workers, timeouts | Media service | OPEN |
| RISK-013 | Long uploads/jobs fail on mobile networks/app restarts | High | Medium | Resumable upload, persistent job state, idempotent retries, retry/resume UI | Android/backend | OPEN |
| RISK-014 | User media retained by external AI provider | Medium | High | Per-provider retention disclosure, consent, provider selection, deletion notice | Privacy | OPEN |
| RISK-015 | Model hallucination invents details in reverse-engineering report | High | High | Observed/inferred/unknown labels, timestamp evidence, human review | AI analysis | OPEN |
| RISK-016 | Export to target editor loses effects/timing/layers | High | High | Per-format capability matrix, loss report, actual target-app round-trip tests | Interchange | OPEN |
| RISK-017 | GPU queue or model downloads exceed capacity/budget | High | High | Optional worker activation, queue quota, cost gate, timeouts, cancellation | Cloud ops | OPEN |
| RISK-018 | VFR, timebase, fractional FPS cause frame drift | Medium | High | Rational/integer timeline model, source PTS support, frame/audio sync regression suite | Engine | OPEN |
| RISK-019 | Fonts/media missing in external export or font substitution changes layout | High | Medium | Asset manifest, font refs/embedding rights reviewed by user, fallback report | Export | OPEN |
| RISK-020 | 3D/3rd-party plugin crashes or accesses project broadly | Medium | High | Isolated worker, sandbox, scoped permissions, time/RAM/GPU budget | Plugin host | OPEN |
| RISK-021 | App scope too broad to deliver in one build iteration | High | High | Staged vertical slices, feature matrix, P0 first, explicit deferrals | Product | OPEN |
| RISK-022 | Cloud/database/storage vendor choice creates lock-in | Medium | Medium | Provider-neutral internal interfaces, exportable project/media manifest | Architecture | OPEN |
| RISK-023 | Backup exists but cannot restore project and media coherently | Medium | High | Restore drill, project snapshot + asset manifest, deletion/retention tests | Operations | OPEN |
| RISK-024 | Friend role permissions are too broad | Medium | High | Least-privilege role matrix, deny-by-default tests, invitation revocation | Identity | OPEN |
| RISK-025 | Cost estimates inaccurate for model output/large video | High | Medium | Quoted estimate + max ceiling + actual usage report; user-controlled stop | Billing | OPEN |
| RISK-026 | Catalogue rows describe old, moved, unavailable or duplicate repos | High | Medium | Preserve original URLs, resolve target separately, pin commits, recheck before integration | Repository audit | OPEN |
| RISK-027 | Skills or MCP servers contain unsafe scripts/network access | Medium | High | Static inspection, permission review, isolated test runner, no auto-install | Tooling | OPEN |
| RISK-028 | Preview frames/crops sent to external provider without user awareness | Medium | Critical | Modalities consent; provider and region display; no silent fallback | Privacy | OPEN |
| RISK-029 | Job retry bills user twice after timeout | Medium | High | Idempotency/task IDs; status reconciliation; retry approval if ambiguous | Job service | OPEN |
| RISK-030 | Renderer preview and final export differ | Medium | High | Golden frame tests, same effect definitions, fixed renderer versions, QC | Rendering | OPEN |
| RISK-031 | Cloud outage makes app/projects unavailable | Medium | High | Status/error UI, job resume, provider-independent export package, backup | Operations | OPEN |
| RISK-032 | Storage plan or location is inaccessible to user/region | Medium | Medium | Verify regional access, billing, card requirements, phone support before adoption | Owner | OPEN |

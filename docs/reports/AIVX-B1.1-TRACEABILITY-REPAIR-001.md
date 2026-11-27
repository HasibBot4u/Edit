# AIVX — Phase B1.1 Traceability, Test Ownership & Phase-Gate Repair Report

**Task ID:** `AIVX-B1.1-TRACEABILITY-REPAIR-001`  
**Phase:** B — Requirements Analysis and Documentation Integrity (`IN PROGRESS / NOT EXITED`)  
**Date:** 2026-11-27 (Asia/Dhaka, UTC+6)  
**Repository Baseline:** `HasibBot4u/Edit` · Branch `main` · Reviewed baseline commit `6f3343e050dc2ff870c60839cc8b1dc16d9440f5`  
**Execution Scope:** Documentation-only repair within the 7 allowed files under `docs/` (`0` Android app/XML/manifest/Gradle/resource/`metadata.json` changes; `0` repository CSV changes; `0` archived B0/B1 report changes; `0` cloud/billing/GPU resources created; `0` app builds or tests executed — `NOT TESTED`)

---

## 1. Findings Verified (`FACT`)

Independent inspection of `docs/PRD_SRS.md`, `docs/TRACEABILITY.md` (v1.1), `docs/TEST_REGISTER.md` (v1.0), `docs/FEAT15_VISUAL_FEEDBACK.md`, `docs/CANONICAL_PROJECT_MODEL.md`, `docs/AI_AGENT_EDIT_PROTOCOL.md`, `docs/PROVIDER_GATEWAY.md`, `docs/EXPORT_INTERCHANGE.md`, `docs/SECURITY_THREAT_MODEL.md`, `docs/ARCHITECTURE.md`, `docs/PROJECT_STATUS.md`, `docs/PROJECT_MANIFEST.md`, `docs/DECISION_LOG.md`, `docs/CHANGELOG.md`, `docs/README.md`, and `docs/reports/AIVX-B1-DOC-CORRECTIONS-001.md` confirmed **all 5 traceability findings plus the Phase Gate defect**:

1. **Finding 1 — `FEAT-06` (Masks, Tracking & Rotoscoping) incorrectly claimed `FEAT-15` and `FEAT-14` requirements (`CONFIRMED / FACT`):**
   - `docs/TRACEABILITY.md` v1.1 mapped `FEAT-06` to `FR-022..029`, `FR-044`, and `SCR-05..09`.
   - In `docs/PRD_SRS.md` §6, `FR-020..029` are exclusively the `FEAT-15` visual feedback / comment / batch Run workflow, and `FR-044` is `FEAT-14` VLM visual analysis. Similarly, `SCR-08` (Visual feedback canvas) and `SCR-09` (Comment queue / batch approval) belong to `FEAT-15`.
   - Only `FR-011` *(adding mask layers)* and shared command primitives `FR-016..017` are genuinely supported in `PRD_SRS.md`; dedicated mask-path, tracking, and rotoscoping FRs are `OPEN`.

2. **Finding 2 — `FEAT-08` (Typography & Text Animation) incorrectly claimed `FEAT-15` requirements, screens, data, and APIs (`CONFIRMED / FACT`):**
   - `docs/TRACEABILITY.md` v1.1 mapped `FEAT-08` to `FR-023..029`, `SCR-06..09`, `DATA-011`, `DATA-012`, `API-023..030`, and `SEC-028`, and listed `TEST-045`, `TEST-046` without explicitly declaring `FEAT-15` as their primary owner.
   - All of `FR-023..029`, `SCR-08..09`, `DATA-011` (`Annotation`), `DATA-012` (`Comment`), `API-023..030` (`Comment create..Batch verify`), and `TEST-045..046` belong to `FEAT-15`.
   - Only shared editable-text layer/transform/keyframe primitives (`FR-011..014`, `FR-016..017`), `DATA-007`/`DATA-008 (TextLayer)`/`DATA-010`/`DATA-019`, and `API-018..019` belong to `FEAT-08`; dedicated typography, Bangla/Unicode complex-script shaping, font fallback, RTL/kerning, and text animation FRs/tests remain `OPEN`.

3. **Finding 3 — `FEAT-13` and `FEAT-14` overlap on `FR-045..046` and `TEST-087..088` (`CONFIRMED / FACT`):**
   - In `docs/PRD_SRS.md` §6, `FR-040..046` share the combined heading *"Analysis and generation"*: `FR-040..044` specify reverse engineering (`FEAT-14`, Journey B), whereas `FR-045` (generated-media asset provenance) and `FR-046` (bounded, task-ID-deduplicated generation retries) primarily specify AI media generation (`FEAT-13`, Journey A; also verified at the provider gateway boundary by `TEST-064`).
   - `docs/TEST_REGISTER.md` v1.0 placed all of `TEST-081..088` under `FEAT-14` without separating primary (`FEAT-13`) vs secondary (`FEAT-14` reconstruction replacement-media generation) ownership of `TEST-087..088`, and `TEST-088` wording conflated generation retries with reverse-analysis retries.

4. **Finding 4 — `PLATFORM-CORE` lumped all `NFR-001..015` instead of separating cross-cutting NFR traceability (`CONFIRMED / FACT`):**
   - `docs/TRACEABILITY.md` v1.1 assigned blanket `NFR-001..015` to both `PLATFORM-CORE` and `ARCHITECTURE-GATES`, obscuring which NFRs belong to foundation services vs BYOK secrets (`NFR-003` -> `FEAT-13`), atomic edits (`NFR-006` -> `FEAT-01`/`FEAT-15`), determinism (`NFR-007` -> `FEAT-01/02/12`), Android accessibility (`NFR-010` -> `SCR-01..14`), worker quotas (`NFR-009`), and cost ceilings (`NFR-013`).

5. **Finding 5 — Additional numeric-adjacency mapping leaks across `FEAT-01`, `FEAT-03`, `FEAT-04`, `FEAT-09`, `FEAT-10`, `FEAT-11`, `FEAT-12`, `FEAT-13`, and `FEAT-14` (`CONFIRMED / FACT`):**
   - `FEAT-01` used `DATA-002..012` (dragging in `FEAT-15` `DATA-011 Annotation` and `DATA-012 Comment`) and `API-010..020` (dragging in `API-012` Render, `API-013` Export, `API-014` Provider profile, `API-015` Connection test, `API-016` Analysis, and `API-017` Transcript/OCR).
   - `FEAT-03` used `DATA-006..013` (dragging in `DATA-011 Annotation` and `DATA-012 Comment`).
   - `FEAT-04`, `FEAT-10`, and `FEAT-11` mapped `SCR-10` (Export settings) and unrelated `FR-033` / `FR-050` instead of `SCR-05`/`SCR-07`/`SCR-11` and `OPEN` dedicated FRs.
   - `FEAT-09` mapped `FR-013` (crop/transform/speed/blend) instead of `FR-003` (source color metadata) and `FR-010` (sequence color config).
   - `FEAT-12` used `DATA-001..013` (dragging in `DATA-011..012`, omitting `DATA-014` subtitles, and not explicitly noting `DATA-017` exclusion per `SEC-004` / `TEST-060`).
   - `FEAT-13` used `SCR-07..09` (dragging in `SCR-07` inspector and `SCR-08` visual feedback canvas) and `API-025..031` (dragging in `API-025` Plan from comments and `API-030` Batch verify as primary `FEAT-13` APIs).
   - `FEAT-14` included `DATA-011` (`Annotation`, owned by `FEAT-15`).

6. **Phase Gate Defect — Tier 2 and Tier 3 decisions were conflated with Phase C entry / Phase B exit (`CONFIRMED / FACT`):**
   - `docs/PROJECT_STATUS.md` and `docs/README.md` previously framed all Tier 1–3 decisions as a single undifferentiated Phase B exit blocker, which risked treating Phase D architecture decisions (Tier 2) and cloud/billing/GPU provisioning decisions (Tier 3) as prerequisites to start Phase C UX/UI design.

---

## 2. Corrections Made (`FACT`)

1. **`docs/TRACEABILITY.md` (updated to v1.2):**
   - Repaired every row in **§1 Feature and Platform Traceability Matrix** so every `FR`, `SCR`, `DATA`, `API`, `SEC`, and `TEST` link is semantically grounded in its source specification with explicit **Primary** vs **Shared / Secondary** labels and zero numeric-adjacency leaks.
   - Removed `FR-022..029`, `FR-044`, `SCR-08..09` from `FEAT-06`; retained shared `FR-011`, `FR-016..017` and kept dedicated mask/tracking/rotoscoping FRs and tests `OPEN`.
   - Removed `FR-023..029`, `SCR-08..09`, `DATA-011..012`, `API-023..030`, primary `SEC-028` from `FEAT-08`; retained shared `FR-011..014`, `FR-016..017` and kept typography/Bangla shaping/font fallback/text-animation FRs and tests `OPEN` (marking `TEST-045..046` as `FEAT-15`-owned).
   - Clarified `FEAT-13` as primary owner of `FR-030..035`, `FR-045..046`, `TEST-060..069`, and `TEST-087..088` (plus shared primary `TEST-053..059` with `FEAT-15`), and `FEAT-14` as primary owner of `FR-040..044` and `TEST-081..086` (with `FR-045..046` and `TEST-087..088` secondary only when reconstruction generates replacement media) — without renumbering any IDs.
   - Removed blanket `NFR-001..015` from `PLATFORM-CORE` and `ARCHITECTURE-GATES`, and added dedicated **§2 Cross-Cutting Non-Functional Requirements (`NFR-001..015`) Traceability** covering Security, Privacy, Reliability, Consistency, Determinism, Performance, Scalability, Accessibility, Observability, Recovery, Cost Governance, Compatibility, and Graceful Degradation.
   - Fixed numeric-adjacency leaks on `FEAT-01`, `FEAT-03`, `FEAT-04`, `FEAT-05`, `FEAT-07`, `FEAT-09`, `FEAT-10`, `FEAT-11`, `FEAT-12`, `FEAT-13`, and `FEAT-14`.

2. **`docs/TEST_REGISTER.md` (updated to v1.1):**
   - Added a **Secondary / Shared Scope** column in §1 Summary Table and split `TEST-081..088` into **§8.1 `TEST-081..086` (`FEAT-14` Primary)** and **§8.2 `TEST-087..088` (`FEAT-13` Primary; `FEAT-14` Secondary)** without renumbering IDs.
   - Tightened `TEST-088` wording to match `FR-046` + `SEC-012` (generation task retries bounded and deduplicated via provider/job task IDs, complementing `TEST-064`).
   - Added explicit ownership notes on `TEST-045..046` (`FEAT-15` primary; `FEAT-08` secondary touchpoint), `TEST-053..059` (`FEAT-13` & `FEAT-15` shared primary), and `TEST-071` (`FEAT-12` primary; export-stage sync touchpoint only).
   - Narrowed §2 (`TEST-001..019`) to foundation-enforced NFRs with pointer to `docs/TRACEABILITY.md` §2, and documented `OPEN` cross-cutting NFR QA criteria in §10. All 95 test IDs (`TEST-001..088` + `TEST-ARCH-001..007`) remain `NOT TESTED`.

3. **`docs/PROJECT_STATUS.md`, `docs/README.md` (v1.3), `docs/PROJECT_MANIFEST.md` (v1.4), and `docs/CHANGELOG.md`:**
   - Recorded `AIVX-B1.1-TRACEABILITY-REPAIR-001` completion and indexed `docs/reports/AIVX-B1.1-TRACEABILITY-REPAIR-001.md`.
   - Replaced undifferentiated Phase B blocker text with explicit **5-state readiness separation** and **Tier 1 / Tier 2 / Tier 3 / Tier 4 phase-specific approval gates**.
   - Preserved all historical `CHANGELOG.md` entries verbatim and marked archived B0 and B1 reports immutable.

---

## 3. Issues Remaining `OPEN` (Including Proposed Edits Outside Allowed Files)

### 3.1 Open Product, Requirement & Decision Items
1. **Tier 1 User Decisions (Mandatory before Phase C UX/UI Design begins):** `DEC-UX-01..05` (`OPEN` in `docs/DECISION_LOG.md`).
2. **Tier 2 User Decisions (Mandatory before Phase D Technical Architecture is finalized):** `ADR-004`/`ADR-005`, `DEC-ARCH-01..03` (`OPEN` — not a blocker to begin Phase C unless exact `SCR-01` auth-button UX requires `DEC-ARCH-03`).
3. **Tier 3 User Decisions (Mandatory before Backend / Cloud / Storage / GPU Provisioning):** `ADR-008`, `ADR-009`, `ADR-010`, `ADR-014`, `ADR-015` (`OPEN` — not a blocker to begin Phase C).
4. **Tier 4 Deferred Decisions (`DEFERRED`):** `ADR-012`, `ADR-017`, `DEC-DEF-01`, `DEC-DEF-02`.
5. **Under-Specified Feature FRs & Acceptance Tests (`OPEN`):** `PLATFORM-CORE (TEST-001..019)`, `FEAT-04 (TEST-039)`, `FEAT-05 (TEST-040)`, `FEAT-06` (mask/tracking/rotoscoping), `FEAT-07` (audio mixing/DSP/LUFS), `FEAT-08` (typography/Bangla shaping/font fallback/text animation), `FEAT-09` (color/OCIO/LUT/HDR), `FEAT-10` (VFX/OpenFX), `FEAT-11` (stabilization/restoration), Cross-Cutting NFR QA benchmarks (`NFR-008..015`), and formal Security QA test IDs (`docs/SECURITY_THREAT_MODEL.md` §6).
6. **Repository & Tooling Items (`OPEN` / `NOT TESTED`):** Full source/build/license audits of the 264 unique repos; account-level AI Studio UI confirmation (emulator/export/device install); container Robolectric SDK 36 HTTP fetch failure; unavailable verbatim `docs/reports/AIVX-A0-INSPECT-001.md`.

### 3.2 Proposed Non-Blocking Edits Outside Allowed Files (`PROPOSAL` — Not Modified in B1.1)
Per task prohibitions, files outside the 7 allowed files were inspected only and **not modified**. The following minor cross-file header refinements are proposed for a future doc-maintenance pass:
- `docs/EXPORT_INTERCHANGE.md` line 4: narrow `DATA-001..024` to `DATA-001..010, DATA-013, DATA-014, DATA-021, DATA-022 (excluding DATA-017 secrets per SEC-004)` so the header does not implicitly include `DATA-017 ProviderProfile`.
- `docs/CANONICAL_PROJECT_MODEL.md` line 5: extend `TEST-020..039` to `TEST-020..040` (since §2 defines `ShapeLayer` used by `FEAT-05` / `TEST-040`).
- `docs/PRD_SRS.md` §6 line 156: add a one-line parenthetical under `### Analysis and generation` noting `FR-040..044` (`FEAT-14` primary) vs `FR-045..046` (`FEAT-13` primary; `FEAT-14` secondary) to mirror `docs/TRACEABILITY.md` v1.2.

---

## 4. Changed & Added Files (`FACT`)

- **Modified Files (`6` — all within ALLOWED FILES):**
  1. `docs/TRACEABILITY.md` (v1.1 → v1.2)
  2. `docs/TEST_REGISTER.md` (v1.0 → v1.1)
  3. `docs/PROJECT_STATUS.md`
  4. `docs/PROJECT_MANIFEST.md` (v1.3 → v1.4)
  5. `docs/README.md` (v1.2 → v1.3)
  6. `docs/CHANGELOG.md`
- **Created File (`1` — within ALLOWED FILES):**
  1. `docs/reports/AIVX-B1.1-TRACEABILITY-REPAIR-001.md`
- **Untouched Protected Files (`0` changes):**
  - Android Kotlin/XML/Manifest/Gradle/resource/`metadata.json` files: **`0` changed**.
  - Repository CSVs & original catalogue (`docs/ORIGINAL_REPOSITORY_CATALOGUE.txt`, `docs/REPOSITORY_OCCURRENCES_412.csv`, `docs/REPOSITORY_UNIQUE_AUDIT.csv`, `public/assets/aistudio/*`): **`0` changed**.
  - Archived B0 and B1 reports (`docs/reports/AIVX-B0-ANALYSIS-RECONCILE-001.md`, `docs/reports/AIVX-B0-REPORT-ERRATA-001.md`, `docs/reports/AIVX-B1-DOC-CORRECTIONS-001.md`): **`0` changed**.

---

## 5. Requirement & Test Mapping Validation Checklist (`FACT`)

| # | Verification Requirement | Result | Evidence |
|---|---|---|---|
| 1 | Every feature row has semantically correct FR ownership | `PASS` | Verified all 17 rows (`PLATFORM-CORE`, `FEAT-01..15`, `ARCHITECTURE-GATES`) in `docs/TRACEABILITY.md` §1 against `docs/PRD_SRS.md` |
| 2 | `FEAT-06` and `FEAT-08` no longer claim `FEAT-15` comment requirements | `PASS` | `FR-022..029`, `FR-044`, `SCR-08..09` removed from `FEAT-06`; `FR-023..029`, `SCR-08..09`, `DATA-011..012`, `API-023..030` removed from `FEAT-08` |
| 3 | `TEST-087` / `TEST-088` ownership explicitly justified without renumbering | `PASS` | `docs/TRACEABILITY.md` §1 & `docs/TEST_REGISTER.md` §1, §8.1–8.2 assign `FEAT-13` Primary / `FEAT-14` Secondary while keeping IDs `TEST-087..088` unchanged |
| 4 | Cross-cutting NFRs clearly identified | `PASS` | Dedicated `docs/TRACEABILITY.md` §2 maps all 15 `NFR-001..015` across quality domains, enforcement layers, affected features/screens, and tests |
| 5 | All test IDs (`TEST-001..088`, `TEST-ARCH-001..007`) are defined, `OPEN`, or `RESERVED` | `PASS` | 95/95 IDs accounted for: `TEST-001..019` (`RESERVED / OPEN`), `TEST-020..038` (`DEFINED (PROPOSAL)`), `TEST-039..040` (`OPEN`), `TEST-041..080` (`DEFINED`), `TEST-081..088` (`DEFINED (PROPOSAL)`), `TEST-ARCH-001..007` (`DEFINED`) |
| 6 | No test is represented as executed | `PASS` | `grep -nE '\| \`(PASS\|FAIL)\` \|$' docs/TEST_REGISTER.md` returned `0` matches; all 95 tests marked `NOT TESTED` |
| 7 | Tier 1/2/3 approval gates have clear phase dependencies | `PASS` | Tier 1 (`DEC-UX-01..05`) -> Phase C entry; Tier 2 (`ADR-004/005`, `DEC-ARCH-01..03`) -> Phase D finalization; Tier 3 (`ADR-008/009/010/014/015`) -> Backend/Cloud/GPU provisioning; Tier 4 -> `DEFERRED` |
| 8 | Original catalogue counts remain 412 occurrences and 264 unique repos | `PASS` | `grep` confirmed `docs/REPOSITORY_OCCURRENCES_412.csv` = `412` and `docs/REPOSITORY_UNIQUE_AUDIT.csv` = `264` (untouched) |
| 9 | No Android source/configuration files changed | `PASS` | Verified `/app/src/main/java/com/example` untouched (`0` app/Gradle/manifest/resource/`metadata.json` edits) |
| 10 | Markdown references and links are internally consistent | `PASS` | All referenced `docs/*.md`, `docs/*.csv`, and `docs/reports/*.md` paths verified (`AIVX-A0-INSPECT-001.md` explicitly marked `NOT AVAILABLE`) |

---

## 6. Phase B and Phase C Readiness Evaluation (`FACT`)

Phase B is **NOT marked complete** merely because decision entries exist. The five readiness dimensions stand as follows:

| Readiness Dimension | Status | Exact Basis |
|---|---|---|
| 1. Requirements audit completed | `PASS` | B0 + B1 + B1.1 reconciled all 12 ID families, spec headers, feature/test ownership, cross-cutting NFRs, and 412/264 CSV integrity without renumbering |
| 2. Requirements fully specified | `PARTIAL / OPEN` | Baseline FRs cover `PLATFORM-CORE`, `FEAT-01..03`, `FEAT-12`, `FEAT-13`, `FEAT-14`, `FEAT-15`; dedicated FRs/tests remain `OPEN` for `FEAT-04..11`, `PLATFORM-CORE` boundaries (`TEST-001..019`), NFR benchmarks, and Security QA |
| 3. User decisions approved | `OPEN` | `0` of Tier 1–3 open decisions approved yet (`docs/DECISION_LOG.md`) |
| 4. Later-phase decisions deferred | `DEFERRED` | Tier 4 (`ADR-012`, `ADR-017`, `DEC-DEF-01`, `DEC-DEF-02`) |
| 5. Phase C (UX/UI Design) entry readiness | **`BLOCKED / NOT READY`** | Blocked **only** on user approval of **Tier 1 (`DEC-UX-01..05`)** and confirming minimum FR readiness for any feature pulled into P0/P1 UX scope (`DEC-UX-01`). **Not** blocked on Tier 2 (`ADR-004/005`, `DEC-ARCH-01..03`) or Tier 3 (`ADR-008/009/010/014/015`), except that exact `SCR-01` sign-in button variants depend on `DEC-ARCH-03` when finalizing `SCR-01`. |

**Phase B Overall Status:** **`IN PROGRESS / NOT EXITED`**.

---

## 7. Verification Evidence (`FACT`)

Read-only verification commands executed after edits (no Android build or unit/UI tests executed — **`NOT TESTED`** for docs-only task):

1. `grep -cE '^[0-9]{3},https://' docs/REPOSITORY_OCCURRENCES_412.csv docs/REPOSITORY_UNIQUE_AUDIT.csv public/assets/aistudio/REPOSITORY_UNIQUE_AUDIT_616fcf9d.csv`
   - Output: `docs/REPOSITORY_OCCURRENCES_412.csv:412`, `docs/REPOSITORY_UNIQUE_AUDIT.csv:264`, `public/assets/aistudio/REPOSITORY_UNIQUE_AUDIT_616fcf9d.csv:264` (`PASS`).
2. `grep -nE 'FEAT-06|FEAT-08|DATA-002\.\.012|DATA-006\.\.013|API-010\.\.020|API-023\.\.030' docs/TRACEABILITY.md`
   - Output: confirmed `0` numeric-adjacency patterns (`DATA-002..012`, `DATA-006..013`, `API-010..020`, `API-023..030`) and verified clean `FEAT-06` and `FEAT-08` rows (`PASS`).
3. `grep -cE '^\| \`NFR-0[0-9]{2}\`' docs/TRACEABILITY.md` → `15` (`NFR-001..015` complete, `PASS`).
4. `grep -cE '^\| \`TEST-([0-9]{3}|ARCH-[0-9]{3})\`' docs/TEST_REGISTER.md` → `78` (`76` individual rows for `TEST-020..088` + `TEST-ARCH-001..007`, plus `2` single-ID summary rows for `TEST-039` and `TEST-040`; together with `19` reserved `TEST-001..019` in §2, all `95` test IDs are accounted for, `PASS`).
5. `grep -nE '\| \`(PASS|FAIL)\` \|$' docs/TEST_REGISTER.md` → `0` matches (no test marked executed, `PASS`).
6. `list_dir` on `/app/src/main/java/com/example` → untouched template (`MainActivity.kt`, `ui/`).
7. App build (`compile_applet`), lint (`lint_applet`), unit/Robolectric tests, and emulator/device tests → **`NOT TESTED`** (prohibited/out-of-scope for documentation-only task).

---

## 8. Recommended Next Bounded Task (`PROPOSAL`)

- **Task ID:** `AIVX-B2-DECISION-SIGNOFF-001`
- **Bounded Scope:** Present the **5 Tier 1 UX Decisions (`DEC-UX-01..05`)** simply to the owner, record the owner's explicit choices in `docs/DECISION_LOG.md`, `docs/PROJECT_STATUS.md`, and `docs/CHANGELOG.md`, and verify whether any under-specified feature (`FEAT-04..11`) is included in P0 UX scope (if yes, specify its minimum UX/FR contract before Phase C).
- **Why this order:** Unlocks **Phase C (UX/UI Design for `SCR-01..14`)** cleanly without forcing premature Tier 2 architecture (`ADR-004/005`, `DEC-ARCH-01..03`) or Tier 3 cloud/billing/GPU decisions (`ADR-008/009/010/014/015`), and without modifying any Android source code or creating any cloud resources.

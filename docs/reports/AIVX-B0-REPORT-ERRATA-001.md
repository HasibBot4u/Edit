# Errata & Post-Archive Reconciliation Supplement for `AIVX-B0-ANALYSIS-RECONCILE-001`

**Document ID:** AIVX-B0-ERRATA-001 · **Version:** 1.0 · **Date:** 2026-11-27 (Asia/Dhaka)  
**Target Archived Report:** `docs/reports/AIVX-B0-ANALYSIS-RECONCILE-001.md` *(preserved verbatim as immutable historical evidence)*  
**Produced By Task:** `AIVX-B1-DOC-CORRECTIONS-001`  
**Status:** `FACT` — Post-archive review errata and reconciliation status tracker

> **Historical Integrity Rule (`APPROVED`):** The archived report `docs/reports/AIVX-B0-ANALYSIS-RECONCILE-001.md` has **NOT** been silently rewritten or altered. All post-archive factual corrections and B1 status transitions are recorded transparently in this supplement.

---

## 1. Factual Errata in Archived B0 Report

| Erratum ID | B0 Report Location | Statement in Archived B0 Report | Verified Correction (`FACT`) |
|---|---|---|---|
| `ERR-B0-01` | Section A.1 (`FR` row) | Stated total defined `FR` count as **40** (`মোট 40টি`). | Actual verified count of defined `FR` entries in `docs/PRD_SRS.md` §6 is **41**: `FR-001..006` (6) + `FR-010..017` (8) + `FR-020..029` (10) + `FR-030..035` (6) + `FR-040..046` (7) + `FR-050..053` (4) = **41**. Unused reserved gaps (`FR-007..009`, `FR-018..019`, `FR-036..039`, `FR-047..049`) remain unchanged. |
| `ERR-B0-02` | Section F.1 (Criterion 3) | Marked Criterion 3 ("সব অনুমোদিত ফিচার (`FEAT-01..15`) + Platform Core-এর acceptance criteria ও security coverage যাচাই সম্পন্ন") as **`PASS`** without distinguishing *audit performed* from *coverage complete*. | Overstated as a Phase B exit readiness claim. While Section B audited every feature, Section B itself proved (`FACT`) that acceptance criteria and feature-level FRs/tests remain incomplete (`OPEN`) for `PLATFORM-CORE`, `FEAT-04`, `FEAT-05`, `FEAT-06`, `FEAT-07` (mixing/DSP), `FEAT-08` (shaping/animation), `FEAT-09`, `FEAT-10`, and `FEAT-11`. Audit completion = `PASS`; feature acceptance-criteria completeness = `PARTIAL / OPEN`. |
| `ERR-B0-03` | Section E (Row 11) | Recorded that Phase A (`AIVX-A0-INSPECT-001`) and Phase B (`AIVX-B0-ANALYSIS-RECONCILE-001`) results were not yet logged in `PROJECT_STATUS.md`, `PROJECT_MANIFEST.md`, and `CHANGELOG.md`. | Historically accurate at the moment B0 ran, but became outdated after the subsequent `AIVX-B0-REPORT-ARCHIVE-001` commit archived the B0 report and logged A0/B0 records in those three files (and further reconciled in `AIVX-B1-DOC-CORRECTIONS-001`). Note also that the full verbatim `AIVX-A0-INSPECT-001` report text is `NOT AVAILABLE` in the repository/session history and has not been fabricated. |
| `ERR-B0-04` | Section C.2 (`CSV allocated_app_module`) | Listed row-specific 2-digit legacy IDs (`API-01..23`, `DATA-01/09`, `NFR-01..03`, `SEC-05/07`, `TEST-01/02`) and proposed converting 2-digit IDs to 3-digit IDs, without calling out that bulk template IDs (`API-30..39`) also carried semantic mismatches against `docs/TRACEABILITY.md` (`API-030..039`), or that `#137 pitivi/pitivi` had an internal `evidence_status` vs `audit_depth` contradiction, or that the repeated CSV `license_policy` string is not a per-repo license audit. | Fully audited and corrected semantically in `AIVX-B1-DOC-CORRECTIONS-001`: every `API-*`, `DATA-*`, `NFR-*`, `SEC-*`, and `TEST-*` reference in `docs/REPOSITORY_UNIQUE_AUDIT.csv` was matched by actual meaning against `docs/TRACEABILITY.md` (with unresolved allocations marked `OPEN / NEEDS REVIEW`), `#137 pitivi/pitivi` was aligned to `Not directly verified`, and the generic `license_policy` caveat was added to `docs/REPOSITORY_AUDIT.md`. |

---

## 2. Status of Original B0 Findings After `AIVX-B1-DOC-CORRECTIONS-001`

### 2.1 Findings Corrected in B1 (`RESOLVED IN DOCS`)

1. **Header ID ceilings & omissions (`PRD_SRS.md`, `ARCHITECTURE.md`, `CANONICAL_PROJECT_MODEL.md`, `FEAT15_VISUAL_FEEDBACK.md`, `PROVIDER_GATEWAY.md`, `AI_AGENT_EDIT_PROTOCOL.md`, `SECURITY_THREAT_MODEL.md`, `RISK_REGISTER.md`):** Corrected to exact verified ranges (`41` FRs in `FR-001..053` with reserved gaps documented, `NFR-001..015`, `DATA-001..024`, `API-001..045`, `SEC-001..030`, `RISK-001..032`, `ADR-001..018`, `TEST-001..088`, `TEST-ARCH-001..007`). Removed `DATA-017` from `FEAT15_VISUAL_FEEDBACK.md` and narrowed `PROVIDER_GATEWAY.md` API references to `API-014, API-015, API-031, API-039`.
2. **Canonical Project Model entity mapping (`docs/CANONICAL_PROJECT_MODEL.md`):** Mapped §2 core entities to `DATA-001..024` and documented companion `DATA-*` entities and unassigned `Marker` as `OPEN` without inventing a production DB schema.
3. **Cross-document test register & traceability fixes (`docs/TEST_REGISTER.md`, `docs/TRACEABILITY.md`):** Created `docs/TEST_REGISTER.md`; added `PLATFORM-CORE` and `ARCHITECTURE-GATES` (`TEST-ARCH-001..007`) rows to `docs/TRACEABILITY.md`; removed incorrect `TEST-*` cross-references on `FEAT-06`, `FEAT-07`, `FEAT-09`, `FEAT-10`, and `FEAT-11`; defined FR-backed acceptance test specifications for `TEST-020..038` and `TEST-081..088` (all `NOT TESTED`); kept `TEST-001..019` `RESERVED / OPEN` and `TEST-039`, `TEST-040` `OPEN`.
4. **Repository audit & CSV reconciliation (`docs/REPOSITORY_UNIQUE_AUDIT.csv`, `docs/REPOSITORY_AUDIT.md`):** Reconciled 7 suspect entries (`#014`, `#043`, `#047`, `#140`, `#290`, `#362`, `#367`) as `BLOCKED / NEEDS SOURCE RECHECK` (`Not directly verified`); aligned `#137 pitivi/pitivi` (`Not directly verified`); reconciled legacy 2-digit and semantically mismatched IDs in `allocated_app_module`; separated `openreelio/openreelio` and `filmcraft-desktop/filmcraft` as non-catalogue `NOT VERIFIED` references; clarified `first_catalogue_number` as the CSV primary key and `license_policy` as a non-audit policy reminder.
5. **Documentation status, paths, manifest & dates (`docs/README.md`, `docs/PROJECT_STATUS.md`, `docs/PROJECT_MANIFEST.md`, `docs/CHANGELOG.md`, `docs/DECISION_LOG.md`):** Updated `docs/` paths, reconciled manifest with `docs/reports/` and `public/assets/aistudio/` snapshots, fixed Asia/Dhaka date consistency, preserved `CHANGELOG.md` history, recorded `AIVX-A0-INSPECT-001.md` as `NOT AVAILABLE`, and added the Open User Decision Matrix to `docs/DECISION_LOG.md`.

### 2.2 Findings Remaining `OPEN` (Require User Decisions or Future Phases)

1. **All Tier 1–4 Open User Decisions (`DEC-UX-01..05`, `ADR-004/005`, `DEC-ARCH-01..03`, `ADR-008/009/010/014/015`, `ADR-012/017`, `DEC-DEF-01..02`):** Remain **`OPEN — User Decision Required`** (or `DEFERRED` for Tier 4). None were selected on the user's behalf.
2. **Under-specified feature FRs & acceptance tests:** `PLATFORM-CORE (TEST-001..019)`, `FEAT-04 (TEST-039)`, `FEAT-05 (TEST-040)`, `FEAT-06`, `FEAT-07` (mixing/DSP), `FEAT-08` (shaping/animation), `FEAT-09`, `FEAT-10`, `FEAT-11`, and Security QA ID mapping remain `OPEN`.
3. **Unresolved canonical data relationships (`DATA-003/005/008/014..016/020/022..024` and `Marker`):** Remain `OPEN` for Phase D detailed schema design.
4. **Full repository source-code, license, build, and runtime verification:** All 264 unique repositories remain `NO — not executed` / `NOT INTEGRATED`; per-repository license audit remains `OUTSTANDING / NOT VERIFIED`; the 7 suspect entries plus previously blocked rows require direct upstream source inspection before any candidate adoption.
5. **Original verbatim `AIVX-A0-INSPECT-001` report:** Marked `NOT AVAILABLE` (only verified A0 summary facts exist in session/repo records).
6. **Account-level AI Studio UI confirmation & Robolectric SDK 36 failure:** Browser emulator, APK/AAB export, physical-device install controls, and container Robolectric SDK 36 HTTP fetch failure remain `OPEN`.

# PROJECT_MANIFEST

**Project:** AIVX — Private Online AI Video Editor  
**Date:** 2026-11-27 (Asia/Dhaka) · **Manifest version:** 1.3  
**Purpose:** Authoritative index of all project documents under `docs/`, archived reports under `docs/reports/`, immutable AI Studio upload snapshots under `public/assets/aistudio/`, and historical external upload-bundle references.

---

## 1. Authoritative Documentation (`docs/`)

| Path | Purpose | Status | Related IDs / Dependencies | Open questions |
|---|---|---|---|---|
| `docs/README.md` | Product context, repository layout, document index, post-B1 workflow | `ACTIVE` | All | Update with each phase |
| `docs/PROJECT_STATUS.md` | Current phase (`B — IN PROGRESS / NOT EXITED`), A0/B0/B1 evidence, verification matrix, next step | `ACTIVE` | All IDs; `AIVX-A0-INSPECT-001`; `AIVX-B0-ANALYSIS-RECONCILE-001`; `AIVX-B1-DOC-CORRECTIONS-001` | Pending Tier 1–3 user decisions to exit Phase B |
| `docs/PROJECT_MANIFEST.md` | Authoritative index of repo docs, reports, snapshots, and external refs | `ACTIVE` | All docs | Update on additions |
| `docs/AI_INSTRUCTIONS.md` | Persistent AI Build instructions | `ACTIVE` | AIVX-AI | Must be read each session |
| `docs/GOOGLE_AI_STUDIO_CUSTOM_INSTRUCTIONS.txt` | Copy/upload-ready persistent instruction content | `READY` | AIVX-AI | Verify custom instruction field and limit in active account |
| `docs/ORIGINAL_REPOSITORY_CATALOGUE.txt` | Original user source catalogue (412 numbered links, verbatim order) | `SOURCE` | 412 occurrences (`#001..412`) | Keep immutable |
| `docs/REPOSITORY_OCCURRENCES_412.csv` | Occurrence ledger with duplicates and original URLs preserved verbatim | `PASS / 412 rows` | 412 occurrences (`#001..412`) | Keep original URLs immutable |
| `docs/REPOSITORY_UNIQUE_AUDIT.csv` | One row per unique valid GitHub repo (264 rows), keyed by `first_catalogue_number` (`001..403`); reconciled in B1 | `PARTIAL SOURCE AUDIT / 264 rows` | `first_catalogue_number` (`001..403`), `FEAT-*`, `API-*`, `DATA-*`, `NFR-*`, `SEC-*` | Full source audit, per-repo license audit, build verification, and blocked/suspect repo rechecks remain `OPEN` |
| `docs/REPOSITORY_AUDIT.md` | Specialty allocation, candidate roles, non-catalogue external refs (`openreelio`, `filmcraft-desktop`), evidence & license caveats | `PARTIAL SOURCE AUDIT` | `first_catalogue_number`, `FEAT-*` | Clone/inspect/test priority repos one at a time |
| `docs/PRD_SRS.md` | Product vision, scope, journeys, 41 defined FRs (`FR-001..053` grouped), `NFR-001..015` | `BASELINE` | `FEAT-01..15`, `FR-001..053` (41 defined), `NFR-001..015`, `SCR-01..14`, `DATA-001..024`, `API-001..045`, `SEC-001..030`, `TEST-001..088`, `TEST-ARCH-001..007` | P0 prioritization (`DEC-UX-01`) and under-specified feature FRs (`FEAT-04..11`) remain `OPEN` |
| `docs/ARCHITECTURE.md` | Native client / cloud control plane / workers architecture & `TEST-ARCH-001..007` | `PROPOSAL` | `ADR-001..018`, `FEAT-01..15`, `FR-001..053`, `NFR-001..015`, `DATA-001..024`, `API-001..045`, `SEC-001..030`, `TEST-001..088`, `TEST-ARCH-001..007`, `RISK-001..032` | Cloud vendor/region, engine, DB, auth, GPU policy (`ADR-004/005/009/010/015`, `DEC-ARCH-01..03`) remain `OPEN` |
| `docs/CANONICAL_PROJECT_MODEL.md` | Canonical editable project entities (`DATA-001..024`), rational timebase & typed commands | `PROPOSAL` | `DATA-001..024`, `API-001..045`, `ADR-003..005`, `TEST-020..039` | Final DB/engine schema and companion entity relationships (`DATA-003/005/008/014..016/020/022..024`, `Marker`) remain `OPEN` |
| `docs/FEAT15_VISUAL_FEEDBACK.md` | Visual region anchors, independent comments, batch Run & `TEST-041..052` | `APPROVED REQUIREMENT / PROPOSAL DESIGN` | `FEAT-15`, `FR-020..029`, `SCR-08`, `SCR-09`, `DATA-011/012/014..016/018..022`, `API-021..030`, `SEC-009..015`, `TEST-041..052`, `ADR-006` | Confidence thresholds and touch tolerance (`DEC-UX-04`) remain `OPEN` |
| `docs/PROVIDER_GATEWAY.md` | BYOK profile, protocol adapters, capability manifests, SSRF/vault rules & `TEST-060..069` | `PROPOSAL` | `FEAT-13/14/15`, `DATA-017`, `API-014/015/031/039`, `SEC-001..008/010..012/017..019`, `TEST-060..069` | Adapter set (`DEC-ARCH-02`) and vault impl (`ADR-008`) remain `OPEN` |
| `docs/AI_AGENT_EDIT_PROTOCOL.md` | Typed tools, dry-run, approval, atomic apply, QC, undo & `TEST-053..059` | `PROPOSAL` | `FEAT-13/14/15`, `API-018..030`, `DATA-018..024`, `SEC-009..020`, `TEST-053..059` | Tool catalogue versioning and thresholds remain `OPEN` |
| `docs/EXPORT_INTERCHANGE.md` | Rendered media, editable interchange formats, loss reports & `TEST-070..080` | `PROPOSAL` | `FEAT-12`, `DATA-001..024`, `API-040..045`, `TEST-070..080`, `RISK-016` | First destination editor beyond MP4/OTIO (`ADR-012` — `DEFERRED`) |
| `docs/SECURITY_THREAT_MODEL.md` | Data assets, trust boundaries, threats, `SEC-001..030` and QA matrix | `REQUIRED BEFORE RELEASE` | `SEC-001..030`, `NFR-001..015`, `DATA-001..024`, `RISK-001..032` | Retention/provider consent (`ADR-014`) and Security QA test IDs remain `OPEN` |
| `docs/RISK_REGISTER.md` | Technical, cost, privacy, and compatibility risks (`RISK-001..032`) | `OPEN` | `RISK-001..032` | Mitigations and verification gates remain `OPEN` |
| `docs/DECISION_LOG.md` | `ADR-001..018` + Tier 1–4 Open User Decision Register (`DEC-UX-01..05`, `DEC-ARCH-01..03`, `DEC-DEF-01..02`) | `ACTIVE` | `ADR-001..018`, `DEC-UX-01..05`, `DEC-ARCH-01..03`, `DEC-DEF-01..02` | All Tier 1–3 decisions require explicit user approval (`OPEN`) |
| `docs/TRACEABILITY.md` | Reconciled feature & `PLATFORM-CORE` → FR/NFR/SCR/DATA/API/SEC/TEST mapping | `BASELINE` | `FEAT-01..15`, `PLATFORM-CORE`, `ARCHITECTURE-GATES`, `FR-001..053`, `SCR-01..14`, `DATA-001..024`, `API-001..045`, `SEC-001..030`, `TEST-001..088`, `TEST-ARCH-001..007` | Implementation links and `OPEN` feature test definitions to be added per phase |
| `docs/TEST_REGISTER.md` | Cross-document test definition register (`TEST-001..088`, `TEST-ARCH-001..007`) | `BASELINE / NOT TESTED` | `TEST-001..088`, `TEST-ARCH-001..007`, `FR-001..053` | `TEST-001..019` `RESERVED/OPEN`; `TEST-039..040` and `FEAT-06..11` tests `OPEN`; `0` tests executed |
| `docs/CHANGELOG.md` | Chronological decision and documentation history (Asia/Dhaka timezone noted) | `ACTIVE` | All | Append only; preserve historical entries |

---

## 2. Archived Task Reports (`docs/reports/`)

| Path | Purpose | Status | Related IDs / Dependencies | Notes |
|---|---|---|---|---|
| `docs/reports/AIVX-A0-INSPECT-001.md` | Full verbatim Phase A0 workspace & capability inspection report | `NOT AVAILABLE` | `AIVX-A0-INSPECT-001`, `ADR-013` | Original verbatim Turn-1 output is unavailable in session/repo history and was **not** reconstructed; verified A0 facts are recorded in `docs/PROJECT_STATUS.md` and `docs/CHANGELOG.md` |
| `docs/reports/AIVX-B0-ANALYSIS-RECONCILE-001.md` | Archived Phase B0 requirements, ID integrity, repository audit, open decision register, and doc correction proposal report | `ARCHIVED REPORT` *(immutable)* | `AIVX-B0-ANALYSIS-RECONCILE-001`, All IDs | Preserved verbatim; see `docs/reports/AIVX-B0-REPORT-ERRATA-001.md` for post-archive errata and B1 status |
| `docs/reports/AIVX-B0-REPORT-ERRATA-001.md` | Post-archive errata supplement for B0 report (FR count 41, F.1 Criterion 3 overstatement, archive timing, CSV bulk IDs) | `ARCHIVED SUPPLEMENT / FACT` | `AIVX-B0-ANALYSIS-RECONCILE-001`, `AIVX-B1-DOC-CORRECTIONS-001` | Preserves immutable B0 history while correcting factual counts/status |
| `docs/reports/AIVX-B1-DOC-CORRECTIONS-001.md` | Phase B1 documentation, ID, canonical model, test register, traceability, and CSV reconciliation completion report | `ARCHIVED REPORT / FACT` | `AIVX-B1-DOC-CORRECTIONS-001`, All IDs | Documentation-only task; `0` app source/config files changed; Phase B remains `NOT EXITED` pending user decisions |

---

## 3. Immutable AI Studio Upload Snapshots (`public/assets/aistudio/`)

| Path | Purpose | Status | Notes |
|---|---|---|---|
| `public/assets/aistudio/AI_STUDIO_UPLOAD_MASTER_2a4612b0.html` | Session upload snapshot of consolidated pre-repo HTML master | `IMMUTABLE SNAPSHOT` | Preserved untouched as archival session evidence; authoritative docs live under `docs/` |
| `public/assets/aistudio/REPOSITORY_OCCURRENCES_412_a17f05e9.csv` | Session upload snapshot of 412-row occurrence CSV | `IMMUTABLE SNAPSHOT` | Preserved untouched; matches `docs/REPOSITORY_OCCURRENCES_412.csv` verbatim |
| `public/assets/aistudio/REPOSITORY_UNIQUE_AUDIT_616fcf9d.csv` | Session upload snapshot of pre-B1 264-row unique audit CSV | `IMMUTABLE SNAPSHOT` | Preserved untouched as pre-B1 baseline; authoritative reconciled CSV is `docs/REPOSITORY_UNIQUE_AUDIT.csv` |

---

## 4. Historical External Upload-Bundle Artefacts (Outside `docs/`)

| Name | Purpose | Status | Related IDs / Dependencies | Notes |
|---|---|---|---|---|
| `GOOGLE_AI_STUDIO_MASTER_BUILD_PROMPT.txt` *(external upload bundle)* | Bounded first Build task: inspect/verify/report | `EXECUTED` (`AIVX-A0-INSPECT-001`) | `AIVX-A0-INSPECT-001` | Historical prompt artefact outside repo `docs/` |
| `REPOSITORY_REGISTER_SUMMARY.md` *(external upload bundle)* | Pre-repo counts, evidence status and next audit method | `EXTERNAL REFERENCE` | Catalogue summary | Historical upload-bundle summary outside repo `docs/` |
| `ALL_PROJECT_DOCS.md` *(external upload bundle)* | Consolidated pre-repo Markdown bundle | `EXTERNAL REFERENCE` | All docs | Regenerate only if consolidated export requested |
| `AI_STUDIO_UPLOAD_MASTER.html` *(external upload bundle)* | Consolidated pre-repo searchable HTML | `EXTERNAL REFERENCE` | All docs | Archived snapshot stored under `public/assets/aistudio/` |
| `UPLOAD_GUIDE.txt` *(external upload bundle)* | Phone-first attachment steps for pre-repo AI Studio sessions | `EXTERNAL REFERENCE` | Google AI Studio prompts | Historical guide outside repo `docs/` |
| `PACKAGE_VERIFICATION.json` *(external upload bundle)* | Pre-repo file inventory, hashes, row counts | `EXTERNAL REFERENCE` | All files | Historical bundle metadata outside repo `docs/` |

---

## 5. Status Meanings

- `SOURCE`: Original user-provided source; preserve verbatim.
- `IMMUTABLE SNAPSHOT`: Session upload snapshot under `public/assets/aistudio/`; preserve untouched.
- `ACTIVE`: Authoritative maintained document under `docs/`.
- `ARCHIVED REPORT` / `ARCHIVED SUPPLEMENT`: Immutable completed task/audit evidence archived in `docs/reports/`.
- `NOT AVAILABLE`: Expected historical artefact whose exact verbatim text is unavailable and not fabricated.
- `APPROVED REQUIREMENT`: User-approved capability/scope, not implemented.
- `BASELINE`: Established requirements/register for future build.
- `PROPOSAL`: Technical design or test/decision plan recommended but not approved as final.
- `PARTIAL SOURCE AUDIT`: Evidence available but not exhaustive source/build/license review.
- `READY`: Prepared for use/upload; not yet executed.
- `EXECUTED`: Bounded prompt task completed; results recorded in `docs/PROJECT_STATUS.md`.
- `EXTERNAL REFERENCE`: Pre-repo upload-bundle artefact not stored inside `docs/`.
- `NOT TESTED`: No runtime/execution evidence exists.

## 6. Document Control Rules

Every material change must update `docs/PROJECT_STATUS.md`, `docs/CHANGELOG.md`, and where relevant this manifest, `docs/DECISION_LOG.md`, `docs/RISK_REGISTER.md`, `docs/TRACEABILITY.md`, and `docs/TEST_REGISTER.md`. Preserve `docs/ORIGINAL_REPOSITORY_CATALOGUE.txt`, `docs/REPOSITORY_OCCURRENCES_412.csv`, `public/assets/aistudio/*`, and archived reports under `docs/reports/`. Never renumber existing IDs, never fabricate unavailable reports, and never mark a feature as implemented or tested without evidence.

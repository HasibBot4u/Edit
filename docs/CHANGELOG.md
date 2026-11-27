# CHANGELOG

All notable project documentation and decision changes are recorded here in chronological order (oldest to newest). Dates use `YYYY-MM-DD` normalized to **Asia/Dhaka (UTC+6)** unless explicitly noted as historical pre-repo baseline entries. Prior entries are preserved verbatim for auditability.

---

## 2026-11-25 — User decisions recorded *(historical pre-repo baseline)*

- Native Android app direction (Kotlin + Jetpack Compose preferred) confirmed.
- Online-only processing selected.
- Visual circle/point/time-range comments and batch Run feature accepted as a product requirement.
- Private use only; no public business or monetization scope.

## 2026-11-26 — Pre-build catalogue and specification update *(historical pre-repo baseline)*

- Re-read the original 412-entry user-supplied repository catalogue from first to last.
- Reconciled 410 well-formed GitHub owner/repo paths, 264 unique GitHub repositories, duplicate identities and non-GitHub/malformed entries.
- Preserved original link order/duplicates in `REPOSITORY_OCCURRENCES_412.csv`.
- Updated 264-row unique allocation/evidence ledger and corrected 53 vague specialty assignments based on README evidence.
- Added full PRD/SRS, architecture, canonical project model, FEAT-15, provider gateway, AI edit protocol, export/interchange, security, repository audit, risk register, decision log and traceability.
- Added separate Google AI Studio Custom Instructions and bounded Master Build Prompt; added one-file HTML and consolidated Markdown for upload without ZIP.
- No app code, Android package, cloud service, bucket, GPU, provider credential or repository integration created.
- All repository builds/runtime tests remain NOT TESTED; full source-level audit of all 264 repos remains incomplete.

## 2026-11-26 — Final upload formats and QA *(historical pre-repo baseline)*

- Added consolidated `ALL_PROJECT_DOCS.md` and `AI_STUDIO_UPLOAD_MASTER.html`; the HTML master contains all principal specifications, prompt files, original catalogue and both CSV tables.
- Added `UPLOAD_GUIDE.txt` with phone-first Google AI Studio attachment steps.
- Added `PACKAGE_VERIFICATION.json` with CSV row counts, file hashes and explicit incomplete audit/build states.
- Verified HTML parsing and CSV occurrence/unique row counts.
- Built an optional ZIP backup for personal storage only; Google AI Studio upload should use TXT/HTML/CSV/MD files, not ZIP.
- No app/cloud code, service, storage bucket, GPU or repository integration was created.

## 2026-11-26 (Asia/Dhaka; originally logged as 2026-11-25 PST) — Phase A0 inspection, verbatim `docs/` import, and B0 report archive (`AIVX-B0-REPORT-ARCHIVE-001`)

- Recorded completion of `AIVX-A0-INSPECT-001`: verified native Android Kotlin + Jetpack Compose template workspace (`AGP 9.1.1`, `Gradle 9.3.1`, `Kotlin 2.4.21`, `KSP 2.3.5`, `Compose BOM 2024.09.00`, `compileSdk = 36`, `targetSdk = 36`, `minSdk = 24`, `namespace/applicationId = com.example`). Baseline A0 checks: standalone `compile_applet` = `PASS`; `gradle :app:testDebugUnitTest` = `1 PASS / 1 FAIL` (`ExampleUnitTest` = `PASS`; `ExampleRobolectricTest` SDK 36 = `FAIL` due to container HTTP fetch error); `lint_applet` = `NOT TESTED`; `androidTest`/emulator/`adb` = `BLOCKED`.
- Saved all 21 verbatim baseline source-of-truth documents and CSV ledgers into `docs/` without altering their content.
- Archived the exact completed `AIVX-B0-ANALYSIS-RECONCILE-001` reconciliation report at `docs/reports/AIVX-B0-ANALYSIS-RECONCILE-001.md`.
- Updated `docs/PROJECT_STATUS.md`, `docs/PROJECT_MANIFEST.md`, and `docs/CHANGELOG.md` to reflect the `docs/` repository layout, A0 inspection results, archived B0 report, and `OPEN` / pending-review status of proposed Section E documentation corrections.
- No requirement-ID corrections, repository classification edits, Android app source/Gradle/manifest/resource modifications, or Firebase/cloud/billing/GPU resources were made. No builds or tests were run for this documentation-only change (`NOT TESTED`).

## 2026-11-27 (Asia/Dhaka) — Phase B1 documentation, ID, test-register, canonical model, and repository-audit reconciliation (`AIVX-B1-DOC-CORRECTIONS-001`)

- **Requirement & design ID reconciliation:** Corrected overstated/incomplete header ranges across `docs/PRD_SRS.md` (`41` defined FRs across `FR-001..053` with documented reserved gaps, `NFR-001..015`, `DATA-001..024`, `TEST-001..088`, `TEST-ARCH-001..007`), `docs/ARCHITECTURE.md` (`ADR-001..018`, `RISK-001..032`, non-catalogue label on `filmcraft-desktop/filmcraft`), `docs/CANONICAL_PROJECT_MODEL.md`, `docs/FEAT15_VISUAL_FEEDBACK.md` (removed unrelated `DATA-017`), `docs/PROVIDER_GATEWAY.md` (`API-014, API-015, API-031, API-039`, `DATA-017`), `docs/AI_AGENT_EDIT_PROTOCOL.md`, `docs/SECURITY_THREAT_MODEL.md`, and `docs/RISK_REGISTER.md`. Zero existing IDs were renumbered and zero FRs were invented.
- **Canonical project model:** Mapped core entities in `docs/CANONICAL_PROJECT_MODEL.md` §2 to `DATA-001..024` and documented companion entities (`DATA-003/005/008/014..016/020/022..024`) and unassigned `Marker` relationships as `OPEN` without creating a production DB schema.
- **Cross-document test register & traceability:** Created `docs/TEST_REGISTER.md` (defining FR-backed `TEST-020..038` and `TEST-081..088`, indexing `TEST-041..080` and `TEST-ARCH-001..007`, reserving `TEST-001..019`, and marking `TEST-039`, `TEST-040`, and under-specified feature acceptance criteria `OPEN` — all `NOT TESTED`). Reconciled `docs/TRACEABILITY.md` by adding `PLATFORM-CORE` and `ARCHITECTURE-GATES` rows and removing erroneous `TEST-*` cross-links on `FEAT-06`, `FEAT-07`, `FEAT-09`, `FEAT-10`, and `FEAT-11`.
- **Repository audit & CSV reconciliation:** Preserved `docs/REPOSITORY_OCCURRENCES_412.csv` (412 rows) and `docs/ORIGINAL_REPOSITORY_CATALOGUE.txt` untouched. Reconciled `docs/REPOSITORY_UNIQUE_AUDIT.csv` (preserving all 264 unique identities, `first_catalogue_number` keys, and original URLs verbatim): marked 7 suspect copy-paste/contradictory entries (`#014`, `#043`, `#047`, `#140`, `#290`, `#362`, `#367`) as `BLOCKED / NEEDS SOURCE RECHECK` (`Not directly verified`), aligned `#137 pitivi/pitivi` (`Not directly verified`), and corrected legacy 2-digit and semantically mismatched `allocated_app_module` IDs against `docs/TRACEABILITY.md`. Updated `docs/REPOSITORY_AUDIT.md` to clarify `first_catalogue_number` as CSV primary key, separate non-catalogue `NOT VERIFIED` references (`openreelio/openreelio`, `filmcraft-desktop/filmcraft`), and document that the generic CSV `license_policy` string is not a per-repo license audit (`OUTSTANDING / NOT VERIFIED`).
- **B0 errata, decision register & status/manifest sync:** Preserved `docs/reports/AIVX-B0-ANALYSIS-RECONCILE-001.md` verbatim and created post-archive errata `docs/reports/AIVX-B0-REPORT-ERRATA-001.md` (documenting actual 41 FR count, Criterion 3 overstatement, archive timing, and bulk CSV IDs). Expanded `docs/DECISION_LOG.md` with Tier 1–4 Open User Decision Register (`OPEN — User Decision Required`, choosing nothing on the user's behalf). Updated `docs/README.md`, `docs/PROJECT_MANIFEST.md` (including `docs/reports/` and immutable `public/assets/aistudio/` snapshots; marking `docs/reports/AIVX-A0-INSPECT-001.md` `NOT AVAILABLE`), and `docs/PROJECT_STATUS.md` (Phase B remains `IN PROGRESS / NOT EXITED`). Archived completion report at `docs/reports/AIVX-B1-DOC-CORRECTIONS-001.md`.
- **Verification boundary:** Documentation-only change. Zero Android app source, XML, Gradle, manifest, resource, or `metadata.json` files were modified; zero cloud, Firebase, GPU, or billing resources were created; no app build or unit/UI tests were run (`NOT TESTED`).

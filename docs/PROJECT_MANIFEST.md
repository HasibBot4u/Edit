# PROJECT_MANIFEST

**Project:** AIVX — Private Online AI Video Editor  
**Date:** 2026-11-25 (baseline manifest dated 2026-11-26) · **Manifest version:** 1.2  
**Purpose:** authoritative index of project documents, status, ownership and dependencies under `docs/`.

| Path | Purpose | Status | Related IDs / Dependencies | Open questions |
|---|---|---|---|---|
| `docs/README.md` | Product context, upload instructions, document index | ACTIVE | All | Update with each phase |
| `docs/PROJECT_STATUS.md` | Current phase, decisions, risks, verified build/tests, next step | ACTIVE | All IDs; `AIVX-A0-INSPECT-001`; `AIVX-B0-ANALYSIS-RECONCILE-001` | Pending B1 doc corrections and Tier 1-3 decisions |
| `docs/PROJECT_MANIFEST.md` | Authoritative doc index | ACTIVE | All docs | Update on additions |
| `docs/AI_INSTRUCTIONS.md` | Persistent AI Build instructions | ACTIVE | AIVX-AI | Must be read each session |
| `docs/GOOGLE_AI_STUDIO_CUSTOM_INSTRUCTIONS.txt` | Copy/upload-ready persistent instruction content | READY | AIVX-AI | Check actual custom instruction field and limit |
| `docs/ORIGINAL_REPOSITORY_CATALOGUE.txt` | User source catalogue, original 412 order | SOURCE | REPO-001..REPO-264 | Keep immutable |
| `docs/REPOSITORY_OCCURRENCES_412.csv` | Occurrence ledger with duplicates intact | PASS / 412 rows | REPO-001..REPO-264 | Revalidate URL corrections when needed |
| `docs/REPOSITORY_UNIQUE_AUDIT.csv` | One row per unique valid GitHub repo with allocation/evidence | PARTIAL SOURCE AUDIT / 264 rows | REPO-001..REPO-264 | Full source audit, build verification, and B0 suspect-entry rechecks pending approval |
| `docs/REPOSITORY_AUDIT.md` | Specialty allocation, candidate roles, evidence/limitations | PARTIAL | REPO, FEAT | Clone/test priority repositories; B0 non-catalogue separation pending approval |
| `docs/PRD_SRS.md` | Product vision, scope, journeys, FR/NFR and phases | BASELINE | FR/NFR/FEAT/SCR/TEST | Prioritization and B0 header/gap corrections pending approval |
| `docs/ARCHITECTURE.md` | Native client/cloud/services/worker architecture | PROPOSAL | ADR/API/DATA/SEC | Cloud vendor/engine/database; B0 header corrections pending approval |
| `docs/CANONICAL_PROJECT_MODEL.md` | Project/timeline/asset/layer/operation data contract | PROPOSAL | DATA/API | Final model, migration plan, and B0 DATA/TEST corrections pending approval |
| `docs/FEAT15_VISUAL_FEEDBACK.md` | Visual anchor comments and batch Run workflow | APPROVED REQUIREMENT / PROPOSAL DESIGN | FEAT-15/SCR-08/09 | Prototype thresholds and UI details; B0 header correction pending approval |
| `docs/PROVIDER_GATEWAY.md` | BYOK profile, protocol adapters, capability manifests and key storage | PROPOSAL | FEAT-13/API/SEC | Provider formats and vault; B0 API header correction pending approval |
| `docs/AI_AGENT_EDIT_PROTOCOL.md` | Typed tools, dry-run, approval, atomic apply, QC and undo | PROPOSAL | FEAT-13/15/API/SEC | Thresholds and tool catalogue |
| `docs/EXPORT_INTERCHANGE.md` | Rendered media and editable project formats/loss reports | PROPOSAL | FEAT-12/API/TEST | First destination editor |
| `docs/SECURITY_THREAT_MODEL.md` | Data assets, trust boundaries, threats, controls and tests | REQUIRED BEFORE RELEASE | SEC/RISK/TEST | Retention/provider policies; B0 header corrections pending approval |
| `docs/RISK_REGISTER.md` | Technical/cost/privacy/compatibility risks | OPEN | RISK | Mitigations and owners; B0 header correction pending approval |
| `docs/DECISION_LOG.md` | Approved, proposed, open decisions | ACTIVE | ADR | Record every user approval |
| `docs/TRACEABILITY.md` | Feature→requirements→screens/data/API/security/tests | BASELINE | FEAT/FR/NFR/SCR/DATA/API/SEC/TEST | Add implementation links as built; B0 mapping/TEST corrections pending approval |
| `docs/CHANGELOG.md` | Decision/document change history | ACTIVE | All | Append, do not overwrite |
| `docs/reports/AIVX-B0-ANALYSIS-RECONCILE-001.md` | Archived Phase B0 requirements, ID integrity, repository audit, open decision register and doc correction proposal report | ARCHIVED REPORT / PROPOSAL | `AIVX-B0-ANALYSIS-RECONCILE-001`, `AIVX-A0-INSPECT-001`, FR/NFR/FEAT/SCR/DATA/API/SEC/TEST/BUG/RISK/ADR/REPO | Corrections proposed in Section E are pending explicit user review/approval (`OPEN`) |
| `GOOGLE_AI_STUDIO_MASTER_BUILD_PROMPT.txt` *(external upload bundle — not in `docs/`)* | Bounded first Build task: inspect/verify/report | EXECUTED (`AIVX-A0-INSPECT-001`) | `AIVX-A0-INSPECT-001` | Historical prompt artefact outside repo `docs/` |
| `REPOSITORY_REGISTER_SUMMARY.md` *(external upload bundle — not in `docs/`)* | Counts, evidence status and next audit method | EXTERNAL REFERENCE | REPO | Historical upload-bundle summary outside repo `docs/` |
| `ALL_PROJECT_DOCS.md` *(external upload bundle — not in `docs/`)* | Consolidated Markdown for AI Studio upload/reference | EXTERNAL REFERENCE | All docs | Regenerate only if consolidated export needed |
| `AI_STUDIO_UPLOAD_MASTER.html` *(external upload bundle — not in `docs/`)* | Consolidated searchable HTML in a single supported file | EXTERNAL REFERENCE | All docs | Original session upload source outside repo `docs/` |
| `UPLOAD_GUIDE.txt` *(external upload bundle — not in `docs/`)* | Phone-first steps for attaching supported files in Google AI Studio | EXTERNAL REFERENCE | Google AI Studio prompts | Historical upload guide outside repo `docs/` |
| `PACKAGE_VERIFICATION.json` *(external upload bundle — not in `docs/`)* | File inventory, hashes, row counts and ZIP check status | EXTERNAL REFERENCE | All files | Regenerate only if external bundle updated |

## Status meanings

- `SOURCE`: original user-provided source; preserve verbatim.
- `ACTIVE`: authoritative maintained document.
- `ARCHIVED REPORT`: immutable completed task/audit evidence archived in `docs/reports/`.
- `APPROVED REQUIREMENT`: user-approved capability/scope, not implemented.
- `BASELINE`: established requirements/data for future build.
- `PROPOSAL`: technical design or correction plan recommended but not approved as final.
- `PARTIAL SOURCE AUDIT`: evidence available but not exhaustive source/build review.
- `READY`: prepared for use/upload; not yet executed.
- `EXECUTED`: bounded prompt task completed; results recorded in `docs/PROJECT_STATUS.md`.
- `EXTERNAL REFERENCE`: pre-repo upload-bundle artefact not stored inside `docs/`.
- `NOT TESTED`: no runtime evidence exists.

## Document control rules

Every material change must update `PROJECT_STATUS.md`, `CHANGELOG.md`, and where relevant this manifest, decision/risk logs and traceability. Preserve the original user catalogue. Never replace a source link silently. Never mark a feature as implemented based on a prompt or mockup.

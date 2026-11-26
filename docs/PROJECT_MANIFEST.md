# PROJECT_MANIFEST

**Project:** AIVX — Private Online AI Video Editor  
**Date:** 2026-11-26 · **Manifest version:** 1.1  
**Purpose:** authoritative index of project documents, status, ownership and dependencies.

| Path | Purpose | Status | Related IDs / Dependencies | Open questions |
|---|---|---|---|---|
| `README.md` | Product context, upload instructions, document index | ACTIVE | All | Update with each phase |
| `PROJECT_STATUS.md` | Current phase, decisions, risks, verified build/tests, next step | ACTIVE | All IDs | Current Build-mode evidence |
| `PROJECT_MANIFEST.md` | Authoritative doc index | ACTIVE | All docs | Update on additions |
| `AI_INSTRUCTIONS.md` | Persistent AI Build instructions | ACTIVE | AIVX-AI | Must be attached/read each session |
| `GOOGLE_AI_STUDIO_CUSTOM_INSTRUCTIONS.txt` | Copy/upload-ready persistent instruction content | READY | AIVX-AI | Check actual custom instruction field and limit |
| `GOOGLE_AI_STUDIO_MASTER_BUILD_PROMPT.txt` | Bounded first Build task: inspect/verify/report | READY | AIVX-A0-INSPECT-001 | Must be executed in Build mode |
| `ORIGINAL_REPOSITORY_CATALOGUE.txt` | User source catalogue, original 412 order | SOURCE | REPO-001..REPO-264 | Keep immutable |
| `REPOSITORY_OCCURRENCES_412.csv` | Occurrence ledger with duplicates intact | PASS / 412 rows | REPO-001..REPO-264 | Revalidate URL corrections when needed |
| `REPOSITORY_UNIQUE_AUDIT.csv` | One row per unique valid GitHub repo with allocation/evidence | PARTIAL SOURCE AUDIT / 264 rows | REPO-001..REPO-264 | Full source audit and build verification outstanding |
| `REPOSITORY_REGISTER_SUMMARY.md` | Counts, evidence status and next audit method | ACTIVE | REPO | Refresh if catalogue changes |
| `REPOSITORY_AUDIT.md` | Specialty allocation, candidate roles, evidence/limitations | PARTIAL | REPO, FEAT | Clone/test priority repositories |
| `PRD_SRS.md` | Product vision, scope, journeys, FR/NFR and phases | BASELINE | FR/NFR/FEAT/SCR/TEST | Prioritization still open |
| `ARCHITECTURE.md` | Native client/cloud/services/worker architecture | PROPOSAL | ADR/API/DATA/SEC | Cloud vendor/engine/database |
| `CANONICAL_PROJECT_MODEL.md` | Project/timeline/asset/layer/operation data contract | PROPOSAL | DATA/API | Final model and migration plan |
| `FEAT15_VISUAL_FEEDBACK.md` | Visual anchor comments and batch Run workflow | APPROVED REQUIREMENT / PROPOSAL DESIGN | FEAT-15/SCR-08/09 | Prototype thresholds and UI details |
| `PROVIDER_GATEWAY.md` | BYOK profile, protocol adapters, capability manifests and key storage | PROPOSAL | FEAT-13/API/SEC | Provider formats and vault |
| `AI_AGENT_EDIT_PROTOCOL.md` | Typed tools, dry-run, approval, atomic apply, QC and undo | PROPOSAL | FEAT-13/15/API/SEC | Thresholds and tool catalogue |
| `EXPORT_INTERCHANGE.md` | Rendered media and editable project formats/loss reports | PROPOSAL | FEAT-12/API/TEST | First destination editor |
| `SECURITY_THREAT_MODEL.md` | Data assets, trust boundaries, threats, controls and tests | REQUIRED BEFORE RELEASE | SEC/RISK/TEST | Retention/provider policies |
| `RISK_REGISTER.md` | Technical/cost/privacy/compatibility risks | OPEN | RISK | Mitigations and owners |
| `DECISION_LOG.md` | Approved, proposed, open decisions | ACTIVE | ADR | Record every user approval |
| `TRACEABILITY.md` | Feature→requirements→screens/data/API/security/tests | BASELINE | FEAT/FR/NFR/SCR/DATA/API/SEC/TEST | Add implementation links as built |
| `CHANGELOG.md` | Decision/document change history | ACTIVE | All | Append, do not overwrite |
| `ALL_PROJECT_DOCS.md` | Consolidated Markdown for AI Studio upload/reference | READY | All docs | Regenerate after changes |
| `AI_STUDIO_UPLOAD_MASTER.html` | Consolidated searchable HTML in a single supported file | READY | All docs | Regenerate after changes |
| `UPLOAD_GUIDE.txt` | Phone-first steps for attaching supported files in Google AI Studio | READY | Google AI Studio prompts | Verify active UI/file limits |
| `PACKAGE_VERIFICATION.json` | File inventory, hashes, row counts and ZIP check status | GENERATED | All files | Regenerate after any edit |

## Status meanings

- `SOURCE`: original user-provided source; preserve verbatim.
- `ACTIVE`: authoritative maintained document.
- `APPROVED REQUIREMENT`: user-approved capability/scope, not implemented.
- `BASELINE`: established requirements/data for future build.
- `PROPOSAL`: technical design recommended but not approved as final.
- `PARTIAL SOURCE AUDIT`: evidence available but not exhaustive source/build review.
- `READY`: prepared for use/upload; not yet executed.
- `NOT TESTED`: no runtime evidence exists.

## Document control rules

Every material change must update `PROJECT_STATUS.md`, `CHANGELOG.md`, and where relevant this manifest, decision/risk logs and traceability. Preserve the original user catalogue. Never replace a source link silently. Never mark a feature as implemented based on a prompt or mockup.

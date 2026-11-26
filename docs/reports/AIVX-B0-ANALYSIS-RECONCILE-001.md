# AIVX — Phase B Requirements Analysis & Documentation Integrity Report

**Task ID:** `AIVX-B0-ANALYSIS-RECONCILE-001`  
**Phase:** B — Requirements Analysis and Documentation Integrity  
**Status:** `PROPOSAL` (Audit ও Correction Plan প্রস্তুত; কোনো ডকুমেন্টে এখনো সংশোধন প্রয়োগ করা হয়নি এবং কোনো app source code পরিবর্তন করা হয়নি)  
**Verification Basis:** কেবল আপলোড করা ২১টি source-of-truth ডকুমেন্ট, ২টি CSV ledger এবং আগের `AIVX-A0-INSPECT-001` রিপোর্টের উপর ভিত্তি করে (`FACT`). কোনো repository source-code audit বা runtime/build test করা হয়নি (`NOT TESTED` / `NOT VERIFIED`).

---

## সংক্ষিপ্ত সারসংক্ষেপ (Executive Summary)

1. **Source-of-Truth ডকুমেন্টেশন `/docs/`-এ সংরক্ষণ (`FACT`):** আপনার নির্দেশ অনুযায়ী ২১টি মূল ডকুমেন্ট ও CSV ফাইল কোনো পরিবর্তন ছাড়াই (verbatim baseline হিসেবে) প্রজেক্টের `/docs/` ফোল্ডারে যুক্ত করা হয়েছে, যাতে ভবিষ্যতে যেকোনো সেশন থেকে আপনি ও এজেন্ট এগুলো পড়তে ও আপডেট করতে পারেন।
2. **অ্যাপ কোড ও ক্লাউড সীমারেখা (`FACT`):** কোনো Android source code (`app/src/...`), Gradle ফাইল, `metadata.json`, বা কোনো পেইড ক্লাউড সার্ভিস/Firebase/GCP/storage bucket/GPU/API key তৈরি বা পরিবর্তন করা হয়নি।
3. **মূল অসঙ্গতি (`FACT`):**
   - কয়েকটি ডকুমেন্টের হেডারে ID range বাড়িয়ে লেখা হয়েছে (`FR-054..090`, `NFR-016..045`, `DATA-025..030`, `RISK-033..040`) — এগুলো কোনো missing requirement নয়, বরং **heading/count error**।
   - `TEST-020..040` এবং `TEST-081..088` বিভিন্ন ডকুমেন্টে রেফারেন্স করা আছে কিন্তু কোথাও সংজ্ঞায়িত নেই (**dangling references / missing definitions**)।
   - `TRACEABILITY.md`-এ `FEAT-07`, `FEAT-09`, `FEAT-10`, `FEAT-11`-এ ভুল `TEST-*` ID লিংক করা হয়েছে এবং `FR-001..006`, `FR-053`, `SCR-01..04`, `SCR-14` কোনো feature row-তে ম্যাপ করা নেই।
   - `REPOSITORY_UNIQUE_AUDIT.csv`-এ `#043`, `#047`, `#140`, `#290` (এবং `#367`)-এ ভুল/কপি-পেস্ট শ্রেণিবিভাগ আছে, `allocated_app_module` কলামে পুরোনো ২-ডিজিট/অমিল ID (`API-01`, `API-05`, `NFR-01..03`, `TEST-01/02` ইত্যাদি) আছে, আর `openreelio/openreelio` ও `filmcraft-desktop/filmcraft` মূল 412/264 ক্যাটালগের বাইরে থেকে উল্লেখ করা হয়েছে।

---

## A. Requirement & Design ID Integrity Audit

> **নীতিমালা (`APPROVED`):** কোনো existing ID renumber করা হবে না এবং ফাঁকা জায়গা ভরতে মনগড়া নতুন requirement বানানো হবে না।

### A.1 সব ID Family-র সার্বিক অডিট

| ID Family | হেডারে দাবিকৃত Range | বাস্তবে সংজ্ঞায়িত ID (`FACT`) | অসঙ্গতির ধরন | ক্ষুদ্রতম Traceable সমাধান (`PROPOSAL`) |
|---|---|---|---|---|
| `FR` | `FR-001..090` (`PRD_SRS.md`, `ARCHITECTURE.md`) | `FR-001..006`, `FR-010..017`, `FR-020..029`, `FR-030..035`, `FR-040..046`, `FR-050..053` (মোট 40টি) | `FR-007..009`, `FR-018..019`, `FR-036..039`, `FR-047..049` = **Unused reserved gaps**; `FR-054..090` = **Header ceiling overstatement** | হেডারগুলো সংশোধন করে `FR-001..053 (grouped; reserved gaps)` লেখা; `FR-001..006` ও `FR-053`-কে `TRACEABILITY.md`-এ Foundation row-তে যুক্ত করা |
| `NFR` | `NFR-001..045` (`PRD_SRS.md`, `ARCHITECTURE.md`) | `NFR-001..015` (মোট 15টি; `SECURITY_THREAT_MODEL.md` সঠিকভাবে `NFR-001..015` লিখেছে) | `NFR-016..045` = **Header ceiling overstatement** | `PRD_SRS.md` ও `ARCHITECTURE.md` হেডারে `NFR-001..015` করা |
| `FEAT` | `FEAT-01..15` | `FEAT-01..15` (মোট 15টি, `PRD_SRS.md` ও `TRACEABILITY.md`-এ মিল আছে) | Foundation/Core platform (`FR-001..006`, `FR-053`, Auth/Offline) কোনো `FEAT` row-তে নেই | কোনো `FEAT` renumber না করে `TRACEABILITY.md`-এ `PLATFORM-CORE (Unassigned FEAT; FR-001..006, FR-053)` রো যোগ করা |
| `SCR` | `SCR-01..14` | `SCR-01..14` (`TRACEABILITY.md` Screen ID map-এ 14টিই সংজ্ঞায়িত) | `SCR-01`, `SCR-02`, `SCR-03`, `SCR-04`, `SCR-14` Feature traceability table-এ অনুপস্থিত | নতুন `PLATFORM-CORE` রো-তে `SCR-01..04, SCR-14` ম্যাপ করা |
| `DATA` | `DATA-001..030` (`PRD_SRS`, `ARCHITECTURE`, `CANONICAL_PROJECT_MODEL`, `SECURITY_THREAT_MODEL`) | `DATA-001..024` (`TRACEABILITY.md` Data ID map-এ 24টি) | `DATA-025..030` = **Header ceiling overstatement**; `CANONICAL_PROJECT_MODEL.md` §2-এর `Marker`/`TextLayer`/`ShapeLayer`-এর `DATA-*` ম্যাপ অস্পষ্ট; `FEAT15_VISUAL_FEEDBACK.md` হেডার `DATA-011..018`-এ ভুলবশত `DATA-017 (ProviderProfile)` ঢুকে গেছে | সব হেডারে `DATA-001..024` লেখা; `CANONICAL_PROJECT_MODEL.md` §2 টেবিলে প্রতিটি entity-র পাশে তার `DATA-xxx` ID উল্লেখ করা; `FEAT15` হেডার `DATA-011..016, DATA-018..022` করা |
| `API` | `API-001..045` (`TRACEABILITY.md`) | `API-001..045` (45টি logical group সংজ্ঞায়িত) | `PROVIDER_GATEWAY.md` হেডার `API-031..045` অতিরিক্ত বিস্তৃত (এর মধ্যে `API-032..038` analysis/worker ও `API-040..045` export পড়ে); CSV-তে ২-ডিজিট `API-01..39` ব্যবহার ও অর্থগত অমিল | `PROVIDER_GATEWAY.md` হেডার `API-014, API-015, API-031, API-039` করা; CSV `allocated_app_module`-এর ২-ডিজিট ID গুলো ৩-ডিজিট সঠিক ID-তে রূপান্তর প্রস্তাব করা |
| `SEC` | `SEC-001..030` (`SECURITY_THREAT_MODEL.md`) | `SEC-001..030` (30টিই সংজ্ঞায়িত) | Core docs-এ পরিষ্কার; কেবল CSV-তে ২-ডিজিট `SEC-05`, `SEC-07` ফরম্যাট অসঙ্গতি | CSV রেফারেন্সগুলো `SEC-005` / `SEC-007` বা সঠিক `SEC-009/013`-এ সংশোধন করা |
| `TEST` | `TEST-001..080` (`PRD_SRS`, `ARCHITECTURE`); `TEST-020..039` (`CANONICAL_PROJECT_MODEL`); `TEST-081..088` (`TRACEABILITY`) | কেবল `TEST-041..080` (40টি) এবং `TEST-ARCH-001..007` (7টি) সংজ্ঞায়িত | 1) `TEST-001..019` = **Unused / Undefined**<br>2) `TEST-020..040` = **Missing definitions (dangling references)**<br>3) `TEST-081..088` = **Missing definitions (`to define`)**<br>4) `TEST-ARCH-001..007` `TRACEABILITY.md`-এ নেই<br>5) `FEAT-07/09/10/11`-এ **Incorrect TEST references** | 1) `TEST-001..019` Auth/Project/Upload/Offline Foundation test ব্লক হিসেবে নথিভুক্ত (বা `RESERVED` চিহ্নিত) করা<br>2) `TEST-020..040` ও `TEST-081..088`-এর স্পষ্ট acceptance test সংজ্ঞা লেখা (Phase B1/C-এ)<br>3) `FEAT-07/09/10/11`-এর ভুল রেফারেন্স সরিয়ে নতুন/সঠিক test slot-এ ম্যাপ করা<br>4) `TEST-ARCH-001..007` `TRACEABILITY.md`-এ যোগ করা |
| `BUG` | Prefix reserved (`AI_INSTRUCTIONS.md`) | 0টি (প্রি-বিল্ড পর্যায়ে স্বাভাবিক) | **Unused ID family** (কোনো ত্রুটি নয়) | প্রথম bug পাওয়ার আগ পর্যন্ত `0 active BUG IDs` হিসেবে রাখা |
| `RISK` | `RISK-001..040` (`RISK_REGISTER`, `ARCHITECTURE`, `SECURITY_THREAT_MODEL`) | `RISK-001..032` (32টি সংজ্ঞায়িত) | `RISK-033..040` = **Header ceiling overstatement** | তিনটি ডকুমেন্টের হেডারেই `RISK-001..032` করা |
| `ADR` | `ADR-001..012` (`ARCHITECTURE.md`); `ADR-001..018` (`DECISION_LOG.md`) | `ADR-001..018` (18টিই সংজ্ঞায়িত) | `ADR-013..018` **Architecture হেডারে বাদ পড়েছে** (missing reference, missing definition নয়) | `ARCHITECTURE.md` হেডারে `ADR-001..ADR-018` আপডেট করা |
| `REPO` | `REPO-001..REPO-264` (`PROJECT_MANIFEST`, `REPOSITORY_AUDIT`) | CSV-তে `REPO-xxx` কলাম নেই; আছে `first_catalogue_number` (`001..403`) | **Missing ID column / naming mismatch** | `PROJECT_MANIFEST.md` ও `REPOSITORY_AUDIT.md`-এ স্পষ্ট করা যে unique ledger-এর প্রাইমারি key হলো `first_catalogue_number` (অথবা অনুমোদন সাপেক্ষে CSV-তে নন-ডিস্ট্রাকটিভ `repo_id` কলাম `REPO-001..264` যোগ করা) |

### A.2 রিপোর্টকৃত নির্দিষ্ট Missing Ranges-এর চূড়ান্ত শ্রেণিবিভাগ

| নির্দিষ্ট Range | শ্রেণিবিভাগ (`FACT`) | ব্যাখ্যা ও প্রমাণ | ক্ষুদ্রতম সমাধান (`PROPOSAL`) |
|---|---|---|---|
| `FR-007..009`, `FR-018..019`, `FR-036..039`, `FR-047..049` | **Unused reserved IDs** | `PRD_SRS.md` §3-এ প্রতিটি ক্যাটাগরি ১০-এর গুণিতক দিয়ে শুরু করা হয়েছে (`001`, `010`, `020`, `030`, `040`, `050`)। কোনো ডকুমেন্ট এগুলো রেফারেন্স করেনি। | ফাঁকা রাখা ও `PRD_SRS.md`-এ "Reserved for future expansion within group" নোট দেওয়া। |
| `FR-054..090` | **Header ceiling overstatement** | `PRD_SRS.md` ও `ARCHITECTURE.md` হেডারে `FR-001..090` লেখা থাকলেও `FR-053`-এর পর আর কোনো FR নেই। | হেডার `FR-001..053` করা। |
| `NFR-016..045` | **Header ceiling overstatement** | `PRD_SRS.md` §5-এ `NFR-001..015` পর্যন্তই সংজ্ঞায়িত; `SECURITY_THREAT_MODEL.md`-ও `NFR-001..015` দেখায়। | হেডার `NFR-001..015` করা। |
| `DATA-025..030` | **Header ceiling overstatement** | `TRACEABILITY.md` Data ID map-এ `DATA-001..024` পর্যন্তই আছে; কোনো ডকুমেন্ট `DATA-025..030` সংজ্ঞায়িত বা ব্যবহার করেনি। | সব হেডারে `DATA-001..024` করা। |
| `TEST-001..019` | **Unused / Undefined range** | মূল কোনো MD ডকুমেন্টে সংজ্ঞা বা রেফারেন্স নেই (শুধু CSV-তে ২-ডিজিট `TEST-01/02` আছে)। | Foundation (Auth/Project/Upload/Offline) acceptance tests-এর জন্য সংরক্ষিত রাখা। |
| `TEST-020..040` | **Missing definitions (Dangling references)** | `CANONICAL_PROJECT_MODEL.md` (`TEST-020..039`) এবং `TRACEABILITY.md` (`FEAT-01..05, 10`) এগুলো রেফারেন্স করেছে, কিন্তু একটিও সংজ্ঞায়িত নেই। | `CANONICAL_PROJECT_MODEL.md` বা একটি নিবেদিত `TEST_PLAN.md`-এ `TEST-020..040`-এর verifiable test cases সংজ্ঞায়িত করা। |
| `TEST-081..088` | **Missing definitions (`to define`)** | `TRACEABILITY.md`-এ `FEAT-14`-এর পাশে সরাসরি `TEST-081..088 (to define)` লেখা আছে এবং `PRD_SRS.md`/`ARCHITECTURE.md` হেডার (`TEST-001..080`)-এ বাদ পড়েছে। | `FEAT-14` Reverse Engineering-এর জন্য `TEST-081..088` সংজ্ঞায়িত করা এবং হেডার `TEST-001..088` (প্লাস `TEST-ARCH-001..007`) আপডেট করা। |
| `RISK-033..040` | **Header ceiling overstatement** | `RISK_REGISTER.md`-এ মোট ৩২টি ঝুঁকি (`RISK-001..032`) আছে। | হেডার `RISK-001..032` করা। |
| `ADR-013..018` | **Missing header reference (Defined in `DECISION_LOG.md`)** | `DECISION_LOG.md`-এ `ADR-013..018` সম্পূর্ণভাবে সংজ্ঞায়িত আছে; শুধু `ARCHITECTURE.md` হেডারে `ADR-001..ADR-012` পুরোনো রেঞ্জ থেকে গেছে। | `ARCHITECTURE.md` হেডার `ADR-001..ADR-018` করা। |

### A.3 `TRACEABILITY.md`-এ চিহ্নিত ভুল `TEST` ক্রস-রেফারেন্স (`FACT`)
- **`FEAT-07 (Audio)`** -> `TEST-043` রেফারেন্স করেছে, অথচ `TEST-043` হলো **FEAT-15: "20 independent comments"** টেস্ট!
- **`FEAT-09 (Color)` ও `FEAT-10 (VFX)`** -> `TEST-073` রেফারেন্স করেছে, অথচ `TEST-073` হলো **Export: "30/60/120fps frame count verified"** টেস্ট!
- **`FEAT-11 (Stabilization/Restoration)`** -> `TEST-074` রেফারেন্স করেছে, অথচ `TEST-074` হলো **Export: "OTIO import/export round-trip"** টেস্ট!

---

## B. Requirements & Acceptance Criteria Coverage Audit

নিচে প্রতিটি অনুমোদিত ফিচার (`FEAT-01..15`) এবং অ-ম্যাপকৃত কোর প্ল্যাটফর্ম ফাউন্ডেশনের জন্য FR, User Journey, Normal/Boundary/Failure আচরণ, টেস্টযোগ্য Acceptance Criteria, Security এবং `TEST` ID লিংকের অবস্থা যাচাই করা হলো (`FACT` — নতুন কোনো scope অনুমোদন করা হচ্ছে না; কেবল ফাঁকা জায়গা চিহ্নিত করা হচ্ছে):

| Feature / Area | Clear FR? | User Journey (`PRD_SRS` §4)? | Normal / Boundary / Failure Spec? | Testable Acceptance Criteria? | Security / Privacy Links? | Linked `TEST` IDs | মূল ঘাটতি (Gaps — `PROPOSAL` for refinement) |
|---|---|---|---|---|---|---|---|
| **Platform Core** (Auth, Project/Media, Friend Sharing, Offline) | আংশিক (`FR-001..006`, `FR-053`) | নেই (ইম্প্লিসিট) | অসম্পূর্ণ (ফাইল সাইজ, VFR/corrupt ingest, invite expiry, offline error UX নির্দিষ্ট নয়) | নেই | আছে (`SEC-001..003, 006, 007, 026`, `NFR-001..002`) | **নেই** (`TRACEABILITY.md`-এ অনুপস্থিত) | `TRACEABILITY.md`-এ Foundation রো যোগ, Auth/Upload/Offline-এর জন্য `TEST-001..019` সংজ্ঞা ও boundary rules (max file size, resumable upload retry) নির্ধারণ। |
| **FEAT-01** Timeline & Core NLE | আছে (`FR-010..017`) | নেই (ম্যানুয়াল এডিট জার্নি আলাদা নেই) | আংশিক (rational time ও optimistic lock আছে, কিন্তু zero-length clip, track limit, ripple conflict boundary নেই) | আংশিক (`NFR-006..008`) | আছে (`SEC-002, 003, 013`) | `TEST-020..029` (**Undefined**) | ম্যানুয়াল এডিট user journey + `TEST-020..029` সংজ্ঞায়ন। |
| **FEAT-02** Keyframe & Motion | আছে (`FR-013..015`) | নেই | নেই (Bezier overshoot, duplicate timestamp keyframe, easing failure নেই) | নেই | আছে (`SEC-013`) | `TEST-030..033` (**Undefined**) | Keyframe boundary/failure spec + `TEST-030..033` সংজ্ঞায়ন। |
| **FEAT-03** Layering & Compositing | আছে (`FR-011..014`) | নেই | নেই (blend mode fallback, layer z-order/alpha premultiplication সীমা নেই) | নেই | আছে (`SEC-008, 020`) | `TEST-034..038` (**Undefined**) | Compositing boundary spec + `TEST-034..038` সংজ্ঞায়ন। |
| **FEAT-04** 3D Scene / Camera / Assets | **নেই** (শুধু সাধারণ `FR-011, 033, 050`-এ ম্যাপ) | নেই | নেই (`GLB/OBJ/FBX` সাইজ, polygon limit, GPU timeout নেই) | নেই | আছে (`SEC-008, 020`) | `TEST-039` (**Undefined**) | 3D specialist worker-এর জন্য আলাদা FR প্রস্তাব (`DEFERRED` হতে পারে) + `TEST-039` সংজ্ঞায়ন। |
| **FEAT-05** Vector / Drawing / Motion Graphics | অস্পষ্ট (`FR-011..015`) | নেই | নেই (SVG/Lottie/code-renderer sandbox timeout ও editable-vs-rendered সীমা নেই) | নেই | আছে (`SEC-020`) | `TEST-040` (**Undefined**) | Vector/graphics editable contract ও `TEST-040` সংজ্ঞায়ন। |
| **FEAT-06** Masks, Tracking & Rotoscoping | আংশিক (`FR-011, 022..029, 044`) | আংশিক (Journey C-এ শুধু raster text) | নেই (subject occlusion, tracking drift, SAM2/ProPainter failure fallback নেই) | নেই (শুধু FEAT-15 টেস্ট লিংকড) | আছে (`SEC-007, 008, 010`) | `TEST-041..052` (এগুলো FEAT-15 টেস্ট, tracking টেস্ট নয়) | Mask/tracking failure & occlusion acceptance criteria ও নিবেদিত টেস্ট। |
| **FEAT-07** Multitrack Audio Studio | অস্পষ্ট (`FR-003, 011, 042` — মিক্সিং/ডাকিং/LUFS FR নেই) | নেই | নেই (sample-rate mismatch, clipping, LUFS target, ASR Bangla accuracy নেই) | আংশিক (শুধু export audio sync `TEST-070..072`) | আছে (`SEC-007, 010`) | `TEST-043` (**ভুল লিংক**), `TEST-070..072` | Audio editing/mixing FR, ভুল `TEST-043` অপসারণ এবং অডিও-নির্দিষ্ট টেস্ট। |
| **FEAT-08** Typography & Text Animation | আংশিক (`FR-011..014, 023..029`) | আংশিক (Journey C/D) | আংশিক (raster vs native আছে, কিন্তু font fallback, Bangla/Unicode shaping, RTL/kerning boundary নেই) | আংশিক (`TEST-045, 046`) | আছে (`SEC-013, 028`) | `TEST-045, 046` | বাংলা/Unicode ফন্ট রেন্ডারিং ও text animation acceptance criteria। |
| **FEAT-09** Color Management & Grading | অস্পষ্ট (`FR-010, 013, 050` — LUT/OCIO/HDR FR নেই) | নেই | নেই (SDR/HDR tone-mapping fallback, invalid `.cube` LUT error নেই) | **নেই** | আছে (`SEC-020`) | `TEST-073` (**ভুল লিংক**) | Color/LUT FR + সঠিক color-accuracy test সংজ্ঞা। |
| **FEAT-10** VFX & Filters | অস্পষ্ট (`FR-013, 033`) | নেই | নেই (effect chain limit, unsupported OpenFX fallback নেই) | **নেই** | আছে (`SEC-008, 020`) | `TEST-039` (**Undefined**), `TEST-073` (**ভুল লিংক**) | VFX parameter/fallback spec + সঠিক test ID। |
| **FEAT-11** Stabilization & Restoration | অস্পষ্ট (`FR-003, 033, 050`) | নেই | নেই (gyro metadata না থাকলে fallback, GPU upscale cost/timeout নেই) | **নেই** | আছে (`SEC-007, 008, 011`) | `TEST-074` (**ভুল লিংক**) | Stabilization/upscale/interpolation FR, ভুল `TEST-074` অপসারণ ও নিবেদিত টেস্ট। |
| **FEAT-12** Export & Interchange | **স্পষ্ট** (`FR-050..052`) | আংশিক (Journey A-র শেষে) | **ভালো** (`EXPORT_INTERCHANGE.md`-এ loss report ও unsupported target নিয়ম আছে) | **আছে** (`TEST-070..080`) | আছে (`SEC-027`) | `TEST-070..080` (**Defined**) | Export cancel/resume ও partial download retry acceptance criteria যোগ করা উপকারী। |
| **FEAT-13** AI Creation & Editing Assistant | **স্পষ্ট** (`FR-030..035, 045..046`) | **আছে** (Journey A & E) | **ভালো** (`AI_AGENT_EDIT_PROTOCOL.md` ও `PROVIDER_GATEWAY.md`-এ dry-run, ambiguity, SSRF, timeout আছে) | **আছে** (`TEST-053..069`) | **শক্তিশালী** (`SEC-004, 009..012, 018, 019, 028`) | `TEST-053..069` (**Defined**) | Custom HTTP adapter-এর schema mismatch error UX ও cost-cap breach টেস্ট আরও স্পষ্ট করা। |
| **FEAT-14** Video Reverse Engineering | **স্পষ্ট** (`FR-040..046`) | **আছে** (Journey B) | আংশিক (confidence/raster limitation আছে, কিন্তু long-video chunking/timeout ও partial analysis failure নেই) | **নেই** (`TEST-081..088` এখনো `to define`) | আছে (`SEC-010, 028`) | `TEST-081..088` (**Undefined**) | `TEST-081..088` সংজ্ঞায়ন ও analysis timeout/partial-result behavior নির্ধারণ। |
| **FEAT-15** Visual Feedback & Batch Comments | **সবচেয়ে স্পষ্ট** (`FR-020..029`) | **আছে** (Journey C & D) | **ভালো** (`FEAT15_VISUAL_FEEDBACK.md`-এ stale anchor, conflict, raster text, atomic rollback আছে) | **আছে** (`TEST-041..052`, `TEST-053..059`) | **শক্তিশালী** (`SEC-009, 010, 013, 014, 028`) | `TEST-041..059` (**Defined**) | Confidence threshold-এর নির্দিষ্ট সংখ্যা ও Android touch-precision tolerance (`OPEN`) চূড়ান্ত করা। |

---

## C. Repository Audit Integrity Review

> **সততা ও প্রমাণ সীমারেখা (`FACT`):** এই পর্যালোচনাটি কেবল আপলোড করা `REPOSITORY_AUDIT.md`, `REPOSITORY_UNIQUE_AUDIT.csv`, `REPOSITORY_OCCURRENCES_412.csv`, ও `ORIGINAL_REPOSITORY_CATALOGUE.txt`-এর মধ্যে থাকা রেকর্ডের উপর ভিত্তি করে করা হয়েছে। কোনো repository-র সোর্স কোড এখানে ফেচ বা রান করা হয়নি; তাই উৎস-স্তরের প্রমাণ না থাকা সব শ্রেণিবিভাগকে **`NOT VERIFIED`** হিসেবে চিহ্নিত করা হয়েছে।

### C.1 নির্দিষ্ট সন্দেহজনক এন্ট্রি ও Out-of-Catalogue রেফারেন্স অডিট

| এন্ট্রি / রেফারেন্স | ক্যাটালগ / CSV উপস্থিতি (`FACT`) | নথির ভেতরের বর্তমান অবস্থান ও অসঙ্গতি (`FACT`) | অডিট মূল্যায়ন ও প্রস্তাবিত সমাধান (`PROPOSAL`) |
|---|---|---|---|
| **`#043 tnfe/FFCreator`** | মূল ক্যাটালগে আছে (`#043`, `#265`) | `REPOSITORY_AUDIT.md` §3.8 একে `"Python/Node wrappers or composition APIs"` বলেছে; অথচ `REPOSITORY_UNIQUE_AUDIT.csv` রো `043`-এ কপি-পেস্ট করে `"Video understanding / object analysis / scene research"` (`FEAT-14/15; API-33`) লেখা হয়েছে। | **Classification: `NOT VERIFIED` (Cross-document contradiction + CSV copy-paste error).** CSV-তে `specialty`/`allocated_app_module` `NEEDS RECHECK — probable Node/FFmpeg composition API` হিসেবে ফ্ল্যাগ করে upstream README/source যাচাইয়ের আগ পর্যন্ত `NOT VERIFIED` রাখা। |
| **`#047 GStreamer/gstreamer`** | মূল ক্যাটালগে আছে (`#047`, `#268`) | `REPOSITORY_AUDIT.md` §3.1 একে `"Optional ingest/playback integration reference \| Mature multimedia pipeline"` বলেছে; অথচ `REPOSITORY_UNIQUE_AUDIT.csv` রো `047`-এ কপি-পেস্ট করে `"Video understanding / object analysis / scene research"` (`FEAT-14/15; API-33`) লেখা হয়েছে। | **Classification: `NOT VERIFIED` (CSV misclassification contradicting `REPOSITORY_AUDIT.md` §3.1).** CSV রো `047` সংশোধন করে `REPOSITORY_AUDIT.md` §3.1-এর সাথে মিলিয়ে media pipeline reference হিসেবে চিহ্নিত করা; build/runtime `NOT TESTED`. |
| **`#140 openvideodev/react-video-editor`** | মূল ক্যাটালগে আছে (`#140`) | `REPOSITORY_AUDIT.md`-এ উল্লেখ নেই। `REPOSITORY_UNIQUE_AUDIT.csv` রো `140`-এ কোনো repo-specific প্রমাণ ছাড়াই একই কপি-পেস্ট টেমপ্লেট `"Video understanding / object analysis / scene research"` (`FEAT-14/15; API-33`) বসানো হয়েছে। | **Classification: `NOT VERIFIED` (Unsupported copy-paste template in CSV).** Upstream README/source সরাসরি পরীক্ষা না করা পর্যন্ত এটিকে `BLOCKED / NEEDS SOURCE RECHECK` ও `NOT VERIFIED` হিসেবে চিহ্নিত করা। |
| **`#290 AILab-CVC/VideoCrafter`** | মূল ক্যাটালগে আছে (`#290`) | `REPOSITORY_AUDIT.md` §3.6 একে `"Generation and ComfyUI ecosystem"`-এ রেখেছে; অথচ `REPOSITORY_UNIQUE_AUDIT.csv` রো `290`-এ একে `"Enhancement / interpolation / matting / lip-sync / stabilization"` (`FEAT-06/11; API-34`) লেখা হয়েছে। | **Classification: `NOT VERIFIED` (Cross-document contradiction between §3.6 and CSV row 290).** CSV রো `290`-কে `REPOSITORY_AUDIT.md` §3.6-এর সাথে মিলিয়ে `NEEDS RECHECK — generative video model candidate` হিসেবে ফ্ল্যাগ করা; build/runtime `NOT TESTED`. |
| **`openreelio/openreelio`** | **মূল ক্যাটালগ (412) ও দুই CSV-তে অনুপস্থিত** | `README.md`, `PROJECT_STATUS.md`, ও `REPOSITORY_AUDIT.md` §3.2-এ `"Command/event-sourcing and plugin security reference"` হিসেবে উল্লেখ করা হয়েছে। | **Out-of-Catalogue External Reference — `NOT VERIFIED`.** মূল 412/264 ক্যাটালগ অপরিবর্তিত রেখে `REPOSITORY_AUDIT.md`-এ আলাদা `"External Research References (Non-Catalogue)"` সেকশনে স্থানান্তর করা এবং pinned commit/source audit ছাড়া কোনো capability দাবি না করা। |
| **`filmcraft-desktop/filmcraft`** | **মূল ক্যাটালগ (412) ও দুই CSV-তে অনুপস্থিত** | `ARCHITECTURE.md` §4 ও `REPOSITORY_AUDIT.md` §3.2-এ `#004 storytold/filmcraft`-এর সাথে নামের মিল থাকা আলাদা repo হিসেবে disambiguation-এর জন্য উল্লেখ আছে। | **Non-Catalogue Disambiguation Target — `NOT VERIFIED`.** মূল 264 সংখ্যায় কখনো যোগ না করে `REPOSITORY_AUDIT.md` ও `ARCHITECTURE.md`-এ স্পষ্টভাবে `Non-catalogue disambiguation target (not counted in 264)` লেবেল দেওয়া। |

### C.2 CSV অডিটে পাওয়া অতিরিক্ত অসঙ্গতি (`FACT`)
1. **অতিরিক্ত সম্ভাব্য কপি-পেস্ট শ্রেণিবিভাগ (`NOT VERIFIED`):** `#367 cclank/lanshu-create-ai-presenter-video` (CSV-তে `"Video understanding / object analysis / scene research"`), `#014 chang416/cutcraft` ও `#362 Vincentwei1021/video-talkcraft` (উভয়কেই `"Enhancement / interpolation / matting / lip-sync / stabilization"` টেমপ্লেট দেওয়া হয়েছে, নির্দিষ্ট README প্রমাণ ছাড়া) — এগুলোও `NOT VERIFIED` হিসেবে চিহ্নিত থাকা উচিত।
2. **CSV `allocated_app_module`-এ ২-ডিজিট ও অর্থগত অমিল ID (`FACT`):**
   - `003 openfilm`: `API-05` (সঠিক ফরম্যাট `API-005` / `API-021..022`)
   - `004 filmcraft`: `DATA-01; API-01` (`API-001` হলো Auth, NLE engine নয়!)
   - `008 FireRed-OpenStoryline`: `API-11` (`API-011` হলো Probe, creative planner নয়!)
   - `021 blender`: `API-16`, `023 Natron`: `API-15` (`API-015` হলো Connection test; specialist worker হলো `API-037`!)
   - `037 FFmpeg`: `API-02` (`API-002` হলো Workspace; media probe/render হলো `API-011/012`!)
   - `046 OpenTimelineIO`: `DATA-09` (`DATA-009` হলো Effect; interchange API হলো `API-041..043`!)
   - `139 Clypra`: `NFR-01..03; TEST-02` (`NFR-001..003` হলো Auth/Secrets, timing নয় — timing হলো `NFR-007/008`!)
   - `141 openreel-video`: `API-13; SEC-05` (`API-013` Export; agent plan/approval হলো `API-025..029` ও `SEC-009/013`!)
   - `142 inematds/mcp-video`: `API-12`, `193 rea-video`: `API-10`, `216 Qwen3-VL`: `API-18`, `226 sam2`: `API-19`, `301 ProPainter`: `API-22`, `303 gyroflow`: `API-23`, `323 playwright`: `TEST-01/02; SEC-07` — সবগুলোই পুরোনো ২-ডিজিট স্কিমা থেকে রয়ে গেছে এবং `TRACEABILITY.md`-এর ৩-ডিজিট ম্যাপের সাথে অমিল।

---

## D. Open Decision Register (৪টি ধাপে বিভক্ত)

> **নীতিমালা (`APPROVED CONSTRAINT` — `ADR-010`):** পেইড ক্লাউড সার্ভিস, ক্লাউড ভেন্ডর, রিজিয়ন, বিলিং প্ল্যান, বা ইউজার অথেনটিকেশন পদ্ধতি আপনার হয়ে নির্বাচন করা হয়নি। সেগুলো স্পষ্টভাবে `OPEN — User Decision Required` রাখা হয়েছে।

### Tier 1 — UX/UI ডিজাইন শুরুর আগে অবশ্যই সিদ্ধান্ত নিতে হবে

| Decision ID | বিষয় ও কেন গুরুত্বপূর্ণ | বিকল্পসমূহ (Options) | সুবিধা-অসুবিধা (Trade-offs) | নির্ভরতা (Dependencies) | প্রস্তাবিত দিকনির্দেশনা (`PROPOSAL`) |
|---|---|---|---|---|---|
| **`DEC-UX-01`** | **P0 বনাম P1/P2 ভার্টিক্যাল স্লাইস অগ্রাধিকার:** প্রথম ব্যবহারযোগ্য Android UI-তে কোন স্ক্রিন ও এডিট ফিচার আগে আসবে তা ঠিক না করলে UI অতিরিক্ত জটিল হয়ে যাবে। | **A:** P0 = Auth (`SCR-01`), Workspace/Project (`SCR-02..03`), Media Upload/Proxy (`SCR-04`), Preview + Basic Timeline (`SCR-05..06`), **FEAT-15 Visual Feedback + Comment Queue (`SCR-08..09`)**, BYOK Settings (`SCR-12`), Basic MP4 Export (`SCR-10..11`)। বাকি (`FEAT-04/05/09/10/11/14`) P1/P2।<br>**B:** শুরুতেই ১৫টি FEAT-এর সব প্যানেল একসাথে ডিজাইন করা। | **A:** দ্রুত ব্যবহারযোগ্য ও টেস্টযোগ্য; ফোনের ছোট স্ক্রিনে পরিষ্কার UX।<br>**B:** UX ওভারলোড, ধীর ডেলিভারি ও বেশি বাগ ঝুঁকি। | `PRD_SRS.md`, `SCR-01..14` | **Option A প্রস্তাবিত (`PROPOSAL`)** — কোনো অনুমোদিত ফিচার বাদ না দিয়ে কেবল ধাপে ধাপে ডেলিভারি ক্রম ঠিক করা। |
| **`DEC-UX-02`** | **Android টার্গেট ডিভাইস, ওরিয়েন্টেশন ও `minSdk`:** বর্তমানে টেমপ্লেট `minSdk = 24`, কিন্তু প্রো-টাইমলাইন ও ভিডিও প্রিভিউ ফোনে Portrait না Landscape-এ প্রধান হবে তা UX লেআউট নির্ধারণ করে। | **A:** Phone-first Portrait + Landscape উভয় সমর্থন (Timeline/Canvas-এ Landscape রোটেশন সাপোর্টসহ), `minSdk 26+` (বা `24` রাখা)।<br>**B:** শুধু Portrait-only মোবাইল লেআউট। | **A:** মাল্টিট্র্যাক টাইমলাইন ও FEAT-15 ড্রয়িং ল্যান্ডস্কেপে অনেক আরামদায়ক।<br>**B:** প্রফেশনাল টাইমলাইন ব্যবহারে জায়গা কম পড়ে। | `NFR-015`, Android `build.gradle.kts` | **Option A প্রস্তাবিত (`PROPOSAL`)**, আর `minSdk` আপনার ও বন্ধুদের ফোনের সর্বনিম্ন Android ভার্সন অনুযায়ী ঠিক করুন (`OPEN`)। |
| **`DEC-UX-03`** (`ADR-016`) | **বন্ধুদের রোল ও ইনভাইট UX:** প্রাইভেট অ্যাপে বন্ধুদের কী অনুমতি থাকবে (View / Comment / Edit / BYOK Key ব্যবহার করতে পারবে কি না) — এটি `SCR-09` ও `SCR-14` সরাসরি বদলায়। | **A:** Owner, Editor, Commenter, Viewer — এবং কেবল Owner/নিজস্ব BYOK key ব্যবহার করতে পারবে (অন্যের key-তে খরচ নয়)।<br>**B:** সবাই সমান Editor। | **A:** খরচ ও প্রজেক্ট নিরাপত্তা সুরক্ষিত থাকে।<br>**B:** সহজ UI, কিন্তু অনাকাঙ্ক্ষিত ডিলিট বা API খরচের ঝুঁকি বেশি। | `FR-053`, `SEC-002`, `DATA-023` | **Option A প্রস্তাবিত (`PROPOSAL`)** — আপনার অনুমোদন প্রয়োজন (`OPEN`)। |
| **`DEC-UX-04`** (`ADR-006`) | **FEAT-15 এনোটেশন ও কনফিডেন্স থ্রেশহোল্ড UX:** অটো-রিজলভ কখন সরাসরি টার্গেট দেখাবে, কখন ইউজারকে পছন্দ করতে বলবে, আর রাস্টারাইজড টেক্সটে সতর্কবার্তা কেমন হবে। | **A:** Confidence >= `0.85` হলে pre-selected + editable; `< 0.85` হলে mandatory disambiguation picker; `RASTERIZED` হলে সবসময় ইনপেইন্ট+নতুন লেয়ার অপশন ও ঝুঁকি ব্যাজ দেখাবে।<br>**B:** সব কমেন্টেই ম্যানুয়াল টার্গেট কনফার্মেশন। | **A:** দ্রুত অথচ নিরাপদ (ভুল টার্গেট এডিট হয় না)।<br>**B:** ২০টি কমেন্টে ক্লিক বেশি লাগে। | `FEAT15_VISUAL_FEEDBACK.md`, `FR-020..029` | **Option A প্রস্তাবিত (`PROPOSAL`)** (`OPEN`)। |
| **`DEC-UX-05`** (`ADR-018`) | **অফলাইন/দুর্বল নেটওয়ার্ক আচরণ:** অনলাইন-অনলি নীতি অনুযায়ী নেট না থাকলে অ্যাপ কী দেখাবে। | **A:** Strict online-only ব্যানার + চলমান আপলোড/রেন্ডার অটো-রিজিউম, কোনো লোকাল এডিট নয়।<br>**B:** প্রজেক্ট তালিকা ও পুরোনো কমেন্ট read-only ক্যাশ দেখানো, কিন্তু সব মিউটেশন/AI/রেন্ডার ব্লক রাখা। | **A:** সবচেয়ে সরল ও জিরো sync-conflict।<br>**B:** নেট গেলে স্ক্রিন ফাঁকা হয় না, তবে লোকাল ক্যাশ ক্লিয়ার/সিকিউরিটি নীতি লাগবে। | `ADR-003`, `ADR-018`, `RISK-031` | **Option A (P0-তে) -> Option B (P1-এ)** প্রস্তাবিত (`PROPOSAL`) (`OPEN`)। |

### Tier 2 — Technical Architecture অনুমোদনের আগে অবশ্যই সিদ্ধান্ত নিতে হবে

| Decision ID | বিষয় ও কেন গুরুত্বপূর্ণ | বিকল্পসমূহ (Options) | সুবিধা-অসুবিধা (Trade-offs) | নির্ভরতা (Dependencies) | প্রস্তাবিত দিকনির্দেশনা (`PROPOSAL`) |
|---|---|---|---|---|---|
| **`ADR-004` / `ADR-005`** | **ক্যানোনিকাল প্রজেক্ট স্কিমা ও NLE ইঞ্জিন নির্বাচন:** `storytold/filmcraft` ক্লাউডে বিল্ড ও রান হয় কি না তা যাচাই না করে মূল এডিট ইঞ্জিন চূড়ান্ত করা যাবে না। | **A:** Linux ক্লাউড কনটেইনারে `storytold/filmcraft` feasibility spike চালানো; সফল হলে primary NLE engine, ব্যর্থ হলে FFmpeg + custom canonical timeline engine।<br>**B:** শুরু থেকেই নিজস্ব FFmpeg-ভিত্তিক ক্যানোনিকাল ইঞ্জিন বানানো। | **A:** FilmCraft সফল হলে পেশাদার NLE ফিচার দ্রুত পাওয়া যেতে পারে; ব্যর্থ হলে fallback নিশ্চিত থাকে।<br>**B:** নিয়ন্ত্রণ বেশি, কিন্তু কীফ্রেম/কম্পোজিটিং/অডিও ইঞ্জিন নিজ হাতে বানাতে সময় বেশি লাগে। | `CANONICAL_PROJECT_MODEL.md`, `RISK-001`, `RISK-028` | **Option A (Bounded Feasibility Spike)** প্রস্তাবিত (`PROPOSAL`); চূড়ান্ত ইঞ্জিন এখনো `OPEN`। |
| **`DEC-ARCH-01`** | **Android প্রিভিউ স্ট্রিমিং ও ফ্রেম-স্ন্যাপ ট্রান্সপোর্ট:** ফোনে স্মুথ স্ক্রাবিং ও FEAT-15 এর ফ্রেম-নির্ভুল এনোটেশনের জন্য প্রিভিউ কীভাবে আসবে। | **A:** Server-side FFmpeg proxy MP4/HLS (ExoPlayer/Media3-তে স্ট্রিম) + paused frame-এ server-side exact frame reference/crop।<br>**B:** রিয়েল-টাইম WebRTC/server-rendered ফ্রেম স্ট্রিম। | **A:** কম ব্যান্ডউইথ, সস্তা, কম ল্যাটেন্সি ও অ্যান্ড্রয়েড Media3-র সাথে সহজ।<br>**B:** GPU/ব্যান্ডউইথ খরচ অনেক বেশি। | `ARCHITECTURE.md` §5, `FEAT-15`, `NFR-008` | **Option A প্রস্তাবিত (`PROPOSAL`)** (`OPEN`)। |
| **`DEC-ARCH-02`** (`ADR-007`) | **BYOK Provider Adapter স্কোপ:** কোন প্রোটোকলগুলো প্রথম ধাপে সমর্থিত হবে এবং Custom HTTP JSON-mapping-এর সীমা কতটুকু। | **A:** P0-তে ৩টি স্ট্যান্ডার্ড অ্যাডাপ্টার (`OpenAI-compatible`, `Anthropic-compatible`, `Google Gemini-compatible`) + কঠোর allow-listed `Custom HTTP` (SSRF ব্লকসহ)।<br>**B:** কেবল ১টি নির্দিষ্ট প্রোভাইডার দিয়ে শুরু। | **A:** আপনার BYOK চাহিদা পূরণ করে এবং মিথ্যা "any API works" দাবি এড়ায়।<br>**B:** BYOK লক্ষ্য সীমিত করে ফেলে। | `PROVIDER_GATEWAY.md`, `SEC-004`, `SEC-018` | **Option A প্রস্তাবিত (`PROPOSAL`)** (`OPEN`)। |
| **`DEC-ARCH-03`** (`ADR-016` Auth) | **অথেনটিকেশন ও প্রাইভেট অ্যাক্সেস মডেল:** প্রাইভেট অ্যাপে আপনি ও আমন্ত্রিত বন্ধুরা কীভাবে লগইন করবেন। | **A:** Google Sign-In (Android Credential Manager) + server-side invite allowlist।<br>**B:** Email/Password বা Passkey (custom auth backend) + invite token। | **A:** ফোনে ১-ট্যাপ লগইন ও পাসওয়ার্ড ম্যানেজমেন্টের ঝামেলা নেই।<br>**B:** কোনো নির্দিষ্ট ইকোসিস্টেমের উপর নির্ভর নয়, কিন্তু রিকভারি/ইমেইল সার্ভিস বানাতে হয়। | `SCR-01`, `SEC-001..003`, `NFR-001..002` | **`OPEN — User Decision Required`** (কোনো auth ভেন্ডর আপনার সম্মতি ছাড়া বেছে নেওয়া হয়নি)। |

### Tier 3 — Backend / Cloud ইমপ্লিমেন্টেশন শুরুর আগে অবশ্যই সিদ্ধান্ত নিতে হবে

| Decision ID | বিষয় ও কেন গুরুত্বপূর্ণ | বিকল্পসমূহ (Options) | সুবিধা-অসুবিধা (Trade-offs) | নির্ভরতা (Dependencies) | প্রস্তাবিত দিকনির্দেশনা (`PROPOSAL`) |
|---|---|---|---|---|---|
| **`ADR-010`** | **বিলিং, পেমেন্ট কার্ড ও মাসিক/জব-ভিত্তিক খরচ সীমা:** ক্লাউড রিসোর্স বা GPU বানাতে কার্ড/ফ্রি-টিয়ার সীমা আগে স্পষ্ট করতে হবে। | **A:** কেবল zero-cost / free-tier রিসোর্স দিয়ে শুরু (কোনো GPU worker নয়, কেবল BYOK API + ফ্রি-টিয়ার কন্ট্রোল প্লেন)।<br>**B:** নির্দিষ্ট মাসিক বাজেট ক্যাপ (যেমন hard stop) দিয়ে পেইড ক্লাউড/GPU চালু। | **A:** কোনো অপ্রত্যাশিত বিল নেই, কিন্তু ভারী ভিডিও রেন্ডার/GPU সীমিত থাকবে।<br>**B:** দ্রুত রেন্ডার ও হেভি AI সম্ভব, কিন্তু কার্ড ও বিলিং অ্যাকাউন্ট প্রয়োজন। | `RISK-025`, `NFR-013` | **`OPEN — User Decision Required`** (ক্লাউড তৈরির আগে অবশ্যই ফ্রি-টিয়ার, কার্ড রিকোয়ারমেন্ট ও খরচ যাচাই করা হবে)। |
| **`ADR-015`** | **ক্লাউড ভেন্ডর, রিজিয়ন, ডাটাবেস, অবজেক্ট স্টোরেজ ও জব কিউ নির্বাচন:** ব্যাকএন্ড কোথায় হোস্ট হবে। | **A:** Google Cloud (Cloud Run + Cloud Storage + Postgres/Firestore) — রিজিয়ন ইউজার-সিলেক্টেড।<br>**B:** অন্যান্য ক্লাউড/সেল্ফ-হোস্টেড VPS + S3-compatible storage (যেমন Cloudflare R2 / Backblaze B2) + Postgres/Redis। | **A:** এক প্ল্যাটফর্মে ইন্টিগ্রেশন সহজ, তবে egress ও billing কার্ড লাগতে পারে।<br>**B:** স্টোরেজ egress সস্তা হতে পারে, কিন্তু আলাদা সার্ভিস ম্যানেজ করতে হয়। | `ADR-010`, `ARCHITECTURE.md` §3, `RISK-025` | **`OPEN — User Decision Required`** (কোনো ভেন্ডর বা রিজিয়ন নির্বাচন করা হয়নি)। |
| **`ADR-009`** | **হেভি AI / GPU ওয়ার্কার চালু করার নীতি:** ASR, SAM2, ProPainter, Upscale, Diffusion কীভাবে চলবে। | **A:** P0-তে শুধু BYOK API (VLM/LLM/ASR API) + CPU FFmpeg; সেল্ফ-হোস্টেড GPU ওয়ার্কার `DEFERRED`।<br>**B:** অন-ডিমান্ড serverless GPU worker চালু করা। | **A:** শূন্য idle GPU খরচ ও সহজ অপারেশন।<br>**B:** ইনপেইন্ট/ম্যাটিং/রি-রেন্ডার নিজস্ব মডেলের মাধ্যমে করা যায়, কিন্তু GPU বিল আসে। | `ADR-010`, `ADR-015`, `RISK-025` | **`OPEN — User Decision Required`** (খরচ কমাতে P0-তে Option A সাধারণত নিরাপদ, তবে চূড়ান্ত সিদ্ধান্ত আপনার)। |
| **`ADR-014`** | **মিডিয়া রিটেনশন, ডিলিশন ও এক্সটার্নাল AI প্রোভাইডারে ফ্রেম/ক্লিপ পাঠানোর নীতি:** প্রাইভেট ভিডিও কতদিন স্টোরেজে থাকবে এবং কোন প্রোভাইডারে পাঠানো যাবে। | **A:** ইউজার-নিয়ন্ত্রিত retention (যেমন proxy/export ৩০ দিন, original ম্যানুয়াল ডিলিট) + প্রতি প্রোভাইডার প্রোফাইলে explicit "Allow media upload" টগল।<br>**B:** স্থায়ী স্টোরেজ, কোনো অটো-ডিলিট নয়। | **A:** স্টোরেজ খরচ ও প্রাইভেসি ঝুঁকি কম।<br>**B:** সময়ের সাথে স্টোরেজ বিল দ্রুত বাড়ে। | `SEC-010`, `SEC-024`, `RISK-027` | **Option A প্রস্তাবিত (`PROPOSAL`)**, নির্দিষ্ট সময়কাল ও নীতি `OPEN`। |
| **`ADR-008` / `SEC-004`** | **সার্ভার-সাইড BYOK Secret Vault পদ্ধতি:** এনক্রিপ্টেড কী কোথায় ও কীভাবে রাখা হবে। | **A:** Managed Secret Manager / KMS envelope encryption (DB-তে কেবল encrypted ciphertext)।<br>**B:** App-level KMS-less AES-GCM with environment master key। | **A:** ইন্ডাস্ট্রি-স্ট্যান্ডার্ড key rotation ও audit logging।<br>**B:** সস্তা কিন্তু key rotation ও backup জটিল। | `ADR-015`, `PROVIDER_GATEWAY.md` | **`OPEN — User Decision Required`** (`ADR-015` ক্লাউড নির্বাচনের সাথে যুক্ত)। |

### Tier 4 — পরের ধাপের জন্য নিরাপদে Deferred রাখা যাবে (`DEFERRED`)

| Decision ID | বিষয় | কেন এখন Deferred রাখা নিরাপদ | নির্ভরতা | প্রস্তাবিত অবস্থান |
|---|---|---|---|---|
| **`ADR-012`** | **MP4/OTIO-র বাইরে এক্সটার্নাল এডিটর এক্সপোর্ট অগ্রাধিকার** (`CapCut`, `Alight Motion`, `Node Video`, `Premiere`, `DaVinci Resolve`) | প্রথমে ক্যানোনিকাল প্রজেক্ট, MP4/WAV এক্সপোর্ট এবং OpenTimelineIO (OTIO) রাউন্ড-ট্রিপ প্রমাণ করা জরুরি; প্রতিটি থার্ড-পার্টি এডিটরের জন্য আলাদা import verification টেস্ট লাগবে। | `FEAT-12`, `EXPORT_INTERCHANGE.md` | **`DEFERRED`** (P1/P2) |
| **`ADR-017`** | **3D (`Blender`) ও Node VFX (`Natron` / `OpenFX`) স্পেশালিস্ট ওয়ার্কার** | এগুলো ভারী Linux/GPU কনটেইনার ওয়ার্কার; মূল টাইমলাইন, FEAT-15 এবং AI কমান্ড প্রোটোকল স্থিতিশীল হওয়ার পর যোগ করা নিরাপদ। | `FEAT-04`, `FEAT-10`, `ADR-009` | **`DEFERRED`** (P2) |
| **`DEC-DEF-01`** | **ট্যাবলেট/ফোল্ডেবল অ্যাডভান্সড মাল্টি-পেন লেআউট** | `WindowSizeClass` ফাউন্ডেশন কোডে রাখা যাবে, তবে প্রথম ধাপে আপনার ফোন-ফার্স্ট UX প্রাধান্য পাবে। | `DEC-UX-02` | **`DEFERRED`** (P2) |
| **`DEC-DEF-02`** | **ঐচ্ছিক ComfyUI / Diffusion / Lip-Sync / Restoration / TTS ওয়ার্কার** | প্রতিটি মডেল আলাদা VRAM, লাইসেন্স/সিকিউরিটি ও GPU খরচ বহন করে; BYOK ও কোর NLE স্থিতিশীল হওয়ার পর একটি করে যোগ করা উচিত। | `ADR-009`, `ADR-010`, `REPOSITORY_AUDIT.md` | **`DEFERRED`** (P2+) |

---

## E. Document Correction Plan (`PROPOSAL` ONLY — কোনো ডকুমেন্ট এখনো এডিট করা হয়নি)

নিচের প্রতিটি পরিবর্তন কেবল **প্রস্তাবনা (`PROPOSAL`)**। আপনার অনুমোদনের পর পরবর্তী bounded টাস্ক (`AIVX-B1-DOC-CORRECTIONS-001`)-এ এগুলো `/docs/` ফোল্ডারে প্রয়োগ করা হবে।

| # | Document Path | Existing Issue (`FACT`) | Evidence / Source | Proposed Correction (`PROPOSAL`) | Related IDs | Impact on Other Docs |
|---|---|---|---|---|---|---|
| 1 | `/docs/PRD_SRS.md` | হেডারে `FR-001..090`, `NFR-001..045`, `DATA-001..030`, `TEST-001..080` লেখা, কিন্তু বাস্তবে `FR-001..053`, `NFR-001..015`, `DATA-001..024` আছে এবং `TEST-081..088` বাদ পড়েছে। | `PRD_SRS.md` §§3,5; `TRACEABILITY.md` | হেডার ঠিক করে `FR-001..053 (grouped; reserved gaps)`, `NFR-001..015`, `DATA-001..024`, `TEST-001..088` করা; §3-এ reserved gap নোট যোগ করা; ম্যানুয়াল এডিট Journey F ও `FEAT-04/05/07/09/10/11`-এর gap নোট যুক্ত করা। | `FR-001..053`, `NFR-001..015`, `DATA-001..024`, `TEST-001..088` | `ARCHITECTURE.md`, `TRACEABILITY.md`, `PROJECT_MANIFEST.md` |
| 2 | `/docs/ARCHITECTURE.md` | হেডারে `FR-001..FR-090`, `NFR-001..NFR-045`, `DATA-001..DATA-030`, `RISK-001..RISK-040`, `ADR-001..ADR-012`, `TEST-001..TEST-080` আছে; `ADR-013..018` বাদ পড়েছে; §4-এ `filmcraft-desktop/filmcraft` non-catalogue বলে স্পষ্ট নয়। | `DECISION_LOG.md` (`ADR-001..018`), `RISK_REGISTER.md` (`RISK-001..032`) | হেডারে সব রেঞ্জ বাস্তব সংখ্যার সাথে মিলিয়ে `FR-001..053`, `NFR-001..015`, `DATA-001..024`, `RISK-001..032`, `ADR-001..018`, `TEST-001..088`, `TEST-ARCH-001..007` করা; §4-এ `filmcraft-desktop/filmcraft`-কে `(non-catalogue disambiguation target)` লেবেল দেওয়া। | `ADR-013..018`, `TEST-ARCH-001..007`, `RISK-001..032` | `TRACEABILITY.md`, `REPOSITORY_AUDIT.md` |
| 3 | `/docs/CANONICAL_PROJECT_MODEL.md` | হেডারে `DATA-001..030` লেখা; `TEST-020..039` রেফারেন্স করা হলেও সংজ্ঞায়িত নেই; §2 entity টেবিলে `DATA-001..024` ম্যাপ ও `Marker`/`TextLayer`/`ShapeLayer` সম্পর্ক অস্পষ্ট। | `CANONICAL_PROJECT_MODEL.md` §2, `TRACEABILITY.md` Data ID map | হেডার `DATA-001..024` করা; §2 টেবিলে প্রতিটি entity-র `DATA-xxx` ID কলাম যোগ করা (যেমন `TextLayer`/`ShapeLayer` -> `DATA-008 LayerObject` subtypes, `Marker` -> `DATA-002` sub-entity বা `OPEN`); `TEST-020..039` acceptance test তালিকা এই ফাইলে (বা `TEST_PLAN.md`-এ) সংজ্ঞায়িত করা। | `DATA-001..024`, `TEST-020..039` | `TRACEABILITY.md`, `FEAT15_VISUAL_FEEDBACK.md` |
| 4 | `/docs/FEAT15_VISUAL_FEEDBACK.md` | হেডারে `DATA-011..018` লেখা, যাতে ভুলবশত `DATA-017 (ProviderProfile)` অন্তর্ভুক্ত হয়ে গেছে। | `TRACEABILITY.md` Data ID map (`DATA-017` = `ProviderProfile`) | হেডার সংশোধন করে `DATA-011..016, DATA-018..022` করা। | `DATA-011..022`, `FEAT-15` | `TRACEABILITY.md` |
| 5 | `/docs/PROVIDER_GATEWAY.md` | হেডারে `API-031..045` লেখা, যা analysis/worker (`API-032..038`) ও export (`API-040..045`) ঢুকিয়ে ফেলেছে; অথচ মূল provider API হলো `API-014, 015, 031, 039`। | `TRACEABILITY.md` API ID map | হেডার সংশোধন করে `API-014, API-015, API-031, API-039` করা। | `API-014, 015, 031, 039` | `TRACEABILITY.md` |
| 6 | `/docs/SECURITY_THREAT_MODEL.md` | হেডারে `DATA-001..030` এবং `RISK-001..040` লেখা (বাস্তবে `DATA-001..024` ও `RISK-001..032`)। | `TRACEABILITY.md`, `RISK_REGISTER.md` | হেডার `DATA-001..024` ও `RISK-001..032` করা। | `DATA-001..024`, `RISK-001..032`, `SEC-001..030` | কোনো কাঠামোগত পরিবর্তন নেই |
| 7 | `/docs/RISK_REGISTER.md` | হেডারে `RISK-001..040` লেখা, কিন্তু টেবিলে `RISK-001..032` আছে। | `RISK_REGISTER.md` | হেডার `RISK-001..032` করা। | `RISK-001..032` | `ARCHITECTURE.md`, `SECURITY_THREAT_MODEL.md` |
| 8 | `/docs/TRACEABILITY.md` | 1) `FR-001..006`, `FR-053` ও `SCR-01..04, 14` টেবিলে ম্যাপড নয়।<br>2) `FEAT-07` (`TEST-043`), `FEAT-09/10` (`TEST-073`), `FEAT-11` (`TEST-074`) ভুল টেস্ট রেফারেন্স।<br>3) `TEST-020..040` ও `TEST-081..088` অসংজ্ঞায়িত।<br>4) `TEST-ARCH-001..007` অনুপস্থিত। | `FEAT15_VISUAL_FEEDBACK.md`, `EXPORT_INTERCHANGE.md`, `ARCHITECTURE.md` §10 | 1) `PLATFORM-CORE` রো যোগ করে `FR-001..006, FR-053`, `SCR-01..04, 14` ও `TEST-001..019` (to define) ম্যাপ করা।<br>2) `FEAT-07/09/10/11`-এর ভুল `TEST` লিংক সরিয়ে `NEEDS TEST DEFINITION` (বা নিবেদিত নতুন রেঞ্জ `TEST-089+`) রাখা।<br>3) `TEST-ARCH-001..007` আর্কিটেকচার যাচাই রো যোগ করা। | `FR-001..053`, `SCR-01..14`, `TEST-001..088`, `TEST-ARCH-001..007` | `PRD_SRS.md`, `CANONICAL_PROJECT_MODEL.md` |
| 9 | `/docs/REPOSITORY_AUDIT.md` | 1) `REPO-001..REPO-264` বলা হয়েছে কিন্তু CSV-তে এই কলাম নেই।<br>2) `openreelio/openreelio` ও `filmcraft-desktop/filmcraft` মূল 412/264 ক্যাটালগের বাইরে থেকে §3.2-এ মিশে আছে। | `ORIGINAL_REPOSITORY_CATALOGUE.txt`, উভয় CSV | 1) স্পষ্ট করা যে unique ledger key হলো `first_catalogue_number` (অথবা অনুমোদন সাপেক্ষে `REPO-001..264` কলাম যোগ)।<br>2) আলাদা `"External Research References (Non-Catalogue)"` সেকশনে `openreelio/openreelio` ও `filmcraft-desktop/filmcraft`-কে `NOT VERIFIED` লেবেলসহ সরানো। | `REPO-001..264` | `PROJECT_MANIFEST.md`, `README.md`, `PROJECT_STATUS.md` |
| 10 | `/docs/REPOSITORY_UNIQUE_AUDIT.csv` | 1) `#043`, `#047`, `#140`, `#290` (ও `#367/#014/#362`)-এ কপি-পেস্ট/পরস্পরবিরোধী specialty।<br>2) `allocated_app_module`-এ ২-ডিজিট ও অর্থগত অমিল ID (`API-01..39`, `DATA-01/09`, `NFR-01..03`, `SEC-05/07`, `TEST-01/02`)। | `REPOSITORY_AUDIT.md`, `TRACEABILITY.md` | 1) `#043`, `#047`, `#140`, `#290` (ও `#367`) রো-তে `evidence_status` ও `audit_notes`-এ `NOT VERIFIED — requires direct upstream README/source recheck` যুক্ত করা এবং স্পষ্ট cross-doc বিরোধ নোট করা।<br>2) `allocated_app_module`-এর সব ID ৩-ডিজিট ও `TRACEABILITY.md`-এর প্রকৃত ID-র সাথে মেলানো। (কোনো URL বা `first_catalogue_number` পরিবর্তন করা হবে না।) | `DATA-*`, `API-*`, `NFR-*`, `SEC-*`, `TEST-*` | `REPOSITORY_AUDIT.md`, `TRACEABILITY.md` |
| 11 | `/docs/PROJECT_MANIFEST.md`, `/docs/PROJECT_STATUS.md`, `/docs/README.md`, `/docs/CHANGELOG.md` | 1) `PROJECT_MANIFEST.md`-এ `REPO-001..264` উল্লেখ।<br>2) `README.md` ও `PROJECT_STATUS.md`-এ `openreelio/openreelio` ক্যাটালগ-বহির্ভূত বলে স্পষ্ট নয়।<br>3) Phase A (`AIVX-A0-INSPECT-001`) ও Phase B (`AIVX-B0-ANALYSIS-RECONCILE-001`) ফলাফল এখনো লগ করা হয়নি। | Turn 1 ও Turn 2 ফলাফল | Phase B সংশোধন অনুমোদিত হলে `PROJECT_STATUS.md`, `PROJECT_MANIFEST.md` ও `CHANGELOG.md`-এ Phase A (Android toolchain `PASS`, Robolectric SDK 36 `FAIL`) ও Phase B reconciliation ইতিহাস নথিভুক্ত করা। | All IDs | পুরো `/docs/` সেটের single source of truth আপ-টু-ডেট হবে |

---

## F. Phase B Exit Criteria, Checklist & পরবর্তী ধাপ

### F.1 Phase B Measurable Exit Criteria Checklist

| ক্রম | Exit Criterion (পরিমাপযোগ্য মানদণ্ড) | বর্তমান অবস্থা | প্রমাণ / বাকি কাজ |
|---|---|---|---|
| 1 | ২১টি source-of-truth ডকুমেন্ট ও CSV যাচাই এবং `/docs/`-এ বেসলাইন কপি সংরক্ষিত | **`PASS`** | `/docs/`-এ ২১টি ফাইল তৈরি ও যাচাইকৃত (`REPOSITORY_UNIQUE_AUDIT.csv` = 264 unique rows, `REPOSITORY_OCCURRENCES_412.csv` = 412 rows)। |
| 2 | সব ১২টি ID family (`FR..REPO`) ও সব রিপোর্টকৃত missing range অডিট সম্পন্ন | **`PASS`** | Section A-তে সব range-এর শ্রেণিবিভাগ ও non-renumbering সমাধান প্রস্তুত। |
| 3 | সব অনুমোদিত ফিচার (`FEAT-01..15`) + Platform Core-এর acceptance criteria ও security coverage যাচাই সম্পন্ন | **`PASS`** | Section B-তে পূর্ণ ম্যাট্রিক্স প্রস্তুত। |
| 4 | সন্দেহজনক ৪টি repo (`#043, #047, #140, #290`) ও ২টি out-of-catalogue রেফারেন্স (`openreelio`, `filmcraft-desktop`) অডিট সম্পন্ন | **`PASS`** | Section C-তে প্রমাণসহ `NOT VERIFIED` চিহ্নিত। |
| 5 | Section E-এর অনুমোদিত ডকুমেন্ট সংশোধনগুলো `/docs/`-এ প্রয়োগ ও `TEST-020..040`, `TEST-081..088`, `TEST-001..019` সংজ্ঞায়িত | **`OPEN`** | আপনার অনুমোদনের অপেক্ষায় (`AIVX-B1-DOC-CORRECTIONS-001`)। |
| 6 | Tier 1 (`DEC-UX-01..05`) সিদ্ধান্তসমূহ ইউজার কর্তৃক অনুমোদিত ও `DECISION_LOG.md`-এ লগকৃত | **`OPEN`** | UX/UI ডিজাইন শুরুর আগে প্রয়োজন। |
| 7 | Tier 2 (`ADR-004/005`, `DEC-ARCH-01..03`) সিদ্ধান্তসমূহ অনুমোদিত | **`OPEN`** | Technical Architecture অনুমোদনের আগে প্রয়োজন। |
| 8 | Tier 3 (`ADR-010, 015, 009, 014, 008`) সিদ্ধান্তসমূহ অনুমোদিত | **`OPEN`** | Backend/Cloud সার্ভিস তৈরির আগে প্রয়োজন (এখনই ব্লকার নয়)। |

### F.2 পরিবর্তিত ফাইলের রিপোর্ট (Changed Files Report — `FACT`)
- **App Source / Gradle / Manifest / `metadata.json` পরিবর্তিত ফাইল:** **`0`টি** (কোনো অ্যাপ কোড বা বিল্ড কনফিগ স্পর্শ করা হয়নি)।
- **নতুন তৈরি ফাইল (`/docs/`-এ ২১টি verbatim baseline ফাইল — আপনার অনুরোধ অনুযায়ী, কোনো কন্টেন্ট এডিট ছাড়াই):**
  1. `/docs/GOOGLE_AI_STUDIO_CUSTOM_INSTRUCTIONS.txt`
  2. `/docs/README.md`
  3. `/docs/PROJECT_STATUS.md`
  4. `/docs/PROJECT_MANIFEST.md`
  5. `/docs/AI_INSTRUCTIONS.md`
  6. `/docs/PRD_SRS.md`
  7. `/docs/ARCHITECTURE.md`
  8. `/docs/CANONICAL_PROJECT_MODEL.md`
  9. `/docs/FEAT15_VISUAL_FEEDBACK.md`
  10. `/docs/PROVIDER_GATEWAY.md`
  11. `/docs/AI_AGENT_EDIT_PROTOCOL.md`
  12. `/docs/EXPORT_INTERCHANGE.md`
  13. `/docs/SECURITY_THREAT_MODEL.md`
  14. `/docs/REPOSITORY_AUDIT.md`
  15. `/docs/RISK_REGISTER.md`
  16. `/docs/DECISION_LOG.md`
  17. `/docs/TRACEABILITY.md`
  18. `/docs/CHANGELOG.md`
  19. `/docs/REPOSITORY_UNIQUE_AUDIT.csv`
  20. `/docs/REPOSITORY_OCCURRENCES_412.csv`
  21. `/docs/ORIGINAL_REPOSITORY_CATALOGUE.txt`
- **বিল্ড/টেস্ট অবস্থা (Turn 1 থেকে অপরিবর্তিত):** `compile_applet` = `PASS`, `ExampleUnitTest` = `PASS`, `ExampleRobolectricTest` (SDK 36) = `FAIL` (container network restriction), `lint_applet` = `NOT TESTED`, `androidTest`/device = `BLOCKED`.

### F.3 প্রস্তাবিত পরবর্তী Bounded টাস্ক (`PROPOSAL`)
- **Task ID:** `AIVX-B1-DOC-CORRECTIONS-001`
- **কাজের পরিধি:** Section E-এর অনুমোদিত ডকুমেন্ট সংশোধনগুলো `/docs/`-এ প্রয়োগ করা, `TEST-001..019`, `TEST-020..040`, `TEST-081..088`-এর টেস্টযোগ্য সংজ্ঞা লেখা, এবং আপনার দেওয়া Tier 1 সিদ্ধান্তগুলো `DECISION_LOG.md`, `PROJECT_STATUS.md` ও `CHANGELOG.md`-এ রেকর্ড করা — যাতে এরপর নিরাপদে Phase C (UX/UI ডিজাইন ও নেভিগেশন স্কেলেটন) শুরু করা যায়।

---

### আপনার অনুমোদনের জন্য একটি নির্দিষ্ট প্রশ্ন

**পরবর্তী ধাপ `AIVX-B1-DOC-CORRECTIONS-001`-এর জন্য কি আমি Section E-এর সব ডকুমেন্ট সংশোধন `/docs/` ফোল্ডারে প্রয়োগ করব — এবং সেই সাথে Tier 1-এর ৫টি সিদ্ধান্ত (`DEC-UX-01` থেকে `DEC-UX-05`) নিয়ে আপনার পছন্দ (যেমন: প্রস্তাবিত Option A গুলো গ্রহণ করবেন কি না, আর `minSdk` কত রাখতে চান) জানিয়ে দেবেন?**

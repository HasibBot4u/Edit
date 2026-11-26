# Repository Catalogue Audit and Allocation Report

**Document ID:** AIVX-REPO-001 · **Version:** 1.0 · **Date:** 2026-11-26  
**Status:** CATALOGUE INVENTORY COMPLETE; SOURCE/BUILD AUDIT PARTIAL  
**Source:** user-uploaded `ORIGINAL_REPOSITORY_CATALOGUE.txt` (`turn167file0`)  
**Related:** `REPOSITORY_OCCURRENCES_412.csv`, `REPOSITORY_UNIQUE_AUDIT.csv`, REPO-001..REPO-264

## 1. Exact catalogue reconciliation

The original file contains 412 numbered occurrences and was read from first to last. Counts generated from that file:

- 412 numbered occurrences total.
- 411 URLs are GitHub-hosted; one URL points to GitLab.
- 410 well-formed GitHub owner/repository paths; one GitHub URL is malformed (`https://github.com/cavalry`, catalogue #315).
- 264 unique valid GitHub owner/repository identities after case normalization.
- 108 identities appear more than once; their repeated references add 146 extra occurrences.
- GitLab Pitivi is preserved as its own original occurrence (#025) and must not be conflated with GitHub mirrors.

The 412-row occurrence ledger preserves exact user order and duplicates. The 264-row unique audit register has an allocation/status for each unique GitHub identity. The malformed URL and GitLab source are separately described in the README and ledger.

## 2. What “deep audit” means here — and what was actually done

### Completed evidence

- Catalogue parsed and exact counts reconciled.
- Public GitHub repository identity and default branch checked for a large subset via the connected GitHub source reader.
- README and primary overview fetched where available; selected architecture, API, data model, project format, performance, plugin and test documents fetched for high-priority repositories.
- Priority repo assignments and compatibility issues assessed.
- Unique audit CSV contains evidence status, audit depth, candidate module, decision and technical notes.

### Not completed

This pass did **not** clone and inspect every source file in all 264 repositories. It did not build each repo, install dependencies, run every unit/integration/e2e test, benchmark workers, audit all transitive dependencies, verify every release artifact, or test integrations against the chosen cloud stack. Some README files were not readable in the connector; some original URLs were deleted/moved/renamed/wrong. The CSV intentionally marks these rows.

Do not treat a README feature list as verified implementation. No repository has been integrated into AIVX and no repository build has been marked PASS.

## 3. Allocation decisions

Allocation terms:

- `ADOPT ... CANDIDATE`: candidate for a bounded feasibility spike; not yet approved as production dependency.
- `ADAPT`: reuse selected ideas/APIs/algorithms behind an AIVX adapter.
- `OPTIONAL WORKER`: run remotely only when user invokes it; isolated from project authority.
- `REFERENCE`: design/UX/algorithm research; do not embed.
- `DEFER`: no immediate role or immature source.
- `BLOCKED`: source inaccessible or identity requires recheck.
- `N/A`: no product function; catalogue/index/research helper only.

### 3.1 Core NLE and media foundation

| Repository | Allocation | Rationale / caveat |
|---|---|---|
| `storytold/filmcraft` | Primary engine candidate (ADOPT CANDIDATE) | Headless Rust engine; exact time, command registry, undo, CPU/GPU rendering, scopes, project format and interchange. Needs cloud build, API and performance gates. |
| `FFmpeg/FFmpeg` | Media foundation (ADOPT) | Probe, decode, encode, mux, filters, scaling and audio. Not a canonical editable project. |
| `AcademySoftwareFoundation/OpenTimelineIO` | Interchange adapter (ADOPT) | Editorial timeline exchange and plugin adapters; media files/effects are not fully represented. |
| `GStreamer/gstreamer` | Optional ingest/playback integration reference | Mature multimedia pipeline; not a second primary engine unless an exact need appears. |
| `Vanilagy/mediabunny` | Browser media primitive reference | WebCodecs media demux/decode/encode. Not cloud renderer authority. |
| `ffmpegwasm/ffmpeg.wasm` | Defer/browser utility | WASM processing is constrained; cloud workers better suit large media. |
| `mltframework/mlt` | Optional render integration reference | Used by Shotcut/Kdenlive family; do not combine multiple render engines in one default path without benchmark. |
| `OpenShot/libopenshot` | Reference/optional adapter | Existing NLE render library; test if FilmCraft cannot satisfy a specific feature. |

### 3.2 Editor UX and agent control

| Repository | Allocation | Rationale / caveat |
|---|---|---|
| `openfilm/openfilm` | Primary FEAT-15 UX reference | User can click a moment, drag a time span or circle a frame region, then agent knows target. Its HTML/CSS film format is not adopted as canonical project. |
| `0xsline/OpenChatCut` | AI-native editor/tool UX reference | Real editable tracks, agent writes operations, undo/redo, MCP and media-generation flows. Not native Android. |
| `Augani/openreel-video` | Agent action/dry-run architecture reference | Typed tools, confirmation, undoable agent turns and project-as-source-of-truth; its own docs expose readiness gaps. |
| `openreelio/openreelio` | Command/event-sourcing and plugin security reference | Append-only command log, JSON commands, jobs, QC and WASM plugin permission model. Not Android UI. |
| `jub0t/Concat` | NLE feature and mobile platform reference | Repository claims Android/iOS plus Rust/FFmpeg; product is local-first and therefore conflicts with online-only processing. |
| `filmcraft-desktop/filmcraft` | Related engine identity to investigate | Similar FilmCraft brand/architecture; must determine fork/relation before treating as independent implementation. Primary candidate selection is `storytold/filmcraft`. |
| `Monet-AI-Editor/Monet` | Reference | macOS editor, timeline and agent terminal; platform-incompatible. |
| `cartesiancs/cartcut` | Reference/adapt selected MCP UX | Browser editor, live timeline via MCP. |
| `ronak-create/FableCut` | Reference/adapt JSON timeline pattern | Browser editor; editable timeline represented as JSON and live updates. |
| `VelornLabs/velorn` | Optional generation workflow reference | AI workstation with ComfyUI workflows, MCP and timeline. Desktop app. |
| `pireel/pireel` | Reference/adapter review | Engine package and separate hosted connector; inspect data/service boundary before any use. |
| `MartinDelophy/ai-video-editor` | Reference | Browser Timeline Studio; README explicitly notes some preview path analyses metadata rather than frames/audio. |
| `trykimu/videoeditor` | Reference | Full-stack cloud-oriented editor and separate renderer; not native Android. |
| `OpenCut-app/OpenCut` | Defer | Rewrite declared in progress; inspect future release later; classic is separate. |

### 3.3 Visual feedback and reverse analysis

| Repository | Allocation | Rationale / caveat |
|---|---|---|
| `JuneYaooo/rea-video` | Reverse-analysis worker candidate | Shot-level live/AI/code/mixed analysis, timing, audio, text and VIDEO.md package. |
| `SamurAIGPT/rea-video-turbo` | Optional analysis/replication planner | Exports VIDEO.md/report/shot prompts; generation service is external and requires cost/consent control. |
| `videomd/videomd` | Analysis interchange format candidate | Layered video evidence package; schema versioning/validation required. |
| `FireRedTeam/FireRed-OpenStoryline` | Optional creative producer | Script, storyboard, media search, conversational refinement and skills. Model/API dependencies and task costs need review. |
| `sharon-laicc/viral-video-decomposer` | Optional narrative analysis skill | Shot structure/emotion/retention and HTML report; not editor. |
| `liuliu-66-create/ll-video-decomposer` | Optional multimodal evidence skill | Combines transcript, sampled frames, cut changes, text/audio and report; evidence quality depends on full source. |
| `sato-note/reverse-engineer-ai-video-tutorial` | Reference skill | Evidence-backed tutorial extraction, not a renderer. |
| `openfilm/openfilm` | Annotation UX | Point/circle/time-span mapping primary reference. |

### 3.4 Timeline analysis, ASR, subtitles and audio

- `openai/whisper`, `SYSTRAN/faster-whisper`, `ggml-org/whisper.cpp`, `m-bain/whisperX`, `modelscope/FunASR`, `pyannote/pyannote-audio`: ASR, word timings, diarization and language worker candidates; compare accuracy, model size, provider costs and concurrent throughput. Not every engine should run on every asset.
- `smacke/ffsubsync`: subtitle/audio timing correction worker.
- `Aegisub`, `SubtitleEdit`: subtitle authoring/reference, not main timeline.
- `YaoFANGUK/video-subtitle-extractor` / `video-subtitle-remover`: optional OCR/inpaint research; require quality review, do not assume a removed subtitle can restore the original pixels.
- `DataAnts-AI/CutScript`: transcript-based editing reference, WhisperX/FastAPI/Electron/FFmpeg.
- `x007xyz/flycut-caption`: bilingual captions, word times, web/desktop ASR and hard-burn export reference.
- `facebookresearch/demucs`, `Anjok07/ultimatevocalremovergui`, `kwatcharasupat/bandit`: optional source separation workers. Use one selected backend per task and benchmark first.
- `OHF-Voice/piper1-gpl`, `resemble-ai/chatterbox`, `coqui-ai/TTS`, `hexgrad/kokoro`: optional TTS worker candidates; chatterbox README states it is retired/not maintained as of August 2026, therefore do not select as preferred provider without revalidation.
- `facebookresearch/audiocraft`: music/SFX generation research worker; not a licensed asset catalogue or audio editor.
- `audacity/audacity`, `Ardour/ardour`: desktop audio workstation reference only, not Android core.

### 3.5 VFX, computer vision, restoration and tracking

- `facebookresearch/sam2`, `gaomingqi/Track-Anything`, `PeterL1n/RobustVideoMatting`: segmentation/matting workers.
- `princeton-vl/RAFT`: optical-flow research primitive; can inform motion estimation but is not a complete optical-flow UI.
- `hzwer/ECCV2022-RIFE`, `Fannovel16/ComfyUI-Frame-Interpolation`: frame interpolation optional worker; artifact and scene-cut protection required.
- `sczhou/ProPainter`: video inpainting/object removal; use only with mask and post-render review.
- `k4yt3x/video2x`, `xinntao/Real-ESRGAN`, `TencentARC/GFPGAN`, `bloc97/Anime4K`, `nagadomi/waifu2x`, `nihui/waifu2x-ncnn-vulkan`, `AaronFeng753/Waifu2x-Extension-GUI`: optional image/video restoration/upscale, not default workflow.
- `gyroflow/gyroflow`: stabilization specialist; source includes Android/iOS and a separate core, but AIVX must still test worker integration and metadata handling.
- `opencv/opencv`, `Breakthrough/PySceneDetect`, `soCzech/TransNetV2`, `dmlc/decord`: vision, shot detection and frame access primitives.
- `QwenLM/Qwen3-VL`, `OpenGVLab/InternVideo`, `DAMO-NLP-SG/VideoLLaMA2`, `LLaVA-VL/LLaVA-NeXT`, `OpenGVLab/VideoMAEv2`, `facebookresearch/vjepa2`: VLM/video understanding/embeddings research workers. Evaluate model input resolution, time alignment, temporal consistency and cloud GPU cost.
- `facebookresearch/Ego4d`, `iejMac/video2dataset`: research datasets/data tooling; not app runtime. Dataset access/size/privacy must be separately controlled.

### 3.6 Generation and ComfyUI ecosystem

`Wan-Video/Wan2.2`, `Tencent/HunyuanVideo`, `Lightricks/LTX-Video`, `THUDM/CogVideo`, `hpcaitech/Open-Sora`, `PKU-YuanGroup/Open-Sora-Plan`, `AILab-CVC/VideoCrafter`, plus `ComfyUI` and custom nodes/wrappers are optional remote generation backends. They are heavy model-serving workloads; model weights, VRAM, queueing, latency and cost make them unsuitable as Android APK dependencies. AComfyUI adapter must validate workflow JSON, pin node/model versions, restrict file/network access, and return assets/provenance, not raw access to internal runtime.

### 3.7 3D, vector, compositing and graphics

- `blender/blender`: 3D scene/animation/render worker; import/export GLB/GLTF/OBJ/FBX support must be validated per format.
- `NatronGitHub/Natron`: node compositing, masks, roto, tracking, OFX, headless render; optional VFX worker.
- `AcademySoftwareFoundation/openfx`: plugin interface standard/reference; host must sandbox plugin execution.
- `NatronGitHub/openfx-io`: media reader/writer plugins; mirror repo path differs from original #318.
- `OpenColorIO`, `AcademySoftwareFoundation/openfx`, `Glaxnimate`, `OpenToonz`, `Synfig`, `Lottie`, `Theatre.js`, `p5.js`, `Manim`, `svg.js`, `Processing`, `Motion Canvas`: color, vector, animation and scene tools; each should be a specialized plugin/worker, not bundled wholesale.

### 3.8 Other media, capture and utility tools

- `MediaInfo`: metadata inspection; use if FFprobe does not expose a needed field or compare with independent probe.
- `HandBrake`, `Shutter Encoder`, `Videomass`, `Tdarr`, `GPAC`, `mpv`, `ShareX`, `OBS Studio`, `Screenity`, `RecordRTC`, `Kap`, `Peek`, `Playwright`, `Playwright MCP`, `VHS`: transcoding, packaging, playback, capture and QA references or adapters. No default end-user system access without user consent.
- `yt-dlp`, `gallery-dl`, YouTube transcript tools: optional media retrieval connectors only if user explicitly supplies a URL and the remote service/availability permits it. Do not make external downloading the default or bypass access restrictions.
- `ffmpeg-python`, `PyAV`, `MoviePy`, `editly`, `FFCreator`: Python/Node wrappers or composition APIs, not the primary canonical engine.

### 3.9 Skills and indexes

The various awesome lists, `SKILL.md` repositories, motion/effect libraries and coding-agent toolkits are research/catalogue/recipe material. They are not all runtime services. Before adapting a skill: inspect its complete entry file, scripts, downloaded assets, network targets and dependencies; convert only its relevant recipe into an internal tested AIVX tool. Do not install a 100+ skill pack indiscriminately.

## 4. Corrections, moved repositories and blocked identities

Examples found during review: `edenfun/reelmimic` resolves to `edenfunf/reelmimic`; `ComfyUI-Manager` is now discoverable under `Comfy-Org/ComfyUI-Manager`; `NatronGitHub/openfx-io` was accessible while the original `AcademySoftwareFoundation/openfx-io` URL returned 404. Other entries returned 404 or were not readable (`HKUDS/VideoAgent`, some ComfyUI wrapper links, OpenMontage README, etc.). Keep the user's original URLs unchanged in the occurrence CSV; place verified correction/mirror in the unique register only.

## 5. Recommendation: integrate by contract, not by copying every repository

AIVX should define an internal capability registry with adapter contracts: `MediaProbe`, `VideoDecoder`, `TimelineEngine`, `RenderEngine`, `SpeechRecognizer`, `Diarizer`, `OCR`, `VideoUnderstanding`, `ObjectSegmenter`, `ObjectTracker`, `OpticalFlow`, `Inpaint`, `Upscaler`, `Interpolator`, `Stabilizer`, `TTS`, `MusicGenerator`, `3DRenderer`, `Compositor`, `InterchangeAdapter`, `QualityChecker`. Each integration declares supported formats, input limits, cost model, timeout, security permissions, output schema, provenance, tests, and fallback. This avoids a brittle monolith.

## 6. Priority integration sequence

1. FilmCraft feasibility spike + FFmpeg probe/render worker.
2. Canonical project API + command validation + undo.
3. OpenFilm-inspired FEAT-15 annotation/anchor and OpenReel-inspired dry-run/approval loop.
4. REA Video + ASR/OCR/VLM analysis pipeline.
5. Text/audio timeline, provider gateway and safe agent protocol.
6. OTIO plus one target export round-trip.
7. Add optional segmentation/tracking/inpaint/interpolation/3D/VFX workers by user demand.
8. Add less-used catalogue tools only when a measurable acceptance test needs them.

## 7. Repository audit evidence status

See `REPOSITORY_UNIQUE_AUDIT.csv`. `README / PRIMARY DOCS REVIEWED` means overview text was available; it does not mean full source audit. `README + selected technical docs` means architecture/API/test docs were also fetched. `CATALOGUED; SOURCE REVIEW INCOMPLETE` and `BLOCKED / NEEDS SOURCE RECHECK` must remain open. All build/runtime columns are NO / NOT EXECUTED. All integrations are NOT INTEGRATED.

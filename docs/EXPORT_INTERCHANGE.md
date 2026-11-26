# Export, Interchange and Editable Project Compatibility

**Document ID:** AIVX-EXP-001 · **Version:** 1.0 · **Status:** PROPOSAL  
**Related:** FEAT-12, DATA-001..024, API-040..045, TEST-070..080, RISK-016

## 1. Two different outputs

1. **Rendered media:** MP4/MOV/WebM/GIF/image sequence/audio outputs. These are flattened deliverables. They do not preserve the entire editable project.
2. **Editable project/interchange:** track/clip order, trims, timing, media references, transforms, text, keyframes, effects, masks, transitions and metadata. This is a different export with potential feature loss.

The export screen must identify which kind is being generated.

## 2. Native AIVX project package

A project archive should include: versioned canonical project JSON; assets manifest; proxy/thumbnail manifest; supported generated source files (e.g. SVG/HTML/3D scene file) where needed; user fonts/links only when allowed; effect/plugin IDs and versions; timeline metadata; audio metadata; and a compatibility report. Private source media can be externalized or included based on user choice. All package paths must be relative and validated against path traversal.

## 3. Common interchange candidates

- OpenTimelineIO `.otio`/`.otioz`: editorial timeline/cut data and references; not a media container and not a complete representation of every compositor/effect.
- Final Cut Pro XML / FCPXML: timeline interchange with host-specific capabilities and version differences.
- CMX 3600 EDL: simple cut lists; very limited layers/effects/audio/animation.
- AAF/OMF: professional interchange for editorial/audio workflows; media essence, plugin and effect mapping varies.
- Premiere XML/AAF/FCPXML imports and DaVinci Resolve timeline interchange must be validated on exact app version.
- Subtitle formats: SRT/VTT/ASS/SCC as appropriate; subtitle styling/animation can be lost when flattened to simple text timing.

FilmCraft's interchange documentation claims EDL, Final Cut Pro 7 XML, FCPXML, OTIO, AAF, OMF and ALE import/export. Its own module documents unsupported concepts and report warnings. This makes it an important candidate, not proof of full fidelity to every destination editor.

## 4. App-specific caution

- CapCut has multiple regional/mobile/desktop formats and changing import behavior. No universal third-party project compatibility should be claimed without tests on the actual app/version/device.
- Alight Motion's project-package workflow is different from ordinary XML/OTIO; validate its documented current import/share process before designing an adapter.
- Node Video uses its own project/template workflows; do not assume open timeline interchange.
- Premiere Pro and DaVinci Resolve support professional interchange pathways, but the set of preserved effects, fonts, media relinks, nested sequences, keyframes and color transforms still varies.

## 5. Export matrix

| Output | Initial support proposal | Required verification |
|---|---|---|
| MP4 H.264 + AAC | P0 | Android playback, audio sync, duration, frame rate, audio peak, decoder compatibility |
| MOV ProRes | Optional | worker build, decoder, color/alpha handling, target editor open |
| WebM VP9/AV1 | Optional | device playback and alpha if supported |
| GIF | Optional | color palette/quality/file size |
| PNG/JPEG frame sequence | Optional | frame count, order, timestamps, alpha |
| WAV/FLAC/MP3/AAC | Optional | sample rate, channel layout, loudness/peak |
| SRT/VTT/ASS | P1 | text, word timings, style differences |
| OTIO | P2 | read/write, media relink, round-trip and loss report |
| FCPXML/EDL/AAF/OMF | P2 | destination editor import; feature parity report |
| CapCut/Alight Motion/Node Video native project | DEFERRED | exact target format, app version and round-trip tests |

## 6. Feature-loss report

Every interchange export should list:
- Preserved: clip timing, source trim, tracks, supported transforms, supported text/audio items.
- Approximation: font substitution, effects converted to baked video, speed curves approximated, flattening.
- Dropped: unsupported 3D camera, plugin effect, nested composition, advanced mask, proprietary generation metadata.
- Required media: missing files, linked assets, proxy/original references.
- Target app version and adapter version used.

## 7. Acceptance tests

TEST-070 rendered MP4 probe and playback pass; TEST-071 A/V sync within agreed tolerance; TEST-072 alpha verified with checkerboard; TEST-073 30/60/120fps frame count verified; TEST-074 OTIO import/export round-trip preserves supported clips; TEST-075 unsupported effects appear in loss report; TEST-076 Premiere import test; TEST-077 Resolve import test; TEST-078 CapCut import test on selected app version; TEST-079 Alight Motion package import test; TEST-080 Node Video project import test. No target passes before the actual import is verified.

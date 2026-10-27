# Verifikationsprotokoll / Verification record

**Date:** 27 October 2026 (Europe/Berlin)

**Source:** private `IamRedi/arboriculture-knowledge-studio`, isolated local branch `showcase/2026-10-27` at `a34199f1fe9c244f068110c0ed4ea217a488ea6f`, based on `936ed54b44bb67d54be8fe2c7643516b7fd93feb`. The public repository contains no application source or private Git history.

**Status distinction:** accepted `master` through AK-20.1; AK-20.2 on a private feature branch is verified for review, with owner acceptance and merge pending.

## Local evidence

| Check | Observation |
|---|---|
| Repository sync | Local feature HEAD matched the corresponding GitHub remote ref before work. The canonical GitHub branch was `master`; an older private registry reference still said `main`. |
| Isolation | Tests and screenshots used a separate Git worktree and synthetic SQLite database. The original owner database's SHA-256 was checked before and after; it was unchanged. |
| Automated tests | Full `pytest tests -q` in the isolated worktree: **261 passed**. The first run was 260 passed, 1 failed because a test assumed the ignored owner database exists in every worktree. The corrected test creates its own synthetic sentinel; a focused rerun passed, followed by the full rerun. |
| V4 smoke | Full `python tests/smoke_test.py`: PASS. Covered loopback startup, source/knowledge/editorial workflows, DOCX, backup/restore, guided publishing, retrieval, fake-provider AI, and Study stop/restart/resume; temporary state was cleaned. |
| End-to-end synthetic flow | Application routes created 2 fictional Sources, 3 Knowledge Units and provenance links; created a book and chapter; linked evidence; saved a version; created and resolved a comment; approved chapter and book; exported a DOCX; created a Course and viewed coverage. All expected routes returned success. |
| Browser | Chrome/Playwright checked 10 routes at 1440 × 900 and 390 × 844: 20 successful views, expected content, no page-level horizontal overflow, JavaScript errors or 404 responses. The checks were repeated on all 20 views with the English presentation translation. The five published screenshots were opened and visually checked. |
| Visual correction | A missing favicon caused a browser 404. A self-authored SVG favicon and HTML link removed that error. |
| Real AI API | Exactly 2 capped requests against the configured `gpt-5.6-terra` provider, one draft and one review, with synthetic case data. Both returned `authentication` and no model content or token usage. There were no retries. Live quality/citation correctness remains **not verified**. |
| Regression AI | The repository test suite uses a deterministic fake provider to check bounded request scope, rejection paths and persistence. This is not evidence of live model quality. |
| DOCX | The generated fictional case DOCX was checked as a ZIP-based DOCX payload. No DOCX is published here to avoid presenting the synthetic case as a professional manual. |

The live API attempts were constrained to at most 2,048 completion tokens each. The current [official GPT-5.6 Terra API price](https://developers.openai.com/api/docs/models/gpt-5.6-terra) is $2 per million input tokens and $12 per million output tokens. Both attempts were rejected before a model response; this record does not claim a measured invoice amount.

## Scope and limitations

- The runtime was local and bound to loopback. No hosted deployment or Production behavior was tested.
- The app is single-user/local-first; no login or multi-user authorization is implemented. Rights and evidence-scope gates were tested as application controls, not as identity authentication.
- The screenshots display self-authored fictional records. They do not display the owner's real literature, attachments, canonical database or private documents.
- Optional semantic retrieval was covered by repository tests and prior project evidence, but the public demo used the local lexical/default path; no model download was initiated for the showcase.

## Phase 2 — historical film and publication checks (superseded by bilingual edition)

| Check | Observation |
|---|---|
| Footage | Chrome/Playwright `recordVideo` captured the real local application at 1920 × 1080 and a portrait viewport, using the same isolated fictional Nordpark 07 database. Before capture, a browser-only text translation presented the existing UI labels in English. This is not a product localization: application source, routes, functions and data were unchanged. Original title and architecture cards are editorial graphics, not app screens. |
| Editing | Local FFmpeg encoded H.264/AAC MP4. German narration uses a local Windows system TTS voice. No paid media service, licensed music, stock footage, avatar or cloned voice was used. |
| Main film | **90.567 seconds**, 1920 × 1080, 30 fps. Full decode succeeded; 45 frames sampled across the entire timeline contained no black/blank scene. Audio mean/peak: −19.5/−0.7 dB. |
| Social film | **34.633 seconds**, 1080 × 1920, 30 fps. Full decode succeeded; 17 frames sampled across the entire timeline contained no black/blank scene. Audio mean/peak: −19.8/−1.3 dB. |
| Captions | German captions burnt into both films; German and English text subtitle tracks are also embedded. Separate DE/EN SRT files contain 16 synchronized cues for the main film and five for the social cut. Cue bounds were validated against film duration. |
| Visual review | Opening, application, editorial, study and closing frames were visually inspected at both aspect ratios. After the language correction, representative app frames across every application scene and all five screenshots were inspected for English UI labels and German fictional case content. Portrait cards and caption size were corrected after the first render. |
| AI credential diagnosis | A read-only `GET /v1/models/gpt-5.6-terra` against the configured OpenAI base returned **HTTP 401 `invalid_api_key`**. No secret was logged or changed, and no additional generation was attempted. Live AI output remains unverified. |
| Sources and rights | The raw recordings, original narration, scripts, timelines and captions are retained in a local source ZIP with a SHA-256 manifest. Public media and source package passed a file-list and content-safety audit. |

New external-service spend for Phase 2: **0 €**. A read-only credential check does not generate tokens.

## Final bilingual edition — 27 October 2026

The original two local-TTS films described above were preserved in the project archive and replaced in the public showcase by four Azure AI Speech editions. No application code, owner database, private branch or draft PR was changed during this edition.

| Version | Narrator | Format | Final duration |
|---|---|---|---|
| Master DE | `de-DE-ConradNeural` | 1920 × 1080, H.264/AAC, 30 fps | 98.667 s |
| Master EN | `en-GB-RyanNeural` | 1920 × 1080, H.264/AAC, 30 fps | 97.000 s |
| Social DE | `de-DE-ConradNeural` | 1080 × 1920, H.264/AAC, 30 fps | 37.500 s |
| Social EN | `en-GB-RyanNeural` | 1080 × 1920, H.264/AAC, 30 fps | 38.800 s |

The existing real-application recordings were reused. English editorial cards were prepared separately; app labels remain an English browser-only presentation translation. Azure's voice list confirmed the chosen Neural voices and the tested alternatives `de-DE-KatjaNeural`, `en-GB-SoniaNeural`, `en-US-GuyNeural` and `en-US-JennyNeural`. Short trials were generated before the final scripts. The Azure Speech resource was an existing **F0** instance in Germany West Central; 2,542 final-script characters were synthesized, with no new paid resource. The service key was passed through a local memory-only bridge and excluded from files and the public repository. The 0 € incremental cost is based on the F0 tier and usage below the published monthly allowance; it is not an invoice measurement.

Each video has one narration language, two selectable embedded text-subtitle tracks and separate SRT/VTT files for both languages. Subtitle cues were aligned to measured sentence audio boundaries. The website switches both video files, captions, metadata and download links together. Local full-decode, frame sampling, volume/peak, browser playback and public-link checks were performed for the final files; the automated checks and their limits are documented in the source archive. A machine cannot replace a human listening review of accent and pronunciation.

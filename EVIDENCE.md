# Verifikationsprotokoll / Verification record

**Date:** 27 October 2026 (Europe/Berlin)

**Source:** private `IamRedi/arboriculture-knowledge-studio`, isolated local branch `showcase/2026-10-27` based on `936ed54b44bb67d54be8fe2c7643516b7fd93feb`. The public repository contains no application source or private Git history.

**Status distinction:** accepted `master` through AK-20.1; AK-20.2 on a private feature branch is verified for review, with owner acceptance and merge pending.

## Local evidence

| Check | Observation |
|---|---|
| Repository sync | Local feature HEAD matched the corresponding GitHub remote ref before work. The canonical GitHub branch was `master`; an older private registry reference still said `main`. |
| Isolation | Tests and screenshots used a separate Git worktree and synthetic SQLite database. The original owner database's SHA-256 was checked before and after; it was unchanged. |
| Automated tests | Full `pytest tests -q` in the isolated worktree: **261 passed**. The first run was 260 passed, 1 failed because a test assumed the ignored owner database exists in every worktree. The corrected test creates its own synthetic sentinel; a focused rerun passed, followed by the full rerun. |
| V4 smoke | Full `python tests/smoke_test.py`: PASS. Covered loopback startup, source/knowledge/editorial workflows, DOCX, backup/restore, guided publishing, retrieval, fake-provider AI, and Study stop/restart/resume; temporary state was cleaned. |
| End-to-end synthetic flow | Application routes created 2 fictional Sources, 3 Knowledge Units and provenance links; created a book and chapter; linked evidence; saved a version; created and resolved a comment; approved chapter and book; exported a DOCX; created a Course and viewed coverage. All expected routes returned success. |
| Browser | Chrome/Playwright checked 10 routes at 1440 × 900 and 390 × 844: 20 successful views, expected content, no page-level horizontal overflow, JavaScript errors or 404 responses. The screenshots were opened and visually checked. |
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
- No demo video is included. The available local capture setup produced still images only; this omission does not affect the feature claims above.

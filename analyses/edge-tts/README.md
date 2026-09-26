# Edge-TTS

Reverse-engineered Python client for Microsoft Edge's "Read Aloud" TTS websocket.

- **Upstream:** <https://github.com/rany2/edge-tts>
- **Analyzed release:** `7.2.8` (2026-03-22)
- **Snapshot:** `sources/edge-tts/` — `git clone --depth=1 --branch=7.2.8`
- **Analysis:** `analysis.md`
- **Analyzed:** 2026-09-27

## Files

| Path | What it is |
| --- | --- |
| `analysis.md` | Architecture, protocol, API surface, risk analysis, release history, design notes |
| `../../sources/edge-tts/` | Full source tree of upstream at tag `7.2.8` (read-only snapshot) |

## TL;DR from the analysis

Pure-Python client to `speech.platform.bing.com`. ~6.6 M downloads/month, 12 k
stars. No API key needed. Solid for personal / OSS / research use; risky for
commercial SLAs because MS rotates the `TRUSTED_CLIENT_TOKEN` and
`CHROMIUM_FULL_VERSION` roughly every quarter (release history shows 5 patches
between 2025-08 and 2026-03 alone).

The biggest correctness change (PR #468) replaced metadata-based offset
compensation with byte-count math against the CBR 48 kbps mono MP3 stream —
subtitle timings are now monotonic for any text length.
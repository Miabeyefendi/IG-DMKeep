# Changelog

All notable changes to **IG-DMKeep** are recorded here. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and this project uses
[Semantic Versioning](https://semver.org/spec/v2.0.0.html).

[README](./README.md) · [Releases](https://github.com/Miabeyefendi/IG-DMKeep/releases)

---

## [Unreleased]

### Changed

- Repository renamed from `InstaDM-Scraper` to `IG-DMKeep`. The old URL
  redirects, so existing links and clones keep working. The tool exports your
  own conversations, which is data portability rather than scraping, and the
  name now says so.
- Relicensed from MIT to AGPL-3.0, with the attribution and commercial terms in
  `NOTICE`.
- README published in five languages: English, Turkish, Spanish, Chinese and
  Russian.
- The tutorial was one file holding three languages at once. It is now five
  separate files, one per language, so they can drift apart visibly instead of
  silently.
- Language files renamed from `README.tr.md` and `README.es.md` to
  `README_TR.md` and `README_ES.md`, matching the convention used across all
  repositories.

### Fixed

- **The `v2.0.0` tag pointed at the first commit**, so the release archive
  shipped the v1 script instead of v2. Anyone who downloaded the v2.0.0 source
  archive received 342 lines of v1 rather than the 3700-line v2 tool. The tag
  now points at the commit that actually contains v2.
- The script header advertised itself as `v2.0.0-beta` while the release was
  published as `v2.0.0`, and linked to the old repository name.
- Documented the requirement that an actual DM thread must be open before the
  script runs. This was the cause of the "Conversation container not found"
  report in issue #1 and had never been written down.
- **Short conversations failed with "Conversation container not found"** even
  with the thread open (issue #2). The container search only accepted a
  message list that overflowed by more than 200px, so a thread that fit on one
  screen was never found. It now falls back to the scrollable message list
  when nothing overflows.
- **The minimized overlay still blocked the whole page.** Its invisible
  full-screen box kept catching clicks and scrolling, so you could not open
  another conversation or leave the current one. Only the visible panel takes
  input now, and the minimized panel is a compact bar in the bottom-right
  corner.

---

## [2.0.0] - 2026-03-23

A rewrite around an overlay interface and real media capture. The v1 script
printed to the console and exported text; this one is a tool with a UI.

### Added

- An overlay panel injected into the page, replacing raw console output. Scan
  control, timeline filtering and export options all live there.
- Media capture through network interception. Fetch and XHR are hooked and the
  `PerformanceObserver` is monitored to recover direct links for reels, voice
  messages and full-resolution images that never appear in the DOM.
- ZIP export. Media files are downloaded and packaged alongside the text into a
  single structured archive, built in the browser.
- Voice message transcription, collecting Instagram's own transcripts so voice
  notes end up searchable in the export.
- Four export formats: JSON, TXT, Markdown and ZIP.
- Keyword search, and filters to narrow the timeline to images, audio or reels.
- Per-message selection, so an export can be a subset rather than everything.
- Localised export output. Headers follow the chosen language, so a Turkish
  export writes `Gönderilen:` rather than `Sent:`.
- Reel metadata resolution, finding direct MP4 URLs and thumbnails.

---

## [1.0.0] - 2026-02-07

### Added

- Browser console DM exporter in 342 lines.
- Full chat history extraction with timestamps and sender detection.
- Story replies, reactions and media labels in the output.
- Text export, with no dependency on any API key or extension.
- Handles Instagram's virtual scrolling, which unloads messages from the page
  as you move through a thread.

---

[Unreleased]: https://github.com/Miabeyefendi/IG-DMKeep/compare/v2.0.0...HEAD
[2.0.0]: https://github.com/Miabeyefendi/IG-DMKeep/compare/v1.0.0...v2.0.0
[1.0.0]: https://github.com/Miabeyefendi/IG-DMKeep/releases/tag/v1.0.0

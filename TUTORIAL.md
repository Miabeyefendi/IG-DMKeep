<div align="center">

# 📖 IG-DMKeep Tutorial

**v2.0.0 · Last updated 2026-08-18**

**English** · [Türkçe](./TUTORIAL_TR.md) · [Español](./TUTORIAL_ES.md) · [简体中文](./TUTORIAL_ZH.md) · [Русский](./TUTORIAL_RU.md)

[Back to README](./README.md) · [Changelog](./CHANGELOG.md)

</div>

---

This document explains how IG-DMKeep works underneath. If you only want to run
it, the [README](./README.md) is shorter.

## 📑 Contents

- [Overview](#-overview)
- [Installation](#-installation)
- [Interface tour](#️-interface-tour)
- [Feature reference](#-feature-reference)
- [Configuration reference](#️-configuration-reference)
- [Troubleshooting](#-troubleshooting)
- [FAQ](#-faq)
- [Glossary](#-glossary)

---

## 🔭 Overview

### What it does

Instagram gives you a data download, but what arrives is an archive built for
compliance rather than for reading. IG-DMKeep takes the opposite approach: it
reads the conversation you are looking at, in the browser you are already
logged into, and writes it out in a shape you can actually use.

### How it works

```
  DM thread open in the page
        |
        |  scroll driver walks the thread backwards
        v
  DOM parser  ------------------> message records
        |                          text, timestamp, sender, reactions
        |
  network hooks (fetch / XHR / PerformanceObserver)
        |                          direct media URLs the DOM never shows
        v
  merge by message id
        |
        +--> JSON        structured, for processing
        +--> TXT         plain, for reading
        +--> Markdown    for publishing
        +--> ZIP         text plus the downloaded media files
```

The important part is the second input. Instagram does not put a usable link to
a reel or a voice note in the DOM, so parsing the page alone gives you a message
that says "there was a video here". The hooks watch the traffic the page itself
generates and keep the URLs that go past.

### File layout

| Path | What it is |
|---|---|
| `instadm-scraper-v2.js` | The current tool, 3700 lines, everything described here |
| `instadm-scraper.js` | The original 342-line version, console output and text export |

---

## 📦 Installation

### Requirements

- A desktop browser. The mobile site does not render the conversation the same
  way and is not supported.
- Your own Instagram account, logged in at `www.instagram.com`.
- Nothing else. No extension, no build step, no API key.

### Step by step

1. Open `www.instagram.com` and log in.
2. Open the DM thread you want to save. **Not the inbox list, the thread
   itself.** The script reads what is rendered, and on the inbox there is no
   conversation to read.
3. Wait until the messages are visible.
4. Open the console with `F12`, or `Ctrl + Shift + J` on Chrome and Edge,
   `Ctrl + Shift + K` on Firefox, `Cmd + Option + J` on a Mac.
5. Paste the whole of `instadm-scraper-v2.js` and press Enter.

Some browsers block pasted code in the console until you type `allow pasting`
once. That is a browser safety feature, not an error from this script.

### Verifying it worked

The overlay panel appears over the page. If instead you see
`Conversation container not found`, step 2 did not happen: go into the thread
and try again.

### Uninstalling

Reload the page. Nothing is installed and nothing persists.

---

## 🖥️ Interface tour

The panel is injected into the page and floats above it. The layout underneath
is untouched, so Instagram keeps working while the panel is open.

| Area | What it holds |
|---|---|
| Scan | Start, progress, and the running message count |
| Filter | Keyword box, and type filters for images, audio and reels |
| Timeline | The collected messages, each with a checkbox |
| Export | Format picker, language picker, media and transcription toggles |

---

## 🧩 Feature reference

### Media capture and the hook system

**What it does.** Recovers direct URLs for reels, voice messages and
full-resolution images.

**How it works.** Before scanning starts, `fetch` and `XMLHttpRequest` are
wrapped so every request the page makes passes through the tool first. In
parallel a `PerformanceObserver` watches resource timing entries, which catches
media the page loads through paths the wrappers do not see. Blob URLs are
intercepted as well, because Instagram serves some media as blobs that would
otherwise be unreachable once the page moves on. Whatever looks like media is
kept in a table keyed by message.

**Limits.** A hook only sees traffic that happens while the tool is running.
Media that loaded before you pasted the script has already been and gone, which
is one reason the scan walks the thread rather than reading what is on screen.

### Sender detection

**What it does.** Decides, for each message, whether you sent it or the other
person did.

**How it works.** Instagram does not label this in a way that survives its own
redesigns, so direction is inferred from layout and structural position rather
than from a class name that changes every few months. Messages are grouped by
run, because a block of consecutive messages from one person shares its
direction.

**Limits.** Group threads with several participants are harder than one to one
conversations, and unusual message types can be misattributed.

### Voice message transcription

**What it does.** Turns voice notes into searchable text in the export.

**How it works.** It does not run speech recognition. Instagram already
generates transcripts for voice messages; this mode requests and collects them,
then attaches each one to its message.

**Limits.** If Instagram has no transcript for a note, there is nothing to
collect. Accuracy is Instagram's, not this tool's.

### ZIP export

**What it does.** Packages the conversation text together with the actual media
files into one archive.

**How it works.** The archive is built in the browser. Each captured media URL
is fetched, held in memory, and written into a structured ZIP alongside the
text export.

**Limits.** This is the slow path, because it downloads every file. Long threads
with many reels take a while and use real bandwidth. Very large conversations
can run into browser memory limits; export in sections if that happens.

---

## ⚙️ Configuration reference

### Export

| Option | Values | Effect |
|---|---|---|
| Format | JSON, TXT, Markdown, ZIP | Output shape. ZIP is the only one that includes media files. |
| Selection | All, or ticked messages | Export everything, or just what you selected |
| Language | English, Turkish, Spanish | Language of the headers written into the file |

### Filter

| Option | Effect |
|---|---|
| Keyword | Show only messages containing the text |
| Type | Narrow to images only, audio only, or reels only |

### Media

| Option | Effect |
|---|---|
| Download media | Fetch the real files and include them in the ZIP |
| Transcription | Collect Instagram's transcripts for voice messages |

### Where anything is stored

Nowhere. Nothing is written outside the export file your browser saves, and
nothing is kept between runs. Reloading the page ends everything.

---

## 🔧 Troubleshooting

### "Conversation container not found. Open a DM thread first."

**Cause.** The script found no rendered conversation. Being logged in, or
sitting on the inbox list, is not enough.
**Fix.** Click into the thread, wait until messages are visible, then paste. If
the thread is open and the error persists, Instagram has changed its markup;
open an issue with your browser and version.

### Old messages are missing from the export

**Cause.** Instagram unloads messages from the page as you scroll, so they are
not in the DOM to be read.
**Fix.** Let the scan run to completion. It walks the thread backwards on
purpose. Long conversations take time.

### Media is missing, or the ZIP has fewer files than expected

**Cause.** The media loaded before the hooks were installed, or its URL expired
before the download ran.
**Fix.** Reload the page, paste the script first, and only then scan. Do not
browse the thread manually before starting.

### The browser refuses to accept the pasted script

**Cause.** A browser safety feature against paste-based social engineering.
**Fix.** Type `allow pasting` in the console once, then paste.

### The tab freezes or runs out of memory

**Cause.** A very long thread with a lot of media held in memory for the ZIP.
**Fix.** Export as TXT or JSON instead, or export in sections using the message
selection.

### Collecting a log for a bug report

Copy the console output. **Before posting it, remove anything that identifies
you or the other person:** usernames, message text, session cookies and any
URL containing a token. An issue is public and permanent.

---

## ❓ FAQ

**Does anything leave my machine?**
Only the requests Instagram would make anyway. There is no server belonging to
this project, and no analytics.

**Can it read conversations I am not part of?**
No. It can only see what your own logged-in session can already display.

**Why is there still a v1 file?**
Because 342 lines can be read in one sitting and verified by eye. Some people
would rather audit a small script than trust a large one.

**Does it work on the mobile site?**
No. The conversation is rendered differently and the selectors do not apply.

---

## 📕 Glossary

| Term | Meaning |
|---|---|
| Hook | A wrapper around `fetch` or `XHR` that lets the tool see requests the page makes |
| PerformanceObserver | A browser API reporting loaded resources, used to catch media the hooks miss |
| Blob URL | A temporary in-memory URL, used by Instagram for some media |
| Virtual scrolling | Removing off-screen items from the page to save memory, which is why the scan walks the thread |
| Direction | Whether a message was sent by you or received |

---

<div align="center">
<img src="./assets/divider.svg" width="100%" height="3" alt="">
<br/>
<sub>Built by <b><a href="https://github.com/Miabeyefendi">Miabeyefendi</a></b> · <a href="./README.md">Back to README</a></sub>
</div>

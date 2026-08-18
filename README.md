<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/logo-dark.svg">
  <img src="./assets/logo.svg" width="120" alt="IG-DMKeep">
</picture>

# IG-DMKeep

**Save your own Instagram conversations before you lose them. Full history with timestamps, senders, reactions and media, exported to JSON, TXT, Markdown or a ZIP. Everything happens in your browser.**

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-A78BFA?style=for-the-badge&logo=gnu&logoColor=white)](./LICENSE)
[![Version](https://img.shields.io/github/v/release/Miabeyefendi/IG-DMKeep?style=for-the-badge&color=F59E0B&label=version)](https://github.com/Miabeyefendi/IG-DMKeep/releases/latest)
[![Platform](https://img.shields.io/badge/Browser_Console-1E293B?style=for-the-badge&logo=googlechrome&logoColor=white)](#-installation)
[![Status](https://img.shields.io/badge/status-active-22C55E?style=for-the-badge)](#)
[![Author](https://img.shields.io/badge/by-Miabeyefendi-0EA5E9?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Miabeyefendi)

**English** · [Türkçe](./README_TR.md) · [Español](./README_ES.md) · [简体中文](./README_ZH.md) · [Русский](./README_RU.md)

[Install](#-installation) · [Features](#-highlights) · [Usage](#-quick-start) · [Tutorial](./TUTORIAL.md) · [Changelog](./CHANGELOG.md)

<a href="https://github.com/Miabeyefendi/IG-DMKeep/releases/latest">
  <img src="./assets/btn-download.svg" height="52" alt="Download the latest release">
</a>
<a href="./TUTORIAL.md">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./assets/btn-tutorial-dark.svg">
    <img src="./assets/btn-tutorial.svg" height="52" alt="Read the tutorial">
  </picture>
</a>

</div>

---

## ✨ Highlights

- **Your data stays yours** - everything runs locally in your browser. No server, no extension, no API key, no analytics. Nothing about your conversations leaves your machine.
- **An overlay, not a wall of console output** - a panel is injected into the page where you control the scan, filter the timeline and choose what to export.
- **Four export formats** - JSON for processing, TXT for reading, Markdown for publishing, or a ZIP that packages the media alongside the text.
- **Media that the page does not show you** - the tool watches network traffic and the `PerformanceObserver` to recover direct links for reels, voice messages and full-resolution images that never appear in the DOM.
- **Voice messages as text** - a dedicated mode collects Instagram's own transcripts for voice notes so the export is searchable.
- **Filter and search before exporting** - find messages by keyword, or narrow the timeline to images, audio or reels only.
- **Export a selection, not just everything** - tick the messages you actually want.
- **Output in your language** - the export headers follow your language choice, so a Turkish export reads `Gönderilen:` rather than `Sent:`.
- **Survives virtual scrolling** - Instagram unloads messages as you scroll; the scan is built around that instead of fighting it.

---

## 📦 Installation

### Requirements

| | |
|---|---|
| Browser | Chrome, Edge or Firefox on desktop |
| Account | Your own Instagram account, with a DM thread open |
| Install | None. This is a console script. |

![JavaScript](https://img.shields.io/badge/JavaScript-1E293B?style=for-the-badge&logo=javascript&logoColor=A78BFA)
![Instagram](https://img.shields.io/badge/Instagram-1E293B?style=for-the-badge&logo=instagram&logoColor=A78BFA)

### Pick a version

| Version | File | What it is |
|---|---|---|
| **v2** | [`instadm-scraper-v2.js`](./instadm-scraper-v2.js) | The current one. Overlay UI, media capture, ZIP export, transcription. |
| **v1** | [`instadm-scraper.js`](./instadm-scraper.js) | The original. Console output only, text export, 342 lines. Kept for anyone who wants something small they can read end to end. |

<details>
<summary><b>Prefer to clone?</b></summary>

```bash
git clone https://github.com/Miabeyefendi/IG-DMKeep.git
```

No build step and no dependencies.

</details>

---

## 🚀 Quick Start

1. Open [www.instagram.com](https://www.instagram.com/) on desktop and log in.
2. **Open the DM thread you want to save.** The script reads the conversation that is currently on screen, so this step is not optional.
3. Open the console. `F12` or `Ctrl + Shift + J` on Chrome and Edge, `Ctrl + Shift + K` on Firefox. On a Mac, `Cmd + Option + J`.
4. Paste [`instadm-scraper-v2.js`](./instadm-scraper-v2.js) in full and press Enter.
5. The overlay appears. Start the scan, wait for it to walk back through the thread, then choose an export format.

> **If you get "Conversation container not found", you are not inside a thread.** Opening the inbox is not enough. Click into the actual conversation first, wait for the messages to render, then paste the script.

---

## ⚙️ Configuration

Everything is set in the overlay, nothing is edited in the file.

| Group | Option | What it does |
|---|---|---|
| Export | Format | JSON, TXT, Markdown or ZIP |
| Export | Selection | The whole conversation, or only the messages you tick |
| Export | Language | Language of the headers written into the export file |
| Filter | Keyword | Show only messages containing a word or phrase |
| Filter | Type | Images only, audio only, or reels only |
| Media | Download media | Fetch the actual files and package them into the ZIP |
| Media | Transcription | Collect Instagram's transcripts for voice messages |

How each of these works underneath, and what to do when one of them misbehaves, is in the [tutorial](./TUTORIAL.md).

---

## 📖 Documentation

- [**Tutorial**](./TUTORIAL.md) - how the capture, sender detection, transcription and ZIP engines actually work
- [**Changelog**](./CHANGELOG.md) - what changed in each release
- [**Contributing**](./CONTRIBUTING.md) - how to send a change
- [**Security**](./SECURITY.md) - how to report a vulnerability privately

---

## ❓ FAQ

<details>
<summary><b>"Conversation container not found. Open a DM thread first."</b></summary>

The script did not find a rendered conversation on the page. Being logged in or sitting on the inbox list is not enough. Open the specific thread, wait until the messages are visible, and only then paste the script. If the thread is open and you still see this, Instagram has changed its markup; open an issue with your browser version.

</details>

<details>
<summary><b>Does this send my messages anywhere?</b></summary>

No. Everything runs in the page you already have open, and the export is written by your browser to your own disk. There is no server, no extension and no analytics. That is the entire reason this is a console script.

</details>

<details>
<summary><b>Can I export someone else's DMs?</b></summary>

No. The script can only read what your own logged-in session can already display. It is a way to keep a copy of your own conversations, nothing more.

</details>

<details>
<summary><b>Why does the ZIP take so long?</b></summary>

Because it downloads the actual media files one by one and packages them in the browser. A long thread with many reels and voice notes is a lot of traffic. Text-only exports are close to instant.

</details>

<details>
<summary><b>Some old messages are missing.</b></summary>

Instagram unloads messages as you scroll, so the scan has to walk back through the thread to bring them into the page. Let it finish. On very long conversations this takes a while.

</details>

<details>
<summary><b>Should I use v1 or v2?</b></summary>

v2, unless you specifically want something small enough to read in one sitting. v1 is 342 lines and exports plain text; v2 is the full tool.

</details>

---

## 🤝 Contributing

Contributions are welcome. Read [CONTRIBUTING.md](./CONTRIBUTING.md) and [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md) first. By contributing you agree to license your work under the AGPL-3.0.

<div align="center">
<a href="https://github.com/Miabeyefendi/IG-DMKeep/issues/new?template=bug_report.yml">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./assets/btn-report-bug-dark.svg">
    <img src="./assets/btn-report-bug.svg" height="52" alt="Report a bug">
  </picture>
</a>
<a href="https://github.com/Miabeyefendi/IG-DMKeep/stargazers">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./assets/btn-star-dark.svg">
    <img src="./assets/btn-star.svg" height="52" alt="Star this repository">
  </picture>
</a>
</div>

---

## 🛡️ Security

Found a vulnerability? Do not open a public issue. Follow the private process in [SECURITY.md](./SECURITY.md).

---

## 📜 License

IG-DMKeep is licensed under the **GNU Affero General Public License v3.0 (AGPL-3.0)**, together with the supplemental terms in the [NOTICE](./NOTICE) file. In short:

- You may use, study, modify, redistribute and even make money with this work for free, **as long as** you keep the complete source code available under the AGPL-3.0, including for any hosted, SaaS or network use (AGPL Section 13), and you preserve the author attribution below.
- To use this work in a closed-source or proprietary product, or to run it as a closed SaaS, you need a **separate written commercial license**, which may include a royalty or revenue share. See [NOTICE](./NOTICE), Section 8, and contact me.

### Attribution (required)

Per AGPL-3.0 Section 7(b), the following attribution must be preserved, visibly and unmodified, in any copy, fork or deployment of this project:

> **Miabeyefendi (Mustafa Ihsan Albayrak)** - https://github.com/Miabeyefendi

### Disclaimer

This software is provided "as is", without warranty of any kind. You run it entirely at your own risk and are solely responsible for your own use, including compliance with the terms of service of any third-party platform it interacts with, notably Instagram. Instagram is not affiliated with or endorsing this project; its name and trademarks belong to their owner. The author accepts no liability for account bans, data loss or any other damages, to the maximum extent permitted by applicable law. Full terms are in the [LICENSE](./LICENSE) and [NOTICE](./NOTICE) files.

---

## 📬 Contact

- GitHub: [@Miabeyefendi](https://github.com/Miabeyefendi)
- For commercial licensing or revenue-sharing enquiries, reach me through my GitHub profile.

<div align="center">
<br/>
<img src="./assets/divider.svg" width="100%" height="3" alt="">
<br/>
<sub>Built by <b><a href="https://github.com/Miabeyefendi">Miabeyefendi</a></b></sub>
</div>

# 📨 InstaDM-Scraper V2: Ultimate Instagram DM Toolkit | By: @miabeyefendi

## Export, Capture, and Transcribe Instagram DMs with a Professional Dashboard — No Extension, No API
**InstaDM-Scraper V2** is a massive evolution of the original browser-based exporter. It transforms from a simple console script into a full-featured **Interactive Dashboard** injected directly into your Instagram DM page. 

Developed by **@miabeyefendi**, V2 now features **Live Media Interception**, **Localized Outputs (EN/TR/ES)**, **Audio-to-Text Transcription**, and **Binary ZIP Exports**. It bypasses Instagram's 24-hour data wait time by scraping directly from your active session with a user-friendly UI.

[![JavaScript](https://img.shields.io/badge/JavaScript-ES2020+-F7DF1E.svg?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Platform](https://img.shields.io/badge/Platform-Browser_Console-4285F4.svg?style=for-the-badge&logo=googlechrome&logoColor=white)](https://github.com/Miabeyefendi/InstaDM-Scraper)
[![Localization](https://img.shields.io/badge/Languages-EN%20|%20TR%20|%20ES-rebeccapurple.svg?style=for-the-badge)](https://github.com/Miabeyefendi/InstaDM-Scraper)
[![No API](https://img.shields.io/badge/API-Not_Required-success.svg?style=for-the-badge)](https://github.com/Miabeyefendi/InstaDM-Scraper)

[TR | Türkçe Oku](README.tr.md) | [ES | Leer en Español](README.es.md)

---

## 🔥 Why Upgrade to V2?

V1 was a script; **V2 is a toolkit.** 

- 🖥️ **Interactive Overlay UI**  
  No more looking at the raw console. Control your scan, filter messages, and choose export options from a modern dashboard injected into the page.

- 🌍 **Fully Localized Exports**  
  The tool and the output files now respect your language choice. If set to English, headers are `Sent:`. If Turkish, `Gönderilen:`. If Spanish, `Enviado:`.

- 📻 **Live Media Capture (Hooks)**  
  V2 intercepts network requests (XHR/Fetch) and monitors the `PerformanceObserver` to catch direct links for Reels, Voice Messages, and high-res images that aren't usually visible in the DOM.

- 📦 **Binary ZIP Export**  
  Don't just export text. V2 can attempt to download the physical media files (Images, Audio, Reel MP4s) and package them into a single structured ZIP file.

- 🎙️ **Voice-to-Text (Transcription)**  
  A specialized mode that automates the collection of Instagram's internal transcripts for voice messages.

---

## ✨ Core Features

- **Multi-Format Export**  
  Download your chat history as **JSON**, **TXT**, **Markdown (MD)**, or a full **ZIP** archive.

- **Deep Media Discovery**  
  Automatically resolves Reel metadata to find direct MP4 video URLs and thumbnails.

- **Smart Filtering & Search**  
  Instantly find messages using keywords or filter the timeline by "Images Only", "Audio Only", or "Reels Only".

- **Message Selection**  
  Export the entire conversation or use checkboxes to select only specific messages you need.

- **Privacy-First Design**  
  Runs 100% locally in your browser. Your data never leaves your computer. No third-party servers, no extensions, no analytics.

---

## 🛠️ Getting Started

### Usage

1. Open an Instagram DM conversation: `https://www.instagram.com/direct/t/XXXXXXXXX/`
2. Open DevTools (**F12** or **Ctrl+Shift+I**) and click the **Console** tab.
3. Paste the entire content of `instadm-scraper-v2.js` and press **Enter**.
4. The **InstaDM Dashboard** will appear on your screen.
5. Select your language (EN/TR/ES) and click **"Start Scan"**.
6. Wait for the auto-scroller to finish. Once done, use the sidebar to filter, search, or download your data.

---

## 📋 Localized Output Example (EN vs TR)

V2 adapts its labels based on your selected UI language:

| Language | Date Header | Sender Label | Media Tag |
|---|---|---|---|
| **English** | `Date: 12 May 2025` | `Sent:` / `Received:` | `[Image]`, `[Audio]` |
| **Turkish** | `Tarih: 12 May 2025` | `Gönderilen:` / `Gelen:` | `[Görsel]`, `[Ses]` |
| **Spanish** | `Fecha: 12 May 2025` | `Enviado:` / `Recibido:` | `[Imagen]`, `[Audio]` |

---

## 🔧 Technical Overview (V2 Enhancements)

| Feature | Technical Implementation |
|---|---|
| **Network Interception** | Overrides `window.fetch` and `XMLHttpRequest` to capture media metadata. |
| **Blob Handling** | Hooks into `URL.createObjectURL` to identify voice message blobs. |
| **ZIP Generation** | Uses a zero-dependency custom ZIP builder with CRC32 checksums. |
| **Reel Resolver** | Asynchronously fetches Reel pages to extract `og:video` and `og:image` tags. |
| **Adaptive UI** | Built with pure CSS/JS Blur-morphism, responsive to viewport changes. |

---

## 📈 Version History

**v2.0.0 (Latest)**
- Added Interactive Overlay UI.
- Multi-language support (EN, TR, ES) for UI and Output.
- Added ZIP, JSON, and Markdown export formats.
- Real-time media interception (Voice, Reels, Images).
- Voice message transcript extraction tool.
- Selection, Search, and Category filtering.

**v1.0.0**
- Initial release. Console-based .txt exporter.

---

## 👨‍💻 Author

**Miabeyefendi**
- GitHub: [@Miabeyefendi](https://github.com/Miabeyefendi)
- Project: **InstaDM-Scraper**

*Built for privacy, designed for simplicity.*

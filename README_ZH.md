<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/logo-dark.svg">
  <img src="./assets/logo.svg" width="120" alt="IG-DMKeep">
</picture>

# IG-DMKeep

**在弄丢之前，把你自己的 Instagram 私信存下来。完整的聊天记录，带时间戳、发送者、表情回应和媒体文件，可导出为 JSON、TXT、Markdown 或 ZIP。全过程都在你的浏览器里完成。**

[![许可证: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-A78BFA?style=for-the-badge&logo=gnu&logoColor=white)](./LICENSE)
[![版本](https://img.shields.io/github/v/release/Miabeyefendi/IG-DMKeep?style=for-the-badge&color=F59E0B&label=version)](https://github.com/Miabeyefendi/IG-DMKeep/releases/latest)
[![平台](https://img.shields.io/badge/Browser_Console-1E293B?style=for-the-badge&logo=googlechrome&logoColor=white)](#-安装)
[![状态](https://img.shields.io/badge/status-active-22C55E?style=for-the-badge)](#)
[![作者](https://img.shields.io/badge/by-Miabeyefendi-0EA5E9?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Miabeyefendi)

[English](./README.md) · [Türkçe](./README_TR.md) · [Español](./README_ES.md) · **简体中文** · [Русский](./README_RU.md)

[安装](#-安装) · [功能](#-亮点) · [用法](#-快速开始) · [教程](./TUTORIAL_ZH.md) · [更新日志](./CHANGELOG.md)

<a href="https://github.com/Miabeyefendi/IG-DMKeep/releases/latest">
  <img src="./assets/btn-download.svg" height="52" alt="下载最新版本">
</a>
<a href="./TUTORIAL_ZH.md">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./assets/btn-tutorial-dark.svg">
    <img src="./assets/btn-tutorial.svg" height="52" alt="阅读教程">
  </picture>
</a>

</div>

---

## ✨ 亮点

- **你的数据仍然是你的** - 一切都在你的浏览器里本地运行。没有服务器，没有扩展，没有 API 密钥，没有埋点。你的聊天内容不会离开你的电脑。
- **是一个界面，不是一屏控制台输出** - 脚本会往页面里注入一个面板，你在那里控制扫描、筛选时间线、决定导出什么。
- **四种导出格式** - JSON 用于处理，TXT 用于阅读，Markdown 用于发布，ZIP 则把媒体和文字打包在一起。
- **页面不给你看的媒体** - 工具监听网络请求和 `PerformanceObserver`，把 reels、语音消息和高清图片那些从不出现在 DOM 里的直链找回来。
- **语音消息转成文字** - 专门的模式会收集 Instagram 自己的语音转写结果，让导出内容可以被搜索。
- **导出前先筛选和搜索** - 用关键词找消息，或者把时间线收窄到只看图片、只看语音、只看 reels。
- **可以只导出选中的部分** - 勾选你真正需要的消息。
- **输出用你的语言** - 导出文件里的表头跟随你的语言选择，土耳其语导出写的是 `Gönderilen:` 而不是 `Sent:`。
- **扛得住虚拟滚动** - Instagram 会随着滚动卸载消息，扫描是按照这个前提设计的，而不是跟它对着干。

---

## 📦 安装

### 环境要求

| | |
|---|---|
| 浏览器 | 桌面端 Chrome、Edge 或 Firefox |
| 账号 | 你自己的 Instagram 账号，并且已经打开一个私信会话 |
| 安装 | 无。这是一个控制台脚本。 |

![JavaScript](https://img.shields.io/badge/JavaScript-1E293B?style=for-the-badge&logo=javascript&logoColor=A78BFA)
![Instagram](https://img.shields.io/badge/Instagram-1E293B?style=for-the-badge&logo=instagram&logoColor=A78BFA)

### 选一个版本

| 版本 | 文件 | 是什么 |
|---|---|---|
| **v2** | [`instadm-scraper-v2.js`](./instadm-scraper-v2.js) | 当前版本。浮层界面、媒体捕获、ZIP 导出、语音转写。 |
| **v1** | [`instadm-scraper.js`](./instadm-scraper.js) | 最初的版本。只有控制台输出、文本导出，342 行。留给想要一个能从头读到尾的小东西的人。 |

<details>
<summary><b>更想用克隆？</b></summary>

```bash
git clone https://github.com/Miabeyefendi/IG-DMKeep.git
```

没有构建步骤，也没有依赖。

</details>

---

## 🚀 快速开始

1. 在桌面端打开 [www.instagram.com](https://www.instagram.com/) 并登录。
2. **打开你要保存的那个私信会话。** 脚本读取的是当前显示在屏幕上的会话，所以这一步不是可选的。
3. 打开控制台。Chrome 和 Edge 按 `F12` 或 `Ctrl + Shift + J`，Firefox 按 `Ctrl + Shift + K`。Mac 上按 `Cmd + Option + J`。
4. 把 [`instadm-scraper-v2.js`](./instadm-scraper-v2.js) 整个粘贴进去，回车。
5. 界面出现。启动扫描，等它沿着会话往回走完，然后选择导出格式。

> **如果你看到 "Conversation container not found"，说明你不在会话里面。** 打开收件箱是不够的。先点进具体的那个会话，等消息渲染出来，然后再粘贴脚本。

---

## ⚙️ 配置

一切都在界面里设置，不用改文件。

| 分组 | 选项 | 作用 |
|---|---|---|
| Export | Format | JSON、TXT、Markdown 或 ZIP |
| Export | Selection | 整段会话，或者只导出你勾选的消息 |
| Export | Language | 写进导出文件的表头使用的语言 |
| Filter | Keyword | 只显示包含某个词或短语的消息 |
| Filter | Type | 只看图片、只看语音，或只看 reels |
| Media | Download media | 下载真实的媒体文件并打包进 ZIP |
| Media | Transcription | 为语音消息收集 Instagram 的转写文本 |

这些功能底层是怎么运作的、其中某一项出问题时该怎么办，都写在[教程](./TUTORIAL_ZH.md)里。

---

## 📖 文档

- [**教程**](./TUTORIAL_ZH.md) - 捕获、发送者识别、语音转写和 ZIP 引擎实际是怎么工作的
- [**更新日志**](./CHANGELOG.md) - 每个版本改了什么
- [**参与贡献**](./CONTRIBUTING.md) - 如何提交修改
- [**安全**](./SECURITY.md) - 如何私下报告漏洞

---

## ❓ 常见问题

<details>
<summary><b>"Conversation container not found. Open a DM thread first."</b></summary>

脚本在页面上没有找到已渲染的会话。仅仅登录了、或者停在收件箱列表上是不够的。点进具体的会话，等消息可见，然后再粘贴脚本。如果会话已经打开、消息也看得见却仍然报这个错，那就是 Instagram 改了页面结构，请附上你的浏览器版本提一个 issue。

</details>

<details>
<summary><b>它会把我的消息发到什么地方吗？</b></summary>

不会。一切都在你已经打开的那个页面里运行，导出文件由你的浏览器写到你自己的硬盘上。没有服务器，没有扩展，没有埋点。这正是它做成控制台脚本的全部原因。

</details>

<details>
<summary><b>我能导出别人的私信吗？</b></summary>

不能。脚本只能读取你自己已登录的会话本来就能显示的内容。它的用途是给自己的对话留一份备份，仅此而已。

</details>

<details>
<summary><b>ZIP 为什么这么慢？</b></summary>

因为它要把真实的媒体文件一个个下载下来，再在浏览器里打包。一段包含大量 reels 和语音的长会话意味着相当多的流量。纯文本导出几乎是瞬间完成的。

</details>

<details>
<summary><b>有些旧消息丢了。</b></summary>

Instagram 会随着滚动把消息卸载掉，所以扫描必须沿着会话往回走，把它们重新加载进页面。让它跑完。非常长的对话会花一些时间。

</details>

<details>
<summary><b>我该用 v1 还是 v2？</b></summary>

用 v2，除非你就是想要一个小到能一口气读完的东西。v1 是 342 行、导出纯文本；v2 才是完整的工具。

</details>

---

## 🤝 参与贡献

欢迎贡献。请先阅读 [CONTRIBUTING.md](./CONTRIBUTING.md) 和 [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)。提交贡献即表示你同意以 AGPL-3.0 许可你的成果。

<div align="center">
<a href="https://github.com/Miabeyefendi/IG-DMKeep/issues/new?template=bug_report.yml">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./assets/btn-report-bug-dark.svg">
    <img src="./assets/btn-report-bug.svg" height="52" alt="报告问题">
  </picture>
</a>
<a href="https://github.com/Miabeyefendi/IG-DMKeep/stargazers">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./assets/btn-star-dark.svg">
    <img src="./assets/btn-star.svg" height="52" alt="给这个仓库点星">
  </picture>
</a>
</div>

---

## 🛡️ 安全

发现漏洞了？不要公开提 issue。请按 [SECURITY.md](./SECURITY.md) 中的私密流程处理。

---

## 📜 许可证

IG-DMKeep 依据 **GNU Affero General Public License v3.0 (AGPL-3.0)** 授权，并附带 [NOTICE](./NOTICE) 文件中的补充条款。简单说：

- 只要你把完整源代码继续以 AGPL-3.0 提供出去（包括任何托管、SaaS 或网络形式的使用，见 AGPL 第 13 条），并保留下面的作者署名，你就可以**免费**使用、研究、修改、再分发本软件，甚至用它赚钱。
- 若要把本作品用于闭源或专有产品，或作为闭源 SaaS 运行，你需要一份**单独的书面商业许可**，其中可能包含分成或版税。见 [NOTICE](./NOTICE) 第 8 节，并与我联系。

### 署名（强制）

根据 AGPL-3.0 第 7(b) 条，以下署名必须在本项目的任何副本、复刻或部署中原样、可见地保留：

> **Miabeyefendi (Mustafa Ihsan Albayrak)** - https://github.com/Miabeyefendi

### 免责声明

本软件按"原样"提供，不含任何形式的担保。你完全自担风险运行它，并对自己的使用独自负责，包括遵守它所交互的任何第三方平台的服务条款，尤其是 Instagram。Instagram 与本项目没有关联，也未为其背书；其名称和商标归其所有者。在适用法律允许的最大范围内，作者对账号封禁、数据丢失或任何其他损害不承担责任。完整条款见 [LICENSE](./LICENSE) 与 [NOTICE](./NOTICE) 文件。

---

## 📬 联系方式

- GitHub：[@Miabeyefendi](https://github.com/Miabeyefendi)
- 商业授权或分成相关事宜，请通过我的 GitHub 主页联系我。

<div align="center">
<br/>
<img src="./assets/divider.svg" width="100%" height="3" alt="">
<br/>
<sub>由 <b><a href="https://github.com/Miabeyefendi">Miabeyefendi</a></b> 制作</sub>
</div>

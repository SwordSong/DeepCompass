# DeepCompass

**A local-first desktop workspace for finding off-market properties from public county records.**

DeepCompass pulls property data (owner, mailing address, assessed value, sales, building and land details) directly from official county property appraiser and GIS sources, stores everything in a database on your own computer, and gives you a lightweight CRM to work leads and match them with buyers — without a $99+/month subscription.

> Built by an independent developer. Currently in **free beta** (Windows x64). This repository hosts the official downloads, release notes and issue tracker.

<!-- Replace with a real screenshot or GIF: docs/screenshot.png -->
<!-- ![DeepCompass screenshot](docs/screenshot.png) -->

### [⬇ Download the latest version](../../releases/latest)

---

## Why

Most lead platforms resell data that originally comes from public county records, then charge a monthly fee to cover their servers. That's a lot of pressure for newer investors who haven't closed a deal yet.

DeepCompass takes a different approach:

- **Your computer does the work.** Data is fetched from public county sources and saved locally. There's no cloud backend storing your leads, so there's no server bill to pass on to you.
- **Your data stays yours.** Property lists, buyer lists and notes live in a local database. Nothing is uploaded or shared with other users.
- **Only the "how", not the data, is distributed.** The app downloads county *rules* (which endpoints and fields to read) so new counties can be added without reinstalling. It never downloads someone else's data.

## Features

### Property data
- **Search the official website, keep the results.** Browse a county's official property search inside the app; parcels you find are recognized, highlighted and saved automatically, then filled in with full details.
- **Batch collection.** Choose search criteria (address, owner, subdivision, parcel number, or an imported APN/Folio list), preview, then run a bounded collection job with pause / resume and a failure list.
- **Official bulk files.** Where counties publish certified tax roll files (e.g. Florida NAL), DeepCompass can use them as a data source.
- **Full detail retained.** Assessment history, taxable values, sales, exemptions, buildings, land and extra features are kept alongside the summary fields.
- **Local search & filters**, tags and notes on any property.
- **Export** to CSV / XLSX (APNs keep their leading zeros) or full JSON per record.

### Deal workflow (local CRM)
- Leads & deals workspace with status tracking and follow-ups
- Buyer pool with import, and automatic property ↔ buyer preference matching
- Deal underwriting, contract contingency tracking and pitch cards
- Deed and ownership signals to help spot motivated sellers

### Other
- **Bilingual UI** — English and 简体中文
- **Optional AI analysis** — bring your own API key (cloud provider or a local OpenAI-compatible server). Off by default; keys are encrypted locally.
- **Proxy support** — system, HTTP/HTTPS, SOCKS4/5
- **Automatic county rule updates** with rollback to built-in rules

## Supported counties

| State | County | Data sources |
|---|---|---|
| Florida | Miami-Dade | ArcGIS Property Point View + CAMA details |
| Florida | Broward | BCPA JSON API + County GIS |
| Florida | Orange | OCPA ArcGIS REST + Florida DOR NAL |
| Florida | Hillsborough | HCPA parcel file + ArcGIS + CAMA |
| Florida | Duval (Jacksonville) | DCPAO tax roll + ArcGIS REST |
| Florida | Lee | LeePA NAL + Lee County GIS |

New counties are delivered through rule updates, usually without downloading a new version. **Want your county supported?** [Open an issue](../../issues/new) with the county name and its property appraiser website.

## Install

**Requirements:** Windows 10 / 11 (64-bit), about 1 GB of free disk space, and an internet connection to reach county sources.

1. Download `DeepCompass-<version>-win-x64.exe` from the [latest release](../../releases/latest).
2. *(Optional)* Verify the file against the SHA-256 checksum listed in the release notes:
   ```powershell
   Get-FileHash .\DeepCompass-<version>-win-x64.exe -Algorithm SHA256
   ```
3. Run the `.exe`. It's a portable app — no installer, no admin rights needed.

> **Windows SmartScreen warning:** the beta build is not code-signed yet, so Windows may say it "protected your PC". Click **More info → Run anyway**. Only download DeepCompass from this repository's Releases page.

The first launch takes a little longer while the local database is set up.

## Updating

Download the newer `.exe` from [Releases](../../releases) and run it in place of the old one. Your data is stored separately from the program, so it carries over automatically.

Watch this repository (**Watch → Custom → Releases**) to get notified of new versions.

## Where your data lives

| What | Location |
|---|---|
| Database, settings, downloaded rules | `%APPDATA%\DeepLuopan` |
| Logs (kept 14 days) | `%APPDATA%\DeepLuopan\logs` |

The built-in database only listens on `127.0.0.1` and is stopped when the app closes.

**Uninstall:** delete the `.exe`. To remove all data as well, delete the `%APPDATA%\DeepLuopan` folder. This permanently erases your saved properties and buyers, so export anything you want to keep first.

## Privacy: what the app connects to

DeepCompass has no account system and no analytics. It only makes these network requests:

| Connection | When |
|---|---|
| Official county property appraiser / GIS websites | When you search or run a collection job |
| `property.veyshore.com` — county rules | Rule update checks (downloads rules only, never uploads your data) |
| `property.veyshore.com` — diagnostics | Only when you click **Submit report**. You choose what's attached; property and buyer data are excluded from auto-generated logs. |
| Your AI provider | Only if you turn on AI analysis and enter your own API key |

## Responsible use

DeepCompass only reads **publicly available** records from official government sources, and is designed to be a polite client:

- Requests are sent one at a time, with a delay between each request — no burst traffic
- Collection jobs are bounded and can be paused at any time
- The app does not bundle or redistribute any county website's code, styles or assets
- There is no shared data network between users

You are responsible for how you use the data. Some states restrict using certain public records for commercial solicitation, and outreach is subject to laws such as the TCPA and Do-Not-Call rules. Check the terms of each county source and your local regulations.

## Roadmap

- [ ] More Florida counties, then other states
- [ ] Code-signed builds and auto-update
- [ ] Backup / restore management in the UI
- [ ] macOS support

## Feedback & support

This project is built by one person, and real-world input from agents, wholesalers, flippers and land investors shapes what gets built next.

- 🐛 **Bug or wrong data** → [open an issue](../../issues). In the app, **Settings → Diagnostics → Save as ZIP** creates a report you can attach.
- 💡 **Feature idea or missing county** → [start a discussion](../../discussions)

## License

DeepCompass is free to download and use during the beta. The software is proprietary — © DeepCompass. All rights reserved. Redistribution, resale or reverse engineering is not permitted.

Property data belongs to its respective public sources. DeepCompass is not affiliated with or endorsed by any county or government agency.

---

## 中文说明

DeepCompass 是一款**本地优先**的美国房产数据桌面工具：直接从县政府官方评估办公室和 GIS 公开数据源获取房产信息（业主、邮寄地址、评估值、交易记录等），全部保存在你自己的电脑上，并内置轻量 CRM（线索 / 交易看板、买家池、智能匹配），无需每月支付高额订阅费。

- **下载**：在 [Releases](../../releases/latest) 下载最新的 `.exe`，便携版，双击即可运行，无需安装
- **支持范围**：佛罗里达州 6 个县 —— Miami-Dade、Broward、Orange、Hillsborough、Duval、Lee
- **界面语言**：中英文切换
- **数据位置**：`%APPDATA%\DeepLuopan`，更新程序不影响已有数据
- **反馈**：欢迎通过 [Issues](../../issues) 反馈问题或提出想要支持的县

测试版暂未进行代码签名，首次运行如遇 Windows SmartScreen 提示，点击「更多信息 → 仍要运行」即可。

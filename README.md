# 🚀 Daily Tech Pulse

> AI-powered daily digest of GitHub's hottest trending repositories — updated every morning automatically.

[![Daily Tech Digest](https://github.com/fournarin/daily-tech-pulse-/actions/workflows/daily_digest.yml/badge.svg)](https://github.com/fournarin/daily-tech-pulse-/actions/workflows/daily_digest.yml)

---

## 🤖 What This Does

Every day at **~8:17 AM Bangkok time** (with automatic fallbacks at 9:17 and 10:17), this bot automatically:

| Step | Action |
|------|--------|
| 1 | 📡 Fetches the hottest new GitHub repos (last 7 days by stars) |
| 2 | 🧠 Analyzes them with **Gemini AI** |
| 3 | 📝 Writes a Markdown digest report |
| 4 | 🌿 Creates a new branch `report/YYYY-MM-DD` |
| 5 | 💾 Commits the report + updates this README |
| 6 | 🔀 Opens a PR and auto-merges it to `main` |
| 7 | 📋 Opens a daily Issue with highlights |

---

## ⚙️ Tech Stack

| Tool | Purpose |
|------|---------|
| GitHub Actions | Automation & scheduling |
| Gemini API (gemini-2.0-flash) | AI-powered analysis |
| PyGithub | GitHub API client |
| Python 3.11 | Core language |

---

<!-- LATEST_REPORT_START -->
## 📊 Latest Report: [2026-06-18](reports/2026-06-18.md)

Top repo: **[DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail)** (⭐ 33,277)

[Read full report →](reports/2026-06-18.md)
<!-- LATEST_REPORT_END -->

---

## 📁 Reports Archive

All daily reports are stored in [`reports/`](reports/).

---

## 🛠️ Setup

See **[SETUP.md](SETUP.md)** for step-by-step instructions.

---

*Built with ❤️ and 🤖 · Powered by [Gemini](https://ai.google.dev)*

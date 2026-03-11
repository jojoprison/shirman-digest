# 📡 shirman-digest

> 🤖 Claude Code skill for automated AI & Tech trends digest from [shir-man.com](https://shir-man.com)

[![Claude Code](https://img.shields.io/badge/Claude_Code-skill-blueviolet?style=flat-square&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0IiBmaWxsPSJ3aGl0ZSI+PHBhdGggZD0iTTEyIDJDNi40OCAyIDIgNi40OCAyIDEyczQuNDggMTAgMTAgMTAgMTAtNC40OCAxMC0xMFMxNy41MiAyIDEyIDJ6Ii8+PC9zdmc+)](https://claude.ai)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)
[![shir-man.com](https://img.shields.io/badge/source-shir--man.com-orange?style=flat-square)](https://shir-man.com)
[![Telegram Channel](https://img.shields.io/badge/Telegram-@denissexy-blue?style=flat-square&logo=telegram)](https://t.me/denissexy)
[![Telegram News](https://img.shields.io/badge/Telegram-@denis__news__feed-blue?style=flat-square&logo=telegram)](https://t.me/denis_news_feed)

**[English](#-what-it-does)** | **[Русский](#-что-делает)**

---

## 🎯 What It Does

Automatically collects a daily AI & Tech trends digest:

- 🔍 **GitHub Trending** — fastest-growing repositories
- 🧡 **Hacker News** — top discussions
- 🦞 **Lobsters** — expert-curated content
- 🤖 **AI Agents** — new tools and frameworks
- 📰 **Deep Reads** — long-form analysis articles
- 🧪 **Try Now** — things you can try right now

Generates a beautiful **HTML report** with 7 tabs, dark/light theme toggle, colored source badges, and clickable links to every original article.

## 🏗 Architecture

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│  PinchTab    │────▶│  WebFetch    │────▶│  HTML Report │
│  (SPA nav)   │     │  (articles)  │     │  (7 tabs)    │
└─────────────┘     └──────────────┘     └─────────────┘
     │                     │                     │
  snapshot            parallel              dark/light
  + clicks           fetch ×N              theme toggle
```

## 📦 Installation

### Global (recommended)

```bash
mkdir -p ~/.claude/skills/shirman-digest
curl -sL https://raw.githubusercontent.com/jojoprison/shirman-digest/main/SKILL.md \
  -o ~/.claude/skills/shirman-digest/SKILL.md
```

### Per-project

```bash
mkdir -p .claude/skills/shirman-digest
curl -sL https://raw.githubusercontent.com/jojoprison/shirman-digest/main/SKILL.md \
  -o .claude/skills/shirman-digest/SKILL.md
```

## 🚀 Usage

In Claude Code:

```
/shirman-digest
```

The generated report includes:
- 🌓 Dark/light theme toggle (persisted in localStorage)
- 🔗 Clickable links to all original articles
- 📊 7 category tabs
- 🏷 Color-coded source badges (GitHub=green, HN=orange, Lobsters=red, AI=purple)
- 💡 "Key takeaway" blocks for important articles

## ⚡️ Requirements

- [Claude Code](https://claude.ai/claude-code) with MCP support
- **PinchTab MCP** — for SPA navigation
- **WebFetch** — for reading articles (built into Claude Code)

## 🏷 Alternative Names

| Command | Style |
|---------|-------|
| `/shirman-digest` | 🎯 Current — tied to the source |
| `/tech-digest` | 📰 Neutral, clear |
| `/trend-radar` | 📡 Trend radar metaphor |
| `/daily-signal` | 📶 Daily signal from noise |
| `/hacker-brief` | 🗞 HN-style briefing |
| `/ai-pulse` | 💓 AI industry pulse |

## 🔗 Links

- 🌐 [shir-man.com](https://shir-man.com) — data source
- 📱 [@denissexy](https://t.me/denissexy) — Telegram channel (author)
- 📰 [@denis_news_feed](https://t.me/denis_news_feed) — Telegram news feed
- 📚 [Claude Code Skills docs](https://docs.anthropic.com/en/docs/claude-code)
- 🐛 [Issues](https://github.com/jojoprison/shirman-digest/issues)

---

# 🇷🇺 Русский

## 🎯 Что делает

Автоматически собирает дайджест AI & Tech трендов за день:

- 🔍 **GitHub Trending** — самые быстрорастущие репозитории
- 🧡 **Hacker News** — лучшие обсуждения
- 🦞 **Lobsters** — экспертный контент
- 🤖 **AI Agents** — новые инструменты и фреймворки
- 📰 **Deep Reads** — длинные статьи с анализом
- 🧪 **Попробовать** — что можно попробовать прямо сейчас

Генерирует HTML-отчёт с 7 вкладками, переключателем тёмной/светлой темы, цветными бейджами источников и кликабельными ссылками на все оригинальные статьи.

## 📦 Установка

### Глобально (рекомендуется)

```bash
mkdir -p ~/.claude/skills/shirman-digest
curl -sL https://raw.githubusercontent.com/jojoprison/shirman-digest/main/SKILL.md \
  -o ~/.claude/skills/shirman-digest/SKILL.md
```

### В проект

```bash
mkdir -p .claude/skills/shirman-digest
curl -sL https://raw.githubusercontent.com/jojoprison/shirman-digest/main/SKILL.md \
  -o .claude/skills/shirman-digest/SKILL.md
```

## 🚀 Использование

В Claude Code:

```
/shirman-digest
```

Генерирует HTML-отчёт с:
- 🌓 Переключатель тёмной/светлой темы (localStorage)
- 🔗 Все ссылки на оригинальные статьи
- 📊 7 вкладок по категориям
- 🏷 Цветные бейджи по источникам
- 💡 Блоки «Ключевой вывод» для каждой статьи

## 🔗 Ссылки

- 🌐 [shir-man.com](https://shir-man.com) — источник данных
- 📱 [@denissexy](https://t.me/denissexy) — Telegram-канал автора
- 📰 [@denis_news_feed](https://t.me/denis_news_feed) — новостная лента
- 📚 [Документация Claude Code Skills](https://docs.anthropic.com/en/docs/claude-code)
- 🐛 [Issues](https://github.com/jojoprison/shirman-digest/issues)

---

Made with 🤖 by [Claude Code](https://claude.ai) + [jojoprison](https://github.com/jojoprison)

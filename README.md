# shirman-digest

> Claude Code plugin for automated AI & Tech trends digest from [shir-man.com](https://shir-man.com/homepage/)

[![Claude Code](https://img.shields.io/badge/Claude_Code-plugin-blueviolet?style=flat-square&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0IiBmaWxsPSJ3aGl0ZSI+PHBhdGggZD0iTTEyIDJDNi40OCAyIDIgNi40OCAyIDEyczQuNDggMTAgMTAgMTAgMTAtNC40OCAxMC0xMFMxNy41MiAyIDEyIDJ6Ii8+PC9zdmc+)](https://claude.ai)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)
[![shir-man.com](https://img.shields.io/badge/source-shir--man.com-orange?style=flat-square)](https://shir-man.com/homepage/)
[![Telegram Channel](https://img.shields.io/badge/Telegram-@denissexy-blue?style=flat-square&logo=telegram)](https://t.me/denissexy)
[![Telegram News](https://img.shields.io/badge/Telegram-@denis__news__feed-blue?style=flat-square&logo=telegram)](https://t.me/denis_news_feed)

**[English](#what-it-does)** | **[Русский](#что-делает)**

---

## What It Does

Automatically collects a daily AI & Tech trends digest from [shir-man.com](https://shir-man.com/homepage/) and generates a beautiful HTML report.

**4 tabs, zero duplicates:**

| Tab | Content |
|-----|---------|
| **GitHub Trending** | Fastest-growing repositories |
| **Hacker News** | Top discussions and articles |
| **Lobsters** | Expert-curated technical content |
| **AI Agents** | New tools and frameworks |

Each article appears in **exactly one tab**. Priority: AI Agents > GitHub Trending > Hacker News > Lobsters.

### Three-Question Filter

Every item passes a quality gate before inclusion:

| Question | Passes if... |
|----------|-------------|
| **Novelty** — is this actually new? | New project, fresh release, original approach |
| **Credibility** — backed by production usage? | GitHub stars, production users, benchmarks |
| **Applicability** — solves a real problem? | Applicable to your workflows or stack |

Items scoring 0/3 are excluded. This filters ~80% of noise.

## Architecture

```
┌─────────────┐     ┌──────────────┐     ┌──────────────┐     ┌─────────────┐
│  PinchTab    │────▶│  URL Resolve  │────▶│  WebFetch    │────▶│  HTML Report │
│  (SPA nav)   │     │  (parallel)   │     │  (articles)  │     │  (4 tabs)    │
└─────────────┘     └──────────────┘     └──────────────┘     └─────────────┘
     │                     │                     │                     │
  snapshot            HN Algolia            parallel              dark/light
  + clicks           + WebSearch           fetch x8              theme toggle
```

## Installation

### Option 1: Plugin Marketplace (recommended)

```bash
# Add marketplace
claude plugin marketplace add jojoprison/shirman-digest

# Install plugin
claude plugin install shirman-digest@shirman-digest
```

### Option 2: Manual (skill only)

```bash
mkdir -p ~/.claude/skills/shirman-digest
curl -sL https://raw.githubusercontent.com/jojoprison/shirman-digest/main/plugins/shirman-digest/skills/shirman-digest/SKILL.md \
  -o ~/.claude/skills/shirman-digest/SKILL.md
```

## Usage

In Claude Code:

```
/shirman-digest
```

The generated report includes:
- Dark/light theme toggle (persisted in localStorage)
- Clickable links to all original articles
- 4 deduplicated category tabs
- Color-coded source badges (GitHub=green, HN=orange, Lobsters=red, AI=purple)
- "Key takeaway" blocks for important articles

## Requirements

- [Claude Code](https://claude.ai/claude-code) with MCP support
- **PinchTab MCP** — for SPA navigation

## Plugin Structure

```
shirman-digest/
├── .claude-plugin/
│   └── marketplace.json          # Marketplace manifest
├── plugins/
│   └── shirman-digest/
│       ├── .claude-plugin/
│       │   └── plugin.json       # Plugin manifest
│       └── skills/
│           └── shirman-digest/
│               └── SKILL.md      # Skill instructions
├── SKILL.md                      # Standalone (for manual install)
├── CHANGELOG.md                  # English changelog
├── CHANGELOG.ru.md               # Russian changelog
├── README.md
└── LICENSE
```

## Links

- [shir-man.com](https://shir-man.com/homepage/) — data source
- [@denissexy](https://t.me/denissexy) — Telegram channel (author)
- [@denis_news_feed](https://t.me/denis_news_feed) — Telegram news feed

---

# Русский

## Что делает

Автоматически собирает дайджест AI & Tech трендов за день с [shir-man.com](https://shir-man.com/homepage/) и генерирует HTML-отчёт.

**4 вкладки, ноль дублей:**

| Вкладка | Контент |
|---------|---------|
| **GitHub Trending** | Самые быстрорастущие репозитории |
| **Hacker News** | Лучшие обсуждения и статьи |
| **Lobsters** | Экспертный технический контент |
| **AI Agents** | Новые инструменты и фреймворки |

Каждая статья появляется **ровно в одной вкладке**. Приоритет: AI Agents > GitHub Trending > Hacker News > Lobsters.

### Трёхвопросный фильтр

Каждый элемент проходит проверку качества:

| Вопрос | Проходит если... |
|--------|-----------------|
| **Новизна** — это реально новое? | Новый проект, свежий релиз, оригинальный подход |
| **Достоверность** — подкреплено практикой? | GitHub stars, production users, бенчмарки |
| **Применимость** — решает реальную проблему? | Применимо к вашим workflow или стеку |

Элементы с 0/3 исключаются. Фильтр отсеивает ~80% шума.

## Установка

### Вариант 1: Plugin Marketplace (рекомендуется)

```bash
# Добавить маркетплейс
claude plugin marketplace add jojoprison/shirman-digest

# Установить плагин
claude plugin install shirman-digest@shirman-digest
```

### Вариант 2: Вручную (только скилл)

```bash
mkdir -p ~/.claude/skills/shirman-digest
curl -sL https://raw.githubusercontent.com/jojoprison/shirman-digest/main/plugins/shirman-digest/skills/shirman-digest/SKILL.md \
  -o ~/.claude/skills/shirman-digest/SKILL.md
```

## Использование

В Claude Code:

```
/shirman-digest
```

Генерирует HTML-отчёт с:
- Переключатель тёмной/светлой темы (localStorage)
- Все ссылки на оригинальные статьи
- 4 дедуплицированные вкладки
- Цветные бейджи по источникам
- Блоки «Ключевой вывод» для важных статей

## Требования

- [Claude Code](https://claude.ai/claude-code) с поддержкой MCP
- **PinchTab MCP** — для навигации SPA

## Ссылки

- [shir-man.com](https://shir-man.com/homepage/) — источник данных
- [@denissexy](https://t.me/denissexy) — Telegram-канал автора
- [@denis_news_feed](https://t.me/denis_news_feed) — новостная лента

---

Made with Claude Code by [jojoprison](https://github.com/jojoprison)

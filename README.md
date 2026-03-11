# 📡 shirman-digest

> 🤖 Claude Code skill для автоматического дайджеста AI & Tech трендов с [shir-man.com](https://shir-man.com)

[![Claude Code](https://img.shields.io/badge/Claude_Code-skill-blueviolet?style=flat-square&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0IiBmaWxsPSJ3aGl0ZSI+PHBhdGggZD0iTTEyIDJDNi40OCAyIDIgNi40OCAyIDEyczQuNDggMTAgMTAgMTAgMTAtNC40OCAxMC0xMFMxNy41MiAyIDEyIDJ6Ii8+PC9zdmc+)](https://claude.ai)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)
[![shir-man.com](https://img.shields.io/badge/source-shir--man.com-orange?style=flat-square)](https://shir-man.com)

---

## 🎯 Что делает

Автоматически собирает дайджест AI & Tech трендов за день:

- 🔍 **GitHub Trending** — самые быстрорастущие репозитории
- 🧡 **Hacker News** — лучшие обсуждения
- 🦞 **Lobsters** — экспертный контент
- 🤖 **AI Agents** — новые инструменты и фреймворки
- 📰 **Deep Reads** — длинные статьи с анализом
- 🧪 **Try Now** — что можно попробовать прямо сейчас

## 🏗 Архитектура

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│  PinchTab    │────▶│  WebFetch    │────▶│  HTML Report │
│  (SPA nav)   │     │  (articles)  │     │  (7 tabs)    │
└─────────────┘     └──────────────┘     └─────────────┘
     │                     │                     │
  snapshot            parallel              dark/light
  + clicks           fetch ×N              theme toggle
```

## 📦 Установка

### Глобально (рекомендуется)

```bash
mkdir -p ~/.claude/skills/shirman-digest
cp SKILL.md ~/.claude/skills/shirman-digest/SKILL.md
```

### В проект

```bash
mkdir -p .claude/skills/shirman-digest
cp SKILL.md .claude/skills/shirman-digest/SKILL.md
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
- 💡 Блоки "Ключевой вывод" для каждой статьи

## 🏷 Альтернативные названия

| Команда | Стиль |
|---------|-------|
| `/shirman-digest` | 🎯 Текущее — привязка к источнику |
| `/tech-digest` | 📰 Нейтральное, понятное |
| `/trend-radar` | 📡 Метафора радара трендов |
| `/daily-signal` | 📶 Ежедневный сигнал из шума |
| `/hacker-brief` | 🗞 HN-стиль брифинг |
| `/ai-pulse` | 💓 Пульс AI индустрии |

## ⚡️ Требования

- [Claude Code](https://claude.ai/claude-code) с MCP
- **PinchTab MCP** — для навигации SPA
- **WebFetch** — для чтения статей (встроен в Claude Code)

## 🔗 Ссылки

- 🌐 [shir-man.com](https://shir-man.com) — источник данных
- 📚 [Claude Code Skills docs](https://docs.anthropic.com/en/docs/claude-code)
- 🐛 [Issues](https://github.com/jojoprison/shirman-digest/issues)

---

Made with 🤖 by [Claude Code](https://claude.ai) + [jojoprison](https://github.com/jojoprison)

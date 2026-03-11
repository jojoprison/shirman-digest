---
name: shirman-digest
description: "Дайджест AI & Tech трендов с shir-man.com — PinchTab навигация + WebFetch чтение + HTML отчёт с вкладками"
---

# /shirman-digest — AI & Tech Trends Daily Digest

Источник: [shir-man.com](https://shir-man.com/homepage/) — SPA дашборд с AI/Tech трендами.

## Алгоритм

### Шаг 1: Навигация PinchTab

1. `pinchtab_navigate(url: "https://shir-man.com/homepage/")`
2. `pinchtab_wait(seconds: 3)` — дождаться загрузки SPA
3. `pinchtab_snapshot(filter: "interactive", format: "compact")` — получить элементы
4. Переключить селекторы:
   - Midjourney → **GitHub** (клик по селектору первой колонки)
   - Hype Replicate → **Lobsters** (клик по селектору третьей колонки)
5. Пройти вкладки внизу (кружочки): Top signals, HN Best Show, GitHub Fastest rising, Popular
   - **Пропустить:** Virality map, Topic cloud (нет полезных ссылок)
6. На каждой вкладке: `pinchtab_snapshot` → собрать все ссылки из StaticText нод

### Шаг 2: Чтение статей через WebFetch

1. Собрать уникальные URL из всех snapshot'ов
2. Запустить WebFetch **параллельно** (до 8 одновременно) для каждого URL
3. Извлечь: заголовок, основной текст, ключевые тезисы
4. Если WebFetch вернул 404/ошибку — пропустить, не ретраить

### Шаг 3: Генерация HTML отчёта

Создать файл `claudedocs/shir-man-daily-report-YYYY-MM-DD.html` с:

**Структура:**
- 7 вкладок: Обзор, GitHub Trending, Hacker News, Lobsters, AI Agents, Deep Reads, Попробовать
- Каждая вкладка — карточки с: заголовок, описание, ссылка на оригинал, бейдж источника
- Блок "Ключевой вывод" (takeaway) для важных статей

**Стиль:**
- CSS variables для тёмной (по умолчанию) и светлой темы
- Переключатель темы с сохранением в localStorage
- Градиентные заголовки, цветные бейджи по источнику:
  - GitHub → зелёный, HN → оранжевый, Lobsters → красный, AI → фиолетовый
- Responsive grid, max-width: 1200px
- Шрифт: system-ui

**Язык:** Весь текст отчёта на РУССКОМ. Технические термины — оригинал.

### Шаг 4: Открыть отчёт

```bash
open claudedocs/shir-man-daily-report-YYYY-MM-DD.html
```

### Шаг 5: Убить PinchTab

```bash
pkill -f pinchtab
```

**ОБЯЗАТЕЛЬНО** убивать после работы — процессы копятся между сессиями.

## Gotchas

- **PinchTab eval не работает** (404 баг) — данные только через snapshot StaticText
- **PinchTab type не работает** на macOS — humanType баг, React state не обновляется
- **WebFetch эффективнее** PinchTab для чтения статей в 5-10x (параллельно, без ожидания)
- **shir-man.com — SPA** без публичного API, все данные на главной странице
- **Snapshot refs** (`e0`, `e1`...) меняются после навигации — пере-snapshot после каждого клика

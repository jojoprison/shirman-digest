---
name: shirman-digest
description: "Собирает дайджест AI & Tech трендов за день с shir-man.com и генерирует красивый HTML-отчёт с вкладками. Используй когда пользователь просит: дайджест, тренды, новости AI, что нового в tech, shirman, shir-man, ежедневный обзор технологий, tech digest, trend report — даже если не упоминает shir-man напрямую."
---

# /shirman-digest — Ежедневный дайджест AI & Tech трендов

Скилл автоматически собирает самое важное за день из мира AI и технологий с [shir-man.com/homepage/](https://shir-man.com/homepage/) — SPA-дашборда, агрегирующего GitHub Trending, Hacker News, Lobsters и AI-новости. Результат — готовый HTML-отчёт с 7 вкладками, темой и ссылками на оригиналы.

## Зачем

shir-man.com — это единственная точка входа для обзора трендов, но сайт SPA без API, данные не парсятся обычным скрапером. Скилл решает эту проблему: навигирует SPA через headless-браузер, параллельно читает статьи, и упаковывает всё в удобный отчёт. Без скилла это занимает 30-40 минут ручной работы.

## Алгоритм

### Шаг 1: Навигация по SPA (PinchTab)

shir-man.com — SPA, поэтому нужен headless-браузер для навигации. PinchTab snapshot даёт accessibility tree с минимумом токенов.

1. `pinchtab_navigate(url: "https://shir-man.com/homepage/")`
2. `pinchtab_wait(seconds: 3)` — SPA грузит данные асинхронно
3. `pinchtab_snapshot(filter: "interactive", format: "compact")` — получить элементы (~19 нод vs 269 в полном DOM)
4. Переключить селекторы колонок:
   - Первая колонка: Midjourney → **GitHub** (самые быстрорастущие репозитории)
   - Третья колонка: Hype Replicate → **Lobsters** (экспертный контент)
5. Пройти вкладки внизу (кружочки-переключатели):
   - **Собрать:** Top signals, HN Best Show, GitHub Fastest rising, Popular
   - **Пропустить:** Virality map, Topic cloud (визуализации без парсируемых ссылок)
6. На каждой вкладке: snapshot → извлечь ссылки из StaticText нод

> **Почему StaticText, а не eval?** PinchTab eval возвращает 404 (известный баг [#225](https://github.com/pinchtab/pinchtab/issues/225)). Данные извлекаются из snapshot accessibility tree — менее точно, но работает стабильно.

### Шаг 1.5: Извлечение URL из ссылок (ОБЯЗАТЕЛЬНО)

PinchTab compact snapshot показывает текст ссылок, но НЕ href. Для каждой карточки в отчёте **ОБЯЗАТЕЛЬНА** кликабельная ссылка на оригинал. Без ссылки карточка бесполезна.

**Способы получения URL:**

1. **GitHub репо** — URL строится из текста ссылки: `https://github.com/{link_text}` (текст уже содержит `owner/repo`)
2. **HN статьи** — домен виден в StaticText (напр. `GIST.GITHUB.COM`, `SAMHENRI.GOLD`). Для получения точного URL:
   - WebSearch: `"{заголовок статьи}" site:{домен}` — быстрый поиск точного URL
   - Или: `WebFetch("https://hn.algolia.com/api/v1/search?query={title}&tags=story")` — HN API возвращает `url` поле
3. **Lobsters статьи** — аналогично HN: домен виден, искать через WebSearch по заголовку + домену
4. **Show HN / Top Signals** — ссылки в карусели: кликнуть на link-ноду (`pinchtab_click`), snapshot → извлечь URL из адресной строки, `pinchtab_back` для возврата

**Правило:** Если URL не удалось найти ни одним способом — пометить карточку `🔗 ссылка не найдена` и указать домен-источник как текст. Но стремиться к 100% покрытию ссылками.

**Параллельность:** Запускать WebSearch/WebFetch для разрешения URL параллельно (до 8 одновременно), чтобы не тратить время.

### Шаг 2: Чтение статей (WebFetch)

WebFetch в 5-10x эффективнее браузера для чтения контента: параллельный fetch без ожидания рендера.

1. Собрать уникальные URL из Шага 1.5 + snapshot'ов
2. Запустить WebFetch **параллельно** (до 8 одновременно)
3. Извлечь из каждой статьи: заголовок, ключевые тезисы, практическую ценность
4. При 404 или ошибке — пропустить без ретрая (URL может быть устаревшим)

### Шаг 3: Генерация HTML-отчёта

Создать `claudedocs/shir-man-daily-report-YYYY-MM-DD.html`.

**7 вкладок:**

| Вкладка | Контент |
|---------|---------|
| Обзор | Топ-5 находок дня, краткие выводы |
| GitHub Trending | Быстрорастущие репозитории с описанием |
| Hacker News | Лучшие обсуждения и статьи |
| Lobsters | Экспертный технический контент |
| AI Agents | Новые инструменты и фреймворки |
| Deep Reads | Длинные статьи с глубоким анализом |
| Попробовать | Инструменты, которые можно попробовать прямо сейчас |

**Каждая карточка ОБЯЗАТЕЛЬНО содержит:**
- Заголовок + **кликабельная ссылка на оригинал** (ОБЯЗАТЕЛЬНО! Без ссылки карточка бесполезна — см. Шаг 1.5)
- Краткое описание (2-3 предложения)
- Цветной бейдж источника
- Блок «Ключевой вывод» для важных статей (выделенный фон, 1-2 предложения)

**⚠️ НЕ допускается:** карточка без `<a href="...">` ссылки на оригинальный ресурс. Если URL не разрешён — использовать домен + заголовок в WebSearch.

**Стиль отчёта:**

```
CSS variables → тёмная тема по умолчанию, светлая по toggle
Переключатель темы → кнопка в шапке, состояние в localStorage
Бейджи источников → GitHub: зелёный, HN: оранжевый, Lobsters: красный, AI: фиолетовый
Layout → responsive CSS grid, max-width: 1200px, system-ui шрифт
Градиенты → заголовок страницы и заголовки вкладок
```

**Язык:** Весь текст на русском. Технические термины (GitHub, Hacker News, API и т.д.) — в оригинале.

**HTML skeleton** — структура отчёта:

```html
<!DOCTYPE html>
<html lang="ru" data-theme="dark">
<head>
  <meta charset="UTF-8">
  <title>AI & Tech Дайджест — YYYY-MM-DD</title>
  <style>
    :root { --bg: #1a1a2e; --card: #16213e; --text: #e0e0e0; --accent: #7c3aed; }
    [data-theme="light"] { --bg: #f5f5f5; --card: #fff; --text: #1a1a2e; --accent: #6d28d9; }
    body { font-family: system-ui; background: var(--bg); color: var(--text); max-width: 1200px; margin: 0 auto; }
    .badge { padding: 2px 8px; border-radius: 12px; font-size: 0.75rem; }
    .badge-github { background: #22c55e20; color: #22c55e; }
    .badge-hn { background: #f9731620; color: #f97316; }
    .badge-lobsters { background: #ef444420; color: #ef4444; }
    .badge-ai { background: #7c3aed20; color: #7c3aed; }
    .takeaway { background: var(--accent)15; border-left: 3px solid var(--accent); padding: 8px 12px; margin-top: 8px; }
    .tabs button { background: none; border: none; color: var(--text); padding: 8px 16px; cursor: pointer; }
    .tabs button.active { border-bottom: 2px solid var(--accent); }
    .card { background: var(--card); border-radius: 8px; padding: 16px; margin: 8px 0; }
  </style>
</head>
<body>
  <header><!-- Заголовок + theme toggle --></header>
  <nav class="tabs"><!-- 7 вкладок --></nav>
  <main><!-- CSS grid карточки --></main>
  <script>/* Theme toggle: localStorage.getItem/setItem('theme') */</script>
</body>
</html>
```

### Шаг 4: Открыть отчёт

```bash
open claudedocs/shir-man-daily-report-YYYY-MM-DD.html
```

### Шаг 5: Очистка

```bash
pkill -f pinchtab
```

PinchTab daemon и MCP-процессы остаются жить между сессиями — их нужно убивать после каждого запуска, иначе они накапливаются.

## Известные ограничения

| Проблема | Причина | Workaround |
|----------|---------|------------|
| `pinchtab_eval` → 404 | Баг PinchTab [#225](https://github.com/pinchtab/pinchtab/issues/225) | Парсить данные из snapshot StaticText |
| `pinchtab_type` не работает | macOS баг [#226](https://github.com/pinchtab/pinchtab/issues/226) | Не нужен для этого скилла (только клики) |
| WebFetch 404 на некоторых URL | Устаревшие ссылки или paywall | Пропускать, не ретраить |
| Snapshot refs меняются | Ожидаемое поведение после навигации | Пере-snapshot после каждого клика |
| shir-man.com без API | SPA рендерит всё на клиенте | Только headless-браузер (PinchTab) |

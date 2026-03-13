# Changelog

## 1.1.0

- Added mandatory source URLs for every card in the report — cards without `<a href>` links are no longer allowed
- Added Step 1.5: URL resolution via HN Algolia API (`hn.algolia.com/api/v1/search`), WebSearch by title + domain, and URL construction from link text
- Added parallel URL resolution (up to 8 concurrent WebSearch/WebFetch calls)
- Added fallback marker `🔗 ссылка не найдена` for unresolved URLs with domain hint
- Improved card requirements: each card now explicitly requires a clickable link to the original resource

## 1.0.0

- Added SPA navigation via PinchTab headless browser (accessibility tree snapshots)
- Added 3-column data collection: Hacker News, GitHub Trending, Lobsters
- Added carousel tab scraping: Top signals, HN Best Show, GitHub Fastest rising, Popular
- Added parallel article reading via WebFetch (up to 8 concurrent)
- Added HTML report generation with 7 tabs: Overview, GitHub Trending, Hacker News, Lobsters, AI Agents, Deep Reads, Try It
- Added dark/light theme toggle with localStorage persistence
- Added colored source badges: GitHub (green), HN (orange), Lobsters (red), AI (purple)
- Added "Key Takeaway" blocks for important articles
- Added responsive CSS grid layout (max-width 1200px)
- Added PinchTab daemon cleanup step after each run
- Added plugin marketplace structure for `claude plugin install`

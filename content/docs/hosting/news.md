---
title: News in Ubisoft Connect
weight: 30
---

# News in Ubisoft Connect

Ubisoft Connect's start page shows your server's news. By default that is a welcome (the server's `name` and `motd`
from `config.toml`) and how many players are in the game.

Add your own in `data/news.json`, next to `powder.db`. The server reads it again when it changes; no restart needed.

```json
{
  "server_items": true,
  "items": [
    {
      "id": "winter-race",
      "title": "Winter race on Saturday",
      "text": "Meet at the Mont Blanc summit, 8 pm CET.\n\nBring your fastest skis.",
      "image": "winter.jpg",
      "link": "https://example.org/winter-race",
      "link_label": "Details",
      "date": "2026-11-09",
      "placements": ["Homepage carousel", "Latest news"],
      "priority": 1
    }
  ]
}
```

| Field | What |
| --- | --- |
| `id` | Required. Letters, digits, `-` and `_`. |
| `title` | Required. |
| `text` | Plain text; blank lines make paragraphs. |
| `summary` | The line on the tile; defaults to the text's first paragraph. |
| `image` | A file in `data/news/` (png, jpg, webp or gif). Put it there before you save `news.json`. |
| `link`, `link_label` | An `http(s)://` address, opened in the player's browser, and its text (default "Open"). |
| `date` | `YYYY-MM-DD` or a full timestamp; defaults to the file's time. |
| `placements` | Where on Connect's start page: `Homepage carousel`, `Latest news`, `Top news banner`, `Featured 1`, `Spotlight`, ... (default: the carousel and Latest news). |
| `priority` | Lower comes first (default 10; the server's own items are 100 and 101). |

`"server_items": false` turns the server's own items off. Up to 50 items.

Everything reaches Connect as plain text: HTML and Markdown show as typed. Images from other sites are not shown, so
no other site learns your players' addresses. An item with a link or image that isn't allowed is dropped; the
server's log says why.

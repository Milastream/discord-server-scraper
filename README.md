[Discord Server Scraper](https://apify.com/cryptosignals/discord-server-scraper?fpr=data)

Find and analyze public Discord communities at scale — no bot tokens, no OAuth, no authentication required. This actor extracts structured data from Discord's public server discovery pages so you can research communities, analyze competitors, or build niche directories without writing a single line of scraping code.

## Why this is hard to do yourself

Discord's discovery surface looks simple in a browser, but pulling it programmatically is painful:

- The official Discord API requires bot tokens and explicit server membership — useless for discovery.
- The public discovery page is heavily client-rendered and rate-limited.
- Pagination, category filters, and search behave differently than the visible UI suggests.
- Building this in-house means maintaining yet another scraper that breaks every time Discord ships a redesign.

This actor handles all of that for you. You give it a keyword, a category, or a list of invite codes — you get clean JSON back.

## Features

- **No authentication required** — only public data Discord exposes to anonymous visitors.
- **Search by keyword** — find servers about gaming, Python, crypto, anime, etc.
- **Filter by category** — Gaming, Education, Music, Science & Tech, and more.
- **Direct invite-code lookup** — paste a list of invites and get them resolved in bulk.
- **Member counts and verification status** — for community-size benchmarking.

## Input

```
{
  "keywords": "python",
  "category": "science-and-tech",
  "maxServers": 50,
  "inviteCodes": [],
  "proxyConfiguration": { "useApifyProxy": true }
}
```

| Field | Type | Description |
| --- | --- | --- |
| `keywords` | string | Search term (e.g. `gaming`, `python`, `crypto`). Leave empty to browse all. |
| `category` | string | Optional category filter. One of `gaming`, `entertainment`, `education`, `science-and-tech`, `music`, `content-creator`, `anime-and-manga`, `movies-and-tv`. |
| `maxServers` | integer | Max servers to return (1–500). |
| `inviteCodes` | array | Optional list of invite codes/URLs (e.g. `python`, `https://discord.gg/gaming`). When set, discovery is skipped. |
| `proxyConfiguration` | object | Proxy settings — recommended for larger runs. |

## Output

Each item in the dataset:

```
{
  "server_name": "Python",
  "description": "The official Python community on Discord.",
  "member_count": 412503,
  "online_count": 18342,
  "category": "Science & Tech",
  "invite_url": "https://discord.gg/python",
  "is_verified": true,
  "boost_level": 3
}
```

## Use cases

- **Community research** — map the landscape of servers in your niche.
- **Competitive analysis** — track member growth across rival communities.
- **Lead lists** — find communities to partner with or sponsor.
- **Directory building** — power a "best Discord servers for X" site.
- **Academic research** — study online community structure at scale.

## Get started

1. Click **Run** and try the default input.
2. Adjust `keywords`, `category`, or `maxServers` for your use case.
3. Export results to JSON, CSV, or Excel — or pipe them into your own pipeline via the Apify API.

Pay-per-result pricing — you only pay for servers actually returned.
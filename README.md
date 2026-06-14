[Discord Server Scraper](https://apify.com/magicfingers/discord-server-scraper?fpr=data)

Scrapes publicly accessible Discord server information from multiple sources. No login or Discord account required.

## What it does

This actor collects metadata from publicly listed Discord servers, including:

- **Server name** and **description**
- **Member count** and **online count**
- **Categories** and **tags**
- **Server icon**, **banner**, and **splash images**
- **Boost level**, **verification level**
- **Verified** and **partnered** status
- **Invite code** and **vanity URL**

## Data sources

| Source | Description |
| --- | --- |
| **Discord Discovery** | Official server discovery at discord.com/servers |
| **Discord Invites** | Public invite pages (discord.gg/xxx) |
| **Disboard.org** | Popular third-party server directory |
| **Discord.me** | Third-party server listing site |

## Input configuration

### Mode

Choose which source(s) to scrape:

- `discovery` — Discord's official server discovery (default)
- `invite` — Scrape specific invite links you provide
- `disboard` — Disboard.org server listings
- `discordme` — Discord.me server listings
- `all` — Scrape all sources

### Search Keywords

Comma-separated keywords to search for servers. Used in discovery, disboard, and discord.me modes.

Example: `gaming, programming, crypto`

### Categories

Filter Discord discovery by category. Options include Gaming, Music, Entertainment, Science & Tech, Education, Programming, and more.

### Invite Codes

List of Discord invite codes or URLs to scrape. Accepts:

- Plain codes: `python`
- Short URLs: `discord.gg/python`
- Full URLs: `https://discord.com/invite/python`

### Max Results

Maximum number of servers to collect per run. Default: 100. Set to 0 for unlimited.

### Max Pages

Maximum listing pages to scrape from Disboard and Discord.me. Default: 10.

### Proxy Configuration

Uses Apify Proxy by default. Recommended for avoiding rate limits.

## Example input

```
{
    "mode": "all",
    "searchKeywords": "programming, python",
    "categories": ["Programming", "Science & Tech"],
    "inviteCodes": ["python", "discord.gg/reactjs", "https://discord.gg/typescript"],
    "maxResults": 500,
    "maxPages": 10,
    "proxyConfiguration": {
        "useApifyProxy": true
    }
}
```

## Output format

Each result contains:

```
{
    "name": "Python",
    "description": "The official Python community server.",
    "id": "267624335836053506",
    "memberCount": 350000,
    "onlineCount": 45000,
    "category": "Programming",
    "tags": ["python", "coding", "programming"],
    "iconUrl": "https://cdn.discordapp.com/icons/267624335836053506/abc123.png?size=256",
    "bannerUrl": null,
    "splashUrl": null,
    "inviteCode": "python",
    "inviteUrl": "https://discord.gg/python",
    "boostLevel": 3,
    "verificationLevel": 3,
    "isVerified": true,
    "isPartnered": true,
    "vanityUrl": "https://discord.gg/python",
    "source": "discord_discovery",
    "scrapedAt": "2026-03-19T12:00:00.000Z"
}
```

## Pricing

This actor uses **Pay-Per-Event** pricing at **$1.00 per 1,000 results** ($0.001 per result).

## Legal and ethical notes

- This actor **only** scrapes publicly accessible server metadata
- It does **not** access private channels, messages, or user data
- It does **not** require Discord login or authentication
- All data collected is already publicly visible on the web
- Users are responsible for complying with Discord's Terms of Service and applicable laws

## Technical details

- Built with **Apify SDK v3** and **Crawlee PlaywrightCrawler**
- Uses Playwright with Chromium for JavaScript rendering
- Includes anti-bot detection countermeasures (stealth mode, randomized delays)
- Deduplicates results across sources by server ID
- Handles Cloudflare challenges on third-party sites
- Supports pagination with configurable limits
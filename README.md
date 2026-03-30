# Reddit → Discord n8n Workflow

Fetches the latest posts from [r/technews](https://reddit.com/r/technews) every hour and sends them to a Discord channel.

No Reddit credentials required — uses Reddit's public JSON API.

## Workflow Overview

```
Schedule Trigger (hourly)
  → RSS Feed Read → https://www.reddit.com/r/technews/new.rss
  → Format Discord Message (Set node)
  → Send to Discord (Discord node)
```

## Setup

### 1. Import the workflow

In n8n: **Workflows → Import from file** → select `reddit-technews-to-discord.json`

### 2. Configure Discord credentials

You need a Discord Bot token:

1. Go to https://discord.com/developers/applications and create a new application
2. Under **Bot**, click **Add Bot** and copy the token
3. Under **OAuth2 → URL Generator**, select `bot` scope + `Send Messages` permission, then invite the bot to your server
4. In n8n: **Credentials → New → Discord Bot API** and paste the token
5. Open the **Send to Discord** node and:
   - Set your **Server ID** (right-click server icon in Discord → Copy Server ID)
   - Set your **Channel ID** (right-click channel in Discord → Copy Channel ID)
   - Select the Discord Bot credential

### 3. Activate

Toggle the workflow to **Active**. It will run every hour and post the 5 newest r/technews posts to your Discord channel.

## Discord Message Format

Each post is sent as a separate message:

```
**Post Title Here**

https://article-link.com

> Posted by u/username | 142 upvotes | 37 comments
> https://reddit.com/r/technews/comments/...
```

## Customization

| What to change | Where |
|---|---|
| Subreddit | `Get r/technews Posts` → URL (replace `technews`) |
| Sort order | `Get r/technews Posts` → URL (change `new` to `hot` or `top`) |
| Run frequency | `Schedule Trigger` → `hoursInterval` |
| Message format | `Format Discord Message` → `discordMessage` expression |

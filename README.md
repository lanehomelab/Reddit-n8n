# Reddit → Discord n8n Workflow

Fetches the latest posts from [r/technews](https://reddit.com/r/technews) every hour and sends them to a Discord channel.

## Workflow Overview

```
Schedule Trigger (hourly)
  → Get r/technews Posts (Reddit node, top 5)
  → Format Discord Message (Set node)
  → Send to Discord (Discord node)
```

## Setup

### 1. Import the workflow

In n8n: **Workflows → Import from file** → select `reddit-technews-to-discord.json`

### 2. Configure Reddit credentials

You need a Reddit OAuth2 app:

1. Go to https://www.reddit.com/prefs/apps and create a **script** app
2. Note your **Client ID** (under the app name) and **Client Secret**
3. In n8n: **Credentials → New → Reddit OAuth2 API**
4. Fill in Client ID, Client Secret, your Reddit username and password
5. Open the **Get r/technews Posts** node and select this credential

### 3. Configure Discord credentials

You need a Discord Bot token:

1. Go to https://discord.com/developers/applications and create a new application
2. Under **Bot**, click **Add Bot** and copy the token
3. Under **OAuth2 → URL Generator**, select `bot` scope + `Send Messages` permission, then invite the bot to your server
4. In n8n: **Credentials → New → Discord Bot API** and paste the token
5. Open the **Send to Discord** node and:
   - Set your **Server ID** (right-click server icon → Copy Server ID)
   - Set your **Channel ID** (right-click channel → Copy Channel ID)
   - Select the Discord Bot credential

### 4. Activate

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
| Subreddit | `Get r/technews Posts` → `subreddit` field |
| Number of posts | `Get r/technews Posts` → `limit` field |
| Run frequency | `Schedule Trigger` → `hoursInterval` |
| Message format | `Format Discord Message` → `discordMessage` expression |

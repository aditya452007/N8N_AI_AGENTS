# Discord Workflows

This directory contains n8n workflows designed to send automated updates and information to your Discord server.

---

## 🚀 Workflows

### 📺 Update Whenever New YouTube Video Comes

This workflow monitors a list of YouTube channels and sends a notification to Discord and Telegram whenever a new video is uploaded.

#### Workflow Details

- **Trigger**: Can be run manually or on a schedule (e.g., every 24 hours).
- **YouTube Channels**: Fetches the latest videos from a predefined list of YouTube channel IDs.
- **RSS Feed**: Uses the RSS feed of each YouTube channel to get the latest video information.
- **Filtering**: Filters for videos that have been published within the last two days.
- **Notifications**: Sends a message to a Discord channel and a Telegram chat with the video title, creator, and link.

#### Setup

1.  **YouTube Channel IDs**:
    - In the "YOUTUBE CHANNEL ID" node, replace the example channel IDs with the IDs of the channels you want to monitor.

2.  **Discord Webhook**:
    - In the "Discord" node, you will need to provide a Discord webhook URL. You can create a webhook in your Discord server's settings.
    - Add the webhook URL to your n8n credentials for the Discord node.

3.  **Telegram Bot**:
    - In the "Send a text message" (Telegram) node, you will need to provide your Telegram bot token and the chat ID of the channel or user you want to send the message to.
    - Add your Telegram bot token to your n8n credentials.

---

### 📰 News Summarizer

This workflow fetches the latest articles from an RSS feed, uses an AI model to summarize them, and then posts the summaries to a Discord channel.

#### Workflow Details

- **Trigger**: Can be run manually or on a schedule.
- **RSS Feed**: Fetches the latest articles from a specified RSS feed URL (the example uses `krebsonsecurity.com/feed/`).
- **Limit**: Limits the number of articles to process (the example is set to 5).
- **AI Summarization**: For each article, it uses a **Google Gemini** model to generate a 2-3 sentence summary.
- **Discord Notification**: Posts the summarized news, including the creator, title, summary, and a link to the original article, to a Discord channel.

#### Setup

1.  **RSS Feed URL**:
    - In the "RSS Read" node, change the URL to the RSS feed you want to monitor.

2.  **Discord Webhook**:
    - In the "Discord" node, provide a Discord webhook URL.
    - Add the webhook URL to your n8n credentials for the Discord node.

3.  **Google Gemini API**:
    - You will need a Google Gemini (formerly PaLM) API key.
    - Add the API key to your n8n credentials and select it in the "Google Gemini Chat Model" node.

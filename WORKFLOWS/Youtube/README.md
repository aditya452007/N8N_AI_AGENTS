# YouTube Workflows

This directory contains n8n workflows designed to automate tasks related to YouTube, such as monitoring for new videos and summarizing content.

---

## 🚀 Workflows

### 📺 Update Whenever New YouTube Video Comes

This workflow monitors a list of YouTube channels and sends a notification to Discord and Telegram whenever a new video is uploaded.

#### Workflow Details

- **Trigger**: Can be run manually or on a schedule.
- **YouTube Channels**: Fetches the latest videos from a predefined list of YouTube channel IDs via their RSS feeds.
- **Filtering**: Filters for videos published within the last two days.
- **Notifications**: Sends a message to a Telegram chat and a Discord channel with the video title, creator, and link.

#### Setup

1.  **YouTube Channel IDs**: Edit the "YOUTUBE CHANNEL ID" node to include the channel IDs you want to monitor.
2.  **Telegram Bot**: Configure the "Send a text message" node with your Telegram bot token and chat ID.
3.  **Discord Webhook**: Provide a Discord webhook URL in the "Discord" node.

---

### 🎬 YouTube Summary to Telegram

This workflow allows a user to send a YouTube video URL to a Telegram bot, which then returns an AI-generated summary of the video.

#### Workflow Details

- **Trigger**: Starts when a user sends a message (a YouTube URL) to the Telegram bot.
- **Transcript Fetching**: An **HTTP Request** node calls an external service (Tactiq) to get the transcript of the YouTube video.
- **Summarization**: The transcript is processed and summarized by an **AI Agent** powered by **Google Gemini**.
- **Response**: The summary is sent back to the user in the Telegram chat.

#### Setup

1.  **Telegram Bot**:
    - This workflow uses a **Chat Trigger** that is connected to a Telegram bot. You will need to configure your Telegram credentials.
    - Set the `chatId` in the "Send a text message" node to your own chat ID for testing, or configure it to dynamically use the ID of the user who sent the message.

2.  **Google Gemini API**:
    - You will need a Google Gemini (formerly PaLM) API key.
    - Add your API key to your n8n credentials and select it in the "Google Gemini Chat Model" node.

3.  **Transcript Service**:
    - The "HTTP Request1" node is configured to use `tactiq.io` to fetch transcripts. This is a third-party service and may have its own limitations or requirements.

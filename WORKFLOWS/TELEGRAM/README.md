# Telegram Workflows

This directory contains n8n workflows designed to automate tasks and provide AI-powered assistance directly within Telegram.

## 🚀 Workflows

### 1. Telegram YouTube Summary
**File:** `telegram youtube summary.json`

This workflow creates an AI agent that listens to your Telegram chat, accepts YouTube video links, fetches the transcript, summarizes the video, and sends the summary back to you.

#### How it works:
1.  **Telegram Trigger**: Listens for new messages in a Telegram chat.
2.  **HTTP Request**: Sends the YouTube URL to **Tactiq.io** to fetch the video transcript.
3.  **Summarize & Split**: Processes the transcript.
4.  **AI Agent**: Uses **Google Gemini** (with memory) to generate a concise, structured summary of the video. It can handle educational content, stories, or interviews differently.
5.  **Send Message**: Replies to the user with the summary.

#### Requirements:
*   **Telegram Bot Token**: To communicate with the bot.
*   **Google Gemini (PaLM) API Key**: For the AI summarization.

---

### 2. Update Whenever New YouTube Video Comes
**File:** `Update whenever new Youtube video comes.json`

This workflow acts as a feed monitor, checking specific YouTube channels for new uploads and notifying you via Telegram (and Discord).

#### How it works:
1.  **Schedule Trigger**: Runs daily (or on your preferred schedule).
2.  **Set Channel IDs**: Defines a list of YouTube Channel IDs to monitor.
3.  **RSS Read**: Fetches the RSS feed for each channel.
4.  **Filter**: Checks if the latest video was published within the last 2 days.
5.  **Notifications**: Sends the video title, author, and link to:
    *   **Telegram**: Via the Telegram node.
    *   **Discord**: Via a Webhook.

#### Requirements:
*   **YouTube Channel IDs**: The IDs of the channels you want to track.
*   **Telegram Bot Token & Chat ID**: For Telegram notifications.
*   **Discord Webhook URL**: For Discord notifications.

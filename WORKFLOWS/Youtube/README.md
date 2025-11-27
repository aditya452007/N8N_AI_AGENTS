# YouTube Workflows

This directory contains n8n workflows designed to automate YouTube-related tasks, such as tracking new videos and generating summaries via Telegram.

## 🚀 Workflows

### 1. Update Whenever New YouTube Video Comes
**File:** `Update whenever new Youtube video comes.json`

This workflow monitors specific YouTube channels for new uploads and sends notifications to Discord and Telegram.

#### How it works:
1.  **Schedule Trigger**: Runs daily to check for updates.
2.  **Set Channel IDs**: Defines a list of YouTube Channel IDs to track.
3.  **RSS Read**: Fetches the RSS feed for each channel.
4.  **Filter**: Checks if the video was published in the last 2 days.
5.  **Notifications**: Sends the video details (Title, Creator, Link) to:
    *   **Discord**: Via a Webhook.
    *   **Telegram**: Via the Telegram node.

#### Requirements:
*   **YouTube Channel IDs**: To monitor.
*   **Telegram Bot Token & Chat ID**: For Telegram alerts.
*   **Discord Webhook URL**: For Discord alerts.

---

### 2. YouTube Summary Telegram
**File:** `Youtube_Summary_telegram.json`

This is an AI-powered agent that takes a YouTube video link sent in a Telegram chat and replies with a summary of the video content.

#### How it works:
1.  **Telegram Trigger**: Listens for messages containing YouTube links.
2.  **HTTP Request**: Uses **Tactiq.io** to fetch the video transcript.
3.  **Summarize & Split**: Prepares the transcript text.
4.  **AI Agent**: Uses **Google Gemini** (with memory) to summarize the transcript. It follows specific rules to ignore filler words and capture key points.
5.  **Send Message**: Sends the generated summary back to the Telegram chat.

#### Requirements:
*   **Telegram Bot Token**: To receive links and send summaries.
*   **Google Gemini (PaLM) API Key**: For the AI summarization logic.

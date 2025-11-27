# Reddit Workflows

This directory contains n8n workflows designed to monitor Reddit for viral content and notifications.

## 🚀 Workflows

### 1. Reddit Viral Posts
**File:** `reddit viral posts.json`

This bot automatically fetches the **top viral posts of the day** from a curated list of subreddits and sends them to a **Telegram chat**. It is useful for keeping up with trends in niche communities without manually checking Reddit.

#### How it works:
1.  **Manual Trigger**: The workflow starts when executed manually (can be changed to a schedule).
2.  **Subreddit List**: Defines a list of subreddits to check (e.g., `PromptEngineering`, `n8n`, `psychology`).
3.  **HTTP Request**: Fetches the "Top" posts for "Today" from each subreddit via Reddit's JSON API.
4.  **Merge & Filter**: Combines the results and filters for the top 5 posts per subreddit based on a weighted score of upvotes and comments.
5.  **Format Message**: Converts the post details into a clean HTML format suitable for Telegram.
6.  **Send Telegram**: Dispatches the formatted message to your Telegram chat.

#### Requirements:
*   **Telegram Bot Token & Chat ID**: To receive the updates.
*   **No Reddit API Key Required**: This workflow uses the public JSON endpoints (`.json`), so no OAuth setup is needed for basic usage.

#### Configuration:
*   **Subreddits**: You can customize the list of subreddits in the `SUB_REDDITS_LIST` code node.
*   **Target Platform**: The workflow includes disabled nodes for Discord, Slack, WhatsApp, and Email, which you can enable and configure if preferred over Telegram.

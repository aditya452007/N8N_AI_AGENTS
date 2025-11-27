# GitHub Workflows

This directory contains n8n workflows designed to monitor and summarize activity on GitHub repositories.

## 🚀 Workflows

### 1. Github Repo Updates
**File:** `Github Repo Updates.json`

This workflow monitors the [n8n repository](https://github.com/n8n-io/n8n) (or any other repository) for new Pull Requests, summarizes the changes using AI, and sends a notification to Telegram.

#### How it works:
1.  **Schedule Trigger**: Runs automatically every day at 10 AM.
2.  **Fetch Latest Pull Request**: Retrieves the most recent pull request from the specified GitHub repository.
3.  **Filter**: Checks if the pull request was created today to avoid duplicate or old notifications.
4.  **Extract Summary**: Extracts the body/description of the pull request.
5.  **Generate AI Summary**: Uses **Google Gemini** to process the technical details and generate a user-friendly summary in bullet points.
6.  **Telegram Notification**: Sends the formatted summary to a specified Telegram channel or chat.

#### Requirements:
*   **GitHub Credentials**: To authenticate with the GitHub API.
*   **Google Gemini (PaLM) API Key**: For the AI summarization.
*   **Telegram Bot Token & Chat ID**: To send the notifications.

#### Configuration:
*   **Repository**: Currently set to `n8n-io/n8n`. You can change this in the "Fetch Latest Pull Request" node.
*   **Schedule**: Adjust the "Daily Check" node to your preferred time.

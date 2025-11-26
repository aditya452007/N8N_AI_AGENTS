# GitHub Repo Updates Workflow

This n8n workflow automates the process of monitoring a GitHub repository for new pull requests, summarizing the updates using AI, and sending a notification to a Telegram channel.

---

## 🚀 Features

- **Scheduled Monitoring**: Automatically checks for new pull requests at a specified time.
- **AI-Powered Summaries**: Uses a Large Language Model (LLM) to generate clear, human-readable summaries of technical pull request descriptions.
- **Telegram Notifications**: Keeps your team or community informed by sending updates directly to a Telegram channel.
- **Filtering**: Ensures that you only receive notifications for updates made on the current day.

---

## ⚙️ Workflow Details

1.  **Trigger**: The workflow is triggered by a **Schedule Trigger** node, which is set to run daily at 10 AM.

2.  **Fetch Latest Pull Request**: A **GitHub** node connects to the specified repository (e.g., `n8n-io/n8n`) and retrieves the most recent pull request.

3.  **Filter Today's Updates Only**: A **Filter** node checks if the pull request was created on the current day to avoid sending duplicate notifications.

4.  **Extract PR Summary**: An **Edit Fields** node extracts the body of the pull request, which contains the summary of the changes.

5.  **Generate AI Summary**: A **Basic LLM Chain** node, powered by **Google Gemini**, processes the technical summary and creates a simplified, easy-to-understand version in bullet points.

6.  **Send to Telegram Channel**: A **Telegram** node sends the AI-generated summary to a specified Telegram chat or channel.

---

## 🛠️ Setup

To use this workflow, you will need to configure the following:

1.  **GitHub Credentials**:
    - In the "Fetch Latest Pull Request" node, you will need to select your GitHub credentials. If you haven't connected your GitHub account to n8n yet, you will need to do so.

2.  **Repository to Monitor**:
    - By default, this workflow monitors the `n8n-io/n8n` repository. You can change this in the "Fetch Latest Pull Request" node by modifying the `owner` and `repository` fields.

3.  **Telegram Bot**:
    - You will need a Telegram bot token and the chat ID of the channel or user you want to send the notifications to.
    - In the "Send to Telegram Channel" node, enter your `chatId` and select your Telegram API credentials.

4.  **Google Gemini API**:
    - This workflow uses **Google Gemini** to summarize the pull requests. You will need a Google Gemini (formerly PaLM) API key.
    - Add the API key to your n8n credentials and select it in the "Google Gemini Chat Model" node.

5.  **Schedule**:
    - Adjust the schedule in the "Daily Check at 10 AM" node to fit your needs.

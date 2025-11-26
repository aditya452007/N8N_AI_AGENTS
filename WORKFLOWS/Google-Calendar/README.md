# Google Calendar Workflows

This directory contains n8n workflows that integrate with Google Calendar to automate tasks related to events and scheduling.

---

## 🚀 Workflows

### 🇮🇳 Get Holidays in India

This workflow automatically fetches a list of holidays from a public Google Calendar, formats the dates, and sends them to a Telegram chat.

#### Workflow Details

- **Trigger**: A **Schedule Trigger** node runs the workflow on a recurring basis (the example is set to run weekly).
- **Fetch Events**: A **Google Calendar** node retrieves all events from a specified public holiday calendar (the example uses "Holidays in India").
- **Format Data**: A **Code** node processes the list of events to:
    - Format the date as `dd-mm-yyyy`.
    - Extract the summary (the name of the festival).
    - Sort the holidays by date.
- **Notification**: A **Telegram** node sends each holiday as a separate message to a specified chat.

#### Setup

1.  **Google Calendar Credentials**:
    - In the "Get many events" node, you will need to select your Google Calendar credentials.

2.  **Calendar to Monitor**:
    - The workflow is pre-configured to use the "Holidays in India" public calendar. You can change this in the "Get many events" node by selecting a different calendar from the list.

3.  **Telegram Bot**:
    - You will need a Telegram bot token and the chat ID of the user or channel where you want to send the holiday notifications.
    - In the "Send a text message" node, enter your `chatId` and select your Telegram API credentials.

4.  **Schedule**:
    - Adjust the schedule in the "Schedule Trigger" node to change how often you receive updates (e.g., weekly, monthly).

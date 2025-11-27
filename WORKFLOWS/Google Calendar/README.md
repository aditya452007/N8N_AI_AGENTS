# Google Calendar Workflows

This directory contains n8n workflows for interacting with Google Calendar.

## 🚀 Workflows

### 1. Get Holidays
**File:** `Get Holidays.json`

This workflow acts as an automated holiday fetcher and notifier. It periodically retrieves upcoming holidays from Google Calendar and sends them to a Telegram chat.

#### How it works:
1.  **Schedule Trigger**: Runs once a week (every Sunday).
2.  **Get Many Events**: Fetches all events from the "Holidays in India" calendar (can be changed to any other calendar).
3.  **Code**: Formats the date to `dd-mm-yyyy` and sorts the events by date.
4.  **Telegram**: Sends a message to a specified Telegram chat for each holiday found.

#### Requirements:
*   **Google Calendar Credentials**: To access the holiday calendar.
*   **Telegram Bot Token & Chat ID**: To send the notifications.

#### Configuration:
*   **Calendar**: Currently set to `en-gb.indian#holiday@group.v.calendar.google.com`. You can change this in the "Get many events" node to your preferred holiday calendar ID.
*   **Chat ID**: Update the "Send a text message" node with your Telegram Chat ID.

# AI Personal Assistant for Telegram

This n8n workflow transforms a Telegram bot into a powerful AI-powered personal assistant. It can understand natural language commands to manage your Google Calendar, Tasks, Gmail, and Google Drive, and can also interact with Google Chat. The assistant is powered by Google Gemini.

---

## 🚀 Features

- **Natural Language Understanding**: Uses an AI agent to understand commands given in plain English.
- **Multi-Tool Integration**: Connects to various services to perform a wide range of tasks.
- **Telegram Integration**: Interacts with users through a Telegram bot.
- **Scheduled Triggers**: Can be configured to run at specific times for daily briefings or other automated tasks.
- **Voice and Image Support**: Can transcribe voice messages and analyze images.

---

## 🛠️ Services Integrated

This personal assistant can connect to and manage the following services:

- **Google Calendar**: Create, update, delete, and retrieve calendar events.
- **Google Tasks**: Create, update, delete, and retrieve tasks.
- **Gmail**: Send, reply to, and manage emails.
- **Google Drive**: Create, upload, search, and manage files and folders.
- **Google Chat**: Send messages and interact with Google Chat spaces.

---

## ⚙️ Setup

To use this workflow, you will need to configure the following:

1.  **Telegram Bot**:
    - Create a new Telegram bot by talking to the [BotFather](https://t.me/botfather).
    - Get the API token for your bot and add it to your n8n credentials.
    - Set up the Telegram Trigger node with your bot's credentials.

2.  **Google Credentials**:
    - You will need to create OAuth credentials for each of the Google services you want to use (Calendar, Tasks, Gmail, Drive, Chat).
    - Add these credentials to your n8n instance.
    - In the workflow, select your credentials for each of the Google service nodes.

3.  **Google Gemini API**:
    - You will need a Google Gemini (formerly PaLM) API key.
    - Add the API key to your n8n credentials.
    - Select your Gemini credentials in the Google Gemini Chat Model nodes.

---

## 📖 Usage

Once the workflow is set up and active, you can interact with your personal assistant by sending messages to your Telegram bot.

**Examples:**

- "What's on my calendar for today?"
- "Create a new task to buy groceries."
- "Send an email to john.doe@example.com with the subject 'Meeting tomorrow' and the message 'Hi John, let's meet at 10 AM.'"
- "Find the document named 'Project Proposal' in my Google Drive."

The workflow can also be triggered on a schedule to provide daily summaries or perform other automated tasks.

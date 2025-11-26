# Website AI Agent Workflows

This directory contains a collection of n8n workflows designed to integrate AI-powered agents and automation into your website.

---

##  workflows

### 🤖 AI Chatbot

This workflow creates an AI-powered chatbot that can be embedded on any website. It uses a webhook to receive messages, an AI agent to generate responses, and maintains a simple memory to hold a conversation.

#### Workflow Details

- **Trigger**: Receives a message from the website chat widget via a webhook.
- **AI Agent**: Processes the user's message and generates a response using a chat model (OpenRouter in this case).
- **Session Management**: Maintains a conversation by using a session ID. A new session ID is generated for new conversations.
- **Response**: Sends the AI-generated response back to the website chat widget.

#### Setup

1.  **n8n Webhook**:
    - Make sure your n8n instance is publicly accessible.
    - Use the production URL of the webhook in the HTML snippet below.

2.  **Embed on your website**:
    - Add the following code to your website's HTML:

    ```html
    <link href="https://cdn.jsdelivr.net/npm/@n8n/chat/dist/style.css" rel="stylesheet" />
    <script type="module">
        import { createChat } from 'https://cdn.jsdelivr.net/npm/@n8n/chat/dist/chat.bundle.es.js';

        createChat({
            webhookUrl: 'YOUR_PRODUCTION_WEBHOOK_URL'
        });
    </script>
    ```

3.  **Credentials**:
    - This workflow uses **OpenRouter** for the AI chat model. You will need to add your OpenRouter API key to your n8n credentials.

---

### 📝 Receive Feedback from User

This workflow automates the process of collecting and analyzing user feedback from your website. It uses an AI to summarize the feedback, suggest improvements, and even draft a social media post.

#### Workflow Details

- **Trigger**: A webhook receives feedback submitted through a form on your website.
- **AI Analysis**: The feedback is sent to an AI model to:
    - Summarize positive points.
    - Suggest improvements.
    - Generate a social media post based on the positive feedback.
- **Notifications**:
    - An email report with the AI analysis is sent to your team.
    - A draft of the social media post is sent to a Telegram chat.

#### Setup

1.  **Website Form**:
    - Create a form on your website that sends a POST request to the webhook URL with a `feedback` field.

2.  **Credentials**:
    - **Email**: Configure the "Send Feedback Report" node with your email credentials.
    - **Telegram**: Configure the "Send Social Draft" node with your Telegram bot token and chat ID.
    - **AI Provider**: The "Analyze with AI" node uses a generic HTTP Request node. You will need to configure it with the API endpoint and credentials for your chosen AI provider (e.g., DeepSeek, OpenAI).

---

### 🤓 Conversion Rate Optimizer

This workflow provides an automated Conversion Rate Optimization (CRO) audit of any landing page. Submit a URL, and an AI agent will "roast" the page and provide detailed recommendations for improvement.

#### Workflow Details

- **Trigger**: A form trigger where you can submit the URL of the landing page you want to analyze.
- **Website Scraping**: The workflow scrapes the content of the submitted URL.
- **AI Analysis**: An AI agent, powered by **Google Gemini**, analyzes the scraped content based on a detailed prompt that instructs it to act as a world-class CRO expert. The agent provides:
    - A "roast" of the landing page.
    - 10 specific and creative CRO recommendations.
- **Response**: The analysis is displayed directly in the n8n UI through a form completion message.

#### Setup

1.  **Run the workflow**:
    - This workflow is designed to be run manually or triggered via its form.

2.  **Credentials**:
    - This workflow uses **Google Gemini**. You will need to add your Google Gemini (PaLM) API key to your n8n credentials.

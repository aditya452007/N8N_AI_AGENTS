# Image Workflows

This directory contains n8n workflows for automated AI image generation.

## 🚀 Workflows

### 1. Automated AI Image Creator
**File:** `Automated AI Image Creator.json`

This workflow allows you to generate high-quality AI images directly from a Telegram chat. It uses an AI Agent (powered by Google Gemini) to refine your text prompt and then sends it to an image generation API (Pollinations AI).

#### How it works:
1.  **Telegram Trigger**: Listens for incoming messages in a specific Telegram chat.
2.  **Fields - Set Values**: Sets default parameters like image model (`flux`), width (`1080`), and height (`1920`).
3.  **AI Agent - Create Image From Prompt**: Uses **Google Gemini** to take the user's message and convert it into a detailed, professional image generation prompt. It follows a structured format including scene, key elements, lighting, and technical parameters.
4.  **Code - Clean Json**: Cleans the output from the AI agent to extract the JSON prompt.
5.  **Code - Get Prompt**: Prepares the final payload for the image generation API.
6.  **HTTP Request - Create Image**: Sends the prompt to **Pollinations AI** to generate the image.
7.  **Telegram Response**: Sends the generated image back to the Telegram chat.

#### Requirements:
*   **Telegram Bot Token**: To receive messages and send images.
*   **Google Gemini (PaLM) API Key**: For the prompt refinement agent.
*   **Pollinations AI**: This workflow uses the free Pollinations AI API (no key required in the default setup, but check their documentation for limits).

#### Usage:
1.  Start the workflow.
2.  Send a text description of the image you want to the connected Telegram bot.
3.  The bot will reply with the generated image.

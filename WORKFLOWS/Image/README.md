# AI Image Creator Workflow

This n8n workflow automates the creation of images from text prompts using an AI model and sends the generated image to a Telegram chat.

---

## 🚀 Features

- **Text-to-Image Generation**: Converts a text prompt into an image.
- **AI-Powered**: Uses **Google Gemini** to create a detailed image prompt from a simple text input.
- **Telegram Integration**: Can be triggered by a Telegram message and sends the resulting image back to the chat.
- **Customizable**: Allows for setting the image dimensions and model.

---

## ⚙️ Workflow Details

1.  **Trigger**: The workflow can be triggered in two ways:
    - **Telegram Trigger**: Starts when a message is received in a specified Telegram chat.
    - **Chat Trigger**: A generic chat trigger that can be integrated with other platforms.

2.  **Set Image Parameters**: An **Edit Fields** node sets the default values for the image `width`, `height`, and the `model` to be used for image generation.

3.  **Generate AI Prompt**: An **AI Agent** node takes the user's text input and, using **Google Gemini**, expands it into a detailed, structured prompt suitable for an image generation model.

4.  **Image Generation**:
    - The detailed prompt is sent to the **Pollinations AI** image generation API via an **HTTP Request** node.
    - The workflow sets a filename for the generated image.

5.  **Send Image**: The final image is sent as a photo to the Telegram chat from which the command was initiated.

---

## 🛠️ Setup

To use this workflow, you will need to configure the following:

1.  **Telegram Bot**:
    - You will need a Telegram bot token and the chat ID of the user or group you want to interact with.
    - Configure the "Telegram Trigger" and "Telegram Response" nodes with your bot's credentials and the appropriate chat ID.

2.  **Google Gemini API**:
    - This workflow uses **Google Gemini** to generate the detailed image prompts. You will need a Google Gemini (formerly PaLM) API key.
    - Add your API key to your n8n credentials and select it in the "Google Gemini Chat Model" node.

3.  **Image Parameters**:
    - In the "Fields - Set Values" node, you can change the default `width`, `height`, and `model` for the generated images.

4.  **Pollinations AI**:
    - This workflow uses the free Pollinations AI API for image generation, which does not require an API key. If you wish to use a different image generation service, you will need to modify the "HTTP Request - Create Image" node accordingly.

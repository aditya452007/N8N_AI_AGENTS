# AI Prompt Generator Agent

This n8n workflow provides a multi-step form that guides users through the process of creating a detailed and effective prompt for an AI agent. It asks a series of questions to understand the user's goal and then generates a structured prompt that can be used with a large language model (LLM).

---

## 🚀 Features

- **Interactive Form**: Uses a series of forms to gather information from the user about their goals.
- **Dynamic Question Generation**: Employs an AI model to generate relevant follow-up questions based on the user's initial input.
- **Structured Prompt Generation**: Creates a well-structured and detailed prompt that is optimized for use with AI agents.
- **AI-Powered**: Uses **Google Gemini** for both question and prompt generation.

---

## ⚙️ Workflow Details

1.  **Initial Form**: The workflow starts with a **Form Trigger** that presents the user with a form to describe the AI agent they want to build. The user provides information about the agent's purpose, the tools it can access, and the expected input and output.

2.  **Generate Clarifying Questions**: The user's initial input is passed to a **RelatedQuestionAI** (an LLM chain powered by Google Gemini) which generates up to three clarifying questions to gather more specific details.

3.  **Ask Follow-up Questions**: The workflow then loops through the generated questions, presenting each one to the user in a new form.

4.  **Consolidate Information**: All of the user's answers (from both the initial form and the follow-up questions) are merged together.

5.  **Generate Final Prompt**: The consolidated information is passed to the **PromptGenerator** (another LLM chain), which creates a final, structured prompt. This prompt is formatted to be easily understood by another AI agent and includes sections for:
    - `<role>`
    - `<inputs>`
    - `<tools>`
    - `<instructions>`
    - `<constraints>`
    - `<conclusions>`

6.  **Display Prompt**: The final prompt is displayed to the user in a completion message, ready to be copied and used.

---

## 🛠️ Setup

To use this workflow, you will need to configure the following:

1.  **Google Gemini API**:
    - This workflow heavily relies on **Google Gemini**. You will need a Google Gemini (formerly PaLM) API key.
    - Add your API key to your n8n credentials and select it in both the "Google Gemini Chat Model" and "Google Gemini Chat Model1" nodes.

2.  **Run the Workflow**:
    - This workflow is designed to be triggered by its initial form. Once activated, you can access the form via its URL.

3.  **Customization**:
    - The prompts for both the question-generating AI and the final prompt-generating AI can be customized in the "RelatedQuestionAI" and "PromptGenerator" nodes, respectively.
    - The appearance of the forms can be customized using the CSS in each of the form nodes.

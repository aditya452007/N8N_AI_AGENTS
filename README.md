# n8n AI Agents & Automation Workflows

Welcome to the **n8n AI Agents & Automation Workflows** repository! This collection features a variety of custom-built agents and workflows designed to automate tasks, integrate services, and leverage AI to enhance productivity.

Whether you're looking to automate your daily workspace setup, manage social media, track free courses, or build intelligent chatbots, this repository provides the templates you need.

---

## 📂 Repository Structure

The repository is organized into two primary sections:

### 1. [POWER AUTOMATE](./POWER%20AUTOMATE)
A collection of flows for **Microsoft Power Automate Desktop (PAD)**.
*   **Workspace Starter**: Automates opening your essential daily websites and applications.

### 2. [WORKFLOWS](./WORKFLOWS)
A comprehensive library of **n8n workflows** categorized by service or purpose:

*   **[AI-AGENT-KIT](./WORKFLOWS/AI-AGENT-KIT)**: Modular kits for building AI-powered agents (Telegram, Website, WhatsApp).
*   **[Discord](./WORKFLOWS/Discord)**: Automations for Discord notifications and news summaries.
*   **[Free Courses List](./WORKFLOWS/Free%20Courses%20List)**: Track and fetch coupons for free Udemy courses.
*   **[Github](./WORKFLOWS/Github)**: Monitor GitHub repositories for updates.
*   **[Google Calendar](./WORKFLOWS/Google%20Calendar)**: Manage holidays and calendar events.
*   **[Image](./WORKFLOWS/Image)**: automated AI image generation workflows.
*   **[Linkedin](./WORKFLOWS/Linkedin)**: Automate job searches and cold email outreach.
*   **[Prompting Agent](./WORKFLOWS/Prompting%20Agent)**: An agent designed to help generate and refine prompts.
*   **[Reddit](./WORKFLOWS/Reddit)**: Monitor viral posts on Reddit.
*   **[TELEGRAM](./WORKFLOWS/TELEGRAM)**: Telegram bots for YouTube summaries and holiday updates.
*   **[Youtube](./WORKFLOWS/Youtube)**: YouTube automation for video updates and summaries.

---

## 🚀 Getting Started

### Prerequisites

*   **n8n**: You need a running instance of [n8n](https://n8n.io/). It can be the self-hosted version or n8n Cloud.
*   **Power Automate Desktop**: For the flows in the `POWER AUTOMATE` directory, you need Microsoft Power Automate Desktop installed on Windows.

### How to Use n8n Workflows

1.  **Clone or Download**: Clone this repository or download the specific JSON file for the workflow you want.
2.  **Import to n8n**:
    *   Open your n8n dashboard.
    *   Click on **"Import from..."** in the top right corner or create a new workflow.
    *   Select **"Import from File"** and choose the `.json` file.
    *   Alternatively, copy the content of the JSON file and paste it directly into the n8n editor (Ctrl+V / Cmd+V).
3.  **Configure Credentials**:
    *   Most workflows require credentials (e.g., API keys for OpenAI, Telegram, Discord, etc.).
    *   Double-click on the nodes that show an error or require authentication and set up your credentials in n8n.
4.  **Activate**: Once configured, toggle the **Active** switch to enable the workflow.

### How to Use Power Automate Flows

1.  Navigate to the `POWER AUTOMATE` directory.
2.  Follow the instructions in the [README](./POWER%20AUTOMATE/README.md) to set up the flow in your Power Automate Desktop application.

---

## 🤝 Contributing

Contributions are welcome! If you have a useful workflow or agent you'd like to share:

1.  Fork the repository.
2.  Create a new branch for your feature.
3.  Add your workflow file (export it as JSON from n8n).
4.  Add a `README.md` explaining what it does and how to set it up.
5.  Submit a Pull Request.

---

## 📝 License

This project is open-source. Please check the [LICENSE](./LICENSE) file for details.

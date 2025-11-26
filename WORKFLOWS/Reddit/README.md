# Reddit Viral Posts Workflow

This n8n workflow fetches the top 5 most viral posts from a list of specified subreddits based on upvotes and comments, and sends them to a Telegram channel.

---

## 🚀 Features

- **Multi-Subreddit Monitoring**: Fetches posts from a customizable list of subreddits.
- **Viral Post Filtering**: Identifies the top 5 posts of the day from each subreddit by sorting them based on a combination of upvotes and comments.
- **Telegram Notifications**: Sends a formatted message to a Telegram chat for each viral post, including the title, upvotes, comments, and a link to the post.
- **Extensible**: Includes disabled nodes for sending notifications to Discord, Gmail, WhatsApp, and Slack, which can be easily configured and enabled.

---

## ⚙️ Workflow Details

1.  **Trigger**: The workflow can be started manually with a **Manual Trigger** node.

2.  **Subreddit List**: A **Code** node (`SUB_REDDITS_LIST`) contains an array of subreddit names to monitor.

3.  **Fetch Posts**: An **HTTP Request** node iterates through the list of subreddits and fetches the top 50 posts from the last 24 hours for each one.

4.  **Filter Top 5 Posts**: A **Code** node (`TOP_5_POST`) processes the fetched posts for each subreddit, sorts them by a combined score of upvotes and comments, and selects the top 5.

5.  **Format Message**: A **Code** node (`TELEGRAM_FREINDLY_MSG`) formats the details of each of the top 5 posts into an HTML message suitable for Telegram.

6.  **Send Notification**: A **Telegram** node sends the formatted message to the specified chat.

---

## 🛠️ Setup

To use this workflow, you will need to configure the following:

1.  **Subreddit List**:
    - In the "SUB_REDDITS_LIST" node, you can edit the `subs` array to include the subreddits you want to monitor.

2.  **Telegram Bot**:
    - You will need a Telegram bot token and the chat ID for the channel or user you want to send the posts to.
    - In the "Send Reddit VIRAL Post" node, enter your `chatId` and select your Telegram API credentials.

3.  **Other Platforms (Optional)**:
    - The workflow includes disabled nodes for Discord, Gmail, WhatsApp, and Slack. To use them:
        - Enable the desired node.
        - Configure it with the necessary credentials and settings.
        - Connect it to the "TELEGRAM_FREINDLY_MSG" node (or create a new formatting node for that platform).

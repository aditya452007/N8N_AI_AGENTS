# PAD Workspace Starter

## 🚀 Introduction

This is a simple Power Automate Desktop (PAD) flow designed to act as a **"workspace starter."** It automates the daily ritual of opening all your essential websites.

When run, this flow launches a single Google Chrome window and automatically opens a predefined set of frequently used work, study, and communication sites, getting you ready to start your day with one click.

---

## 📋 What It Does

The flow executes the following steps in order:

1.  **Launches Google Chrome**: It opens a new, maximized Chrome window, starting with `youtube.com`.
2.  **Opens New Tabs**: It then proceeds to open the following websites in new, separate tabs:
    * Udemy (My Courses)
    * GeeksforGeeks
    * Telegram Web
    * LinkedIn Feed
    * Gmail
    * TradingView

---

## 💡 Recommendations & Customization

This flow is a great personal template. Here are a few recommendations for making it more robust and customizing it for your own use.

### 1. Customize Your URLs
The URLs are currently hardcoded. You should edit the `Url:` parameter in each step to match your personal links.

**Example:**
The flow uses `...mail.google.com/mail/u/2/#inbox`. This `u/2/` part refers to a specific Google profile. You should change this to match your primary account (which might be `u/0/` or just `mail.google.com`). The same applies to your specific TradingView chart.

### 2. Use Standard "Wait" Actions
The script currently uses `LaunchChromeNoWait` and `CreateNewTabNoWait`. This tells PAD to execute the next step immediately, without confirming if the browser or tab has actually finished loading. This can be unreliable.

* **Recommendation:** For better stability, use the standard **`LaunchChrome`** and **`CreateNewTeb`** actions. These actions will wait for the page to be ready before moving to the next step, ensuring your flow doesn't fail if a site is loading slowly.

### 3. Clean Up Output Variables
In your script, you are storing the output of each new tab into variables like `NewBrowser2`, `NewBrowser3`, etc. You also overwrite the `NewBrowser2` variable multiple times.

* **Recommendation:** Since you aren't using these variables later (e.g., you're not interacting with the "GeeksforGeeks" tab specifically), you can simplify your flow. In the `CreateNewTab` action, you can just **disable the output variable** (or delete the variable name `NewBrowser2` from the "BrowserInstance" output field). This makes your flow cleaner and easier to read.

# LinkedIn Workflows

This directory contains n8n workflows designed to automate LinkedIn-related tasks such as job searching and cold email outreach.

## 🚀 Workflows

### 1. LinkedIn Job Search
**File:** `Linkedin_Job_search.json`

This workflow acts as a specialized job scraper, searching for recent LinkedIn job postings using Google Custom Search and saving them to a Google Sheet.

#### How it works:
1.  **Set Fields**: Initializes pagination parameters (start index, pages to scrape).
2.  **Google Search**: Uses **Google Custom Search API** to find LinkedIn job postings.
    *   **Query**: Searches for "junior" or "entry level" roles related to "AI developer", "AI engineer", or "prompt engineer" on `site:linkedin.com/jobs`.
    *   **Date Restrict**: Limits results to the last 24 hours (`d1`).
3.  **Extract Results**: Processes the search results to extract titles, snippets, and URLs.
4.  **Wait**: Adds a delay to avoid hitting API rate limits.
5.  **Append to Google Sheet**: Saves the job listings to a Google Sheet.
6.  **Pagination**: Calculates the next page of results and loops back to fetch more if available.

#### Requirements:
*   **Google Custom Search API Key & CX ID**: You need a custom search engine set up to search LinkedIn.
*   **Google Sheets**: To store the job results.

---

### 2. Send Cold EMAILS
**File:** `Send_Cold_EMAILS.json`

This workflow automates the process of finding CEO contact information from LinkedIn profiles via Google Search and sending them cold emails.

#### How it works:
1.  **Search LinkedIn Emails**: Uses **Google Custom Search API** to find LinkedIn profiles of CEOs who have their email (gmail/yahoo) visible in their profile summary.
    *   **Query**: `site:linkedin.com/in (intitle:"CEO" OR "Chief Executive Officer") (intext:"@gmail.com" OR intext:"@yahoo.com")`.
2.  **Extract & Save**: Extracts the search results and saves them to a Google Sheet.
3.  **Process Rows**: Reads the saved rows from the Google Sheet.
4.  **Code (Clean Data)**: Uses JavaScript to extract the name and email address from the search snippet and title.
5.  **Filter**: Validates the extracted email addresses.
6.  **Send Email**: Uses **Gmail** to send a cold email to the extracted address.
7.  **Update Sheet**: Updates the Google Sheet to mark the email as sent.

#### Requirements:
*   **Google Custom Search API Key & CX ID**: Configured for the search query.
*   **Google Sheets**: For storing leads and tracking status.
*   **Gmail Credentials**: To send the emails.

**⚠️ Note**: Use this workflow responsibly and adhere to anti-spam laws (like CAN-SPAM or GDPR) and LinkedIn's terms of service.

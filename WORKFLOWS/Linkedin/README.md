# LinkedIn Workflows

This directory contains n8n workflows designed to automate tasks related to LinkedIn, such as job searching and lead generation.

---

## 🚀 Workflows

### 🔎 LinkedIn Job Search

This workflow uses Google Custom Search to find recent job postings on LinkedIn for specific roles and keywords, then saves the results to a Google Sheet.

#### Workflow Details

- **Custom Search**: Uses the Google Custom Search API to perform a targeted search on `linkedin.com/jobs`.
- **Keyword Targeting**: The search query is configured to find "junior" or "entry level" roles related to "ai developer," "ai engineer," or "prompt engineer."
- **Time-Based Filtering**: The search is restricted to results from the last 24 hours.
- **Pagination**: The workflow is designed to loop through multiple pages of search results.
- **Google Sheets Sync**: The job postings (title, snippet, and URL) are appended to a Google Sheet.

#### Setup

1.  **Google Custom Search API**:
    - You will need a **Google API Key** and a **Custom Search Engine ID (cx)**.
    - In the "Google search2" node, replace `"Your_Key"` and `"Your value"` with your API key and search engine ID.

2.  **Search Query**:
    - You can customize the search query in the `q` parameter of the "Google search2" node to target different roles, keywords, or locations.

3.  **Google Sheet**:
    - Create a Google Sheet to store the job listings.
    - In the "Append or update row in sheet2" node, select your Google Sheets credentials and specify the Document ID and Sheet Name.

---

### 📧 Send Cold Emails to LinkedIn Leads

This workflow scrapes LinkedIn for profiles of CEOs with publicly listed Gmail or Yahoo email addresses, extracts their names and emails, and then sends them a cold email.

#### Workflow Details

- **Lead Scraping**: Uses Google Custom Search to find LinkedIn profiles of CEOs that have `@gmail.com` or `@yahoo.com` in the text.
- **Data Extraction**: A **Code** node uses regular expressions to extract the name and email address from the search results.
- **Email Sending**: A **Gmail** node sends a personalized cold email to each extracted email address.
- **Tracking**: After sending an email, the workflow updates a Google Sheet to mark the lead as contacted.
- **Pagination**: The workflow paginates through the search results to find more leads.

#### Setup

1.  **Google Custom Search API**:
    - You will need a **Google API Key** and a **Custom Search Engine ID (cx)**.
    - In the "Search Linkedin Emails1" node, replace `"your key"` and `"your cx"` with your API key and search engine ID.

2.  **Google Sheet for Leads**:
    - Set up a Google Sheet to store and track the leads.
    - Configure the "Append or update row in sheet2" and "Append or update row in sheet3" nodes with your Google Sheets credentials, Document ID, and Sheet Name.

3.  **Gmail Account**:
    - In the "Send a message1" node, select your Gmail credentials.

4.  **Email Template**:
    - Customize the subject and body of your cold email in the "Send a message1" node.

# Free Udemy Courses Workflows

This directory contains n8n workflows designed to automatically find and track free Udemy courses.

---

## 🚀 Workflows

### 💸 Get Free Udemy Course Coupon

This workflow fetches Udemy courses with coupons, filters for the ones that are completely free, and syncs them to a Google Sheet.

#### Workflow Details

- **Trigger**: Runs on an hourly schedule.
- **API Integration**: Fetches a list of Udemy courses from the `udemy-paid-courses-for-free-api`.
- **Filtering**: Filters the results to include only courses where the `sale_price_usd` is 0.
- **Google Sheets Sync**: Adds or updates the free courses in a specified Google Sheet.
- **Error Handling**: Sends an email notification if the API call fails.

#### Setup

1.  **API Key**:
    - You will need an API key from **RapidAPI** for the "Udemy Paid Courses for Free API".
    - In the "Fetch Udemy Coupons" node, replace `"your_api_key"` with your actual RapidAPI key.

2.  **Google Sheet**:
    - Create a Google Sheet to store the course information.
    - In the "Sync Courses to Google Sheet" node, select your Google Sheets credentials and specify the Document ID and Sheet Name.

3.  **Email Notifications**:
    - Configure the "Send Error Notification" node with your SMTP credentials to receive email alerts on failure.

4.  **Query**:
    - In the "Fetch Udemy Coupons" node, you can change the `query` parameter to search for courses on a different topic (the default is "python").

---

### 📈 Track Free Udemy Courses

This workflow is similar to the one above but uses a different API to fetch and track free Udemy courses.

#### Workflow Details

- **Trigger**: Runs on an hourly schedule.
- **API Integration**: Fetches featured Udemy courses from the `udemy-coupons-and-courses` API on RapidAPI.
- **Filtering**: Filters for courses where the `sale_price` is 0.
- **Google Sheets Sync**: Appends or updates the course data in a Google Sheet, matching by course ID.
- **Error Handling**: Sends an email if the API call is not successful.

#### Setup

1.  **API Key**:
    - You will need a RapidAPI key for the "Udemy Coupons and Courses" API.
    - In the "Fetch Udemy Coupons1" node, replace `"your key"` with your RapidAPI key.

2.  **Google Sheet**:
    - Set up a Google Sheet to track the courses.
    - In the "Sync Courses to Google Sheet1" node, configure your Google Sheets credentials, Document ID, and Sheet Name.

3.  **Email Notifications**:
    - Configure the "Send Error Notification1" node with your SMTP credentials.

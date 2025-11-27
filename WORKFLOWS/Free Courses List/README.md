# Free Courses List Workflows

This directory contains n8n workflows designed to track and aggregate free courses, specifically from Udemy, and organize them into Google Sheets.

## 🚀 Workflows

### 1. Get Free Udemy Course Coupon
**File:** `Get Free Udemy Course Coupon.json`

This workflow periodically searches for Udemy courses related to "python" that are currently free (100% off) and adds them to a Google Sheet.

#### How it works:
1.  **Schedule Trigger**: Runs every hour.
2.  **Fetch Udemy Coupons**: Calls a RapidAPI endpoint (`udemy-paid-courses-for-free-api`) to search for courses.
3.  **Check Success**: Verifies the API response is 200 OK.
4.  **Filter**: Uses JavaScript to filter only courses where `sale_price_usd` is 0.
5.  **Google Sheets**: Appends or updates the course details (Name, Category, Image, Link, etc.) in a Google Sheet.
6.  **Error Handling**: Sends an email notification if the API call fails.

#### Requirements:
*   **RapidAPI Key**: You need to subscribe to the `udemy-paid-courses-for-free-api` on RapidAPI and get an API key.
*   **Google Sheets**: A Google Sheet set up with columns like `name`, `category`, `image`, `url`, etc.
*   **SMTP Credentials**: For sending error emails.

---

### 2. Track Free Udemy Courses
**File:** `Track Free Udemy Courses.json`

This workflow is similar to the first one but targets a different API endpoint (`udemy-coupons-and-courses`) to fetch featured free courses.

#### How it works:
1.  **Schedule Trigger**: Runs every hour.
2.  **Fetch Udemy Coupons**: Calls the `featured.php` endpoint of the `udemy-coupons-and-courses` API via RapidAPI.
3.  **Check Success**: Verifies the API response.
4.  **Filter**: Filters courses where `sale_price` is 0.
5.  **Google Sheets**: Syncs the course data (ID, Name, Coupon Code, etc.) to a Google Sheet.
6.  **Error Handling**: Sends an email notification if the API call fails.

#### Requirements:
*   **RapidAPI Key**: Subscription to `udemy-coupons-and-courses` API.
*   **Google Sheets**: A Google Sheet for storing course data.
*   **SMTP Credentials**: For error notifications.

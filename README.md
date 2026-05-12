# 📊 UK Companies House Daily Tracker & AI Analyser

This project is a Python-based automation script designed to be run in Google Colab. It pulls daily data from the UK Companies House API, tracks newly incorporated and dissolved companies, logs the data into a Google Sheet, and uses Google's Gemini 2.0 Flash AI to generate a daily executive summary of business trends.

## ✨ Features

* **Dual API Queries:** Automatically fetches both newly opened and dissolved UK companies for the current day, maxing out at the 5,000 limit per query.
* **Smart Data Extraction:** Pulls exact creation dates, SIC codes (industries), postcodes, and formats full registered addresses.
* **Automated Age Calculation:** Calculates exactly how many years a dissolved company survived before closing.
* **Google Sheets Integration:** Uses `gspread` to securely authenticate and batch-upload thousands of rows in seconds, appending new data daily without overwriting.
* **AI Trend Analysis:** Selects a random, representative sample of the day's data and passes it to Gemini 2.0 Flash to generate a high-level summary of regional and industry trends.

## 🛠️ Prerequisites

Before you can run this script, you will need:
1. A **Google Account** (to use Google Colab and Google Sheets).
2. A **Google Sheet** ready to receive the data.
3. A **Companies House API Key** (Get one [here](https://developer.company-information.service.gov.uk/)).
4. A **Google Gemini API Key** (Get one from [Google AI Studio](https://aistudio.google.com/)).

## 🚀 Setup Instructions

### 1. Prepare Your Google Sheet
Create a new Google Sheet and add the following headers to Row 1:
`[ Fetch Date | Company Name | Number | Status | Creation Date | Years Active | SIC Codes | Postcode | Full Address ]`
*Copy the URL of this Google Sheet—you will need it in the script.*

### 2. Configure Google Colab Secrets
To keep your API keys secure, use Google Colab's built-in Secrets manager:
1. Open your Colab Notebook.
2. Click the **Key icon (🔑)** on the left sidebar.
3. Add a new secret named `COMPANIES_HOUSE_API_KEY` and paste your key.
4. Add another secret named `GEMINI_API_KEY` and paste your key.
5. Make sure the **Notebook access** toggle is turned **ON** for both.

### 3. Update the Script Configuration
In the script's configuration section, update the `SHEET_URL` variable to match the URL of the Google Sheet you created in Step 1.

## 💻 Usage

Simply click the **"Run all"** button in Google Colab (or press `Ctrl/Cmd + Enter` on the code cell). 

The script will:
1. Prompt you to authenticate with your Google account.
2. Fetch up to 10,000 records from Companies House.
3. Process and batch-upload the data to your Google Sheet.
4. Output a clean AI-generated summary directly in the Colab notebook output.

## 📚 Tech Stack

* **Python 3**
* **Requests:** For REST API calls to Companies House.
* **Gspread:** For interacting with the Google Sheets API.
* **Google GenAI SDK:** For prompting the Gemini 2.0 Flash model.
* **Pytz / Datetime:** For precise UK timezone handling.

## ⚠️ Notes on API Limits
* **Companies House:** This script uses the `&size=5000` parameter, which is the maximum allowed per request. If there are more than 5,000 dissolutions or creations in a single day, pagination would be required to fetch the remainder.
* **Gemini Free Tier:** To prevent rate-limiting on the free tier of the Gemini API, the script passes a randomized sample of 300 companies to the AI rather than the full daily dataset.

---
*Built for tracking UK business trends dynamically.*



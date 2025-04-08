# 🧠 AI-Powered News Summarizer using Mistral AI + Google Sheets

This project automatically fetches news articles from **The Hindu's National RSS feed**, extracts the full content, and uses **Mistral AI** to generate:
- ✅ A concise summary (3 sentences)
- 🗺️ The geographic relevance (e.g., National, Maharashtra, Mumbai)
- 🧭 The genre/category (e.g., Politics, Entertainment, Crime, Sports, etc.)

All outputs are stored in a clean and simple **Google Sheet**.

---

## 🔧 Tech Stack

- **Google Apps Script**: Serverless automation inside Google Sheets
- **Mistral AI API**: Powerful open-weight LLMs (using `mistral-small-latest`)
- **RSS Feed**: From [The Hindu – National](https://www.thehindu.com/news/national/feeder/default.rss)
- **Google Sheets**: Your lightweight database and dashboard

---

## 📋 Output Format

Each row in the Google Sheet contains:

| Date       | Title | Link | Summary | Geography | Genre |
|------------|-------|------|---------|-----------|-------|
| Timestamp  | News Title | Article URL | AI-generated summary | National / State / City | Politics / Crime / ... |

---

## 🚀 How It Works

1. **Fetch articles** from The Hindu’s RSS feed
2. **Extract full text** from the linked article pages
3. **Send the content** to Mistral AI with a prompt asking for summary + geography + genre
4. **Parse the JSON** returned by Mistral
5. **Write data** to a pre-configured Google Sheet

---

## ⚙️ Setup Instructions

1. **Create a Google Sheet** with the sheet name: `HinduSummaries`
2. Add columns: `Date`, `Title`, `Link`, `Summary`, `Geography`, `Genre`
3. Open `Extensions > Apps Script` and paste the code from this repo
4. Replace `YOUR_API_KEY` with your [Mistral API key](https://console.mistral.ai/api-keys)
5. (Optional) Set a **time-driven trigger** to run the script daily

---

## 🧠 Prompt Design

We use this structured prompt:
```text
You will be given a news article. Analyze the content and return only a valid JSON object with the following fields:
{
  "summary": "A concise, objective summary of the article in 3 sentences.",
  "geography": "The specific geographical scope of the news (e.g., 'India', 'Maharashtra', 'Mumbai'). If it's international, state 'International'.",
  "genre": "The category of the news (e.g., 'Politics', 'Entertainment', 'Sports', 'International', 'Local', 'Crime', etc.)."
}

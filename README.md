# Customer Feedback Intelligence & Automation Platform

An end-to-end Streamlit dashboard that ingests customer reviews, runs AI-powered sentiment analysis on them, stores the results in a SQL database, and visualizes the outcome — with a simulated automated incident-response workflow that triggers when negative feedback crosses a critical threshold.

---

## Screenshots



 <img width="1902" height="785" alt="image" src="https://github.com/user-attachments/assets/f9558791-00db-443f-9521-6926cbdb6399" />
 <img width="1882" height="706" alt="image" src="https://github.com/user-attachments/assets/b9a72dcf-5339-44b2-b559-cefac85b09fe" />

 
---

## What this project does

1. **Data Ingestion** — Load a demo dataset (`reviews_data.csv`) or upload your own CSV file, with flexible column mapping (review text, reviewer name, rating).
2. **Storage** — Reviews are stored and tracked in a local **SQLite** database (`enterprise_feedback.db`).
3. **AI Sentiment Analysis** — A pretrained Hugging Face Transformers model (`distilbert-base-uncased-finetuned-sst-2-english`) classifies each review as **POSITIVE** or **NEGATIVE** with a confidence score.
4. **Batch Processing** — Process all pending (unanalyzed) reviews in one click from the sidebar.
5. **Live Testing** — Type any sentence into the sidebar and get an instant sentiment prediction, without touching the database.
6. **Dashboard & Analytics** — Key metrics (total reviews, negative ratio, system status), an interactive Plotly pie chart, and a live data table of all processed reviews.
7. **Simulated Automated Incident Response** — If the negative-review ratio exceeds **25%**, the dashboard displays a simulated incident log (webhook dispatch → n8n orchestration → Jira ticket creation → SMTP email alert) to illustrate how a real automation pipeline could react to a spike in customer dissatisfaction.

> **Note:** The automation/incident-response section (n8n, Jira, SMTP) is a **visual simulation for demonstration purposes** — it does not make real network calls to any external system. It's meant to showcase *what an automated response would look like* in a production setup.

---

## Tech Stack

| Layer | Technology |
|---|---|
| UI / App Framework | [Streamlit](https://streamlit.io/) |
| Data Handling | Pandas |
| Database | SQLite3 |
| AI / NLP Model | Hugging Face `transformers` (DistilBERT, sentiment-analysis pipeline) |
| Visualization | Plotly Express |
| Simulated Automation Layer | n8n-style webhook / Jira / SMTP audit log (mocked) |

---

## Installation

```bash
# 1. Clone the repository
git clone https://github.com/mira203/Customer-Feedback-Intelligence-Automation-Platform
cd Customer-Feedback-Intelligence-Automation-Platform

# 2. Create a virtual environment (recommended)
python -m venv venv
source venv/bin/activate   # On Windows: venv\Scripts\activate

# 3. Install dependencies
pip install streamlit pandas plotly transformers torch

# 4. Run the app
streamlit run app.py
```

The first run will download the DistilBERT model from Hugging Face (~250MB), so make sure you have an internet connection.

---

## Usage

1. From the sidebar, choose **"Use Demo Starbucks Data"** or **"Upload Custom CSV Dataset"**.
2. If uploading a custom CSV, map the review text, name, and rating columns.
3. Click **"Ingest ... to SQL"** to load the data into the database.
4. Click **"Execute AI Batch Pipeline"** to run sentiment analysis on all pending reviews.
5. Explore the dashboard: metrics, sentiment pie chart, and the full reviews table.
6. Try the **Live Single-Review Tester** in the sidebar to test any custom sentence instantly.
7. If negative sentiment crosses 25% of total reviews, a simulated alert and incident log will appear automatically.

---

## Project Structure

```
.
├── app.py                  # Main Streamlit application
├── reviews_data.csv        # Demo dataset (optional)
├── enterprise_feedback.db  # SQLite database (auto-created on first run)
└── README.md
```

---

## Possible Future Improvements

- Connect the simulated automation layer to real services (actual n8n webhook, Jira API, SMTP server).
- Support multilingual sentiment analysis.
- Add review-level topic/keyword extraction.
- Add authentication for multi-user / enterprise use.
- Deploy via Docker / Streamlit Community Cloud.

---

## 📄 License

This project is open source — feel free to use, modify, and build on it.

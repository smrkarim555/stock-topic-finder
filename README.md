# Stock Topic Finder

A professional SaaS tool for Adobe Stock contributors to discover high-potential, low-competition content topics using AI-powered analysis and Google Trends data.

## Features

- 🔍 **AI Topic Generation** — Uses Groq API (llama-3.3-70b) to generate targeted Adobe Stock topics
- 📊 **Opportunity Scoring** — Smart scoring based on demand, competition, and trend data
- 🔖 **Save & Export** — Bookmark topics and export to CSV or TXT
- 📈 **Search History** — Full search history with result counts
- 🎨 **Clean SaaS UI** — Professional light theme matching reference design

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 18 + Vite + Tailwind CSS |
| Backend | Python FastAPI |
| Database | SQLite |
| AI Engine | Groq API (llama-3.3-70b-versatile) |
| Icons | Lucide React |

## Quick Start

### 1. Backend

```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```

Backend runs at: http://localhost:8000

### 2. Frontend

```bash
cd frontend
npm install --legacy-peer-deps
npm run dev
```

Frontend runs at: http://localhost:5173

### 3. Add Groq API Key

1. Get a free key at https://console.groq.com
2. Go to **API Settings** in the app
3. Enter your key (starts with `gsk_`)

Without a key, the app runs with mock data for demonstration.

## Project Structure

```
stock-topic-finder/
├── backend/
│   ├── main.py              # FastAPI app with all routes
│   ├── requirements.txt
│   └── stock_topics.db      # Auto-created SQLite database
└── frontend/
    ├── src/
    │   ├── components/
    │   │   ├── Sidebar.jsx
    │   │   ├── Sparkline.jsx
    │   │   └── DemandBars.jsx
    │   ├── pages/
    │   │   ├── Dashboard.jsx
    │   │   ├── TopicFinder.jsx
    │   │   ├── SavedTopics.jsx
    │   │   ├── History.jsx
    │   │   ├── ApiSettings.jsx
    │   │   └── SettingsAbout.jsx
    │   ├── hooks/
    │   │   └── useSettings.js
    │   ├── lib/
    │   │   └── api.js
    │   └── App.jsx
    ├── package.json
    └── vite.config.js
```

## API Routes

| Method | Route | Description |
|--------|-------|-------------|
| GET | /api/settings | Get API key status |
| POST | /api/settings/api-key | Save API key |
| DELETE | /api/settings/api-key | Remove API key |
| POST | /api/search | Search/generate topics |
| GET | /api/saved-topics | Get saved topics |
| POST | /api/saved-topics | Save a topic |
| DELETE | /api/saved-topics/{id} | Delete saved topic |
| GET | /api/history | Get search history |
| DELETE | /api/history | Clear history |

## Opportunity Score Formula

```
Score = Demand Weight + Trend Weight + Base(40) - Competition Weight

Demand:      High=40, Medium=25, Low=10
Trend:       trend_percent / 2 (capped -15 to +30)
Competition: Low=0, Medium=-10, High=-25
```

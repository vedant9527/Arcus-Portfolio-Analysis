# Arcus — AI Portfolio Analytics Platform

Institutional-grade portfolio risk analytics for retail investors. Ask questions about your portfolio in natural language and get quantitative answers in seconds.

🌐 **Live:** [arcus-insights.com](https://arcus-insights.com)

---

## What It Does

Retail investors don't have access to the risk analytics tools institutional investors use. Arcus closes that gap.

Describe your portfolio, ask a question, and get a full quantitative breakdown with plain-English interpretations — no Bloomberg terminal required.

| Analysis | What You Get |
|---|---|
| **Health Score (0–100)** | One number summarising portfolio quality |
| **Sharpe / Sortino Ratio** | Risk-adjusted return — are you rewarded for the risk you're taking? |
| **Beta vs S&P 500** | How much your portfolio amplifies market moves |
| **Value at Risk (95% / 99%)** | Worst expected daily loss under normal and tail conditions |
| **Max Drawdown** | Deepest peak-to-trough loss in your history |
| **Monte Carlo Simulation** | 300+ simulated future paths via Geometric Brownian Motion |
| **Efficient Frontier** | Your current vs optimal allocation on a risk-return map |
| **Stress Testing** | Estimated losses under 2008 Crisis, COVID Crash, Dot-Com Bust, custom scenarios |
| **Sector Analysis** | GICS sector breakdown with concentration warnings |
| **Correlation Heatmap** | Pairwise correlations — are your holdings actually diversified? |
| **AI Chat (Arcus AI)** | Ask anything about your portfolio in natural language |

---

## Architecture

The AI layer is built on the Anthropic API. A natural language query enters a classification layer, routes to the appropriate analysis module, retrieves live market data via yfinance, runs the calculation, and returns a grounded plain-language response.

```
User query
    └── LLM classification (20 categories)
            └── Analysis agent (metrics / monte carlo / optimizer / stress test / chat)
                    └── Data pipeline (yfinance → NumPy / Pandas / SciPy)
                            └── FastAPI response → Next.js frontend
```

---

## Tech Stack

**Backend**
- FastAPI — REST API with OpenAPI docs
- Python 3.11+ — Core analytics engine
- NumPy / Pandas — Numerical computation and data manipulation
- SciPy — Portfolio optimisation (SLSQP constrained minimiser)
- yfinance — Historical price data
- Anthropic API — LLM classification and AI chat

**Frontend**
- React 18 + TypeScript
- Vite — Build tooling
- Tailwind CSS — Utility-first styling
- Framer Motion — Animations
- Recharts — Interactive financial charts
- Shadcn/ui — Component library

**Infrastructure**
- FastAPI backend deployed on Render
- Frontend deployed on Vercel
- CI/CD via GitHub Actions

---

## Project Structure

```
Arcus/
├── backend/
│   ├── main.py                  # FastAPI entry point
│   ├── config.py                # Constants and demo portfolios
│   ├── analytics/
│   │   └── metrics.py           # Risk calculations and interpretations
│   ├── data/
│   │   └── fetcher.py           # yfinance data fetching and caching
│   ├── models/
│   │   ├── monte_carlo.py       # GBM simulation engine
│   │   └── optimizer.py         # Sharpe maximisation solver
│   └── routers/
│       ├── portfolio.py         # /api/portfolio/* endpoints
│       ├── chat.py              # AI chat endpoint
│       ├── news.py              # Live market news feed
│       └── adapter.py           # /api/v2/* adapter layer
├── frontend/
│   ├── src/
│   │   ├── pages/               # Onboarding, Dashboard, Results, Chat
│   │   ├── components/          # UI components and charts
│   │   └── lib/                 # API client, utilities
│   └── package.json
└── render.yaml
```

---

## Running Locally

**Prerequisites:** Python 3.11+, Node.js 18+, npm

```bash
# Clone
git clone https://github.com/vedant9527/Arcus-Portfolio-Analysis.git
cd Arcus-Portfolio-Analysis

# Backend
pip install -r requirements.txt
uvicorn backend.main:app --reload --port 8000

# Frontend (new terminal)
cd "Frontend final"
npm install
npm run dev
```

- Frontend: http://localhost:8080
- API docs: http://localhost:8000/docs

---

## Key API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/portfolio/analyze` | Full portfolio analysis |
| `POST` | `/api/portfolio/monte-carlo` | Monte Carlo simulation |
| `POST` | `/api/portfolio/efficient-frontier` | Efficient frontier computation |
| `POST` | `/api/portfolio/stress-test` | Historical stress test scenarios |
| `POST` | `/api/v2/chat` | AI chat conversation |
| `GET` | `/api/news/market` | Live market news feed |

---

## Disclaimer

Educational and demonstration purposes only. Not financial advice. Do your own research before making investment decisions.

---

Built by [Vedant Chawardol](https://vedantchawardolportfolio.netlify.app) · [arcus-insights.com](https://arcus-insights.com)

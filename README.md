# VentureLens: GPT-OSS-20B Startup Idea Analyzer

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![React](https://img.shields.io/badge/react-18+-blue.svg)](https://reactjs.org/)
[![TypeScript](https://img.shields.io/badge/typescript-5+-blue.svg)](https://www.typescriptlang.org/)

## Overview

VentureLens is an AI-powered startup idea analyzer that transforms raw business concepts into structured, evidence-backed insights for validation and strategic planning. Built as an academic semester project, this MVP leverages the power of open-source GPT-OSS-20B model to provide comprehensive startup analysis including market research, competitive intelligence, and revenue forecasting.

The platform serves as a comprehensive toolkit for entrepreneurs, students, and researchers looking to validate startup ideas with data-driven insights and structured business intelligence.

## Problem Statement

Aspiring entrepreneurs and students often struggle with:
- **Lack of structured approach** to validate startup ideas
- **Time-consuming market research** that requires multiple tools and data sources
- **Difficulty in competitive analysis** and positioning
- **Complex revenue modeling** without proper financial expertise
- **Fragmented workflow** across different platforms for business planning

VentureLens addresses these challenges by providing an integrated, AI-powered solution that delivers comprehensive startup analysis in minutes rather than weeks.

## Objectives

### Primary Objectives
- **Democratize startup validation** through accessible AI-powered analysis
- **Accelerate the ideation-to-validation pipeline** for entrepreneurs and students
- **Provide evidence-backed insights** rather than subjective opinions
- **Create a reproducible methodology** for startup idea evaluation

### Academic Objectives
- Demonstrate practical application of large language models in business intelligence
- Showcase integration of multiple technologies in a full-stack application
- Explore the potential of open-source AI models in specialized domains
- Contribute to the open-source ecosystem with educational resources

## Features

### 🔍 **Idea Generator**
- **Structured Output**: Generates comprehensive startup concepts with JSON formatting
- **Key Components**: Title, one-liner, problem statement, target customers, competitors, USP, and validation tests
- **Customizable Parameters**: Industry focus, market size, and innovation level

### 📊 **Market Snapshot**
- **Google Trends Integration**: Real-time sparkline charts showing search interest over time
- **Competitor Intelligence**: Automated web scraping for competitor information and positioning
- **Market Metrics**: TAM/SAM calculations and market opportunity sizing

### 📋 **Business Plan Outline**
- **Comprehensive Structure**: Executive summary, market analysis, business model, and operations
- **Monetization Strategies**: Multiple revenue stream suggestions with viability assessment
- **Go-to-Market Planning**: Channel strategy, customer acquisition, and marketing approach

### 🎯 **Competitor Opportunity Score**
- **Weighted Scoring System**: Multi-factor analysis including market gap, competitive landscape, and execution difficulty
- **Detailed Breakdown**: Transparent scoring methodology with explanations
- **Comparative Analysis**: Position your idea against existing solutions

### 💰 **Revenue Forecast Simulator**
- **Probabilistic Modeling**: P10/P50/P90 revenue projections with confidence intervals
- **Scenario Planning**: Best case, worst case, and most likely outcomes
- **Data Export**: CSV export functionality for further analysis and presentation

## Tech Stack

### Frontend
```
React 18+ with TypeScript
├── Vite (Build tool and dev server)
├── Tailwind CSS (Utility-first styling)
├── Chart.js / Recharts (Data visualization)
├── Axios (HTTP client)
└── React Router (Navigation)
```

### Backend
```
FastAPI (Python web framework)
├── Pydantic (Data validation)
├── SQLAlchemy (ORM)
├── Alembic (Database migrations)
└── Python-multipart (File uploads)
```

### AI/ML Infrastructure
```
Model Runtime:
├── vLLM (GPU acceleration)
└── llama.cpp (CPU fallback)

Model: openai/gpt-oss-20b
Embeddings: sentence-transformers/all-MiniLM-L6-v2
```

### Database & Storage
```
PostgreSQL 15+
└── pgvector (Vector similarity search)
```

### Background Processing
```
Redis (Message broker)
├── RQ (Python job queue)
└── Celery (Alternative task queue)
```

### Web Scraping & Data Collection
```
Playwright (Browser automation)
├── BeautifulSoup4 (HTML parsing)
├── Requests (HTTP requests)
└── Google Trends API integration
```

### DevOps & Deployment
```
Docker & Docker Compose
├── Multi-stage builds
├── Environment management
└── Production-ready configuration
```

### Data Flow Explanation

1. **Request Initiation**: User submits startup idea through React frontend
2. **API Processing**: FastAPI validates and routes requests to appropriate services
3. **AI Analysis**: Core services leverage GPT-OSS-20B for structured analysis
4. **Data Enrichment**: External APIs and web scraping enhance analysis with real-time data
5. **Vector Operations**: Embeddings enable semantic similarity search for competitor matching
6. **Background Processing**: Heavy computations handled asynchronously via Redis queues
7. **Response Assembly**: Results aggregated and returned as structured JSON
8. **Frontend Rendering**: React components visualize insights with interactive charts

## Installation

### Prerequisites

- **Python 3.11+**
- **Node.js 18+** 
- **Docker & Docker Compose**
- **PostgreSQL 15+** (or use Docker setup)
- **Redis** (or use Docker setup)
- **Git**

### Quick Start with Docker

```bash
# Clone the repository
git clone https://github.com/lucifer0906/VentureLens.git
cd VentureLens

# Start all services with Docker Compose
docker-compose up -d

# Wait for services to initialize (30-60 seconds)
# Access the application at http://localhost:3000
```

### Local Development Setup

#### 1. Backend Setup

```bash
# Navigate to backend directory
cd backend

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Set up environment variables
cp .env.example .env
# Edit .env with your configuration

# Initialize database
alembic upgrade head

# Download model weights (optional - will auto-download on first use)
python scripts/download_model.py

# Start the backend server
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

#### 2. Frontend Setup

```bash
# Navigate to frontend directory
cd frontend

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env.local
# Edit .env.local with your API endpoints

# Start development server
npm run dev
```

#### 3. Database Setup

```bash
# Using Docker (recommended)
docker run --name venturelens-postgres \
  -e POSTGRES_DB=venturelens \
  -e POSTGRES_USER=postgres \
  -e POSTGRES_PASSWORD=password \
  -p 5432:5432 \
  -d pgvector/pgvector:pg15

# Or install PostgreSQL with pgvector extension locally
```

#### 4. Redis Setup

```bash
# Using Docker (recommended)
docker run --name venturelens-redis \
  -p 6379:6379 \
  -d redis:7-alpine

# Start background worker
cd backend
python -m rq worker --url redis://localhost:6379
```

### Environment Configuration

Create `.env` file in the backend directory:

```env
# Database
DATABASE_URL=postgresql://postgres:password@localhost:5432/venturelens

# Redis
REDIS_URL=redis://localhost:6379

# AI Model Configuration
MODEL_NAME=openai/gpt-oss-20b
MODEL_RUNTIME=vllm  # or llama_cpp
DEVICE=cuda  # or cpu

# API Keys (optional)
GOOGLE_TRENDS_API_KEY=your_key_here

# Security
SECRET_KEY=your-secret-key-here
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30
```

## Usage

### Basic Workflow

1. **Access the Application**
   ```
   Open http://localhost:3000 in your browser
   ```

2. **Submit Startup Idea**
   - Enter your startup concept in the main input field
   - Select analysis depth (Quick, Standard, Comprehensive)
   - Click "Analyze Idea"

3. **Review Generated Insights**
   - Idea Generator results with structured breakdown
   - Market Snapshot with trends and competitor data
   - Business Plan Outline with monetization strategies
   - Competitor Opportunity Score with detailed metrics
   - Revenue Forecast with probabilistic projections

### API Usage Examples

#### Analyze Startup Idea

```bash
curl -X POST "http://localhost:8000/api/v1/analyze" \
  -H "Content-Type: application/json" \
  -d '{
    "idea": "AI-powered personal finance assistant for college students",
    "analysis_depth": "comprehensive",
    "target_market": "North America"
  }'
```

#### Get Market Snapshot

```bash
curl -X GET "http://localhost:8000/api/v1/market/snapshot?query=personal%20finance%20app&region=US"
```

#### Generate Revenue Forecast

```bash
curl -X POST "http://localhost:8000/api/v1/forecast/revenue" \
  -H "Content-Type: application/json" \
  -d '{
    "business_model": "freemium",
    "target_users": 10000,
    "avg_revenue_per_user": 5.99,
    "growth_rate": 0.15,
    "churn_rate": 0.05,
    "forecast_months": 24
  }'
```

### Python SDK Usage

```python
from venturelens import VentureLensClient

# Initialize client
client = VentureLensClient(api_url="http://localhost:8000")

# Analyze startup idea
result = client.analyze_idea(
    idea="AI-powered personal finance assistant for college students",
    analysis_depth="comprehensive"
)

# Access different analysis components
idea_breakdown = result.idea_generator
market_data = result.market_snapshot
business_plan = result.business_plan_outline
competitor_score = result.competitor_opportunity_score
revenue_forecast = result.revenue_forecast

# Export revenue forecast to CSV
revenue_forecast.export_csv("forecast_results.csv")
```

## Example Output

### Idea Generator Response

```json
{
  "title": "EduFinance AI",
  "one_liner": "AI-powered personal finance assistant specifically designed for college students' unique financial challenges",
  "problem": "College students struggle with managing limited budgets, understanding financial concepts, and building healthy money habits during a critical life stage",
  "target_customers": [
    "Undergraduate students (ages 18-22)",
    "Graduate students with limited income",
    "International students navigating US financial systems"
  ],
  "competitors": [
    {
      "name": "Mint",
      "positioning": "General-purpose budgeting app",
      "gap": "Not tailored for student-specific financial scenarios"
    }
  ],
  "usp": "Student-centric financial guidance with AI tutoring for financial literacy and campus-specific expense tracking",
  "quick_tests": [
    "Survey 100 students about current financial management pain points",
    "Create MVP with basic budgeting features and test with 20 beta users",
    "Partner with one university financial aid office for pilot program"
  ]
}
```

### Market Snapshot Response

```json
{
  "google_trends": {
    "search_term": "student budgeting app",
    "interest_over_time": [65, 72, 68, 74, 69, 71, 75],
    "related_queries": ["college budget app", "student finance tracker"],
    "growth_trend": "stable_with_seasonal_peaks"
  },
  "competitor_analysis": {
    "direct_competitors": 3,
    "indirect_competitors": 12,
    "market_saturation": "medium",
    "avg_competitor_rating": 3.8
  },
  "market_opportunity": {
    "tam": "$2.1B",
    "sam": "$340M", 
    "som": "$12M"
  }
}
```

### Revenue Forecast Output

```json
{
  "forecast_summary": {
    "p10_12m": "$24,000",
    "p50_12m": "$87,000", 
    "p90_12m": "$165,000",
    "p10_24m": "$95,000",
    "p50_24m": "$285,000",
    "p90_24m": "$510,000"
  },
  "key_assumptions": {
    "customer_acquisition_cost": "$12",
    "customer_lifetime_value": "$89",
    "monthly_churn_rate": "5%",
    "conversion_rate_free_to_paid": "8%"
  },
  "sensitivity_analysis": {
    "most_impactful_variables": [
      "User acquisition rate",
      "Conversion to premium",
      "Monthly churn rate"
    ]
  }
}
```

## Contributing

*This section is intentionally left empty as per project requirements. Contributions guidelines will be added in future iterations.*


## Disclaimer

### Academic and Educational Use

This project is developed as an **academic semester project** for educational purposes. While the analysis and insights generated by VentureLens can provide valuable guidance, please note the following:


### 🔬 Research Context

- **Open Source Model**: Uses GPT-OSS-20B, an open-source language model with inherent limitations
- **Data Dependencies**: Analysis quality depends on available web data and API limitations  
- **Experimental Nature**: This is a proof-of-concept implementation exploring AI applications in startup analysis


**Built with ❤️ for the open-source and academic communities**

*VentureLens - Transforming startup ideas into actionable insights through the power of open-source AI*

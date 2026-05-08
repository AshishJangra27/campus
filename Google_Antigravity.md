# Build a Location Intelligence ADK Agent with MCP Servers

> Build an AI-powered bakery intelligence agent using Google ADK, BigQuery, Google Maps, MCP, and Gemini 3.1 Pro.

---

# Introduction

This project demonstrates how to create a Location Intelligence Agent capable of combining:

- BigQuery analytics
- Google Maps intelligence
- MCP server integrations
- Gemini reasoning

The agent helps analyze bakery business opportunities using demographic data, foot traffic, competitor pricing, and location intelligence.

---

# Prerequisites

## Requirements

- Google Cloud Project
- Billing Enabled
- Web Browser
- Basic terminal knowledge

---

# 1. Setup Google Cloud

## Create or Select a Project

1. Open Google Cloud Console
2. Create or select a project
3. Enable billing

---

## Start Cloud Shell

Verify authentication:

```bash
gcloud auth list
```

Verify project:

```bash
gcloud config get project
```

Export project ID:

```bash
export PROJECT_ID=$(gcloud config get project)
```

---

# 2. Clone Repository

Clone repository:

```bash
git clone https://github.com/google/mcp.git
```

Navigate to project:

```bash
cd mcp/examples/launchmybakery
```

---

# 3. Authenticate

Authenticate with Google Cloud:

```bash
gcloud auth application-default login
```

> Re-authenticate if the session exceeds 60 minutes.

---

# 4. Configure Environment & BigQuery

## Run Environment Setup

```bash
chmod +x setup/setup_env.sh
./setup/setup_env.sh
```

This script:

- Enables APIs
- Creates `.env`
- Configures Maps API Key

---

## Setup BigQuery

```bash
chmod +x ./setup/setup_bigquery.sh
./setup/setup_bigquery.sh
```

This script creates:

- Cloud Storage bucket
- BigQuery dataset
- Required tables

---

## Created Dataset

Dataset: `mcp_bakery`

Tables:

- demographics
- bakery_prices
- sales_history_weekly
- foot_traffic

---

# 5. Install ADK

Create virtual environment:

```bash
python3 -m venv .venv
```

Activate environment:

```bash
source .venv/bin/activate
```

Install ADK:

```bash
pip install google-adk==1.28.0
```

Navigate to agent directory:

```bash
cd adk_agent/
```

---

# 6. Project Structure

```text
launchmybakery/
├── data/
├── adk_agent/
│   └── mcp_bakery_app/
│       ├── agent.py
│       ├── tools.py
│       └── .env
├── setup/
└── cleanup/
```

---

# 7. MCP Tool Configuration

## Maps MCP Toolset

Used for:

- Place search
- Competition analysis
- Route calculations
- Location intelligence

### Example

```python
def get_maps_mcp_toolset():
```

Uses:

- Maps API Key
- Streamable HTTP MCP connection

---

## BigQuery MCP Toolset

Used for:

- SQL execution
- Sales analytics
- Demographic analysis
- Forecasting

### Example

```python
def get_bigquery_mcp_toolset():
```

Uses:

- OAuth authentication
- BigQuery MCP server

---

# 8. Agent Definition

The agent uses Gemini 3.1 Pro.

### Example

```python
root_agent = LlmAgent(
    model='gemini-3.1-pro-preview'
)
```

Capabilities:

- BigQuery reasoning
- Maps reasoning
- Unified business intelligence

---

# 9. Run the Agent

Navigate to:

```bash
cd adk_agent/
```

Start ADK web server:

```bash
adk web --allow_origins 'regex:https://.*\.cloudshell\.dev'
```

Expected output:

```text
ADK Web Server started
http://127.0.0.1:8000
```

---

# 10. Open ADK UI

## Option 1

Open:

```text
http://127.0.0.1:8000
```

---

## Option 2

Use Cloud Shell Web Preview:

1. Click Web Preview
2. Change port
3. Enter `8000`

---

# 11. Example Prompts

## Market Discovery

```text
Find the zip code with the highest morning foot traffic score in Los Angeles.
```

---

## Competition Analysis

```text
Search for bakeries in that zip code to see if the market is saturated.
```

---

## Premium Pricing

```text
Find the maximum price for a Sourdough Loaf in the LA Metro area.
```

---

## Revenue Forecast

```text
Forecast December 2025 revenue using historical sales data.
```

---

## Logistics Validation

```text
Find the nearest Restaurant Depot and ensure drive time is under 30 minutes.
```

---

# 12. Cleanup

Run cleanup script:

```bash
chmod +x ../cleanup/cleanup_env.sh
./../cleanup/cleanup_env.sh
```

Removes:

- BigQuery datasets
- Cloud Storage buckets
- API keys

---

# 13. Key Learnings

- Infrastructure automation
- MCP integrations
- Multi-tool AI orchestration
- Location intelligence workflows
- Business reasoning with Gemini

---

# Technologies Used

- Google ADK
- Gemini 3.1 Pro
- MCP
- BigQuery
- Google Maps
- Python
- Cloud Shell

---

# Conclusion

You successfully built a Location Intelligence AI Agent capable of combining:

- Enterprise data analysis
- Real-world mapping intelligence
- Sales forecasting
- Competitive research

Powered by:

- MCP
- Gemini
- BigQuery
- Google Maps

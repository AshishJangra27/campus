# Build a Location Intelligence ADK Agent with MCP Servers

> Build an AI-powered bakery intelligence agent using Google ADK, BigQuery, Google Maps, MCP, and Gemini 3.1 Pro.

---

# Introduction

This project demonstrates how to create a Location Intelligence Agent capable of combining:

- BigQuery analytics
- Google Maps intelligence
- MCP server integrations
- Gemini reasoning

The agent helps analyze bakery business opportunities using:

- demographic data
- foot traffic analysis
- competitor pricing
- sales forecasting
- real-world location intelligence

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

### Screenshot

![Create Google Cloud Project](https://codelabs.developers.google.com/static/adk-mcp-bigquery-maps/img/a3dd2e6dddc8f691_1920.png)

---

# 2. Start Cloud Shell

Activate Cloud Shell from the top-right corner.

### Screenshot

![Activate Cloud Shell](https://codelabs.developers.google.com/static/adk-mcp-bigquery-maps/img/404e4cce0f23e5c5_1920.png)

---

## Verify Authentication

```bash
gcloud auth list
```

---

## Verify Active Project

```bash
gcloud config get project
```

---

## Export Project ID

```bash
export PROJECT_ID=$(gcloud config get project)
```

---

# 3. Clone Repository

Clone repository:

```bash
git clone https://github.com/google/mcp.git
```

Navigate to project:

```bash
cd mcp/examples/launchmybakery
```

---

# 4. Authenticate

Authenticate with Google Cloud:

```bash
gcloud auth application-default login
```

> Re-authenticate if the session exceeds 60 minutes.

---

# 5. Configure Environment & BigQuery

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

# 6. Verify Dataset in BigQuery

Open BigQuery Console:

```text
https://console.cloud.google.com/bigquery
```

Verify dataset:

```text
mcp_bakery
```

Tables created:

- demographics
- bakery_prices
- sales_history_weekly
- foot_traffic

### Screenshot

![Verify Dataset](https://codelabs.developers.google.com/static/adk-mcp-bigquery-maps/img/6bd0a0cd7522dd11_1920.jpeg)

---

# 7. Install ADK

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

# 8. Project Structure

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

# 9. MCP Tool Configuration

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

# 10. Agent Definition

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

# 11. Run the Agent

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

# 12. Open ADK UI

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

### Screenshot

![Change Port](https://codelabs.developers.google.com/static/adk-mcp-bigquery-maps/img/open_adk_ui_1920.png)

---

# 13. Interact with the Agent

Example prompt:

```text
Find the zip code with the highest morning foot traffic score in Los Angeles.
```

### Screenshot

![Interact with Agent](https://codelabs.developers.google.com/static/adk-mcp-bigquery-maps/img/5f2a48bebfc49709_1920.png)

---

# 14. More Example Prompts

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

# 15. Cleanup

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

# 16. Key Learnings

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

# Submission Requirements

Please share the following screenshots in your submission:


---

## 1. Interaction with Relevant Question

Ask the agent a relevant bakery/business intelligence question.

### Example

```text
Find the zip code with the highest morning foot traffic score in Los Angeles.
```

Capture:

- Your prompt
- Agent response
- Tool execution (if visible)

---

## 2. Interaction with Irrelevant Question

Ask the agent an unrelated or irrelevant question.

### Example

```text
What if I want to open it at the moon?
```

or

```text
Who won the football match yesterday?
```

Capture:

- Your prompt
- Agent response

This helps evaluate:

- Agent behavior
- Instruction following
- Response handling for irrelevant queries

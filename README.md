# Data Quality Reporting with Claude API

Automated data cleaning, NL-to-SQL, and report generation using Claude API with structured output, XML prompting, and multi-turn context.

## Overview

This project applies three core Claude API techniques to an HR Employee Attrition dataset (1,470 records, 35 features):

**Module 1 — Data Cleaning & Validation**
Sends raw CSV data with quality issues (typos, missing values, duplicates, invalid entries) to Claude. Uses assistant message prefilling and stop sequences to guarantee structured JSON output containing cleaned records and a list of every issue found.

**Module 2 — Natural Language to SQL**
Converts plain English questions into executable SQL queries. The table schema and user question are wrapped in XML tags (`<table_schema>`, `<question>`, `<rules>`) to give Claude clear structure. Prefilling with ` ```sql ` ensures only the SQL statement is returned.

**Module 3 — Automated Report Generation**
Sends the full dataset directly to Claude for analysis and report generation. A system prompt defines the analyst role and report structure. Multi-turn conversation first provides the data, then requests a focused analysis. Response streaming displays the report in real time as it generates.

## API Techniques

| Module            | Technique                              | Purpose                                          |
| ----------------- | -------------------------------------- | ------------------------------------------------ |
| Data Cleaning     | Prefill + Stop Sequences               | Force pure JSON output, no commentary            |
| NL to SQL         | XML Tag Structuring + Prefill          | Separate schema from question for accurate SQL   |
| Report Generation | System Prompt + Multi-turn + Streaming | Define role, maintain context, real-time display |

Additional parameters: `temperature=0` for deterministic output, `**kwargs` for flexible parameter forwarding, `max_tokens` for response length control.

## Dataset

IBM HR Analytics Employee Attrition & Performance from Kaggle.
Source: https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset

## Prerequisites

- Python 3.10+
- An Anthropic API key ([get one here](https://console.anthropic.com))

## Getting Started

1. Clone the repository:

```bash
git clone https://github.com/ZHLuo-Dev/data-quality-reporting-claude-api.git
cd data-quality-reporting-claude-api
```

2. Install dependencies:

```bash
pip install anthropic python-dotenv pandas
```

3. Create a `.env` file with your Anthropic API key:

```bash
cp .env.example .env
# Then edit .env and replace the placeholder with your real key
```

4. Open `claude_api_data_toolkit.ipynb` in VS Code or Jupyter Notebook and run all cells.

> **Note:** Running the full notebook requires an active Anthropic API key with available credits. You can obtain one at [console.anthropic.com](https://console.anthropic.com).

## Project Structure

```
data-quality-reporting-claude-api/
├── data_quality_reporting_claude_api.ipynb   # Main notebook with all three modules
├── HR-Employee-Attrition.csv       # Dataset (1,470 rows)
├── .env.example                    # Template for API key configuration
├── .gitignore
└── README.md
```

## Tech Stack

Python, Claude API (Anthropic SDK), Pandas

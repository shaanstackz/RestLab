# Apple Health Sleep Analysis

This project analyzes Apple Health sleep data exported from the Health app and builds a full pipeline around sleep trends, exercise correlations, anomaly detection, HRV/stress insights, and weekly report generation.  
It combines Python data processing, machine learning, and LLM-powered summaries to create meaningful sleep insights.

---

## Project Structure

```
Apple Health Sleep Analysis
│
├── data/
│   └── export.xml                     # Raw Apple Health export
│
├── notebooks/
│   ├── data/
│   ├── results/
│   │   ├── figures/                   # Charts and visual outputs
│   │   └── reports/                   # Markdown & PNG reports
│   │       ├── sleep_report_*.md
│   │       ├── weekly_report_*.md
│   │       └── weekly_sleep_*.png
│   ├── daily_sleep_summary.csv        # Cleaned daily metrics
│   ├── sleep_df.csv                   # Raw sleep stage data
│   ├── sleep_summary.csv              # Aggregated nightly metrics
│   ├── 01_sleep_study_analysis.ipynb
│   ├── 02_ai_sleep_model.ipynb
│   ├── 03_exercise_sleep_correlation.ipynb
│   ├── 04_anomaly_detection.ipynb
│   ├── 05_hrv_stress_analysis.ipynb
│   └── 06_weekly_sleep_report.ipynb
│
├── src/
│   ├── ai_sleep.py                    # LLM analysis utilities
│   ├── check_fine_tune.py             # Fine-tune status checker
│   ├── fine_tune_upload.py            # Prepares & uploads JSONL
│   ├── parse_apple_health.py          # Converts export.xml → CSVs
│   ├── sleep_analysis.py              # Core sleep calculations
│   ├── utils.py                       # Shared helpers
│   └── visualization.py               # Plotting functions
│
├── generate_jsonl.py                  # Builds fine-tuning dataset
├── .env                               # API keys + environment vars
└── .gitignore
```

---

## Features

### 1. Apple Health XML Parsing
Converts `export.xml` into structured CSV files.  
Extracts:
- Sleep stages
- Heart rate
- HRV
- Workouts
- Respiratory rate

---

### 2. Daily Sleep Summary
Pulls key nightly metrics:
- Total sleep duration  
- Deep / REM / Core sleep  
- Awakening duration  
- Average heart rate  
- HRV  
- Stress score (derived)  
- Bedtime / wake time estimates  

Notebook: `01_sleep_study_analysis.ipynb`

---

### 3. AI-Powered Sleep Modeling
RandomForest regression predicts nightly sleep duration using:
- Activity levels  
- Prior night’s sleep  
- Sleep debt  
- Heart rate  
- HRV  
- Bedtime consistency  
- Weekday patterns  

Notebook: `02_ai_sleep_model.ipynb`

---

### 4. Exercise–Sleep Correlation Analysis
Quantifies workout impact on sleep:
- Exercise minutes vs. sleep hours  
- Heart-rate-adjusted exertion  
- Correlation heatmaps  
- AI interpretation using a fine-tuned OpenAI model  

Notebook: `03_exercise_sleep_correlation.ipynb`

---

### 5. Sleep Anomaly Detection
Detects unusual nights based on:
- Rolling averages  
- Z-scores  
- Stage distribution shifts  
- Sudden changes in HR/HRV  

Outputs:
- Annotated charts  
- Markdown reports  

Notebook: `04_anomaly_detection.ipynb`

---

### 6. HRV & Stress Trend Analysis
Evaluates recovery and stress load:
- HRV patterns over time  
- Relationship with sleep stages  
- Stress score trends  
- AI-driven insights  

Notebook: `05_hrv_stress_analysis.ipynb`

---

### 7. Weekly Sleep Reports
Automatically generates:
- Weekly metrics overview  
- Stage breakdown  
- Best/worst nights  
- Recommendations  
- AI-written weekly summary  
- Markdown + PNG reports  

Notebook: `06_weekly_sleep_report.ipynb`

---

## AI & Fine-Tuning

Supports:
- Custom prompts for sleep coaching  
- Data-driven scientific explanations  
- Story-style summaries  
- Fine-tuned OpenAI models using personal sleep patterns  

Files:
- `ai_sleep.py`
- `fine_tune_upload.py`
- `generate_jsonl.py`

---

## Requirements

Install dependencies:

```bash
pip install -r requirements.txt
```

Environment variables:

```
OPENAI_API_KEY=your_key
GPT_MODEL=gpt-4o-mini  # or your fine-tuned model ID
```

---

## How to Run

1. Export your Apple Health data  
   - Health App → Profile → Export All Data  
2. Place `export.xml` in `data/`
3. Parse the raw export:

```bash
python src/parse_apple_health.py
```

4. Open the notebooks and run each analysis step.

---

## Reports

Generated reports appear in:

```
notebooks/results/reports/
```

Includes:
- Sleep report markdown  
- Weekly reports  
- Visual trend charts  

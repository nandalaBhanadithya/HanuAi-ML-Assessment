# HanuAi Machine Learning Assessment

This repository contains the complete implementation and deliverables for the HanuAi Machine Learning Assessment, covering two main tasks:
1. **Task 1: Web Scraping & Sentiment Analysis** (E-commerce Customer Reviews from BestBuy Canada)
2. **Task 2: Advanced EDA & Text Mining** (Automotive Infotainment Warranty Claims & Failure Clustering)

---

## Repository Structure

```text
├── task1_web_scraping_sentiment_analysis.ipynb   # Task 1 Jupyter Notebook
├── task1_scraped_reviews_sentiment.csv          # Task 1 Final Dataset (CSV)
├── task1_scraped_reviews_sentiment.xlsx         # Task 1 Final Dataset (Excel)
├── Task1_AntiScraping_and_Sentiment_Report.docx # Task 1 Written Report (Word)
├── Task1_AntiScraping_and_Sentiment_Report.pdf  # Task 1 Written Report (PDF)
│
├── task2_advanced_eda_text_mining.ipynb         # Task 2 Jupyter Notebook
├── task2_enriched_automotive_warranty.csv       # Task 2 Final Enriched Dataset (CSV)
├── task2_enriched_automotive_warranty.xlsx      # Task 2 Final Enriched Dataset (Excel)
├── Task2_Advanced_EDA_Text_Mining_Report.docx   # Task 2 Stakeholder Report (Word)
├── Task2_Advanced_EDA_Text_Mining_Report.pdf    # Task 2 Stakeholder Report (PDF)
├── Hanuai task2 assignment.csv                  # Raw Warranty Dataset (1,000 records)
│
├── eda_visualizations/                          # Generated High-Resolution Charts
│   ├── plant_distribution.png
│   ├── model_distribution.png
│   ├── time_to_failure_distribution.png
│   ├── issue_category_distribution.png
│   └── cluster_visualization.png
│
├── HanuAi ML Assignment.pdf                     # Original Assessment Guidelines
└── README.md
```

---

## Task 1: Web Scraping & Sentiment Analysis

- **Target Product**: Sony MDR-ZX110 Over-Ear Headphones (SKU: `10325154`) on BestBuy Canada.
- **Scraper Implementation**:
  - Handles client-side rendered dynamic data via BestBuy Canada's internal reviews API endpoint.
  - Implements pagination ("Show More" behavior) and sorting filters (`Lowest Rating`, `Highest Rating`, `Most Helpful`, `Newest`) to harvest a balanced review distribution.
  - Extracts mandatory fields: Primary Key, Title, Review Text, Date (`YYYY-MM-DD`), Rating (out of 5), Source, and Reviewer Name.
- **Sentiment & Aspect Categorization**:
  - Cleans and preprocesses text (HTML unescaping, normalization, title + body combination).
  - Employs calibrated VADER sentiment compound scoring (Positive, Negative, Neutral).
  - Categorizes reviews into functional aspect-based sentiment tags (e.g. `['Good Design & Build Quality (Pos)']`, `['Comfort & Ergonomics Concern (Neg)']`, `['Great Value & Affordability (Pos)']`).
- **Reports**:
  - Technical anti-scraping mitigation strategies (IP proxy rotation, request jitter, headers, stealth, exponential backoff).
  - Summary of satisfaction drivers, pain points, and actionable retail recommendations.

---

## Task 2: Advanced EDA & Text Mining

- **Dataset**: 1,000 warranty repair claims for 2020 Model Year vehicles across 4 automotive makes (`ThunderVolt`, `NovaSprint`, `NebulaCruiser`, `TurboFlux`).
- **Exploratory Data Analysis**:
  - Standardized datetimes and derived Time-to-Failure (`Days_In_Service` from vehicle in-use delivery to warranty claim submission, median 227 days).
  - Identified claim concentration across manufacturing assembly plants (Flint, Fort Wayne, and Silao account for 70.9% of claims).
- **Text Mining & Entity Extraction**:
  - The raw dataset contained pre-filled tags for only the first 5 seed records. Using these seed records as a reference ontology, we parsed the unstructured technical verbatims (`CUSTOMER_VERBATIM`, `CAUSAL_VERBATIM`, `CORRECTION_VERBATIM`) to extract structured entity lists across all 1,000 rows:
    - `Trigger`
    - `Failure Component`
    - `Failure Condition`
    - `Additional Context`
    - `Fix Component`
    - `Fix Condition`
  - Grouped claims into high-level issue categories (Internal Hardware Failure, Software/Firmware Glitches, Wiring & Physical Connections, External Connectivity, Power Management).
- **Unsupervised Clustering**:
  - TF-IDF n-gram vectorization and K-Means clustering ($k=5$) to isolate failure groups (Black Screen Inoperative Modules, Reverse Camera Video Loss & Coax Faults, Firmware Update Failures & TAC Calls, SiriusXM Signal Dropout, and Navigation SD Card Hub Errors).
- **Stakeholder Synthesis**:
  - Actionable points targeting root causes (coax resistance testing, dual-bank A/B bootloaders for OTA updates, assembly inspection at Flint/Fort Wayne) to reduce warranty claims and improve First-Time Fix Rates.

---

## Requirements & Setup

To run the notebooks locally, install dependencies via `pip`:

```bash
pip install pandas numpy scikit-learn matplotlib seaborn requests beautifulsoup4 vaderSentiment python-docx reportlab openpyxl
```

Launch Jupyter Lab or Notebook:
```bash
jupyter notebook
```

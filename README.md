# ☕ Cafe Sales — Data Analysis & Power BI Dashboard

End-to-end analytics project on a coffee-shop point-of-sale dataset: raw data cleaning, exploratory analysis, business-question answering, and an interactive Power BI dashboard.

## Project Files

| File | Description |
|---|---|
| `dirty_cafe_sales.csv` | Raw, uncleaned export (10,000 transactions, 8 columns) with missing values and corrupted `"UNKNOWN"` / `"ERROR"` placeholders |
| `dirtycafe.ipynb` | Jupyter notebook containing the full cleaning pipeline |
| `clean_cafe_sales.csv` | Cleaned dataset (9,540 transactions, 12 columns) used for all analysis and the dashboard |
| `cafe_sales_analysis_EN.ipynb` | EDA notebook answering 10 business questions with charts |
| `cafe_sales_powerbi_model.xlsx` | Excel data model with live formulas, KPI cards, charts, and a Power BI import guide |
| `Data_Analysis_Project.docx` | Full written project report (data overview, cleaning steps, findings, recommendations) |
| **`Dashboard.pbix`** | **Power BI Desktop dashboard** (this file, currently zipped as `Dashboard_pbix.zip`) |

> To open the dashboard: unzip `Dashboard_pbix.zip` and rename the extracted file's extension from nothing/`.zip` back to **`.pbix`**, then open it in Power BI Desktop.

## Data Source & Pipeline

The raw dataset simulates a messy POS export for a cafe's 2023 sales. It was cleaned in `dirtycafe.ipynb` by:
1. Converting literal `"UNKNOWN"` / `"ERROR"` placeholders to true nulls
2. Fixing data types (numeric fields, transaction date)
3. Recomputing missing `Total Spent` as `Quantity × Price Per Unit`
4. Dropping the 460 rows with an unrecoverable date
5. Cross-inferring missing `Item` / `Price Per Unit` from the cafe's fixed price list
6. Labeling remaining gaps in `Item`, `Payment Method`, and `Location` as `"Unknown"` (kept, not dropped, to preserve revenue data)
7. Engineering `Year`, `Month`, `Month Name`, and `Day of Week` for time-based analysis

Full details and exact before/after numbers are in `Data_Analysis_Project.docx`.

## Dashboard Contents

The dashboard connects to the `clean_cafe_sales` table and has one page with 8 visuals:

**KPI Cards**
- Number of Sales
- Average Total Spent

**Charts**
| Visual | Type | Shows |
|---|---|---|
| Sales by Month | Pie chart | Share of transactions per month |
| Sales by Payment Method | 100% stacked bar | Payment-method mix over the year |
| Orders in Month | Column chart | Transaction count by month |
| Quantity Sale by Item | Stacked area chart | Units sold per item over time |
| Sales by Item | Clustered column chart | Transaction count by item |
| Transaction Detail Table | Table | Transaction ID, Item, Price Per Unit, Quantity, Total Spent, Location, Payment Method |
| Transaction Search | Text slicer | Free-text lookup by Transaction ID |

## Key Insights

- Revenue is led by **Salad, Sandwich, and Smoothie**; **Coffee** and **Cookie** sell the highest volumes but at low unit prices, so they contribute less revenue.
- No meaningful difference in sales across **In-store vs. Takeaway**, **payment method**, **month**, or **day of week** — the dataset shows a largely flat, uniform pattern.
- **60%+ of transactions** have an `"Unknown"` value in at least one field (mostly `Payment Method` and `Location`), so any channel/payment breakdown should be read with caution — see `Data_Analysis_Project.docx` for the full data-quality discussion and recommendations.

## Requirements

- Power BI Desktop (this file was created from a version compatible with the 2026.04 release train)
- No external data connections — the dataset is embedded in the file, so it opens and refreshes with no setup

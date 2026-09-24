# 🛒 Walmart Retail Sales Analytics Engine (NumPy)

An end-to-end sales analytics pipeline built with **pure NumPy** (no pandas
for the core analysis) — processing 421,570+ weekly sales records across 45
Walmart stores to uncover revenue trends, flag statistical anomalies, and
build a simple demand forecast.

---

## 📌 Problem Statement

Simulates the workflow of a retail data analyst asked to answer:
*"How is the business performing, are there any red flags in the data, and
what can we expect next month?"*

The project deliberately avoids pandas for the analysis logic to demonstrate
fluency with NumPy fundamentals — vectorized operations, boolean masking,
structured arrays, and statistical computation — the foundations pandas
itself is built on.

---

## 🗂️ Data

**Source:** [Walmart Recruiting - Store Sales Forecasting](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting) (Kaggle)

| File | Rows | Description |
|---|---|---|
| `train.csv` | 421,570 | Weekly sales by Store, Department, Date |
| `features.csv` | 8,190 | Temperature, Fuel Price, CPI, Unemployment, Markdowns, Holiday flag |
| `stores.csv` | 45 | Store Type (A/B/C) and Size |

All three files were merged on `Store` (and `Date` for features) into a
single structured NumPy array for analysis.

---

## 🛠️ Approach

1. **Load** — read all three CSVs with `np.genfromtxt` into structured arrays
2. **Clean** — checked for missing values (none found) and validated data
   integrity (found 1,285 rows with negative sales — retained, as they
   reflect real returns exceeding purchases that week)
3. **Merge** — combined sales, store, and economic data using dictionary
   lookups keyed on `Store` and `Date`
4. **Aggregate** — computed total revenue by store, department, and month
   using boolean masking and vectorized sums
5. **Rank** — identified top/bottom performing stores and departments
6. **Detect anomalies** — flagged unusually high/low sales weeks using a
   z-score threshold (±3 standard deviations)
7. **Forecast** — built a simple 4-week moving average using `np.convolve`
8. **Visualize** — plotted trends, rankings, and anomalies with matplotlib

---

## 📊 Key Findings

- **Total revenue** across all stores/departments: **$6.65B+** over 143 weeks (2010–2012)
- **Top-performing store:** Store 20 — **$301.4M** in total revenue
- **Lowest-performing store:** Store 33 — **$37.2M** — an **8x gap** between
  highest and lowest store, suggesting store size/location strongly
  influences revenue
- **Seasonality:** Revenue consistently peaks mid-year (April, July) and
  dips in January/November within the dataset window, with holiday weeks
  (Thanksgiving, Christmas) showing sharp individual spikes
- **Anomalies:** **8,848 weeks (2.10% of all records)** were flagged as
  statistical outliers (±3 std dev from the mean). Most high-anomaly weeks
  cluster around Christmas (Dec 17–24), consistent with expected holiday
  demand rather than data errors — while low-anomaly weeks are candidates
  for further investigation (potential stockouts or store closures)
- **Forecast:** A 4-week moving average projected next week's company-wide
  sales at approximately **$46.1M**, based on recent trend data

---

## 📈 Visualizations



---

## 🚀 How to Run

```bash
git clone <your-repo-url>
cd walmart-sales-analytics
pip install -r requirements.txt
jupyter notebook notebooks/analysis.ipynb
```

Or open directly in Google Colab and upload the `data/` files.

---

## 🧰 Tech Stack

- **NumPy** — core data loading, cleaning, aggregation, and statistical analysis
- **Matplotlib** — visualization
- **Jupyter / Google Colab** — development environment

---

## 📁 Project Structure

```
walmart-sales-analytics/
├── data/                  # raw CSVs (train, features, stores)
├── notebooks/
│   └── analysis.ipynb     # full analysis notebook
├── images/                # saved chart exports
├── README.md
└── requirements.txt
```

---

## 💡 What This Project Demonstrates

- Working with large, real-world, messy datasets (400K+ rows)
- Merging multiple data sources without high-level libraries
- Core NumPy techniques: structured arrays, boolean masking, vectorized
  aggregation, `np.convolve` for time-series smoothing
- Statistical anomaly detection (z-score method)
- Translating raw analysis into a clear, business-readable summary


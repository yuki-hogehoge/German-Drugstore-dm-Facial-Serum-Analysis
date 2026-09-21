# 🧪 German Drugstore (dm) Facial Serum Analysis
> **Scraping, Cleaning, and Analyzing Facial Serums from dm-drogerie markt: Price, Customer Ratings, and Active Ingredient Matrix**

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Zenn](https://img.shields.io/badge/Article-Zenn-blue)](https://zenn.dev/yuki_hogehoge/articles/98cff955fbba69) 

This repository contains an end-to-end data analysis project focusing on facial serums from Germany's leading drugstore chain, **dm (dm-drogerie markt)**. The workflow covers web scraping, missing value imputation, domain-specific text parsing (extracting skin concerns and active ingredients), and exploratory data analysis (EDA).

📖 **Detailed Analysis Article (Japanese)**: [Zennの記事を読む](https://zenn.dev/yuki_hogehoge/articles/98cff955fbba69)

---

## 📌 Project Overview

* **Goal**: Evaluate market structure, price-to-performance ratio, and active ingredient trends across private label (PL) brands (e.g., *Balea*) and national brands (NB) (e.g., *L'Oréal Paris*, *NIVEA*, *Garnier*).
* **Dataset & Sampling**:
  * **Raw Dataset**: 179 facial serum products collected from `dm.de` (Data collected: August 2026).
  * **Focused Analysis Sample ($N=30$)**: To filter out noisy long-tail SKUs with negligible ratings, EDA was conducted on the **top 30 products sorted by review count**.
* **Key Methodologies**:
  * **Data Compliance & Cleaning**: Adhered to site rules (`robots.txt`), sanitized raw inputs, and calculated normalized prices per 100ml (€).
  * **Feature Engineering**: Rule-based boolean flagging for skin concerns (`anti-aging`, `dark_spots`, `dry`, `sensitive`, etc.) using German keywords and active ingredient normalization.
  * **Exploratory Data Analysis (EDA)**: Correlation analysis, scatter plots, and box plots comparing brand types and ingredient matrices.

---

## 🛡️ Data Governance & Compliance

To respect database rights, intellectual property, and site terms of service:
* **No Raw Text Distribution**: The unedited scraped dataset containing long-form German product descriptions is excluded from this public repository.
* **Published Dataset**: Only processed product IDs, calculated price metrics, and engineered feature flags (`skincare_dataset_dm_serum_top30.csv`) are made publicly available.
* **Crawl Politeness**: Data retrieval was executed with minimum 2-second delays between requests, avoiding prohibited paths as specified in `dm.de`'s `robots.txt`.

---

## 📊 Key Findings & Methodological Limitations

> ⚠️ **Note on Sample Size ($N=30$)**: The findings below are based on a small sample of the 30 most-reviewed products, introducing selection bias toward popular SKUs. These observations should be interpreted as **hypotheses and preliminary insights** rather than definitive market-wide conclusions.

1. **Private Label (PL) vs. National Brand (NB) Price Structure**:
   * **Private Labels (*Balea*, *alverde*)**: Strongly compressed in the ultra-low price range (€10–€20 / 100ml), prioritizing affordability. Customer ratings in this top-30 sample centered around a median of **4.1 Stars**.
   * **National Brands (*L'Oréal*, *NIVEA*)**: Span a broader price spectrum with a higher rating median of **4.6 Stars**, suggesting potential differences in consumer expectations or target formulation efficacy.
2. **High-Rating Segment Tendencies**:
   * Among products rated ★4.6 or higher in the sample, National Brands accounted for the vast majority, hinting at strong consumer satisfaction with established brands in high-performance skincare.
3. **Core Skin Concern Focus**:
   * Keyword detection indicated that approximately **70% of the sample** targets **Anti-Aging / Wrinkle Reduction**, marking it as a highly competitive segment alongside **Dark Spots / Brightening** (Niacinamide, Vitamin C, Retinol).

---

## 📸 Visualizations

### 1. Price per 100ml (€) vs. Rating (Stars) Scatter Plot
![Price vs Rating Scatter Plot](images/dm_serum_scatter_plot.png)

### 2. Brand Category Distribution & Rating Comparison (Box Plot)
![PB vs NB Boxplot](images/dm_serum_boxplot.png)

---

## 🛠 Tech Stack

* **Language**: Python 3.10+
* **Environment**: Google Colab / Jupyter Notebook
* **Libraries**:
  * **Data Wrangling**: `pandas`, `numpy`
  * **Visualization**: `matplotlib`, `seaborn`
  * **Text Processing & Parsing**: `re` (Regular Expressions)

---

## 📁 Repository Structure

```text
dm-skincare-serum-analysis/
├── README.md                                # Project documentation (this file)
├── data/
│   └── skincare_dataset_dm_serum_top30.csv  # Feature-engineered dataset (N=30, raw texts omitted for compliance)
├── notebooks/
│   └── dm_serum_analysis.ipynb              # Main Jupyter Notebook (EDA & Plotting)
└── images/
    ├── dm_serum_scatter_plot.png            # Generated scatter plot
    └── dm_serum_boxplot.png                 # Generated box plot

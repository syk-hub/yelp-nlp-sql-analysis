# yelp-nlp-sql-analysis
Exploratory analysis of Yelp reviews using SQL joins, NLP, and visualization.
# Yelp NLP + SQL Analysis

## Overview
This project explores the **Yelp Academic Dataset** to uncover patterns in business reviews and ratings.  
It combines:
- **Structured analysis** (SQL joins, aggregations)
- **Exploratory data analysis** (visualizations, correlations)
- **Basic NLP** (review text cleaning and sentiment scoring)

The goal is to demonstrate end-to-end data handling:  
📊 SQL-style joins → 🐼 Pandas transformations → 📈 Visual storytelling.

---

## Dataset
- Source: [Yelp Open Dataset](https://www.yelp.com/dataset) (~8GB JSON files).  
- For reproducibility, this repo includes **sample datasets** (`business_sample.csv`, `review_sample.csv`).  
- The full dataset was used for original analysis, but is too large to host on GitHub.  
- Results may differ slightly between the sample and the full dataset.

---

## Methods
1. **Data Preparation**
   - Loaded business and review tables.
   - Cleaned columns, derived flags (e.g., Urban vs. Non-Urban).
   - Created a *Predicted vs. Actual Stars (PAS)* metric.

2. **SQL Joins via SQLite**
   - Demonstrated joins between business and reviews.
   - Queried aggregated stats (average stars, review counts).

3. **Analysis**
   - Explored relationships between review count and star rating.
   - Compared ratings across urban vs. non-urban businesses.
   - Identified “hidden gems” outperforming expectations.

4. **Visualization**
   - Boxplots, scatter plots with fitted lines.
   - Ranked bar chart of top businesses by PAS.

---

## Results

### Stars by Urban vs. Non-Urban
![Urban vs Non-Urban](images/stars_by_urban.png)

### Stars vs. Review Count
![Stars vs Review Count](images/stars_vs_review_count.png)

### Hidden Gems by PAS
![Hidden Gems](images/hidden_gems.png)

---

## How to Run
1. Clone this repo:
   ```bash
   git clone https://github.com/your-username/yelp-nlp-sql-analysis.git
   cd yelp-nlp-sql-analysis


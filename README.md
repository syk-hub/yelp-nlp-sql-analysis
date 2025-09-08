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

# Yelp SQL Capstone Project

This project demonstrates loading and analyzing the [Yelp Academic Dataset](https://www.yelp.com/dataset) with PostgreSQL and Python.

## Full Results
Using the full dataset provided by Yelp:
- Businesses loaded: **150,346**
- Coffee & Tea businesses: **6,704**
- Reviews loaded: **X,XXX,XXX** (insert your real number here)

All analysis and insights in the notebook are based on the full dataset.

## Sample Data (for demonstration)
Because the full Yelp dataset is very large (GBs), this repo includes two small CSV files:
- `sample_business.csv` (100 businesses)
- `sample_review.csv` (≈300 reviews)

These samples allow anyone to:
- Load the data into PostgreSQL
- Run through the notebook without needing the full dataset
- Validate that the pipeline (ETL, table creation, queries) works correctly

⚠️ Note: The sample data is not representative. Counts and results will differ from the full dataset.

## How to Reproduce
1. Clone this repo
2. Install requirements
3. Run the notebook with the sample CSVs **or** download the full Yelp dataset and update the file paths.


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


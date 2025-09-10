# Yelp Coffee & Tea Analysis (with NLP)

This project explores the Yelp Academic Dataset for **Coffee & Tea** businesses, combining SQL + Python with **NLP** on reviews to understand what drives customer satisfaction and visibility.

## Dataset & Pipeline
- **Source**: [Yelp Academic Dataset](https://www.yelp.com/dataset)  
- **Scope**: Coffee & Tea businesses + their reviews  
- **Stack**: Jupyter, PostgreSQL, SQLAlchemy, pandas, scikit-learn (TF-IDF)  
- **ETL**: JSON → Postgres raw tables → reduced/cleaned tables → analysis & NLP

## Final Sample Sizes (Full Dataset)
- **Businesses**: 150,346 total → **6,704** Coffee & Tea  
- **Reviews (Coffee & Tea)**: **442,356** (from 6,990,280 total reviews)

> The repo also ships with **small sample CSVs** so anyone can run the pipeline without downloading the full dataset. Results from the sample will differ from the full data.

---

## Hypotheses & Outcomes (Summary)
1) **Popularity vs. Rating** — More reviews do **not** depress ratings; if anything, shops with more reviews have **slightly higher** ratings (modest positive correlation).  
2) **Urban vs. Non-Urban** — Urban shops show **higher ratings** and **more reviews** on average.  
3) **Amenities/Price vs. Rating** — Amenities (Wi-Fi, outdoor seating, etc.) have **weak** relationships with ratings; price level alone is not a strong predictor.

**Takeaway**: Reputation is driven less by amenity checklists and more by **experience/operations** (what happens during the visit), which the **text** of reviews makes very clear.

---

## NLP: Methods & Findings

### What We Did
- **Preprocessing**: lowercasing, punctuation removal, stop-word removal, optional lemmatization.
- **Vectorization**: **TF-IDF** on unigrams and bigrams (n-gram range (1,2)), min-df to filter rare noise.
- **Labeling**: Split reviews into **positive (≥4★)** vs **negative (≤2★)** buckets for contrastive term mining.  
- **Inspection**: Top TF-IDF terms per bucket; simple frequency checks for operational terms (e.g., *order, time, minutes, drive-thru*).

### What We Found
- **Positive reviews** frequently emphasize **taste & hospitality**:  
  *coffee, espresso, latte, delicious, love, favorite, friendly, staff, cozy, ambiance, breakfast, pastry*
- **Negative reviews** center on **operational friction**:  
  *order, time, minutes, wait, line, drive, drive-thru, mobile, wrong, cold, manager, rude*
- **Interpretation**:  
  - High ratings cluster around **product quality** and **staff warmth**.  
  - Low ratings are dominated by **speed/accuracy** failures and **queue management**.  
  - This aligns with the hypothesis results: **operations** are the highest-leverage lever.

### Why TF-IDF (and not just counts)?
TF-IDF down-weights ubiquitous words and surfaces **distinctive** terms within each rating bucket, making contrasts clearer (e.g., “minutes” or “drive-thru” punch above their raw frequency in low-rating reviews).

### Practical Metrics (Prototypes)
- **Friction Index**: share of tokens from an ops-friction dictionary (*order, wait, minutes, wrong, cold, refund, drive-thru*) — track over time/by location.  
- **PAS (Price- & Attention-Adjusted Satisfaction)**: deviation of actual stars from a baseline predicted by review count + price band — highlights “overperformers.”

### Limitations
- TF-IDF is **bag-of-words**: no context, sarcasm, or negation handling.  
- Rating buckets simplify a continuum; future work can model per-sentence sentiment or aspects (service, taste, price).

### How to Extend (Ideas)
- **Aspect-based sentiment** (service vs. taste vs. ambiance) using weak supervision or rule-based patterns.  
- **Topic modeling** (LDA or BERTopic) for themes beyond ops vs. taste.  
- **Transformer sentiment** (e.g., distilBERT) to capture context/negation.  
- **Queue-time signals**: build richer “Friction Index” with bigrams (*long wait, wrong order, mobile order*).

---

## Real Results (Full Dataset)
- **Businesses**: **6,704** Coffee & Tea  
- **Reviews**: **442,356**  
- **Key insights**: modest positive popularity–rating correlation; urban advantage; amenities weak; **NLP shows operations (speed/accuracy) drive dissatisfaction**, while **taste & friendliness** drive praise.

---

## Sample Data in This Repo
To keep the repo lightweight, we include:
- `sample_business.csv` (≈100 rows)
- `sample_review.csv` (≈300 rows)

- Sample data (100 businesses, 300 reviews) is stored in data/raw_data/ 
and regenerates automatically from the SQL script in notebooks/.


These demonstrate the **pipeline** (ETL → SQL → analysis/NLP).  
Counts and charts will **not** match the full dataset.

---

## Reproduce Locally
1. **PostgreSQL** running locally.  
2. `pip install -r requirements.txt`  
3. Open the notebook; it will prompt for your DB password (no secrets in code).  
4. Run with the sample CSVs **or** download the full Yelp dataset and point paths to the JSON files.

---

## Requirements
Python 3.x • PostgreSQL  
`sqlalchemy`, `psycopg2-binary`, `pandas`, `tqdm`, `scikit-learn`, `numpy`, `matplotlib` (and optionally `nltk` for lemmatization/stopwords).

---

## Repo Structure (suggested)
```
.
yelp-coffee-tea/
├─ README.md
├─ requirements.txt
├─ notebooks/
│  ├─ 04_analysis_yelp_clean.ipynb
│  └─ make_samples.ipynb        ← (optional helper, see #3)
├─ data/
│  ├─ samples/                  ← generated here (CSV outputs)
│  └─ raw/                      ← (optional) where full Yelp JSONs live (not committed)
└─ scripts/
   └─ make_samples.py           ← (optional CLI; same logic as the notebook cell)

```

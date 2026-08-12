# Netflix Content Catalog Analysis

## Business Problem
Streaming platforms compete on the breadth and relevance of their content library. This project analyzes Netflix's catalog metadata to understand **what kind of content Netflix has, where it comes from, who makes it, and how the library has grown over time** — insights that can inform content acquisition strategy, regional investment decisions, and catalog gap analysis.

## About the Data
- **Source:** [Netflix Titles dataset — Kaggle](https://www.kaggle.com/datasets/mozartcnx/netflix-titles/code)
- **Size:** 6,234 rows × 12 columns
- **Content:** Title-level metadata including type (Movie/TV Show), director, cast, country, date added, release year, content rating, duration, genre (`listed_in`), and description.

## Data Cleaning
- Dropped the `cast` column (high cardinality, not central to the analysis).
- Filled missing `date_added` with the mode and parsed it into a proper datetime; derived a new `year_added` column from it.
- Filled missing `rating` values using the mode **within each content type** (Movie vs TV Show), rather than a single global mode.
- Filled missing `director` values with `"NA"` as a placeholder.
- Checked for duplicate rows — none found.
- Extracted numeric `duration_min` from the `duration` text field (e.g. "90 min") for movies.
- `country` was left with some missing values (476), since imputing a country is not reliable.

## Analysis & Key Results
- **Content mix:** Movies (4,265) significantly outnumber TV Shows (1,969) in the catalog.
- **Top content-producing countries:** United States leads by a wide margin, followed by India and the United Kingdom.
- **Ratings:** TV-MA is the most common content rating, followed by TV-14 — indicating the catalog skews toward mature and teen audiences.
- **Genres:** International Movies, Dramas, and Comedies are the most frequent genres.
- **Catalog growth:** The number of titles added grew sharply over the years, peaking around 2019.
- **Movie duration:** Most movies run 90–100 minutes; the longest movie in the dataset is 312 minutes.
- **Top directors:** Jan Suter (21 titles), Raúl Campos, and Jay Karas contributed the most titles.
- **Correlation:** `show_id`, `release_year`, `year_added`, and `duration_min` all show weak correlations with each other — no meaningful linear relationships among the numeric fields.

## Next Steps
- Combine `country` and `listed_in` (genre) to find region-specific genre gaps or strengths.
- Analyze content rating trends over `year_added` to see if Netflix's content mix has skewed more mature over time.
- Build a genre/keyword-based content recommendation or similarity model using `description` and `listed_in`.
- Investigate the drop in titles added after 2019 (2020 shows a sharp decline) — likely a data cutoff, worth confirming.
- Cross-reference top directors/countries with subscriber growth or engagement data (if available) to link catalog composition to business outcomes.

## Problems Faced
- **High missingness in key fields:** `director` (1,969 missing), `cast` (570 missing), and `country` (476 missing) required different strategies — placeholder values, dropping the column, or leaving as-is — since imputing creative/production credits isn't meaningful.
- **Inconsistent date formats:** `date_added` required `format='mixed'` parsing to handle inconsistent date string formats in the source file.
- **Rating imputation nuance:** a naive global mode fill for `rating` would have been misleading, since Movies and TV Shows have different typical ratings — this required a groupby-based fill instead.
- **Multi-valued fields:** `country`, `listed_in`, and `director` often contain comma-separated multiple values in a single cell, requiring `str.split().explode()` to analyze correctly rather than treating each cell as one category.
- **Weak correlations:** none of the numeric fields correlated meaningfully with each other, limiting how far a purely statistical (non-text) analysis could go.

## Tools Used
Python, pandas, Matplotlib, Seaborn (Jupyter Notebook)

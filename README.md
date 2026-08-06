# Netflix Content Analysis (Python)

An exploratory data analysis (EDA) of Netflix's content library — cleaning raw data, engineering features, and visualizing patterns across content type, country, genre, ratings, and release trends.

## Dataset

`netflix_titles.csv` — from [Netflix Movies and TV Shows on Kaggle](https://www.kaggle.com/datasets/mozartcnx/netflix-titles/code).

*(Not included in this repo — download the CSV from Kaggle and place it in the same folder as the notebook before running.)*

## Workflow

### 1. Data Preparation & Cleaning
- Inspected structure, size, and null counts (`.info()`, `.isnull().sum()`, `.nunique()`)
- Dropped the low-value `cast` column
- Imputed missing `date_added` with the mode, then parsed it to a proper datetime
- Imputed missing `rating` using the mode **within each content type** (Movie vs TV Show), rather than a single global mode
- Filled missing `director` values with a placeholder
- Checked for and confirmed no duplicate rows

### 2. Feature Engineering
- Extracted `year_added` from the parsed date
- Parsed numeric `duration_min` out of the text duration field using regex (for movies)

### 3. Exploratory Analysis & Visualization
- **Content type split** — Movies vs TV Shows (pie chart)
- **Top contributing countries** — top 15 by title count (horizontal bar chart)
- **Content ratings distribution** — most common ratings across the library
- **Top genres** — top 10 genres by frequency
- **Titles added per year** — trend line over time
- **Movie duration distribution** — histogram
- **Top directors** — top 10 by number of titles
- **Correlation analysis** — pairplot and heatmap across numeric fields (`release_year`, `year_added`, `duration_min`)

## Key Findings

- Movies significantly outnumber TV Shows in Netflix's library.
- The United States contributes the most titles, followed by India — the top two content-producing countries.
- TV-MA is the most common content rating, followed by TV-14, indicating the platform skews toward mature and teen audiences.
- Numeric fields (release year, year added, duration) show weak-to-no linear correlation with each other.

## Tools & Libraries

- **pandas** — data cleaning, transformation, feature engineering
- **matplotlib** — pie, bar, line, and histogram charts
- **seaborn** — pairplot and correlation heatmap

## File

- `netflix_data_analysis.ipynb` — full notebook, from data cleaning through EDA to conclusions.

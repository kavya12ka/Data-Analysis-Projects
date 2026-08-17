# Netflix Content Catalog Analysis
### Understanding What Netflix Streams, Where It Comes From, and Who It's Made For

## 📌 Business Question

Netflix's catalog spans thousands of titles across countries, genres, and ratings — but what does that library actually look like at a glance? This project explores **the composition of Netflix's content catalog: content type mix, top contributing countries, rating/audience skew, genre distribution, and how the library has grown over time**, to help understand Netflix's content strategy and identify gaps or opportunities in the catalog.

## 🎯 Business Problem

- Content and acquisition teams need a clear picture of what's already in the catalog — by type, country, genre, and rating — to plan future acquisitions and originals strategically
- Without this view, it's hard to tell whether the catalog is over-indexed on certain content types, countries, or audience ratings
- Understanding catalog growth over time helps contextualize investment trends and platform expansion

## 📂 Data Source

- **netflix_titles.csv** — a public Netflix catalog dataset sourced from [Kaggle](https://www.kaggle.com/datasets/mozartcnx/netflix-titles/code)
- Contains title-level metadata: type (Movie/TV Show), title, director, cast, country, date added, release year, rating, duration, genres (`listed_in`), and description

## 🧹 Data Cleaning

- Reviewed null counts and unique value counts across all columns before cleaning, and worked on a copy of the original DataFrame
- Dropped the `cast` column — not needed for the catalog-level analysis being performed
- Filled missing `date_added` values with the column's mode (most common date), then parsed the column into proper datetime format
- Filled missing `rating` values using the **mode within each content type** (Movie vs. TV Show), rather than a single global mode, since rating distributions differ between the two
- Derived a `year_added` feature by extracting the year from `date_added`, then cast it to integer type
- Filled missing `director` values with a placeholder (`'NA'`) rather than dropping rows, since director was not critical to most of the catalog-level analysis
- Checked for duplicate rows and confirmed **none were present**
- Extracted numeric `duration_min` for movies by parsing the `duration` text field (e.g., "90 min" → 90), since duration is stored differently for Movies vs. TV Shows (minutes vs. seasons)

## 📊 Analysis Performed

- Content type split — Movies vs. TV Shows
- Top contributing countries (titles split on multi-country listings and exploded to count each country individually)
- Content rating distribution (e.g., TV-MA, TV-14, PG, etc.)
- Top genres (parsed from the multi-value `listed_in` field)
- Titles added per year, to track catalog growth over time
- Movie duration distribution (histogram) for the Movie subset
- Top 10 directors by number of contributed titles
- Correlation analysis across numeric fields (`show_id`, `release_year`, `year_added`, `duration_min`), visualized as a heatmap, plus a pairplot to inspect relationships visually

## ✅ Key Results

- Netflix's catalog is **significantly weighted toward movies over TV shows**, with movies making up the majority of titles
- The **United States contributes the most titles**, followed by **India** — making them the top two content-producing countries in the dataset
- **TV-MA is the most common content rating**, followed by TV-14, indicating the catalog leans toward mature and teen audiences rather than younger viewers
- **International Movies** is among the most frequent genres, alongside Dramas and Comedies
- The number of titles added **grew significantly over the years**, with the **highest volume of additions occurring around 2019**
- Most movies run **around 90–100 minutes**, with the longest movie in the dataset clocking in at **312 minutes**
- The top director by title count is **Jan Suter (21 titles)**, followed by Raúl Campos and Jay Karas
- All numeric correlations (release year, year added, duration) were **weak**, meaning there's no strong linear relationship between these fields — e.g., newer titles aren't systematically longer or shorter

## 🚀 Next Steps

- Bring in viewership or popularity data (not in this dataset) to see whether catalog composition aligns with what audiences actually watch
- Analyze TV show season counts the same way movie duration was analyzed, to compare content "depth" across formats
- Track genre trends over time (not just overall genre counts) to see which genres Netflix has leaned into more recently
- Cross-reference country of origin with genre and rating to see if content strategy differs by region
- Extend the dataset with more recent Netflix catalog data, since this dataset's coverage stops at a fixed snapshot in time

## ⚠️ Problems Faced

- Several fields (`country`, `listed_in`, `director`) contained **multiple comma-separated values per row**, requiring splitting and exploding the data before accurate counts could be produced — a straightforward `value_counts()` would have undercounted contributions
- `duration` meant different things for Movies (minutes) vs. TV Shows (number of seasons), so it couldn't be parsed with a single consistent approach across the whole dataset
- Rating had to be imputed **within content type** rather than globally, since Movie and TV Show ratings follow different conventions
- Numeric correlations were all weak, meaning this dataset alone couldn't explain *why* certain patterns (like the 2019 growth spike) occurred — that would require external context

## 🛠️ Tools Used

- **Python** — core analysis language
- **Pandas** — data cleaning, string parsing, and feature engineering
- **Matplotlib / Seaborn** — visualizations (pie chart, bar charts, histogram, heatmap, pairplot)
- **Jupyter Notebook** — development and documentation environment

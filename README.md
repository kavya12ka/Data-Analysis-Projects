# Netflix Content Catalog Analysis
##Business Problem
Streaming platforms compete on the breadth and relevance of their content library. This project analyzes Netflix's catalog metadata to understand what kind of content Netflix has, where it comes from, who makes it, and how the library has grown over time — insights that can inform content acquisition strategy, regional investment decisions, and catalog gap analysis.

## About the Data
Source: Netflix Titles dataset — Kaggle
Size: 6,234 rows × 12 columns
Content: Title-level metadata including type (Movie/TV Show), director, cast, country, date added, release year, content rating, duration, genre (listed_in), and description.

## Data Cleaning
Dropped the cast column (high cardinality, not central to the analysis).
Filled missing date_added with the mode and parsed it into a proper datetime; derived a new year_added column from it.
Filled missing rating values using the mode within each content type (Movie vs TV Show), rather than a single global mode.
Filled missing director values with "NA" as a placeholder.
Checked for duplicate rows — none found.
Extracted numeric duration_min from the duration text field (e.g. "90 min") for movies.
country was left with some missing values (476), since imputing a country is not reliable.

## Analysis & Key Results
Content mix: Movies (4,265) significantly outnumber TV Shows (1,969) in the catalog.
Top content-producing countries: United States leads by a wide margin, followed by India and the United Kingdom.
Ratings: TV-MA is the most common content rating, followed by TV-14 — indicating the catalog skews toward mature and teen audiences.
Genres: International Movies, Dramas, and Comedies are the most frequent genres.
Catalog growth: The number of titles added grew sharply over the years, peaking around 2019.
Movie duration: Most movies run 90–100 minutes; the longest movie in the dataset is 312 minutes.
Top directors: Jan Suter (21 titles), Raúl Campos, and Jay Karas contributed the most titles.
Correlation: show_id, release_year, year_added, and duration_min all show weak correlations with each other — no meaningful linear relationships among the numeric fields.

## Next Steps
Combine country and listed_in (genre) to find region-specific genre gaps or strengths.
Analyze content rating trends over year_added to see if Netflix's content mix has skewed more mature over time.
Build a genre/keyword-based content recommendation or similarity model using description and listed_in.
Investigate the drop in titles added after 2019 (2020 shows a sharp decline) — likely a data cutoff, worth confirming.
Cross-reference top directors/countries with subscriber growth or engagement data (if available) to link catalog composition to business outcomes.

## Problems Faced
High missingness in key fields: director (1,969 missing), cast (570 missing), and country (476 missing) required different strategies — placeholder values, dropping the column, or leaving as-is — since imputing creative/production credits isn't meaningful.
Inconsistent date formats: date_added required format='mixed' parsing to handle inconsistent date string formats in the source file.
Rating imputation nuance: a naive global mode fill for rating would have been misleading, since Movies and TV Shows have different typical ratings — this required a groupby-based fill instead.
Multi-valued fields: country, listed_in, and director often contain comma-separated multiple values in a single cell, requiring str.split().explode() to analyze correctly rather than treating each cell as one category.
Weak correlations: none of the numeric fields correlated meaningfully with each other, limiting how far a purely statistical (non-text) analysis could go.
## Tools Used
Python, pandas, Matplotlib, Seaborn (Jupyter Notebook)


# Hotel Booking Demand Analysis
## Business Problem
Hotel cancellations are a major source of lost revenue — rooms are held (and unavailable to other guests) for bookings that never materialize. This project analyzes hotel booking data to understand **why, when, and for whom cancellations happen**, so the business can identify high-risk booking patterns and take action (e.g. deposit policies, overbooking strategy, targeted follow-ups) to reduce revenue leakage.

## About the Data
- **Source:** [hotel_bookings.csv](https://github.com/swapnilsaurav/Dataset/blob/master/hotel_bookings.csv)
- **Size:** 119,390 rows × 33 columns (raw)
- **Content:** Booking-level records for a City Hotel and a Resort Hotel, including lead time, stay dates, guest counts, room type, ADR (average daily rate), deposit type, customer type, and cancellation status.

## Data Cleaning
- Dropped the `company` column (mostly unusable).
- Filled missing `children`/`babies` with 0; imputed other missing values with mean (numeric) or mode (categorical).
- Fixed data types (converted floats to ints, parsed `arrival_date` and `reservation_status_date` to datetime).
- Combined `stays_in_weekend_nights` + `stays_in_week_nights` into a single `total_days_stayed`.
- Removed ~32,000 duplicate rows.
- Fixed invalid/sentinel values: negative `total_of_special_requests`, negative `adr`, `total_of_special_requests == 120` (clear data entry errors), `adr > 1000` (extreme outliers).
- Removed 166 bookings with zero total guests.
- Standardized `Undefined` meal codes to `SC`.
- Final cleaned dataset: **~87,100 rows × 29 columns**.

## Analysis & Key Results
- **Cancellation rate:** ~27.5% of all bookings are cancelled — the largest single source of revenue risk.
- **By hotel type:** City Hotel cancels more often than Resort Hotel (30.1% vs 23.5%), despite also having higher booking volume.
- **By lead time:** Cancellation risk rises sharply with how far in advance a booking is made — from ~10% for last-minute bookings up to ~40% for bookings made a year or more ahead.
- **Deposits:** Almost all bookings require no deposit, which likely removes any financial disincentive to cancel.
- **Customer mix:** Transient (individual) travelers dominate, far outweighing group or contract bookings.
- **Seasonality:** Room rates (ADR) follow a clear seasonal curve, peaking in August and bottoming out in November.
- **Room allocation:** A visible share of guests are assigned a different room type than what they originally reserved — a real allocation gap.
- **Correlation:** No single numeric variable strongly correlates with cancellation, suggesting cancellations result from a mix of moderate factors rather than one dominant driver.

## Next Steps
- Build a predictive model (e.g. logistic regression, random forest) to score cancellation risk per booking, since no single variable explains it alone.
- Test whether requiring a deposit (even partial) for long-lead-time bookings reduces cancellations.
- Investigate the room-allocation gap further to see if it correlates with guest dissatisfaction or cancellations.
- Segment analysis by market segment / distribution channel to find channel-specific cancellation drivers.
- Extend the seasonal pricing analysis into a revenue-optimization or dynamic-pricing recommendation.

## Problems Faced
- **Messy/inconsistent raw data:** missing values, mixed types, and a large number (32,012) of duplicate rows had to be identified and handled carefully.
- **Invalid sentinel values:** fields like `total_of_special_requests` (negative values, and a suspicious value of 120) and `adr` (negative values, and extreme outliers up to 5400) required manual inspection to distinguish real outliers from data entry errors.
- **Date parsing:** arrival date was split across three separate columns (year, month name, day) and had to be reconstructed into a single valid datetime.
- **Weak correlations:** none of the numeric features correlated strongly with cancellation, making it hard to pin down a single root cause and pointing toward the need for multivariate/predictive modeling rather than simple correlation analysis.

## Tools Used
Python, pandas, NumPy, Matplotlib, Seaborn (Jupyter Notebook)

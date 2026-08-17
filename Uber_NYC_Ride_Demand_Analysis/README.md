# Uber NYC Ride Demand Analysis
### Uncovering Peak Hours, Weekday Patterns, and Pickup Hotspots (April–September 2014)

## 📌 Business Question

Uber operates across New York City with multiple dispatch bases, but demand isn't uniform — it fluctuates by hour, day, and location. The core question this project set out to answer is: **when and where is Uber demand highest in NYC, and how does it vary across time and dispatch bases** — so that Uber can better align driver supply, surge pricing, and base allocation with actual rider demand patterns.

## 🎯 Business Problem

- Uber needs to understand demand patterns across time (hour, day, month) and geography to optimize driver allocation and reduce idle time or unmet demand
- Uneven distribution of trips across the 5 dispatch bases suggests inefficiencies in how supply is matched to demand
- Without this analysis, Uber risks over- or under-supplying drivers during peak commute windows or in high-density pickup zones

## 📂 Data Source

- Six monthly CSV files of NYC Uber pickup data (April–September 2014), sourced from the [FiveThirtyEight public GitHub repository](https://github.com/fivethirtyeight/uber-tlc-foil-response) (`uber-tlc-foil-response`)
- Each file contains raw trip-level records with `Date/Time`, `Lat`, `Lon`, and `Base` (dispatch base code)
- Combined dataset covers roughly 4.5 million individual trip records after merging

## 🧹 Data Cleaning

- Merged all six monthly files into a single combined DataFrame
- Converted the `Date/Time` column to proper datetime format
- Engineered new features: `Week` (day name), `Month`, `Hour_Of_Day`, `Min_Of_Day`, and later `Day_Type` (Weekday/Weekend)
- Checked for and removed **82,581 duplicate rows**
- Checked for null values across all columns (none found needing imputation)
- Reviewed unique values and column-level statistics to validate data integrity before analysis

## 📊 Analysis Performed

- Trip volume trends by hour of day, day of week, and month
- Month-over-month growth rate calculation (April → September)
- Weekday vs. weekend hourly trip comparison
- Trip density heatmaps (day × hour, day × minute)
- Geographic pickup density visualization (hexbin map of NYC)
- Trip volume breakdown by dispatch base, both monthly and hourly

## ✅ Key Results

- Demand nearly doubled over six months — from ~557K trips in April to ~1M trips in September, with a 23% jump from August to September alone
- Weekdays significantly outpace weekends; Thursday and Wednesday were busiest, Sunday quietest
- Trips peak in the early evening (6–9 PM), reflecting commute/after-work travel
- Weekday and weekend demand follow distinct hourly rhythms — weekdays show sharp commute spikes, weekends are flatter and shifted later
- Pickups cluster in specific hotspots rather than spreading evenly across the city
- Dispatch bases show unequal, non-identical demand patterns by hour and month, suggesting each may serve different rider segments

## 🚀 Next Steps

- Incorporate later years of data (2015 onward) to check if patterns hold or shift over time
- Layer in external factors — weather, holidays, major events — to explain demand spikes/dips
- Build a demand forecasting model (e.g., time-series) for proactive driver allocation
- Cluster pickup coordinates (e.g., k-means/DBSCAN) to formally define hotspot zones instead of visual inspection
- Analyze fare/revenue data (not present in this dataset) to connect demand patterns to profitability by base and zone

## ⚠️ Problems Faced

- Large file sizes (multiple millions of rows) slowed down processing and visualization rendering
- Significant duplicate records (82,581) required careful handling to avoid inflating trip counts
- No fare, trip duration, or drop-off data available — limited analysis to pickup patterns only
- Dataset only covers 6 months of a single year, limiting ability to detect seasonal or multi-year trends
- Overlapping/dense heatmap visuals (e.g., minute-level heatmap) were harder to interpret due to high granularity

## 🛠️ Tools Used

- **Python** — core analysis language
- **Pandas / NumPy** — data cleaning, merging, and feature engineering
- **Matplotlib / Seaborn** — visualizations (line charts, bar charts, heatmaps, hexbin maps)
- **Jupyter Notebook** — development and documentation environment

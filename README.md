# 📊 Data Analysis Portfolio

A collection of end-to-end data analysis projects covering data cleaning, exploratory analysis, statistical testing, and SQL-based querying across transportation, hospitality, entertainment, sports, and retail domains. Each project includes its own detailed README covering the business problem, data source, cleaning steps, analysis, key results, and tools used.

---

## ⭐ Featured Project: Uber NYC Ride Demand Analysis

**[→ View full project](./Uber_NYC_Ride_Demand_Analysis)**

This is the most complete project in the portfolio — combining a large real-world dataset (4.5M+ trip records), thorough data cleaning (82,581 duplicates identified and removed), and a wide range of time-series and geospatial visualizations (hourly/weekly/monthly trends, heatmaps, hexbin pickup density maps). It answers a clear, actionable business question — **when and where is Uber demand highest in NYC** — and turns that into insight on driver allocation and dispatch base efficiency.

**Highlights:**
- Demand nearly doubled over 6 months (April → September 2014), with a 23% MoM spike from August to September
- Clear weekday/evening commute pattern (peak 6–9 PM), distinct from weekend behavior
- Geographic hotspot analysis via hexbin pickup density mapping
- Base-level demand analysis revealing uneven load across Uber's 5 NYC dispatch bases

---

## 📁 Project Summaries

### 🚗 [Uber NYC Ride Demand Analysis](./Uber_NYC_Ride_Demand_Analysis)
Analyzed 6 months of NYC Uber trip data to uncover peak demand hours, weekday vs. weekend patterns, and pickup hotspots — supporting smarter driver allocation and dispatch base planning.
**Tools:** Python, Pandas, Matplotlib, Seaborn

### 🏨 [Hotel Booking Cancellation Analysis](./Hotel_Booking_Cancellation_Analysis)
Investigated why ~27.5% of hotel bookings get cancelled, finding that lead time, deposit type, and hotel type are key drivers — with cancellation risk climbing from ~10% for last-minute bookings to ~40% for bookings made a year+ in advance.
**Tools:** Python, Pandas, Matplotlib, Seaborn

### 🎬 [Netflix Content Catalog Analysis](./Netflix_Content_Catalog_Analysis)
Explored Netflix's global content library to understand content mix, top contributing countries, ratings distribution, and genre trends — revealing the US and India as the top content sources and a steep rise in titles added around 2019.
**Tools:** Python, Pandas, Matplotlib, Seaborn

### ⚽ [Euro Championship Soccer Analysis](./Soccer_Euro_Championship_Analysis)
Used statistical testing (t-tests, correlation) across three linked datasets (results, coaches, lineups) to test whether squad height, age, and attendance actually relate to Euro Championship success — finding winning squads are significantly shorter on average, with no meaningful age difference.
**Tools:** Python, Pandas, SciPy, Matplotlib, Seaborn

### 🛍️ [Customer Purchase Behavior Analysis](./Customer_Purchase_Behavior_Analysis)
Cleaned and modeled a retail transaction dataset in Python, then loaded it into MySQL to answer business questions via SQL — revenue by segment, discount effectiveness, product performance, and customer loyalty tiers (New / Returning / Loyal).
**Tools:** Python, Pandas, MySQL, SQL, SQLAlchemy

---

## 🛠️ Overall Tech Stack

`Python` · `Pandas` · `NumPy` · `Matplotlib` · `Seaborn` · `SciPy` · `MySQL` · `SQL` · `Jupyter Notebook`

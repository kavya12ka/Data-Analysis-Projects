# Euro Championship Soccer Analysis
### What Separates Winning Squads? A Statistical Look at UEFA Euro History

## 📌 Business Question

National football federations and analysts want to know what actually separates a Euro-winning squad from the rest of the field — is it player physicality, squad age, coaching stability, or something else? This project investigates **whether measurable squad and match characteristics (height, age, attendance, coaching tenure) are statistically associated with tournament success**, to help inform data-driven talent selection and team-management decisions.

## 🎯 Business Problem

- Federations and coaching staff need evidence-based insight into what traits correlate with winning, rather than relying on intuition alone
- It's unclear whether physical attributes (height, age) of a squad meaningfully predict success, or whether other factors (coaching stability, tactical setup) matter more
- Attendance and goal-scoring trends are often assumed to move together, but this assumption hadn't been statistically tested

## 📂 Data Source

- Three related datasets covering UEFA Euro Championship history:
  - **Euro Summary** — tournament-level results (year, winner, goals, attendance)
  - **Euro Coaches** — coaching records per team per tournament
  - **Euro Lineups** — player-level squad data (position, height, weight, appearances)

## 🧹 Data Cleaning

- Cast the `attendance` column to integer type for accurate numeric analysis
- Dropped `start_position_x` and `start_position_y` columns — ~49% of values were null and another large portion were `-1` placeholder values, making the columns unreliable for analysis
- Left ~50% missing `height` and `weight` values as null rather than imputing, since filling that large a share of the data with mean/median could artificially bias the distribution
- Checked for and confirmed no duplicate records across the datasets

## 📊 Analysis Performed

- Identified the country with the most Euro titles and tournament with the highest goal count
- Compared average height and age of winning squads vs. the rest of the field, using an independent **t-test** to check statistical significance
- Examined position distribution (starting XI vs. bench), height/weight by position via box plots
- Analyzed total attendance and average goals per match by tournament
- Tracked red cards issued, wins by decade, and age distribution across tournaments
- Measured coaching turnover and identified top coaches by matches coached and by titles won
- Tested the correlation between attendance and total goals, and between attendance and goals *per match*

## ✅ Key Results

- Spain is the most successful Euro nation with **4 titles**; West Germany, Italy, and France each have 2
- Winning squads averaged **181.11 cm** in height and **27.52 years** in age
- The t-test showed winning-squad players were **significantly shorter** on average (p < 0.001), while age showed **no significant difference** (p = 0.1423)
- Attendance and total goals were positively correlated — but once normalized to goals *per match*, the relationship flipped to a **negative correlation** (r = -0.523, p = 0.031), meaning higher-attendance tournaments actually saw slightly fewer goals per match
- Coaching stability varied widely by country, with some teams retaining the same coach across multiple tournaments and others rotating frequently

## 🚀 Next Steps

- Investigate whether coaching stability itself correlates with tournament success
- Source a more complete dataset for player height/weight to strengthen the physical-attribute analysis
- Extend the dataset to include more recent tournaments as new data becomes available
- Explore tactical/formation data if available, to see whether playing style is a stronger predictor of success than physical traits

## ⚠️ Problems Faced

- Nearly half of the height and weight data was missing, limiting the reliability of physical-attribute conclusions
- Positional coordinate data (`start_position_x/y`) was unusable due to extensive nulls and placeholder values, so it had to be dropped entirely
- Working across three separate datasets required careful joining and consistency checks before analysis

## 🛠️ Tools Used

- **Python** — core analysis language
- **Pandas / NumPy** — data cleaning and feature engineering
- **Matplotlib / Seaborn** — visualizations (bar charts, box plots, line charts)
- **SciPy** — statistical testing (t-test, correlation)
- **Jupyter Notebook** — development and documentation environment

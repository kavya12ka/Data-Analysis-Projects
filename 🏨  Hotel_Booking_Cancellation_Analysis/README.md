# Hotel Booking Cancellation Analysis
### What Drives Cancellations, and How Can Hotels Reduce Revenue Leakage?

## 📌 Business Question

Cancellations are one of the biggest sources of lost revenue and planning uncertainty for hotels — but not all bookings carry the same cancellation risk. This project investigates **which booking characteristics (lead time, deposit type, hotel type, customer type) are associated with a booking being cancelled**, so that hotels can identify high-risk bookings early and adjust deposit policies, overbooking strategy, or guest communication accordingly.

## 🎯 Business Problem

- Cancellations directly erode revenue and make demand forecasting and staffing harder to plan
- Hotels don't currently have a clear, data-backed view of *which* bookings are most likely to cancel
- Deposit policy, lead time, and hotel type may all play a role, but their relative impact hadn't been quantified
- A visible gap between reserved and assigned room types suggests possible operational inefficiencies worth investigating alongside cancellations

## 📂 Data Source

- **hotel_bookings.csv** — a public hotel booking dataset covering City Hotel and Resort Hotel reservations, sourced from [this GitHub dataset repository](https://github.com/swapnilsaurav/Dataset/blob/master/hotel_bookings.csv)
- Contains booking-level records: hotel type, arrival date, lead time, length of stay, guest counts, meal plan, deposit type, customer type, ADR (average daily rate), room type (reserved vs. assigned), cancellation status, and more

## 🧹 Data Cleaning

- Reviewed missing value percentages across all columns before touching the data, and worked on a copy of the original DataFrame to preserve the raw version
- Dropped the `company` column (too sparse/unreliable to use)
- Filled missing `babies` and `children` values with 0, and renamed `agent` → `agent_id` for clarity
- Applied a general null-handling rule: numeric columns filled with the column mean, categorical columns filled with the column mode
- Converted numeric fields (adults, children, babies, lead_time, stays, booking_changes, agent_id, etc.) to proper integer types
- Built a proper `arrival_date` datetime field by combining year, month, and day columns, and parsed `reservation_status_date` into datetime as well
- Dropped the now-redundant raw date parts (`arrival_date_year`, `arrival_date_month`, `arrival_date_day_of_month`) after building the combined date
- Created a new `total_days_stayed` feature by summing weekday and weekend night stays, then dropped the two original columns to avoid duplication
- Identified and removed duplicate rows (excluding the `id` column), keeping the first occurrence
- Checked for and corrected invalid/sentinel values:
  - Negative `total_of_special_requests` values set to 0; an implausible outlier value (120) dropped
  - Negative `adr` (average daily rate) values set to 0; extreme outliers (adr > 1000) removed
  - `Undefined` meal plan values recoded to `SC` (self-catering), the standard category it represents
- Removed bookings with **zero total guests** (adults + children + babies = 0), since these aren't valid reservations
- Checked bookings with zero nights stayed that weren't cancelled, to understand same-day/no-show style edge cases

## 📊 Analysis Performed

- Hotel type distribution — booking volume split between City Hotel and Resort Hotel
- Deposit type distribution across bookings
- Customer type distribution (Transient, Contract, Group, etc.)
- Overall cancellation rate — cancelled vs. completed bookings
- ADR (average daily rate) distribution across all bookings
- Lead time distribution — how far in advance guests typically book
- Length of stay distribution (nights per booking)
- Top 10 guest countries of origin by booking volume
- Cancellation rate comparison: City Hotel vs. Resort Hotel
- Relationship between lead time and cancellation likelihood
- Average pricing (ADR) by season
- Comparison of reserved vs. assigned room types (room allocation mismatches)
- Correlation analysis between numeric booking features and cancellation

## ✅ Key Results

- Roughly **1 in 4 bookings (27.5%) ends in cancellation** — making cancellation the single biggest revenue leak in this dataset
- **City Hotel cancels more often than Resort Hotel** (30.1% vs. 23.5%), despite City Hotel also having the higher overall booking volume
- Cancellation risk **rises sharply with lead time** — from ~10% for last-minute bookings to ~40% for bookings made a year or more in advance
- **Almost all bookings require no deposit**, which likely removes any financial disincentive for guests to cancel
- **Transient (individual) travelers dominate** the customer base, far outweighing group or contract bookings
- Room rates follow a **clear seasonal curve**, peaking in August and bottoming out in November
- A visible share of guests are assigned a **different room type than originally reserved**, pointing to a real room-allocation gap
- **No single numeric variable strongly correlates with cancellation** — cancellations appear to be driven by a mix of moderate factors (lead time, deposit type, hotel type) rather than one dominant cause

## 🚀 Next Steps

- Build a classification model (e.g., logistic regression or random forest) to predict cancellation probability at time of booking, using lead time, deposit type, and hotel type as features
- Test whether requiring a partial deposit for high-lead-time bookings reduces cancellation rates
- Investigate the room-allocation mismatch further to see if it correlates with guest satisfaction or repeat bookings
- Segment the analysis by customer type (Transient vs. Group vs. Contract) to see if cancellation drivers differ by segment
- Bring in more recent booking data to check whether these patterns still hold post-pandemic, given major shifts in travel booking behavior

## ⚠️ Problems Faced

- Several columns required different cleaning strategies (mean vs. mode fill, sentinel-value correction, outlier capping), which made the cleaning process lengthy and required careful column-by-column review
- Some values were clearly invalid (negative special requests, negative ADR, a single special-requests value of 120) and required manual inspection rather than automated rules
- Duplicate detection had to explicitly exclude the `id` column, since otherwise no duplicates would ever be detected
- Weak correlations across the board meant no single variable could "explain" cancellation on its own, requiring a more nuanced, multi-factor interpretation of the results

## 🛠️ Tools Used

- **Python** — core analysis language
- **Pandas / NumPy** — data cleaning, type conversion, and feature engineering
- **Matplotlib / Seaborn** — visualizations (bar charts, distributions, correlation analysis)
- **Jupyter Notebook** — development and documentation environment

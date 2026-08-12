# Hotel Booking Cancellation Analysis

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

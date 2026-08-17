# Customer Purchase Behavior Analysis
### Segmenting Shoppers and Uncovering Revenue Drivers with Python + SQL

## 📌 Business Question

A retail business wants to understand **who its customers are, what drives their spending, and how factors like discounts, subscriptions, and shipping choice affect revenue** — so that marketing, pricing, and loyalty strategies can be targeted more effectively instead of applied uniformly across all shoppers.

## 🎯 Business Problem

- The business has customer transaction data but no clear picture of which segments (age, gender, loyalty tier) drive the most revenue
- It's unclear whether discounts and promo codes are actually driving incremental spend or just cutting into margin on purchases that would have happened anyway
- There's no existing view of which products perform best by rating or by discount reliance, or how shipping preference relates to spend
- Without this analysis, marketing and retention efforts risk being generic rather than data-driven

## 📂 Data Source

- A customer shopping behavior dataset (`customer_shopping_behavior.csv`) containing transaction-level records: customer demographics, purchase amount, category, item purchased, review rating, discount/promo usage, subscription status, shipping type, and purchase frequency
- After cleaning in Python, the dataset was loaded into a **MySQL** database (`customer_behavior`) so the deeper analysis could be done using SQL

## 🧹 Data Cleaning

- Filled missing `Review Rating` values using the **median rating within each product category**, rather than a single global median, to preserve category-level rating differences
- Standardized column names (lowercased, replaced spaces with underscores, renamed `purchase_amount_(usd)` → `purchase_amount`)
- Created an `age_group` feature (Young Adults / Adult / Middle Aged / Senior) by splitting `age` into quartile-based buckets
- Converted `frequency_of_purchases` (e.g., "Weekly", "Annually") into a numeric `purchase_frequency_days` field for easier analysis
- Identified that `discount_applied` and `promo_code_used` were always identical — dropped the redundant `promo_code_used` column
- Exported the cleaned dataset into a MySQL table (`customerpurchase`) for SQL-based querying

## 📊 Analysis Performed

Using SQL against the cleaned MySQL table:
- Total revenue overall, and split by gender
- Customers who used a discount **and** spent above the average purchase amount
- Top 5 products by average review rating
- Average purchase amount: Standard vs. Express shipping
- Subscriber vs. non-subscriber comparison (customer count, average spend, total revenue)
- Top 5 products by percentage of discounted sales
- Customer segmentation by purchase history (New / Returning / Loyal, based on previous purchase count)
- Top 3 best-selling items within each product category
- Repeat buyers (5+ purchases) grouped by subscription status
- Revenue contribution by age group

## ✅ Key Results

- Revenue splits cleanly across gender, shipping type, and subscription status, giving a clear baseline for where spend concentrates
- Discount usage and above-average spend overlap for a meaningful share of customers, suggesting discounts may be reaching already high-value shoppers rather than only price-sensitive ones
- Product-level rating and discount-reliance leaders differ from each other — the highest-rated products are not always the most discounted, pointing to different demand drivers per product
- Customer segmentation (New / Returning / Loyal) reveals a workable base of repeat and loyal customers worth targeting for retention campaigns
- Subscription status shows a measurable difference in average spend and repeat-purchase behavior between subscribers and non-subscribers

## 🚀 Next Steps

- Turn the SQL queries into a live dashboard (e.g., Power BI / Tableau) for ongoing monitoring rather than one-off analysis
- Run statistical tests to confirm whether observed differences (e.g., subscriber vs. non-subscriber spend) are significant, not just directional
- Build a customer lifetime value (CLV) model using the segmentation already created
- Test discount effectiveness more rigorously (e.g., cohort or uplift analysis) to see if discounts are actually driving incremental revenue
- Automate the Python-to-MySQL pipeline so new transaction data refreshes the analysis automatically

## ⚠️ Problems Faced

- Missing review ratings needed a thoughtful fill strategy (category median) rather than a blanket global fill, to avoid skewing category-level insights
- Two columns (`discount_applied`, `promo_code_used`) were fully redundant and had to be identified and removed to avoid duplicate signal
- The notebook originally connected to a local MySQL instance with a hardcoded password — this should be moved to environment variables/secrets before sharing or productionizing the code
- Splitting the workflow across Python (cleaning) and SQL (analysis) required keeping schema and column names in sync between the two

## 🛠️ Tools Used

- **Python (Pandas)** — data cleaning and feature engineering
- **MySQL** — storage and querying of the cleaned dataset
- **SQLAlchemy / PyMySQL** — connecting Python to MySQL
- **SQL** — window functions, subqueries, and aggregations for the core analysis
- **Jupyter Notebook** — development and documentation environment

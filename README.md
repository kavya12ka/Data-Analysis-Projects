# Data Analysis Portfolio

This repository contains exploratory data analysis (EDA) projects built using Python, pandas, Matplotlib, and Seaborn in Jupyter Notebooks. Each project covers data cleaning, exploratory analysis, visualization, and business-focused insights.

## Projects

### 1. [Hotel Booking Cancellation Analysis](./hotal_data_analysis.ipynb)
Analyzes ~119K hotel booking records to understand why, when, and for whom cancellations happen, in order to reduce revenue loss from cancelled rooms.
- **Key finding:** ~27.5% of bookings are cancelled, with risk rising sharply as lead time increases.
- 📄 Full write-up: [README.md](./README.md)

### 2. [Netflix Content Catalog Analysis](./netflix_data_analysis.ipynb)
Analyzes Netflix's title catalog metadata to understand content mix, top contributing countries, genres, and catalog growth over time.
- **Key finding:** Movies dominate the catalog, the US and India lead content contribution, and titles added grew sharply through 2019.
- 📄 Full write-up: [README_netflix.md](./README_netflix.md)

## Repository Structure
```
├── hotal_data_analysis.ipynb      # Hotel booking cancellation analysis notebook
├── README.md                      # Hotel project README
├── netflix_data_analysis.ipynb    # Netflix catalog analysis notebook
├── README_netflix.md              # Netflix project README
└── README_main.md                 # This file — repository overview
```

## Tools & Libraries
- Python
- pandas, NumPy
- Matplotlib, Seaborn
- Jupyter Notebook

## How to Use
1. Clone the repository.
2. Install dependencies: `pip install pandas numpy matplotlib seaborn jupyter`
3. Open the notebook for the project you're interested in and run the cells in order.
4. Refer to each project's individual README for detailed findings, next steps, and challenges faced.

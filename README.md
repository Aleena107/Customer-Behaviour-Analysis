# Customer Shopping Behavior Analysis

An end-to-end data analytics project exploring customer shopping patterns, purchase behavior, product reviews, discount usage, shipping preferences, and subscription status using **Python, PostgreSQL, Power BI, and Excel**.

## Project Overview

This project analyzes customer shopping data to identify patterns in purchasing behavior and generate insights that can support business decisions. The workflow includes data inspection and cleaning in Python, loading the prepared dataset into PostgreSQL for SQL analysis, and presenting insights through an interactive Power BI dashboard.

The dataset contains **3,900 customer shopping records**.

## Tools & Technologies

- **Python** — data inspection, cleaning, feature engineering, and preparation
- **Pandas** — data manipulation and transformation
- **PostgreSQL** — querying and aggregating customer data
- **SQL** — filtering, grouping, aggregate functions, subqueries, CTEs, `CASE` expressions, and window functions
- **Power BI** — dashboarding and visual analysis
- **Excel** — working with and reviewing tabular records

## Project Workflow

1. **Inspect the Data:** Reviewed sample records, column information, descriptive statistics, and missing values using Pandas.
2. **Clean the Data:** Filled missing review ratings using the median rating within each product category.
3. **Prepare Columns:** Standardized column names and renamed the purchase amount field for easier analysis.
4. **Create Features:** Grouped customers into age groups and mapped purchase-frequency labels to approximate intervals in days.
5. **Remove Redundant Data:** Checked whether `discount_applied` and `promo_code_used` matched, then removed `promo_code_used` from the prepared dataset.
6. **Load into PostgreSQL:** Used SQLAlchemy and `psycopg2` to load the prepared data into the `customer` table.
7. **Analyze with SQL:** Wrote queries to investigate revenue, ratings, discounts, shipping types, subscriptions, and customer segments.
8. **Visualize in Power BI:** Built a dashboard to present customer behavior patterns and support exploration of the data.

## Business Questions Answered with SQL

The SQL analysis explores the following questions:

1. What does the customer dataset look like?
2. How does total purchase revenue compare by gender?
3. Which customers used a discount and spent at least the overall average purchase amount?
4. Which five products have the highest average review ratings?
5. How do average purchase amounts compare between Standard and Express shipping?
6. Do subscribed customers spend more than non-subscribers in terms of average spend and total revenue?
7. Which five products have the highest percentage of purchases with discounts applied?
8. How many customers fall into New, Returning, and Loyal segments based on previous purchases?
9. What are the top three most-purchased products within each category?
10. Among customers with more than five previous purchases, how many are subscribed versus not subscribed?
11. How much revenue does each age group contribute?

## SQL Concepts Demonstrated

- `SELECT`, `WHERE`, `ORDER BY`, and `LIMIT`
- Aggregate functions: `SUM()`, `AVG()`, and `COUNT()`
- `GROUP BY` and `HAVING`-style analytical thinking
- Subqueries
- `CASE WHEN` conditional aggregation
- Common Table Expressions (CTEs)
- Window functions such as `ROW_NUMBER()`
- Numeric conversion and rounding for review ratings and percentages

## Data Preparation Details

The notebook performs the following transformations:

- Inspects null values and descriptive statistics.
- Fills missing `Review Rating` values with the median for the corresponding `Category`.
- Converts column names to lowercase and replaces spaces with underscores.
- Renames `purchase_amount_(usd)` to `purchase_amount`.
- Creates an `age_group` feature using quartile-based binning.
- Creates `purchase_frequency_days` by mapping purchase-frequency labels to approximate day intervals.
- Removes `promo_code_used` after checking whether its values match `discount_applied`.
- Loads the resulting DataFrame into PostgreSQL using SQLAlchemy.

**Note:** The purchase-frequency intervals are approximate mappings used for analysis; they do not represent exact transaction dates or measured time between purchases.

## Dataset Fields

The dataset includes customer and purchase attributes such as:

- Customer ID and age
- Gender and location
- Item purchased and product category
- Purchase amount (USD)
- Size, color, and season
- Review rating
- Subscription status
- Shipping type
- Discount applied and promo code used
- Previous purchases
- Payment method
- Frequency of purchases

The prepared dataset also includes derived fields such as `age_group` and `purchase_frequency_days`.

## Repository Contents

The repository includes the project notebook, SQL analysis, Power BI dashboard, and dataset. File names may differ depending on the uploaded versions.

- **Jupyter Notebook (`.ipynb`)** — Python-based data inspection, cleaning, feature engineering, and database loading
- **SQL file (`.sql`)** — analytical queries for customer behavior and purchasing patterns
- **Power BI file (`.pbix`)** — interactive dashboard
- **CSV file (`.csv`)** — customer shopping dataset

## How to Run

### 1. Clone the Repository

```bash
git clone <your-github-repository-url>
cd <your-repository-folder>
```

### 2. Install Python Dependencies

```bash
pip install pandas sqlalchemy psycopg2-binary jupyter
```

### 3. Add the Dataset

Place `customer_shopping_behavior.csv` in the location expected by the notebook, or update the `pd.read_csv()` path to match your file.

### 4. Configure PostgreSQL

- Install and start PostgreSQL.
- Create a database named `customer_behaviour`, or update the notebook with your database name.
- Update the connection settings in the notebook to match your local PostgreSQL setup.
- Run the notebook cells in order.

**Security:** Do not commit real database passwords or other credentials to GitHub. Use environment variables or a local configuration file excluded from version control instead of hardcoding credentials.

### 5. Run the SQL Queries

Open the SQL file in a PostgreSQL-compatible client, connect to the database, and run the queries against the `customer` table after the data has been loaded.

### 6. Open the Power BI Dashboard

Open the `.pbix` file in Power BI Desktop. If the report requires a local data source, update its connection settings as needed.

## Key Learning Outcomes

- Practiced data cleaning and feature engineering with Pandas.
- Used PostgreSQL to analyze customer and purchase data.
- Applied SQL aggregation, subqueries, CTEs, conditional logic, and window functions.
- Explored customer segments, revenue contribution, product ratings, shipping, discounts, and subscriptions.
- Connected data preparation, database analysis, and dashboard reporting in one workflow.

## Future Improvements

- Add documented, data-backed findings with exact values from the full dataset.
- Improve the dashboard with clearer KPI cards, slicers, and drill-down views.
- Validate whether discount and promo-code fields are truly equivalent before dropping either field.
- Use environment variables for database configuration.
- Add screenshots of the Power BI dashboard to the repository README.

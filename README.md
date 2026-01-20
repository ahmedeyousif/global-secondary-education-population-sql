
# Global Secondary Education Population Analysis (2015)

##  Project Overview

This project analyzes **public World Bank education data** using SQL to answer the following analytical question:

> **In 2015, how many people were of the official age for secondary education, broken down by world region?**

The objective of this project is to demonstrate the ability to:

* Work with **public datasets**
* Join multiple tables correctly
* Clean and filter real-world data
* Aggregate data at the correct grain
* Produce meaningful, ranked insights using SQL

---

##  Data Source

The data comes from **Google BigQuery Public Datasets**, specifically:

* `world_bank_intl_education.international_education`
* `world_bank_intl_education.country_summary`

These datasets are maintained by the World Bank and contain international education indicators and country-level metadata.

---

##  Analytical Question

**How many people were of the official age for secondary education in 2015, grouped by world region?**

To answer this question, the analysis required:

* Excluding records with missing region data
* Selecting the correct education indicator
* Aggregating population values across countries
* Sorting results to identify regions with the largest populations

---

##  Data Preparation & Logic

Before returning the final result, the following steps were applied:

1. **Joined two tables** using `country_code` as the key to connect education data with regional information.
2. **Filtered out rows with NULL regions** to avoid invalid groupings.
3. **Selected a specific education indicator** related to secondary-school-age population.
4. **Filtered data to a single year (2015)** for consistency.
5. **Aggregated population values** using `SUM()` at the regional level.
6. **Sorted results** to display the highest population regions first.

---

##  SQL Query

```sql
SELECT
    summary.region,
    SUM(edu.value) AS secondary_edu_population
FROM
    `bigquery-public-data.world_bank_intl_education.international_education` AS edu
INNER JOIN
    `bigquery-public-data.world_bank_intl_education.country_summary` AS summary
ON
    edu.country_code = summary.country_code -- country_code is the join key
WHERE
    summary.region IS NOT NULL
    AND edu.indicator_name = 'Population of the official age for secondary education, both sexes (number)'
    AND edu.year = 2015
GROUP BY
    summary.region
ORDER BY
    secondary_edu_population DESC;
```

---

##  Result Interpretation

* Each row in the output represents a **world region**.
* The population values represent the **total number of people of official secondary education age** across all countries in that region.
* Sorting the results in descending order highlights which regions had the **largest secondary-school-age populations** in 2015.

This type of analysis is useful for:

* Education policy planning
* Resource allocation
* Global development research

---

##  Skills Demonstrated

* SQL joins (`INNER JOIN`)
* Working with public datasets
* Filtering data using `WHERE`
* Aggregation using `SUM()`
* Grouping data with `GROUP BY`
* Sorting results with `ORDER BY`
* Writing clean, well-documented analytical SQL

---

##  Why This Project Matters

This project demonstrates the ability to:

* Translate a **business or policy question** into a SQL query
* Analyze **real-world public data**, not toy datasets
* Apply data cleaning and aggregation techniques commonly required in data analyst roles

It is well-suited for **entry-level Data Analyst positions** and complements Excel and BI dashboard projects.

---

##  Author

**Ahmed Yousif**
Aspiring Data Analyst | SQL | Excel | Power BI

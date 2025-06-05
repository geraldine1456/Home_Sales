# 🏡 Home Sales Analysis 

### 📌 Overview

This project analyzes a home sales dataset using **SparkSQL** to uncover trends such as average home prices by bedroom count, home features, and view ratings. The analysis emphasizes **performance tuning** through **caching** and **partitioning** to demonstrate how different Spark optimization strategies perform under various query conditions.

---

### 🗂️ Data Source

* **URL:** `https://2u-data-curriculum-team.s3.amazonaws.com/dataviz-classroom/v1.2/22-big-data/home_sales_revised.csv`  

---

### 📁 Project Structure

```
Home_Sales/
├── Home_Sales.ipynb
├── README.md
```

### 🧰 Tools & Libraries

| Tool         | Version    | Purpose                                         |
| ------------ | ---------- | ----------------------------------------------- |
| Apache Spark | 3.5.6      | Distributed big data processing                 |
| Hadoop       | 3          | Storage layer used by Spark                     |
| Java         | OpenJDK 11 | Required to run Spark                           |
| Python       | 3.9+       | Programming language for analysis               |
| `findspark`  | latest     | Enables Spark integration with Python notebooks |

---

### ⚙️ Setup Instructions

1. Clone the GitHub repository:

   ```bash
   git clone https://github.com/geraldine1456/Home_Sales.git
   cd Home_Sales
   ```
2. Install dependencies:

   ```bash
   pip install pyspark findspark
   ```
3. Launch Jupyter Notebook or Colab and open `Home_Sales.ipynb`.

### 🔍 Analysis Tasks

1. Load and register the CSV data into a temporary SQL table
2. Run SparkSQL queries to:
   * Compute average home price for 4-bedroom homes by year
   * Compute average price for 3-bed, 3-bath homes by build year
   * Filter by additional criteria: square footage and floors

3. Use SparkSQL to compare average price by view rating:
   * Without caching
   * With caching
   * With partitioned Parquet files

4. Measure runtime for each optimization step

---

### 📈 Runtime Results

| Query Type                                   | Runtime        |
| -------------------------------------------- | ---------------|
| Average price per view (uncached)            | 1.0853 seconds |
| Average price per view (cached)              | 0.5494 seconds |
| Average price per view (partitioned Parquet) | 1.1926 seconds |

---

### 💡 Key Insights

* **Caching** provides dramatic performance improvements for repeated queries, reducing runtime by nearly 50% in this analysis.
* **Partitioning** effectiveness depends on query patterns. Since our analysis grouped by view rating rather than the partition key (date_built), partitioned data showed slower performance due to the overhead of reading across multiple partition files.
* This demonstrates a crucial principle in big data optimization: the best strategy depends on how you plan to query your data. Partitioning by date_built would excel for time-based analyses but adds overhead for queries that need to aggregate across all time periods.
* Apache Spark's flexible optimization approaches allow data engineers to choose the right strategy based on their specific use cases and query patterns.

---

# 🚀 Project Summary — Indian Startup Funding Analysis

---

# 🎯 Objective

The objective of this project is to analyze startup funding trends in India (2015–2019) by transforming raw, unstructured data into a clean, scalable, and analysis-ready data model using Power BI.

---

# 🌍 Real-World Problem

Startup funding data is often messy and fragmented, making it difficult for stakeholders to answer critical business questions such as:

* Which sectors are attracting the most investment?
* Who are the most active investors?
* How is funding evolving over time?
* Which startups are consistently receiving funding?

Poorly structured data leads to:

* Incorrect aggregation of funding amounts
* Misidentification of key investors
* Inability to track trends over time

This project solves these issues by building a **reliable and structured analytical model**.

---

# 🧠 Problem Statement (Data-Level)

The original dataset contained multiple structural issues:

* Investors stored as comma-separated values in a single column
* No primary or foreign keys
* Inconsistent text formatting
* Missing values (~35% in funding amounts)
* No clear relationships between entities

These issues made accurate analysis difficult and led to incorrect insights.

---

# 🛠️ Approach

## 🔹 1. Data Cleaning

* Removed irrelevant columns (e.g., Remarks)
* Standardized text fields (Trim, Clean, Case normalization)
* Fixed encoding issues
* Handled missing and ambiguous values

---

## 🔹 1. Exploratory Data Analysis (EDA)

* Performed in Jupyter Notebook using Python (Pandas & visualization libraries):
    * Data inspection and missing value analysis
    * Distribution analysis of funding amounts
* 📊 Key Analysis
    * Answered business-driven questions (top startups, active investors, sector trends)
    * Used Pandas for aggregation and charts for validation of insights
    * Identified inconsistencies and patterns that guided data cleaning and modeling

---

## 🔹 3. Data Transformation

* Split multi-investor column into individual rows
* Extracted:

  * `year` from date
  * `month` from date
* Created surrogate keys:

  * `startup_id`
  * `type_id`
  * `investors_id`
* Built structured dimension tables

---

## 🔹 4. Data Modeling

Implemented a **Star Schema with a bridge table**:

* Fact table for funding events
* Dimension tables for startups, investors, investment types, and dates
* Bridge table to resolve many-to-many relationships

---

# 🧩 Data Model Overview

### Fact Table:

* `fact_funding`

### Dimension Tables:

* `dim_startup`
* `dim_investment_type`
* `dim_date`
* `dim_investors`

### Bridge Table:

* `bridge_investor`

---

# 🔗 Key Design Decisions

* Used surrogate keys instead of text joins for consistency
* Eliminated many-to-many relationships using a bridge table
* Maintained single-direction filtering for model stability
* Separated raw and transformed layers for clarity

---

# 📊 Key Insights Enabled

* Funding trends over time (Yearly & Monthly)
* Top startups by total funding
* Sector-wise investment distribution
* Investor contribution and activity analysis
* Multi-investor funding breakdown

---

# ⚠️ Challenges Faced

* Highly inconsistent investor data
* Multiple investors in a single field
* Ambiguous entries (e.g., “Undisclosed”, “Others”)
* Encoding and formatting issues
* Need for manual cleaning decisions

---

# 💡 Key Learnings

* Data modeling is more critical than visualization for accurate insights
* Real-world datasets are inherently messy and require structured cleaning pipelines
* Proper use of surrogate keys ensures scalability and consistency
* Bridge tables are essential for handling many-to-many relationships
* Small data quality issues can significantly distort business insights
* Separating data preparation (Power Query / Python) from analysis improves reliability

---

# 🛠️ Tools & Technologies

* Power BI (Dashboard & Data Modeling)
* Power Query (ETL)
* DAX (Data Analysis Expressions)
* Python (Jupyter Notebook for EDA)
* Matplotlib / Seaborn (data visualization during EDA)
* Pandas (data manipulation)
* Excel (Basic cleaning)
* Git & GitHub (version control and documentation)

---

# 🚀 Business Value

This project enables:

* Accurate tracking of funding trends across years
* Identification of key investors and their investment patterns
* Better understanding of high-growth sectors
* Reliable decision-making support for:

  * Investors
  * Startup analysts
  * Business strategists

---

# 🔮 Future Improvements

* Investor classification (VC, Angel, Corporate, Individual)
* Standardization of investor naming (entity resolution)
* Advanced KPIs (growth rate, funding velocity)
* Integration with live datasets (real-time analytics)
* Predictive modeling for funding trends using machine learning

---

# 🏁 Conclusion

This project focuses on transforming raw and unstructured data into a structured and scalable analytical model. By addressing data quality issues and implementing a robust schema, it ensures accurate, reliable, and meaningful insights.

---

# 🚀 END

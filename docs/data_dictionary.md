# 📊 Data Dictionary — Indian Startup Funding (2015–2019)

---

# 🧠 1. Overview

This project analyzes startup funding trends in India using a cleaned and structured dataset derived from the Kaggle Indian Startup Funding dataset.

The project includes:

* Raw data cleaning
* Data transformation
* Star schema modeling
* Bridge table implementation for many-to-many relationships

---

# 📂 2. Source

* **Dataset:** Kaggle — Indian Startup Funding Dataset
* **Time Period:** 2015–2019
* **Total Rows:** 3,035
* **Final Columns (raw cleaned):** 11

---

# 🧾 3. Raw Dataset (After Cleaning)

| Column                 | Type     | Description                      | Example          |
| ---------------------- | -------- | -------------------------------- | ---------------- |
| `date`                 | datetime | Date of funding announcement     | 2017-05-12       |
| `startup_name`         | string   | Name of the funded startup       | Flipkart         |
| `industry_vertical`    | string   | Primary sector                   | E-Commerce       |
| `subvertical`          | string   | Sub-category within sector       | Grocery Delivery |
| `country`              | string   | Stratup location                 | India            |
| `city /state location` | string   | Startup location                 | Bangalore        |
| `investors_name`       | string   | Investor names (comma-separated) | Ratan Tata       |
| `investment_type`      | string   | Funding stage                    | Seed Funding     |
| `amount_in_usd`        | Int64    | Funding amount (nullable)        | 1500000          |
| `year`                 | int      | Extracted from date              | 2017             |
| `month`                | string   | Extracted from date              | January          |

---

# ⚠️ 4. Raw Data Challenges

* Multiple investors stored in a single column
* Inconsistent text formatting
* Presence of null and undisclosed values (~35% in funding amount)
* Encoding issues and noisy entries
* No primary/foreign keys available

---

# 🔄 5. Data Transformation

The dataset was transformed to enable scalable analysis:

### Key Steps:

* Split multi-investor column into individual rows
* Standardized text (Trim, Clean, Case normalization)
* Removed ambiguous entries (e.g., “Undisclosed”, “Others”)
* Created surrogate keys:

  * `startup_id`
  * `type_id`
  * `investors_id`
* Built dimension tables from cleaned data

---

# 🧩 6. Data Model (Star Schema)

The final model follows a **star schema with a bridge table** to handle many-to-many relationships.

---

## 🔹 6.1 fact_funding

| Column          | Description              |
| --------------- | ------------------------ |
| funding_id (PK) | Unique funding event     |
| startup_id (FK) | Links to startup         |
| type_id (FK)    | Links to investment type |
| date            | Funding date             |
| amount_in_usd   | Funding amount           |

---

## 🔹 6.2 dim_startup

| Column            | Description               |
| ----------------- | ------------------------- |
| startup_id (PK)   | Unique startup identifier |
| startup_name      | Startup name              |
| industry_vertical | Industry                  |
| subvertical       | Sub-category              |
| city              | Location                  |

---

## 🔹 6.3 dim_investment_type

| Column          | Description            |
| --------------- | ---------------------- |
| type_id (PK)    | Unique funding type ID |
| investment_type | Funding stage          |

---

## 🔹 6.4 dim_date

| Column    | Description |
| --------- | ----------- |
| date (PK) | Date        |
| year      | Year        |
| month     | Month       |

---

## 🔹 6.5 dim_investors

| Column           | Description           |
| ---------------- | --------------------- |
| investors_id (PK) | Unique investor ID    |
| investors_name    | Cleaned investor name |

---

## 🔹 6.6 bridge_investor

| Column           | Description   |
| ---------------- | ------------- |
| funding_id (FK)  | Funding event |
| investors_id (FK) | Investor      |

---

# 🔗 7. Relationships

| From                                   | To          | Type       |
| -------------------------------------- | ----------- | ---------- |
| fact_funding → dim_startup             | startup_id  | Many → One |
| fact_funding → dim_investment_type     | type_id     | Many → One |
| fact_funding → dim_date                | date        | Many → One |
| fact_funding → bridge_investor | funding_id  | One → Many |
| dim_investors → bridge_investor | investor_id | One → Many |

---

# ⚙️ 8. Design Decisions

* Star schema chosen for performance and clarity
* Surrogate keys used to avoid text-based joins
* Bridge table implemented for investor relationships
* Single-direction filtering to prevent ambiguity

---

# 🚀 9. Key Outcomes

* Accurate investor-level analysis
* No duplication of funding values
* Scalable and interview-ready data model
* Clean separation between fact and dimensions

---

# 📌 10. Limitations

* Some investor names remain ambiguous (individuals vs firms)
* “Undisclosed” values reduce completeness of analysis
* Manual standardization required for certain entities

---

# 🏁 END

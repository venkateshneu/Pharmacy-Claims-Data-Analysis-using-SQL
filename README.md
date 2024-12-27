# Pharmacy-Claims-Data-Analysis-using-SQL

# Pharmacy Claims Data Normalization and Analysis

## Introduction
This project organizes and analyzes pharmacy claims data using a relational database approach. The raw data was normalized into **Third Normal Form (3NF)** to eliminate redundancies and improve query efficiency. A **star schema** was created with fact and dimension tables, facilitating business analysis with insights into prescription trends, member demographics, and insurance payments.

---

## Part 1: Data Normalization
### Step 1: From Unnormalized Data to 1NF
- The original data violated the **First Normal Form (1NF)** due to repeating groups for fill dates, copays, and insurance payments.  
- Solution: Flattened repeating groups into individual rows containing atomic data.

### Step 2: From 1NF to 2NF
- Split the table into two, ensuring that all non-key attributes were fully dependent on the **Primary Key (PK)**.

### Step 3: Achieving 3NF
- Further decomposed tables to eliminate transitive dependencies.  
- Final schema includes:
  - **1 Fact Table**: `fact_drug.csv`
  - **4 Dimension Tables**:
    - `dim_member.csv`
    - `dim_drug_ndc.csv`
    - `dim_drug_form_code.csv`
    - `dim_brand_generic.csv`

#### Fact Table Details
- **Grain**: Captures individual prescription fill events.
- **Additive Facts**:
  - `Copay`: Can be summed across dimensions.
  - `InsurancePaid`: Total insurance coverage across dimensions.

---

## Part 2: Database Setup
### Steps Taken
1. Imported the 3NF-structured CSV files into a MySQL database named `final_project`.
2. Converted Excel files to CSV format for seamless integration.

### Foreign Key Constraints
| Foreign Key                   | On DELETE Action | On UPDATE Action | Justification                                           |
|-------------------------------|------------------|------------------|-------------------------------------------------------|
| `fact_drug.member_id`         | SET NULL         | CASCADE          | Keeps historical data intact; cascades updates.       |
| `fact_drug.drug_ndc`          | SET NULL         | CASCADE          | Nullifies references to deleted drugs; ensures consistency. |
| `fact_drug.drug_form_code`    | SET NULL         | CASCADE          | Retains historical integrity for deleted drug forms.  |
| `fact_drug.drug_brand_generic_code` | SET NULL   | CASCADE          | Maintains integrity by nullifying deleted brand codes.|

### Data Conversion
- Converted `fill_date` and `member_birth_date` to **MySQL DATE** type for efficient queries.
- Adjusted column data types (e.g., `VARCHAR(100)`) to comply with MySQL constraints.

---

## Part 3: Queries and Insights
### Query 1: Prescriptions Grouped by Drug Name
- Example Insight: A total of **5 prescriptions** were filled for the drug **Ambien**.

### Query 2: Member Demographics
- **1 unique member** over the age of 65 filled **6 prescriptions**.

### Query 3: Recent Prescription Analysis
- The latest prescription for member ID **10003**:
  - Drug: **Ambien**
  - Insurance Payment: **322**

---

## Conclusion
The normalized database supports efficient querying and reporting by:
1. Eliminating redundancies through 3NF normalization.
2. Creating a well-organized star schema for analytical tasks.

The database design aligns with industry best practices, ensuring data integrity and enabling actionable insights for pharmacy claims management.

---

## References
- Ben-Gan, I. (2020). SQL Server 2019: The complete guide to database normalization.  
  [SQL Server Central](https://www.sqlservercentral.com/articles/sql-server-2019-the-complete-guide-to-database-normalization)

---

## How to Use
1. Clone the repository and import the `CSV` files into MySQL.
2. Execute the provided SQL queries for analysis.
3. Customize queries to derive further insights.

---

## Contact
For questions or collaboration, please reach out at [your-email@example.com].

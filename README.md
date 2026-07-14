# 🏦 Banking Loan Portfolio & Risk Analysis SQL Project

A production-grade SQL project designed to simulate core banking database management, customer credit profiling, and loan risk analysis. This project models a financial dataset using **PostgreSQL** to extract deep business insights regarding customer borrowing behavior, geographic risk exposure, and product demand metrics.

---

## 📌 Project Overview

This project models a retail and commercial banking lending pipeline to track credit distribution, analyze operational risk, and optimize loan product performance.

The analytical infrastructure bridges three vital banking domains:

* 👥 **Customer Demographics:** Risk assessment profiles including age, employment types, regional locations, annual salaries, and credit rankings.
* 📦 **Loan Products:** Strategic structuring constraints including baseline rates, baseline regulatory credit criteria, and maturity caps.
* 💼 **Loan Portfolio Master:** Live transaction books logging individual accounts, active variables (sanctioned principal volumes, applied margin rates), and servicing status indicators.

---

## 🗂️ Database Schema & Architecture

### 1. Customer Demographics (`customer_demographics.csv`)

| Column | Type | Constraints | Description |
| --- | --- | --- | --- |
| `CustomerID` | VARCHAR(100) | PRIMARY KEY | Unique global customer key |
| `CustomerName` | VARCHAR(100) | NOT NULL | Full customer name |
| `Age` | INT | Check (>0) | Age of the account holder |
| `Gender` | VARCHAR(100) | - | Gender classification |
| `MaritalStatus` | VARCHAR(100) | - | Legal marital status |
| `AnnualIncome_INR` | INT | - | Verifiable gross annual revenue |
| `EmploymentType` | VARCHAR(100) | - | Occupation category (e.g., Salaried, Self-Employed) |
| `CreditScore` | VARCHAR(100) | - | Bureau credit rating index |
| `GeographicRegion` | VARCHAR(100) | - | Customer's home city/state registry |

### 2. Loan Product Catalog (`loan_product_catalog.csv`)

| Column | Type | Constraints | Description |
| --- | --- | --- | --- |
| `LoanTypeID` | VARCHAR(100) | PRIMARY KEY | Unique loan product designator |
| `LoanTypeName` | VARCHAR(100) | NOT NULL | Public product title |
| `BaseInterestRate_Pct` | NUMERIC(10,2) | - | Minimum floor baseline interest rate |
| `MinCreditScoreRequired` | INT | - | Policy underwriting risk barrier |
| `MaxTerm_Months` | INT | - | Maximum legally permitted amortization period |

### 3. Loan Portfolio Master (`loan_portfolio_master.csv`)

| Column | Type | Constraints | Description |
| --- | --- | --- | --- |
| `LoanID` | VARCHAR(100) | PRIMARY KEY | Unique lending ledger agreement ID |
| `CustomerID` | VARCHAR(100) | REFERENCES Customer | Borrowing client account linkage |
| `LoanTypeID` | VARCHAR(100) | REFERENCES Product | Associated underwriting product schema |
| `LoanAmount_INR` | INT | NOT NULL | Absolute total principal sanctioned |
| `InterestRate_Pct` | NUMERIC(10,2) | - | Final contracted individual interest rate |
| `Term_Months` | VARCHAR(100) | - | Selected loan maturity profile |
| `StartDate` | DATE | - | Capital disbursement execution date |
| `LoanStatus` | VARCHAR(100) | - | Book status (e.g., Active, Fully Paid, Delinquent) |

---

## 📂 Project Structure

```text
Banking-Loan-Portfolio-SQL/
│
└── README.md    
├── Banking_Loan_Analysis.sql   # Comprehensive DDL tables & 28 business analytics queries
├── customer_demographics.csv    # Raw credit profile data 
├── loan_product_catalog.csv    # Corporate interest rates & underwriting criteria data
├── loan_portfolio_master.csv   # Historical/live ledger transaction records

```
## 📸 Project Screesnhots
![Image Alt](https://github.com/rohitkumardhawan/Banking-Loan-Portfolio-Risk-Analysis-SQL-Project/blob/3cd6cfb30068095f2b60fd8db226b8a1cf350c29/Screenshot%202026-07-06%20153144.png)

![Image Alt](https://github.com/rohitkumardhawan/Banking-Loan-Portfolio-Risk-Analysis-SQL-Project/blob/3cd6cfb30068095f2b60fd8db226b8a1cf350c29/Screenshot%202026-07-06%20153231.png)

![Image Alt](https://github.com/rohitkumardhawan/Banking-Loan-Portfolio-Risk-Analysis-SQL-Project/blob/3cd6cfb30068095f2b60fd8db226b8a1cf350c29/Screenshot%202026-07-06%20153256.png)


## 🚀 How to Run & Set Up This Project

Follow these instructions to reconstruct the banking relational database and run the risk analysis scripts locally on your machine using **PostgreSQL** and **pgAdmin 4**:

### 1. Prerequisites
* **Database Management System:** PostgreSQL (v14 or higher recommended) installed.
* **Database Client:** pgAdmin 4 or any preferred IDE (e.g., DBeaver, DataGrip).
* Ensure you have downloaded the project repository containing the `.sql` and `.csv` files.

### 2. Create the Banking Database
1. Launch **pgAdmin 4** and connect to your active local PostgreSQL server instance.
2. In the left-hand Browser panel, right-click on **Databases** ➔ Select **Create** ➔ **Database...**
3. Set the database name to `indian_banking_portfolio` and click **Save**.

### 3. Initialize the Tables (DDL)
1. Right-click on your newly created `indian_banking_portfolio` database and select **Query Tool**.
2. Open the script file `Indian Banking Loan Portfolio.sql` inside the Query Tool (or copy-paste the structural setup code containing the `CREATE TABLE` commands).
3. Execute the initial blocks of code up to the `INSERT INTO loan_product` query by clicking the **Execute/Play button** (or pressing `F5`). This builds your tables and manually inserts the baseline loan products.

### 4. Data Ingestion Pipeline (CSV Imports)
Because this is an interconnected relational database schema, **you must populate the tables in this specific sequential order** to satisfy entity dependencies:

1. **Customer Demographics:** 
   * Right-click the `customer_demographic` table ➔ select **Import/Export Data...**
   * Toggle the switch to **Import**. Select your local path to `customer_demographics.csv`.
   * Set the format to **csv**, enable the **Header** toggle, and set the delimiter to a comma `,`. Click **OK**.
2. **Loan Products:** 
   *(Note: The basic product catalog values are handled via the INSERT statement in your script. If your catalog expanding file `loan_product_catalog.csv` contains additional rows, import it into `loan_product` using the same settings as above.)*
3. **Loan Portfolio Master:**
   * Right-click the `loan_portfolio` table ➔ select **Import/Export Data...**
   * Toggle to **Import** and target your local `loan_portfolio_master.csv` file. 
   * Turn on **Header**, confirm the comma delimiter, and click **OK**.

### 5. Executing Risk & Portfolio Diagnostics
* Once all datasets are successfully ingested, navigate down through the `Indian Banking Loan Portfolio.sql` script to access queries 1 through 28.
* Highlight any target query block (such as *Query 22: Rank customers using Window Functions* or *Query 20: Analyze average credit scores*) and press `F5` or click **Execute**. 
* Review the resulting metrics directly inside the **Data Output** console pane below your query space.
---

## 📊 SQL Concepts Implemented

* **DDL & Database Housekeeping:** `DROP TABLE IF EXISTS`, transactional resets using `TRUNCATE ... CASCADE`.
* **Advanced Aggregations:** Matrix evaluations utilizing `SUM()`, `AVG()`, `COUNT(DISTINCT)`, `MAX()`, and `MIN()`.
* **Relational Multi-Join Queries:** Consolidating business intelligence by chaining multiple `INNER JOIN` and `LEFT JOIN` operations across customer, product, and portfolio tables.
* **Window Functions (Advanced Analytics):** Deploying analytics partitions like `RANK() OVER (ORDER BY ...)` to establish tiered borrowing hierarchies.
* **Conditional Parsing:** Utilizing type casting `CAST(As INT)` and missing value handling via `COALESCE()`.
* **Set Filtering & Range Management:** `IN()`, comparison matrices (`>`), and programmatic sorting configurations (`ORDER BY DESC LIMIT`).

---

## 📈 Key Business Questions Resolved

The SQL script contains a deep analytical path resolving operational banking requirements:

### 🔹 Credit Profiling & Geographic Exposure

* **Geographic Target Extraction:** Isolates active consumer registries stationed in high-density tier-1 economic hubs (*Mumbai, Pune, Bengaluru*).
* **Affluence & High-Net-Worth Identification:** Filters account owners claiming an annual household income clearing *₹7,00,000*.
* **Portfolio Concentration Mapping:** Segregates absolute total credit volume allocation grouped by state jurisdictions to isolate geographical risk.

### 🔹 Product Performance & Asset Class Analytics

* **Asset Class Popularity Indexing:** Ranks loan catalog items programmatically based on market volume penetration to target low-performing products.
* **Operational Margin Spread Diagnostics:** Evaluates historical variations by contrasting maximum sanctioned capital outlays against absolute minimum interest rates recorded per product.
* **Underwriter Score Audits:** Dynamically parses and converts data types to calculate true mathematical mean customer credit bureau scores per asset category.

### 🔹 Borrower Risk & Customer Lifetime Value (CLV)

* **Concentration Risk (Multi-Loan Accounts):** Isolates high-leverage clients holding more than one active lending facility simultaneously.
* **Demographic Velocity Vectors:** Audits aggregate capital consumption trends relative to chronological ages to isolate peak life-cycle borrowing thresholds.
* **Corporate Liquidity Hierarchies:** Generates ranked lists using **Window Functions** to isolate the top-tier enterprise accounts driving overall portfolio utilization.

---

## 🎯 Portfolio Highlights & Frameworks Demonstrated

* **Financial Data Management:** Experience constructing scalable tables handling correct financial data types like `NUMERIC(10,2)` for fractional percentage accuracy.
* **Underwriting Data Quality:** Demonstrates understanding of structural integrity by accounting for duplicate entity names through unique customer identification keys (`COUNT(DISTINCT CustomerID)`).
* **Risk Reporting:** Formulates logic to check portfolio exposure metrics that simulate direct workflows executed by Credit Risk Analysts and Business Intelligence teams.

---

## 📌 Planned Enhancements

* Design database views (`CREATE VIEW`) summarizing standard risk-weighted asset classifications.
* Implement strict operational `FOREIGN KEY` constraints to prevent orphan data entries across dependencies.
* Build indexing pipelines (`CREATE INDEX`) on frequently grouped variables (`CustomerID`, `LoanTypeID`) to benchmark performance queries on larger sets.

---

## 👤 Portfolio Profile

This project showcases data processing capabilities vital for **Data Analytics, Financial Technology (FinTech), Banking Intelligence, and Credit Risk Analysis** settings.

If you find this repository helpful for portfolio guidance, please leave a ⭐ on GitHub!

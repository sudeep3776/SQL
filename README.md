# Project Title

# Insurance Domain SQL Analytics | Relational Database Analysis Project

# Data used 
-<a href ="https://github.com/sudeep3776/SQL/blob/main/Insurance%20Analytics%20Project%20(1).xlsx">Dataset view 

-<a href ="https://github.com/sudeep3776/SQL/blob/main/Insurance%20project%20sql.sql">Dashboard view 

Screenshot <img width="1082" height="767" alt="Screenshot dashboard" src="https://github.com/user-attachments/assets/049e661d-1611-49d2-b689-128e66129b33" />


# Brief One-Line Summary
An end-to-end SQL project that queries a normalized insurance database to answer 10 critical business questions — covering total policies, customer segmentation, policy expiry alerts, premium growth trends, claim status, and payment tracking.

# Overview
This project simulates the kind of ad-hoc SQL analysis an insurance company's data or business analyst would perform on a production database. Working with three core relational tables — customers, policy_details, and claims/payments — the project answers real operational and strategic business questions using MySQL.
Each query is written to be clean, purposeful, and stakeholder-ready. The analysis covers the full insurance business cycle: from customer onboarding and policy issuance, through premium collection and mid-policy management, to claims processing and payment tracking.

# Problem Statement
## Insurance companies manage thousands of policies, customers, and claims simultaneously. Without structured data analysis, key business questions go unanswered:

How many active policies and unique customers does the company hold?

Which age groups and genders hold the most policies — and are we targeting the right demographics?

Which policy types are most popular, and which are expiring soon (renewal risk)?

Is premium revenue growing year-over-year?

What proportion of claims are approved, rejected, or pending — and what is the total claims liability?

 Are customers paying on time, and how many policies have payment issues?

### This project answers all of the above using structured SQL queries on a normalized relational database.


# Database: 
MySQL | Schema: Insurance domain with 4 relational tables joined via customer_id and policy_id


# Tools & Technologies

ToolPurposeMySQLPrimary database and query engineMySQL WorkbenchQuery writing, execution, and result visualizationSQLSELECT, JOIN, GROUP BY, ORDER BY, WHERE, BETWEEN, YEAR(), SUM(), COUNT(), DISTINCTExcel / Power BI (optional)Result export and visualization layer

# Methods

Database Design

Normalized relational schema with 4 tables linked by primary and foreign keys
customers ← policy_details ← claims / payments (star-like structure)

## SQL Techniques Applied
TechniqueUsed ForCOUNT(DISTINCT ...)Accurate unique counts (customers, policies)JOIN (INNER)Merging customer demographics with policy recordsGROUP BYAggregating by age bucket, gender, policy type, claim status, payment status, yearORDER BY ... DESCRanking policy types and statuses by volumeWHERE ... BETWEENFiltering policies expiring within 2026 for renewal alertsYEAR(date_column)Extracting year from dates for time-series premium trendSUM()Calculating total premium revenue and total claim liability
Query Workflow

### KPI-level counts (total policies, total customers)
### Demographic segmentation (age bucket, gender)
### Product analysis (policy type distribution)
### Operational alerts (policies expiring in 2026)
### Financial tracking (premium growth by year, total claim amount)
### Claims & payments pipeline (status-wise distribution)


# Key Insights
## Business QuestionSQL OutputInsight
Q1 Total PoliciesCOUNT(policy_id) from policy_detailsSingle KPI — baseline size of the portfolio

Q2 Total CustomersCOUNT(DISTINCT customer_id)Unique customer base — detects multi-policy holders

Q3 Age Bucket → Policy CountJOIN + GROUP BY age_bucketIdentifies which age group is the most insured — drives product targeting

Q4 Gender → Policy CountJOIN + GROUP BY genderReveals gender skew — useful for product design and marketing

Q5 Policy Type → CountGROUP BY policy_type ORDER BY DESCRanks Health / Life / Motor / Travel by volume — shows core product lines

Q6 Policies Expiring in 2026WHERE policy_end_date BETWEEN Jan–Dec 2026Renewal risk alert — proactively identifies at-risk revenue

Q7 Premium Growth by YearYEAR(policy_start_date) + SUM(premium_amount)Time-series view of premium revenue — shows business growth trajectory

Q8 Claim Status DistributionGROUP BY claim_statusSplit of Approved / Rejected / Pending claims — measures claims efficiency

Q9 Payment Status DistributionGROUP BY payment_statusTracks Paid / Unpaid / Overdue — flags collection riskQ10Total Claim AmountSUM(claim_amount)Total financial liability — critical for actuarial and reserve planning


# How to Run This Project
Requirements: MySQL Server + MySQL Workbench (both free)
sql-- Step 1: Install MySQL and open MySQL Workbench

-- Step 2: Create the database schema
CREATE DATABASE insurance_db;
USE insurance_db;

-- Step 3: Create the 4 tables
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    gender VARCHAR(10),
    age_bucket VARCHAR(20)
);

CREATE TABLE policy_details (
    policy_id INT PRIMARY KEY,
    customer_id INT,
    policy_type VARCHAR(50),
    policy_start_date DATE,
    policy_end_date DATE,
    premium_amount DECIMAL(10,2),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

CREATE TABLE claims (
    claim_id INT PRIMARY KEY,
    policy_id INT,
    claim_amount DECIMAL(10,2),
    claim_status VARCHAR(20),
    FOREIGN KEY (policy_id) REFERENCES policy_details(policy_id)
);

CREATE TABLE payments (
    payment_id INT PRIMARY KEY,
    policy_id INT,
    payment_status VARCHAR(20),
    FOREIGN KEY (policy_id) REFERENCES policy_details(policy_id)
);

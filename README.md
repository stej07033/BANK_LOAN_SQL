# 🏦 Bank Loan Analysis Using SQL

## 📌 Project Overview

This project focuses on analyzing **bank loan data using SQL** to generate meaningful business insights and Key Performance Indicators (KPIs).

The analysis covers loan applications, funded amounts, received payments, interest rates, DTI, Good Loans, Bad Loans, loan status, monthly trends, states, loan terms, employee length, loan purposes, home ownership, and loan grade analysis.

---

# 🎯 Project Objectives

The main objectives of this project are:

* Analyze total loan applications
* Calculate total funded loan amount
* Calculate total amount received
* Calculate average interest rate
* Calculate average DTI
* Compare MTD and PMTD loan performance
* Identify Good Loans
* Identify Bad Loans
* Analyze loan status
* Analyze monthly loan trends
* Analyze loan performance by state
* Analyze loan terms
* Analyze employee length
* Analyze loan purposes
* Analyze home ownership
* Analyze loan grade performance
* Apply filters for detailed business analysis

---

# 🛠️ Tools & Technologies

* **SQL**
* **MySQL / SQL Server**
* **GitHub**
* **Bank Loan Dataset**

### SQL Concepts Used

* SELECT
* WHERE
* GROUP BY
* ORDER BY
* COUNT()
* SUM()
* AVG()
* CASE WHEN
* Aggregate Functions
* Date Functions
* Conditional Aggregation

---

# 📊 A. BANK LOAN REPORT — SUMMARY

## 1️⃣ Total Loan Applications

Calculates the total number of loan applications.

'''
SELECT COUNT(ID) AS total_loan_appications
FROM Bank_loan_data;
'''

---

## 2️⃣ MTD Loan Applications

Calculates the total loan applications for December.

'''
SELECT COUNT(ID) AS total_mtd_applications
FROM Bank_loan_data
WHERE MONTH(issue_date) = 12;
'''

---

## 3️⃣ PMTD Loan Applications

Calculates the total loan applications for November.

'''
SELECT COUNT(ID) AS total_ptmd_applications
FROM Bank_loan_data
WHERE MONTH(issue_date) = 11;
'''

---

## 4️⃣ Total Funded Amount

Calculates the total amount funded through loans.

'''
SELECT SUM(loan_amount) AS total_loan_amount
FROM Bank_loan_data;
'''

---

## 5️⃣ MTD Total Funded Amount

Calculates the total funded amount for December.

'''
SELECT SUM(loan_amount) AS total_mtd_funded_amount
FROM Bank_loan_data
WHERE MONTH(issue_date) = 12;
'''

---

## 6️⃣ PMTD Total Funded Amount

Calculates the total funded amount for November.

'''
SELECT SUM(loan_amount) AS total_pmtd_funded_amount
FROM Bank_loan_data
WHERE MONTH(issue_date) = 11;
'''

---

## 7️⃣ Total Amount Received

Calculates the total amount received from borrowers.

'''
SELECT SUM(total_payment) AS total_loan_amount
FROM Bank_loan_data;
'''

---

## 8️⃣ MTD Total Amount Received

'''
SELECT SUM(total_payment) AS mtd_total_amount_received
FROM Bank_loan_data
WHERE MONTH(issue_date) = 12;
'''

---

## 9️⃣ PMTD Total Amount Received

'''
SELECT SUM(total_payment) AS pmtd_total_amount_received
FROM Bank_loan_data
WHERE MONTH(issue_date) = 11;
'''

---

## 🔟 Average Interest Rate

Calculates the average interest rate.

'''
SELECT ROUND(AVG(int_rate),4) * 100 AS avg_interest_rate
FROM Bank_loan_data;
'''

---

## 1️⃣1️⃣ MTD Average Interest Rate

'''
SELECT ROUND(AVG(int_rate),4) * 100 AS mtd_avg_interest_rate
FROM Bank_loan_data
WHERE MONTH(issue_date) = 12;
'''

---

## 1️⃣2️⃣ PMTD Average Interest Rate

'''
SELECT ROUND(AVG(int_rate),4) * 100 AS pmtd_avg_interest_rate
FROM Bank_loan_data
WHERE MONTH(issue_date) = 11;
'''

---

## 1️⃣3️⃣ Average DTI

Calculates the average Debt-to-Income ratio.

'''
SELECT ROUND(AVG(DTI),4) * 100 AS avg_dti_rate
FROM Bank_loan_data;
'''

---

## 1️⃣4️⃣ MTD Average DTI

'''
SELECT ROUND(AVG(DTI),4) * 100 AS mtd_avg_dti_rate
FROM Bank_loan_data
WHERE MONTH(issue_date) = 12;
'''

---

## 1️⃣5️⃣ PMTD Average DTI

'''
SELECT ROUND(AVG(DTI),4) * 100 AS pmtd_avg_dti_rate
FROM Bank_loan_data
WHERE MONTH(issue_date) = 11;
'''

---

# ✅ GOOD LOAN ANALYSIS

Good Loans are identified using:

* **Fully Paid**
* **Current**

## Good Loan Percentage

'''
SELECT
(COUNT(
CASE
WHEN loan_status = 'Fully Paid'
OR loan_status = 'Current'
THEN id
END
) * 100) / COUNT(ID) AS total_loan_percentage
FROM Bank_loan_data;
'''

---

## Good Loan Applications

'''
SELECT COUNT(ID) AS good_loan_applications
FROM Bank_loan_data
WHERE loan_status = 'Fully Paid'
OR loan_status = 'Current';
'''

---

## Good Loan Funded Amount

'''
SELECT SUM(loan_amount) AS total_amount
FROM Bank_loan_data
WHERE loan_status = 'Fully Paid'
OR loan_status = 'Current';
'''

---

## Good Loan Amount Received

'''
SELECT SUM(total_payment) AS total_amount
FROM Bank_loan_data
WHERE loan_status = 'Fully Paid'
OR loan_status = 'Current';
'''

---

# ❌ BAD LOAN ANALYSIS

Bad Loans are identified using:

* **Charged Off**

## Bad Loan Percentage

'''
SELECT
(COUNT(
CASE
WHEN loan_status = 'Charged Off'
THEN id
END
) * 100) / COUNT(ID) AS total_loan_percentage
FROM Bank_loan_data;
'''

---

## Bad Loan Applications

'''
SELECT COUNT(ID) AS bad_loan_applications
FROM Bank_loan_data
WHERE loan_status = 'Charged Off';
'''

---

## Bad Loan Funded Amount

'''
SELECT SUM(loan_amount) AS total_amount
FROM Bank_loan_data
WHERE loan_status = 'Charged Off';
'''

---

## Bad Loan Amount Received

'''
SELECT SUM(total_payment) AS total_amount
FROM Bank_loan_data
WHERE loan_status = 'Charged Off';
'''

---

# 📈 LOAN STATUS ANALYSIS

This analysis provides:

* Loan applications
* Total funded amount
* Total amount received
* Average interest rate
* Average DTI

'''
SELECT
loan_status,
COUNT(id) AS total_applications,
SUM(loan_amount) AS total_funded_amount,
SUM(total_payment) AS total_recevied_amount,
ROUND(AVG(int_rate),4) * 100 AS avg_interest_rate,
ROUND(AVG(dti),4) * 100 AS avg_approval_rate
FROM bank_loan_data
GROUP BY loan_status;
'''

---

# 📅 MTD LOAN STATUS

'''
SELECT
loan_status,
SUM(loan_amount) AS MTD_funded_amount,
SUM(total_payment) AS MTD_recevied_amount
FROM Bank_loan_data
WHERE MONTH(issue_date) = 12
GROUP BY loan_status;
'''

---

# ⭐ GRADE ANALYSIS

Analyzes average funded and received amounts according to loan grade.

'''
SELECT
grade,
ROUND(AVG(loan_amount),4) * 100 AS avg_grade_funded_amount,
ROUND(AVG(total_payment),4) * 100 AS avg_grade_recevied_amount
FROM Bank_loan_data
GROUP BY grade;
'''

---

# 📊 B. BANK LOAN REPORT — OVERVIEW

## 📅 MONTHLY ANALYSIS

Analyzes loan applications, funded amounts, and received amounts by month.

'''
SELECT
MONTH(issue_date) AS month_number,
DATENAME(month, issue_date) AS month_name,
COUNT(id) AS total_loan_applications,
SUM(loan_amount) AS total_funded_amount,
SUM(total_payment) AS total_received_amount
FROM Bank_loan_data
GROUP BY
MONTH(issue_date),
DATENAME(month, issue_date)
ORDER BY MONTH(issue_date);
'''

---

# 🗺️ STATE ANALYSIS

Analyzes loan performance by state.

'''
SELECT
address_state,
COUNT(id) AS total_applications_by_state,
SUM(loan_amount) AS total_funded_amount_by_state,
SUM(total_payment) AS total_received_amount_by_state
FROM Bank_loan_data
GROUP BY address_state
ORDER BY address_state;
'''

---

# 📆 TERM ANALYSIS

Analyzes loan performance according to loan term.

'''
SELECT
TERM,
COUNT(id) AS total_applications,
SUM(loan_amount) AS total_funded_dif_term,
SUM(total_payment) AS total_received_dif_term
FROM Bank_loan_data
GROUP BY term;
'''

---

# 👨‍💼 EMPLOYEE LENGTH ANALYSIS

Analyzes loan performance according to employee length.

'''
SELECT
emp_length,
COUNT(id) AS total_applications,
SUM(loan_amount) AS total_funded_dif_emp_len,
SUM(total_payment) AS total_received_dif_emp_Len
FROM Bank_loan_data
GROUP BY emp_length
ORDER BY emp_length DESC;
'''

---

# 🎯 LOAN PURPOSE ANALYSIS

Analyzes loan applications according to purpose.

'''
SELECT
PURPOSE,
COUNT(id) AS total_applications,
SUM(loan_amount) AS total_funded_dif_emp_purpose,
SUM(total_payment) AS total_received_dif_purpose
FROM Bank_loan_data
GROUP BY purpose
ORDER BY purpose DESC;
'''

---

# 🏠 HOME OWNERSHIP ANALYSIS

Analyzes loan performance according to home ownership.

'''
SELECT
home_ownership,
COUNT(id) AS total_applications,
SUM(loan_amount) AS total_funded_dif_emp_home,
SUM(total_payment) AS total_received_dif_home
FROM Bank_loan_data
GROUP BY home_ownership
ORDER BY home_ownership;
'''

---

# 🔎 FILTER ANALYSIS

The project also supports filtering the analysis based on loan grade.

## Grade A Analysis

'''
SELECT
purpose AS PURPOSE,
COUNT(id) AS Total_Loan_Applications,
SUM(loan_amount) AS Total_Funded_Amount,
SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
WHERE grade = 'A'
GROUP BY purpose;
'''

---

# 💡 BUSINESS QUESTIONS

This project helps answer important business questions:

1. How many total loan applications were received?
2. What is the total amount funded?
3. What is the total amount received?
4. What is the average interest rate?
5. What is the average DTI?
6. What percentage of loans are Good Loans?
7. What percentage of loans are Bad Loans?
8. Which loan status has the highest number of applications?
9. Which states have the highest loan activity?
10. Which loan term is most common?
11. Which loan purposes receive the most funding?
12. How does employee length affect loan activity?
13. Which home ownership category has the highest applications?
14. How does loan grade affect loan performance?
15. How does loan performance change month by month?

---

# 📌 KEY INSIGHTS

The SQL analysis can be used to identify:

* Overall loan application performance
* Good Loan vs Bad Loan performance
* Monthly loan trends
* State-wise loan activity
* Loan term distribution
* Employee length distribution
* Loan purpose distribution
* Home ownership distribution
* Loan grade performance
* Funded amount vs received amount

---

# 📁 PROJECT STRUCTURE

'''
Bank-Loan-SQL-Analysis/
│
├── Bank_Loan_Data.csv
│
├── solutions.sql
│
├── README.md
│
└── Dashboard/
└── Bank_Loan_Dashboard.png
'''

---

# 🚀 SKILLS DEMONSTRATED

**SQL | Data Analysis | Business Analysis | KPI Development | Data Exploration | Aggregation | Conditional Logic | Date Analysis | Reporting**

---

# 👨‍💻 AUTHOR

**Sai M**

Aspiring Data Analyst

**Skills:**
SQL | Python | Excel | Power BI | PostgreSQL | Data Analytics

---

# 🔗 CONNECT WITH ME

### 💻 GitHub

https://github.com/stej07033

### 💼 LinkedIn

https://www.linkedin.com/posts/madanapalli-sai-19b835389

---

⭐ **If you find this project useful, please give the repository a star!**

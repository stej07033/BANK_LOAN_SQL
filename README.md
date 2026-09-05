# 🏦 Bank Loan Analysis — SQL Project

## 📌 Project Overview

This project focuses on analyzing **bank loan data using SQL** to generate meaningful business insights and Key Performance Indicators (KPIs).

---

## 🛠️ Tools & Technologies

* SQL
* MySQL / SQL Server
* GitHub
* Bank Loan Dataset

---

# 📊 Bank Loan Report — Summary

## 1. Total Loan Applications

'''
SELECT COUNT(ID) AS total_loan_appications
FROM Bank_loan_data;
'''

## 2. MTD Loan Applications

'''
SELECT COUNT(ID) AS total_mtd_applications
FROM Bank_loan_data
WHERE MONTH(issue_date) = 12;
'''

## 3. PMTD Loan Applications

'''
SELECT COUNT(ID) AS total_ptmd_applications
FROM Bank_loan_data
WHERE MONTH(issue_date) = 11;
'''

## 4. Total Funded Amount

'''
SELECT SUM(loan_amount) AS total_loan_amount
FROM Bank_loan_data;
'''

## 5. Total Received Amount

'''
SELECT SUM(total_payment) AS total_loan_amount
FROM Bank_loan_data;
'''

## 6. Average Interest Rate

'''
SELECT ROUND(AVG(int_rate),4) * 100 AS avg_interest_rate
FROM Bank_loan_data;
'''

## 7. Average DTI

'''
SELECT ROUND(AVG(DTI),4) * 100 AS avg_dti_rate
FROM Bank_loan_data;
'''

---

# ✅ Good Loan Analysis

### Good Loan Percentage

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

### Good Loan Applications

'''
SELECT COUNT(ID) AS good_loan_applications
FROM Bank_loan_data
WHERE loan_status = 'Fully Paid'
OR loan_status = 'Current';
'''

### Good Loan Funded Amount

'''
SELECT SUM(loan_amount) AS total_amount
FROM Bank_loan_data
WHERE loan_status = 'Fully Paid'
OR loan_status = 'Current';
'''

### Good Loan Received Amount

'''
SELECT SUM(total_payment) AS total_amount
FROM Bank_loan_data
WHERE loan_status = 'Fully Paid'
OR loan_status = 'Current';
'''

---

# ❌ Bad Loan Analysis

### Bad Loan Percentage

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

### Bad Loan Applications

'''
SELECT COUNT(ID) AS bad_loan_applications
FROM Bank_loan_data
WHERE loan_status = 'Charged Off';
'''

### Bad Loan Funded Amount

'''
SELECT SUM(loan_amount) AS total_amount
FROM Bank_loan_data
WHERE loan_status = 'Charged Off';
'''

### Bad Loan Received Amount

'''
SELECT SUM(total_payment) AS total_amount
FROM Bank_loan_data
WHERE loan_status = 'Charged Off';
'''

---

# 📈 Loan Status Analysis

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

# 📅 MTD Loan Status

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

# ⭐ Grade Analysis

'''
SELECT
grade,
ROUND(AVG(loan_amount),4) * 100 AS avg_grade_funded_amount,
ROUND(AVG(total_payment),4) * 100 AS avg_grade_recevied_amount
FROM Bank_loan_data
GROUP BY grade;
'''

---

# 📊 Monthly Analysis

'''
SELECT
MONTH(issue_date) AS month_number,
DATENAME(month, issue_date) AS month_name,
SUM(loan_amount) AS total_funded_amount,
SUM(total_payment) AS total_recevied_amount
FROM Bank_loan_data
GROUP BY
MONTH(issue_date),
DATENAME(month, issue_date)
ORDER BY total_funded_amount, total_recevied_amount DESC;
'''

---

# 🗺️ State Analysis

'''
SELECT
address_state,
COUNT(id) AS total_applications_by_state,
SUM(loan_amount) AS total_funded_amount_by_state,
SUM(total_payment) AS total_received_amount_by_state
FROM Bank_loan_data
GROUP BY address_state
ORDER BY total_applications_by_state,
total_received_amount_by_state DESC;
'''

---

# 📆 Loan Term Analysis

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

# 👨‍💼 Employee Length Analysis

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

# 🎯 Loan Purpose Analysis

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

# 🏠 Home Ownership Analysis

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

# 🔎 Grade A Filter Analysis

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

# 📁 Project Structure

'''
Bank-Loan-SQL-Analysis/
│
├── Bank_Loan_Data.csv
├── solutions.sql
├── README.md
│
└── Dashboard/
└── Bank_Loan_Dashboard.png
'''

---

# 💡 Key Business Insights

* Analyze total loan applications
* Calculate funded and received amounts
* Compare MTD and PMTD performance
* Identify Good and Bad Loans
* Analyze loan status
* Analyze monthly trends
* Compare states and loan terms
* Analyze loan purposes
* Analyze employee length
* Analyze home ownership
* Analyze Grade A loans

---

# 👨‍💻 Author

**Sai M**

Aspiring Data Analyst
**SQL | Python | Excel | Power BI | Data Analytics**

⭐ If you find this project useful, consider giving the repository a star!

# 🏦 BANK LOAN ANALYSIS | SQL PROJECT

## 📌 Project Overview

This project focuses on analyzing **Bank Loan Data using SQL**.

The project contains SQL queries for:

* Bank Loan Report | Summary
* Total Loan Applications
* MTD & PTMD Loan Applications
* Total Funded Amount
* MTD & PTMD Funded Amount
* Total Received Amount
* MTD & PTMD Received Amount
* Average Interest Rate
* Average DTI
* Good Loan Analysis
* Bad Loan Analysis
* Loan Status Analysis
* MTD Loan Status
* Average Amount by Grade
* Monthly Analysis
* State Analysis
* Term Analysis
* Employee Length Analysis
* Purpose Analysis
* Home Ownership Analysis
* Grade A Filter Analysis

---

# 🛠️ Tools Used

* SQL
* MySQL / SQL Server
* GitHub
* Bank Loan Dataset

---

# 📊 A. BANK LOAN REPORT | SUMMARY

## Total Loan Applications

'''
-- Total loan applications

SELECT COUNT(ID) AS total_loan_appications
from Bank_loan_data;
'''

## MTD Loan Applications

'''
--MTD loan applications

SELECT COUNT(ID) AS total_mtd_applications
FROM Bank_loan_data
where month(issue_date) = 12;
'''

## PTMD Loan Applications

'''
--PTMD loan applications

SELECT COUNT(ID) AS total_ptmd_applications
from Bank_loan_data
where month(issue_date) = 11;
'''

## Total Funded Amount

'''
--Total funded amount

SELECT SUM(loan_amount) as total_loan_amount
from Bank_loan_data;
'''

## MTD Funded Amount

'''
--MTD funded amount

SELECT SUM(loan_amount) AS total_mtd_amount
FROM Bank_loan_data
where month(issue_date) = 12;
'''

## PTMD Funded Amount

'''
--PTMD funded amount

SELECT sum(loan_amount) AS total_ptmd_amount
from Bank_loan_data
where month(issue_date) = 11;
'''

## Total Received Amount

'''
--Total Recevied amount

SELECT SUM(total_payment) as total_loan_amount
from Bank_loan_data;
'''

## MTD Total Received Amount

'''
--MTD total Recevied amount

SELECT SUM(total_payment) AS total_mtd_amount
FROM Bank_loan_data
where month(issue_date) = 12;
'''

## PTMD Total Received Amount

'''
--PTMD total Recevied amount

SELECT sum(total_payment) AS total_ptmd_amount
from Bank_loan_data
where month(issue_date) = 11;
'''

## Average Interest Rate

'''
--int_rate avg interest rate

SELECT round(AVG(int_rate),4)*100 as avg_interest_rate
from Bank_loan_data;
'''

## MTD Average Interest Rate

'''
--MTD average interest rate

SELECT round(AVG(int_rate),4)*100 as avg_mtd_rate
from Bank_loan_data
where month(issue_date) = 12;
'''

## PTMD Average Interest Rate

'''
--PTMD average interest rate

SELECT round(AVG(int_rate),4)*100 as avg_ptmd_rate
from Bank_loan_data
where month(issue_date) = 11;
'''

## Average DTI Rate

'''
--Dti avg rate

SELECT round(AVG(DTI),4)*100 AS avg_dti_rate
from Bank_loan_data;
'''

## MTD Average DTI Rate

'''
--MTD dti avg_rate

SELECT round(AVG(Dti),4)*100 as avg_mtd_dti_rate
from Bank_loan_data
where month(issue_date) = 12;
'''

## PTMD Average DTI Rate

'''
--PTMD dit avg_rate

SELECT round(AVG(Dti),4)*100 as avg_ptmd_dti_rate
from Bank_loan_data
where month(issue_date) = 11;
'''

---

# ✅ GOOD LOAN ANALYSIS

## Good Loan Percentage

'''
---Good loan applications

SELECT
(COUNT(CASE WHEN loan_status = 'Fully Paid' or loan_status = 'Current' then id end) * 100)
/
COUNT(ID) AS total_loan_percentage
from Bank_loan_data;
'''

## Good Loan Applications

'''
--- Good loan applications

SELECT
COUNT(ID) AS good_loan_applications
from Bank_loan_data
where loan_status = 'Fully Paid' or loan_status = 'Current';
'''

## Good Loan Funded Amount

'''
--Good loan Funded amount

SELECT
SUM(loan_amount) as total_amount
from Bank_loan_data
where loan_status = 'Fully Paid' or loan_status = 'Current';
'''

## Good Loan Received Amount

'''
--Good recevied amount

SELECT
SUM(total_payment) as total_amount
from Bank_loan_data
where loan_status = 'Fully Paid' or loan_status = 'Current';
'''

---

# ❌ BAD LOAN ANALYSIS

## Bad Loan Percentage

'''
---Bad loan applications

SELECT
(COUNT(CASE WHEN loan_status = 'Charged Off' then id end) * 100)
/
COUNT(ID) AS total_loan_percentage
from Bank_loan_data;
'''

## Bad Loan Applications

'''
---Bad loan applications

SELECT
COUNT(ID) AS bad_loan_applications
from Bank_loan_data
where loan_status = 'Charged Off';
'''

## Bad Loan Funded Amount

'''
--Bad loan Funded amount

SELECT
SUM(loan_amount) as total_amount
from Bank_loan_data
where loan_status = 'Charged Off';
'''

## Bad Loan Received Amount

'''
--Bad recevied amount

SELECT
SUM(total_payment) as total_amount
from Bank_loan_data
where loan_status = 'Charged Off';
'''

---

# 📈 LOAN STATUS

'''
---Loan Status

SELECT loan_status,
count(id) as total_applications,
sum(loan_amount) as total_funded_amount,
sum(total_payment) as total_recevied_amount,
round(avg(int_rate),4)*100 as avg_interest_rate,
round(avg(dti),4)*100 as avg_approval_rate
from bank_loan_data
group by loan_status;
'''

---

# 📅 MTD LOAN STATUS

'''
---MTD loan status

SELECT loan_status,
sum(loan_amount) as MTD_funded_amount,
sum(total_payment) as MTD_recevied_amount
from Bank_loan_data
where MONTH(issue_date) = 12
group by loan_status;
'''

---

# ⭐ AVERAGE AMOUNT DIFFERENT GRADE

'''
---AVG amount different grade

SELECT grade,
round(avg(loan_amount),4)*100 as avg_grade_funded_amount,
round(avg(total_payment),4)*100 as avg_grade_recevied_amount
from Bank_loan_data
group by grade;
'''

---

# 📊 B. BANK LOAN REPORT | OVERVIEW

## MONTH

'''
---B.BANK LOAN REPORT | OVERVIEW

-- MONTH

SELECT month(issue_date) as month_number,
datename(month,issue_date) as month_name,
sum(loan_amount) as total_funded_amount,
sum(total_payment) as total_recevied_amount
from Bank_loan_data
group by month(issue_date),
datename(month,issue_date)
order by total_funded_amount,total_recevied_amount desc;
'''

---

# 🗺️ STATE

'''
-- STATE

SELECT address_state,
count(id) as total_applications_by_state,
sum(loan_amount) astotal_applications_by_state,
sum(total_payment) as total_received_amount_by_state
from Bank_loan_data
group by address_state
order by total_applications_by_state,
total_received_amount_by_state desc;
'''

---

# 📆 TERM

'''
--Term

SELECT TERM,
count(id) as total_applications,
sum(loan_amount) as total_funded_dif_term,
sum(total_payment) as total_received_dif_term
from Bank_loan_data
group by term;
'''

---

# 👨‍💼 EMPLOYEE LENGTH

'''
-- EMPLOYEE_LENGTH

SELECT emp_length,
count(id) as total_applications,
sum(loan_amount) as total_funded_dif_emp_len,
sum(total_payment) as total_received_dif_emp_Len
from Bank_loan_data
group by emp_length
order by emp_length desc;
'''

---

# 🎯 PURPOSE

'''
--PURPOSE

SELECT PURPOSE,
count(id) as total_applications,
sum(loan_amount) as total_funded_dif_emp_purpose,
sum(total_payment) as total_received_dif_purpose
from Bank_loan_data
group by purpose
order by purpose desc;
'''

---

# 🏠 HOME OWNERSHIP

'''
--HOME_OWNERSHIP

SELECT home_ownership,
count(id) as total_applications,
sum(loan_amount) as total_funded_dif_emp_home,
sum(total_payment) as total_received_dif_home
from Bank_loan_data
group by home_ownership
order by  home_ownership;
'''

---

# 🔎 GRADE A FILTER — DASHBOARD

'''
--See the results when we hit the Grade A in the filters for dashboards.

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

# 📁 PROJECT STRUCTURE

'''
Bank-Loan-SQL-Analysis/
│
├── Bank_Loan_Data.csv
│
├── solutions(1).sql
│
├── README.md
│
└── Dashboard/
└── Bank_Loan_Dashboard.png
'''

---

# 💡 BUSINESS INSIGHTS

This project can be used to analyze:

* Total loan applications
* Funded loan amounts
* Received loan amounts
* Interest rate performance
* DTI performance
* Good vs Bad loans
* Loan status
* Monthly loan trends
* State-wise loan performance
* Loan term performance
* Employee length
* Loan purpose
* Home ownership
* Loan grade performance

---

# 🚀 SKILLS DEMONSTRATED

**SQL | Data Analysis | KPI Analysis | Business Analysis | Aggregation | Conditional Logic | Date Functions | Data Exploration**

---

# 👨‍💻 AUTHOR

**Sai M**

Aspiring Data Analyst

**Skills:** SQL | Python | Excel | Power BI | PostgreSQL | Data Analytics

---

# 🔗 CONNECT WITH ME

### 💻 GitHub

https://github.com/stej07033

### 💼 LinkedIn

https://www.linkedin.com/posts/madanapalli-sai-19b835389

---

⭐ **If you find this project useful, please give the repository a star!**

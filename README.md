# 🏦 Bank Loan SQL Project

## 📌 Project Overview

This project contains SQL queries for analyzing **Bank Loan Data**.

The project covers loan applications, funded amounts, received amounts, interest rates, DTI, Good Loans, Bad Loans, Loan Status, Grade Analysis, Monthly Analysis, State Analysis, Term Analysis, Employee Length, Purpose, Home Ownership, and Grade A dashboard filtering.

---

# 🗂️ Schema

### Bank Loan Project

```sql
SELECT * FROM Bank_loan_data;
```

---

# 📊 A. BANK LOAN REPORT | SUMMARY

### -- Total loan applications

```sql
SELECT COUNT(ID) AS total_loan_appications
from Bank_loan_data;
```

### --MTD loan applications

```sql
SELECT COUNT(ID) AS total_mtd_applications
FROM Bank_loan_data
where month(issue_date) = 12;
```

### --PTMD loan applications

```sql
SELECT COUNT(ID) AS total_ptmd_applications
from Bank_loan_data
where month(issue_date) = 11;
```

### --Total funded amount

```sql
SELECT SUM(loan_amount) as total_loan_amount
from Bank_loan_data;
```

### --MTD funded amount

```sql
SELECT SUM(loan_amount) AS total_mtd_amount 
FROM Bank_loan_data
where month(issue_date) = 12;
```

### --PTMD funded amount

```sql
SELECT sum(loan_amount) AS total_ptmd_amount
from Bank_loan_data
where month(issue_date) = 11;
```

### --Total Recevied amount

```sql
SELECT SUM(total_payment) as total_loan_amount
from Bank_loan_data;
```

### --MTD total Recevied amount

```sql
SELECT SUM(total_payment) AS total_mtd_amount 
FROM Bank_loan_data
where month(issue_date) = 12;
```

### --PTMD total Recevied amount

```sql
SELECT sum(total_payment) AS total_ptmd_amount
from Bank_loan_data
where month(issue_date) = 11;
```

### --int_rate avg interest rate

```sql
SELECT round(AVG(int_rate),4)*100 as avg_interest_rate
from Bank_loan_data;
```

### --MTD average interest rate

```sql
SELECT round(AVG(int_rate),4)*100 as avg_mtd_rate
from Bank_loan_data
where month(issue_date) = 12;
```

### --PTMD average interest rate

```sql
SELECT round(AVG(int_rate),4)*100 as avg_ptmd_rate
from Bank_loan_data
where month(issue_date) = 11;
```

### --Dti avg rate

```sql
SELECT round(AVG(DTI),4)*100 AS avg_dti_rate
from Bank_loan_data;
```

### --MTD dti avg_rate

```sql
SELECT round(AVG(Dti),4)*100 as avg_mtd_dti_rate
from Bank_loan_data
where month(issue_date) = 12;
```

### --PTMD dit avg_rate

```sql
SELECT round(AVG(Dti),4)*100 as avg_ptmd_dti_rate
from Bank_loan_data
where month(issue_date) = 11;
```

---

# ✅ GOOD LOAN ANALYSIS

### ---Good loan applications

```sql
SELECT 
     (COUNT(CASE WHEN loan_status = 'Fully Paid' or loan_status = 'Current' then id end) * 100)
     /
     COUNT(ID) AS total_loan_percentage
from Bank_loan_data;
```

### --- Good loan applications

```sql
SELECT 
   COUNT(ID) AS good_loan_applications
from Bank_loan_data
where loan_status = 'Fully Paid' or loan_status = 'Current';
```

### --Good loan Funded amount

```sql
SELECT 
    SUM(loan_amount) as total_amount
from Bank_loan_data
where loan_status = 'Fully Paid' or loan_status = 'Current';
```

### --Good recevied amount

```sql
SELECT 
    SUM(total_payment) as total_amount
from Bank_loan_data
where loan_status = 'Fully Paid' or loan_status = 'Current';
```

---

# ❌ BAD LOAN ANALYSIS

### ---Bad loan applications

```sql
SELECT 
     (COUNT(CASE WHEN loan_status = 'Charged Off' then id end) * 100)
     /
     COUNT(ID) AS total_loan_percentage
from Bank_loan_data;
```

### ---Bad loan applications

```sql
SELECT 
   COUNT(ID) AS bad_loan_applications
from Bank_loan_data
where loan_status = 'Charged Off';
```

### --Bad loan Funded amount

```sql
SELECT 
    SUM(loan_amount) as total_amount
from Bank_loan_data
where loan_status = 'Charged Off';
```

### --Bad recevied amount

```sql
SELECT 
    SUM(total_payment) as total_amount
from Bank_loan_data
where loan_status = 'Charged Off';
```

---

# 📈 LOAN STATUS

### ---Loan Status

```sql
SELECT loan_status,
     count(id) as total_applications,
     sum(loan_amount) as total_funded_amount,
     sum(total_payment) as total_recevied_amount,
     round(avg(int_rate),4)*100 as avg_interest_rate,
     round(avg(dti),4)*100 as avg_approval_rate
     from bank_loan_data
     group by loan_status;
```

---

# 📅 MTD LOAN STATUS

### ---MTD loan status

```sql
SELECT loan_status,
       sum(loan_amount) as MTD_funded_amount,
       sum(total_payment) as MTD_recevied_amount
from Bank_loan_data
where MONTH(issue_date) = 12
group by loan_status;
```

---

# ⭐ AVG AMOUNT DIFFERENT GRADE

### ---AVG amount different grade

```sql
SELECT grade,
     round(avg(loan_amount),4)*100 as avg_grade_funded_amount,
     round(avg(total_payment),4)*100 as avg_grade_recevied_amount
from Bank_loan_data
group by grade;
```

---

# 📊 B. BANK LOAN REPORT | OVERVIEW

## MONTH

### -- MONTH

```sql
SELECT month(issue_date) as month_number,
       datename(month,issue_date) as month_name,
       sum(loan_amount) as total_funded_amount,
       sum(total_payment) as total_recevied_amount
from Bank_loan_data
group by month(issue_date),
       datename(month,issue_date)
order by total_funded_amount,total_recevied_amount desc;
```

---

## STATE

### -- STATE

```sql
SELECT address_state,
      count(id) as total_applications_by_state,
      sum(loan_amount) astotal_applications_by_state,
      sum(total_payment) as total_received_amount_by_state
from Bank_loan_data
group by address_state
order by total_applications_by_state,
         total_received_amount_by_state desc;
```

---

## TERM

### --Term

```sql
SELECT TERM,
       count(id) as total_applications,
       sum(loan_amount) as total_funded_dif_term,
       sum(total_payment) as total_received_dif_term
from Bank_loan_data
group by term;
```

---

## EMPLOYEE LENGTH

### -- EMPLOYEE_LENGTH

```sql
SELECT emp_length,
       count(id) as total_applications,
       sum(loan_amount) as total_funded_dif_emp_len,
       sum(total_payment) as total_received_dif_emp_Len
from Bank_loan_data
group by emp_length
order by emp_length desc;
```

---

## PURPOSE

### --PURPOSE

```sql
SELECT PURPOSE,
       count(id) as total_applications,
       sum(loan_amount) as total_funded_dif_emp_purpose,
       sum(total_payment) as total_received_dif_purpose
from Bank_loan_data
group by purpose
order by purpose desc;
```

---

## HOME OWNERSHIP

### --HOME_OWNERSHIP

```sql
SELECT home_ownership,
       count(id) as total_applications,
       sum(loan_amount) as total_funded_dif_emp_home,
       sum(total_payment) as total_received_dif_home
from Bank_loan_data
group by home_ownership
order by  home_ownership;
```

---

# 🔎 GRADE A DASHBOARD FILTER

### --See the results when we hit the Grade A in the filters for dashboards.

```sql
SELECT 
	purpose AS PURPOSE, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
WHERE grade = 'A'
GROUP BY purpose;
```

---

# 💡 PROJECT ANALYSIS

This SQL project demonstrates practical analysis of bank loan data using:

- Loan Application Analysis
- Funded Amount Analysis
- Received Amount Analysis
- Interest Rate Analysis
- DTI Analysis
- Good Loan Analysis
- Bad Loan Analysis
- Loan Status Analysis
- Grade Analysis
- Monthly Analysis
- State Analysis
- Term Analysis
- Employee Length Analysis
- Purpose Analysis
- Home Ownership Analysis

---

# 🛠️ SKILLS USED

**SQL | MySQL | SQL Server | Data Analysis | Business Analysis | KPI Analysis | Aggregation | GROUP BY | CASE WHEN | Date Functions**

---

# 📁 PROJECT STRUCTURE

```text
Bank-Loan-SQL-Analysis/
│
├── Bank_loan_data.csv
│
├── solutions(1).sql
│
└── README.md
```

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

# 🏦 Bank Loan SQL Project

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/21fce5dc-3525-42bd-95c3-2ae75133e1bc" />

## 📌 Project Overview

This project contains SQL queries for analyzing **Bank Loan Data**.

The project covers loan applications, funded amounts, received amounts, interest rates, DTI, Good Loans, Bad Loans, Loan Status, Grade Analysis, Monthly Analysis, State Analysis, Term Analysis, Employee Length, Purpose, Home Ownership, and Grade A dashboard filtering.

---

# 🗂️ Schema

### Bank Loan Project

```sql
SELECT * FROM Bank_loan_data;
```
<img width="1901" height="377" alt="image" src="https://github.com/user-attachments/assets/1da23cca-1681-447c-885a-708877e2ceaa" />


---

# 📊 A. BANK LOAN REPORT | SUMMARY

### -- Total loan applications

```sql
SELECT COUNT(ID) AS total_loan_appications
from Bank_loan_data;
```
<img width="317" height="112" alt="image" src="https://github.com/user-attachments/assets/ab3a8a34-e5d6-490e-9cc0-f018b858a4bb" />


### --MTD loan applications

```sql
SELECT COUNT(ID) AS total_mtd_applications
FROM Bank_loan_data
where month(issue_date) = 12;
```
<img width="422" height="170" alt="image" src="https://github.com/user-attachments/assets/ddcd8798-761b-450d-8f67-a2b1bbf9aeb4" />


### --PTMD loan applications

```sql
SELECT COUNT(ID) AS total_ptmd_applications
from Bank_loan_data
where month(issue_date) = 11;
```
<img width="267" height="105" alt="image" src="https://github.com/user-attachments/assets/3a378567-ec6f-4b95-a67a-e53617641603" />


### --Total funded amount

```sql
SELECT SUM(loan_amount) as total_loan_amount
from Bank_loan_data;
```
<img width="275" height="107" alt="image" src="https://github.com/user-attachments/assets/3aad6ec5-2fc9-4fbd-9786-fd376ed1ef97" />


### --MTD funded amount

```sql
SELECT SUM(loan_amount) AS total_mtd_amount 
FROM Bank_loan_data
where month(issue_date) = 12;
```
<img width="276" height="97" alt="image" src="https://github.com/user-attachments/assets/7c2e71f3-6074-4d72-a696-e145cfdf4b6c" />


### --PTMD funded amount

```sql
SELECT sum(loan_amount) AS total_ptmd_amount
from Bank_loan_data
where month(issue_date) = 11;
```
<img width="302" height="97" alt="image" src="https://github.com/user-attachments/assets/1c9b4ef0-b478-4585-b226-10ca564a6375" />


### --Total Recevied amount

```sql
SELECT SUM(total_payment) as total_loan_amount
from Bank_loan_data;
```
<img width="287" height="77" alt="image" src="https://github.com/user-attachments/assets/1c304589-cc75-4a85-bd58-ea24c951fe2b" />

### --MTD total Recevied amount

```sql
SELECT SUM(total_payment) AS total_mtd_amount 
FROM Bank_loan_data
where month(issue_date) = 12;
```
<img width="322" height="110" alt="image" src="https://github.com/user-attachments/assets/75fd85af-d2cc-4b18-849a-e1eb92a83960" />

### --PTMD total Recevied amount

```sql
SELECT sum(total_payment) AS total_ptmd_amount
from Bank_loan_data
where month(issue_date) = 11;
```
<img width="337" height="105" alt="image" src="https://github.com/user-attachments/assets/01911a07-76d9-4f70-8aff-e54b08a75252" />

### --int_rate avg interest rate

```sql
SELECT round(AVG(int_rate),4)*100 as avg_interest_rate
from Bank_loan_data;
```
<img width="327" height="162" alt="image" src="https://github.com/user-attachments/assets/9d4b5fe6-7e5b-4630-810b-30b5ed341804" />

### --MTD average interest rate

```sql
SELECT round(AVG(int_rate),4)*100 as avg_mtd_rate
from Bank_loan_data
where month(issue_date) = 12;
```
<img width="227" height="121" alt="image" src="https://github.com/user-attachments/assets/0b3bd632-13ce-49a3-868a-55c402647f63" />

### --PTMD average interest rate

```sql
SELECT round(AVG(int_rate),4)*100 as avg_ptmd_rate
from Bank_loan_data
where month(issue_date) = 11;
```
<img width="322" height="170" alt="image" src="https://github.com/user-attachments/assets/f2120aab-a197-4d0d-ad88-f19d8b4a93cb" />

### --Dti avg rate

```sql
SELECT round(AVG(DTI),4)*100 AS avg_dti_rate
from Bank_loan_data;
```
<img width="237" height="110" alt="image" src="https://github.com/user-attachments/assets/85217e43-132a-4805-8928-b768ead56904" />

### --MTD dti avg_rate

```sql
SELECT round(AVG(Dti),4)*100 as avg_mtd_dti_rate
from Bank_loan_data
where month(issue_date) = 12;
```
<img width="252" height="147" alt="image" src="https://github.com/user-attachments/assets/61f13232-3e97-4839-8b27-c9e245d600d1" />

### --PTMD dit avg_rate

```sql
SELECT round(AVG(Dti),4)*100 as avg_ptmd_dti_rate
from Bank_loan_data
where month(issue_date) = 11;
```
<img width="217" height="112" alt="image" src="https://github.com/user-attachments/assets/18f1cbde-b2fe-4bb8-bc2f-cd9e02226635" />

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
<img width="327" height="102" alt="image" src="https://github.com/user-attachments/assets/b6cf6327-1c8a-4b60-91e1-25cacd084bdc" />

### --- Good loan applications

```sql
SELECT 
   COUNT(ID) AS good_loan_applications
from Bank_loan_data
where loan_status = 'Fully Paid' or loan_status = 'Current';
```
<img width="235" height="125" alt="image" src="https://github.com/user-attachments/assets/f33c7b64-14a4-429a-8e36-ef390c884d32" />

### --Good loan Funded amount

```sql
SELECT 
    SUM(loan_amount) as total_amount
from Bank_loan_data
where loan_status = 'Fully Paid' or loan_status = 'Current';
```
<img width="267" height="157" alt="image" src="https://github.com/user-attachments/assets/a8e9711e-bc0f-41e9-a48e-2fcc205310c7" />

### --Good recevied amount

```sql
SELECT 
    SUM(total_payment) as total_amount
from Bank_loan_data
where loan_status = 'Fully Paid' or loan_status = 'Current';
```
<img width="291" height="202" alt="image" src="https://github.com/user-attachments/assets/895f498f-868d-497c-a369-d81297c9799a" />

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
<img width="157" height="55" alt="image" src="https://github.com/user-attachments/assets/969c51a9-1c62-46d9-b490-dd078cf0da37" />

### ---Bad loan applications

```sql
SELECT 
   COUNT(ID) AS bad_loan_applications
from Bank_loan_data
where loan_status = 'Charged Off';
```
<img width="262" height="127" alt="image" src="https://github.com/user-attachments/assets/acdfd15a-1a31-478b-b62d-42213e40d7f3" />


### --Bad loan Funded amount

```sql
SELECT 
    SUM(loan_amount) as total_amount
from Bank_loan_data
where loan_status = 'Charged Off';
```
<img width="197" height="82" alt="image" src="https://github.com/user-attachments/assets/265a0b67-026f-49e2-b965-f689f1ee82f5" />


### --Bad recevied amount

```sql
SELECT 
    SUM(total_payment) as total_amount
from Bank_loan_data
where loan_status = 'Charged Off';
```
<img width="197" height="77" alt="image" src="https://github.com/user-attachments/assets/08b67b71-ad34-4ed3-80e3-b0d002b94b51" />

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
<img width="860" height="127" alt="image" src="https://github.com/user-attachments/assets/d0765969-bba2-4d91-b615-60ffa87f5032" />

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
<img width="412" height="162" alt="image" src="https://github.com/user-attachments/assets/d4be5427-5bb7-4541-b405-0fec63dbd041" />

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
<img width="482" height="207" alt="image" src="https://github.com/user-attachments/assets/b6d179b7-4131-4201-8138-28de16a226c1" />

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
<img width="571" height="302" alt="image" src="https://github.com/user-attachments/assets/2ac0c8da-64b5-4777-a0f6-ccd415081ee9" />

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
<img width="662" height="365" alt="image" src="https://github.com/user-attachments/assets/252617a9-4745-4fa0-afec-7150f3f6c577" />

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
<img width="627" height="162" alt="image" src="https://github.com/user-attachments/assets/1eaaa34e-e999-43bd-9a3a-ee26c59863d0" />

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
<img width="617" height="336" alt="image" src="https://github.com/user-attachments/assets/fcc35d46-f94e-4eca-bafa-eb78bd67dfc6" />

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
<img width="715" height="347" alt="image" src="https://github.com/user-attachments/assets/55b5461e-ede7-474a-aba3-2f2100338e25" />

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
<img width="657" height="210" alt="image" src="https://github.com/user-attachments/assets/5337d7c9-a848-4c4d-8b15-0132fa22b121" />

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
<img width="621" height="337" alt="image" src="https://github.com/user-attachments/assets/7e6b91eb-ef44-4928-99da-eba546241a30" />

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

https://www.linkedin.com/posts/madanapalli-sai-19b835389_best-free-certificate-courses-online-2025-activity-7490432956604268544-Asln?utm_source=share&utm_medium=member_android&rcm=ACoAAF-yhccBFOBRwPFDl9PAbb7jDVPGHyD_Tsc

---

⭐ **If you find this project useful, please give the repository a star!**

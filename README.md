# 🏦 Bank Loan Analysis — SQL Queries & Output

This README contains **every original query** from `solutions(1).sql`, with the query shown first and its dataset output image immediately below it. The output images were generated from the provided `financial_loan.csv` dataset (**38,576 rows × 24 columns**).

## 1. Query 1

```sql
SELECT * FROM Bank_loan_data;
```

### Output

![Query 1 Output](query_outputs/01.png)

> **Output note:** Showing first 20 rows of 38,576 rows returned.

## 2. Total loan applications

```sql
SELECT COUNT(ID) AS total_loan_appications
from Bank_loan_data;
```

### Output

![Query 2 Output](query_outputs/02.png)

## 3. MTD loan applications

```sql
SELECT COUNT(ID) AS total_mtd_applications
FROM Bank_loan_data
where month(issue_date) = 12;
```

### Output

![Query 3 Output](query_outputs/03.png)

## 4. PTMD loan applications

```sql
SELECT COUNT(ID) AS total_ptmd_applications
from Bank_loan_data
where month(issue_date) = 11;
```

### Output

![Query 4 Output](query_outputs/04.png)

## 5. Total funded amount

```sql
SELECT SUM(loan_amount) as total_loan_amount
from Bank_loan_data;
```

### Output

![Query 5 Output](query_outputs/05.png)

## 6. MTD funded amount

```sql
SELECT SUM(loan_amount) AS total_mtd_amount 
FROM Bank_loan_data
where month(issue_date) = 12;
```

### Output

![Query 6 Output](query_outputs/06.png)

## 7. PTMD funded amount

```sql
SELECT sum(loan_amount) AS total_ptmd_amount
from Bank_loan_data
where month(issue_date) = 11;
```

### Output

![Query 7 Output](query_outputs/07.png)

## 8. Total Recevied amount

```sql
SELECT SUM(total_payment) as total_loan_amount
from Bank_loan_data;
```

### Output

![Query 8 Output](query_outputs/08.png)

## 9. MTD total Recevied amount

```sql
SELECT SUM(total_payment) AS total_mtd_amount 
FROM Bank_loan_data
where month(issue_date) = 12;
```

### Output

![Query 9 Output](query_outputs/09.png)

## 10. PTMD total Recevied amount

```sql
SELECT sum(total_payment) AS total_ptmd_amount
from Bank_loan_data
where month(issue_date) = 11;
```

### Output

![Query 10 Output](query_outputs/10.png)

## 11. int_rate avg interest rate

```sql
SELECT round(AVG(int_rate),4)*100 as avg_interest_rate
from Bank_loan_data;
```

### Output

![Query 11 Output](query_outputs/11.png)

## 12. MTD average interest rate

```sql
SELECT round(AVG(int_rate),4)*100 as avg_mtd_rate
from Bank_loan_data
where month(issue_date) = 12;
```

### Output

![Query 12 Output](query_outputs/12.png)

## 13. PTMD average interest rate

```sql
SELECT round(AVG(int_rate),4)*100 as avg_ptmd_rate
from Bank_loan_data
where month(issue_date) = 11;
```

### Output

![Query 13 Output](query_outputs/13.png)

## 14. Dti avg rate

```sql
SELECT round(AVG(DTI),4)*100 AS avg_dti_rate
from Bank_loan_data;
```

### Output

![Query 14 Output](query_outputs/14.png)

## 15. MTD dti avg_rate

```sql
SELECT round(AVG(Dti),4)*100 as avg_mtd_dti_rate
from Bank_loan_data
where month(issue_date) = 12;
```

### Output

![Query 15 Output](query_outputs/15.png)

## 16. PTMD dit avg_rate

```sql
SELECT round(AVG(Dti),4)*100 as avg_ptmd_dti_rate
from Bank_loan_data
where month(issue_date) = 11;
```

### Output

![Query 16 Output](query_outputs/16.png)

## 17. Good loan applications

```sql
SELECT 
     (COUNT(CASE WHEN loan_status = 'Fully Paid' or loan_status = 'Current' then id end) * 100)
     /
     COUNT(ID) AS total_loan_percentage
from Bank_loan_data;
```

### Output

![Query 17 Output](query_outputs/17.png)

## 18. Good loan applications

```sql
SELECT 
   COUNT(ID) AS good_loan_applications
from Bank_loan_data
where loan_status = 'Fully Paid' or loan_status = 'Current';
```

### Output

![Query 18 Output](query_outputs/18.png)

## 19. Good loan Funded amount

```sql
SELECT 
    SUM(loan_amount) as total_amount
from Bank_loan_data
where loan_status = 'Fully Paid' or loan_status = 'Current';
```

### Output

![Query 19 Output](query_outputs/19.png)

## 20. Good recevied amount

```sql
SELECT 
    SUM(total_payment) as total_amount
from Bank_loan_data
where loan_status = 'Fully Paid' or loan_status = 'Current';
```

### Output

![Query 20 Output](query_outputs/20.png)

## 21. Bad loan applications

```sql
SELECT 
     (COUNT(CASE WHEN loan_status = 'Charged Off' then id end) * 100)
     /
     COUNT(ID) AS total_loan_percentage
from Bank_loan_data;
```

### Output

![Query 21 Output](query_outputs/21.png)

## 22. Bad loan applications

```sql
SELECT 
   COUNT(ID) AS bad_loan_applications
from Bank_loan_data
where loan_status = 'Charged Off';
```

### Output

![Query 22 Output](query_outputs/22.png)

## 23. Bad loan Funded amount

```sql
SELECT 
    SUM(loan_amount) as total_amount
from Bank_loan_data
where loan_status = 'Charged Off';
```

### Output

![Query 23 Output](query_outputs/23.png)

## 24. Bad recevied amount

```sql
SELECT 
    SUM(total_payment) as total_amount
from Bank_loan_data
where loan_status = 'Charged Off';
```

### Output

![Query 24 Output](query_outputs/24.png)

## 25. Loan Status

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

### Output

![Query 25 Output](query_outputs/25.png)

## 26. MTD loan status

```sql
SELECT loan_status,
       sum(loan_amount) as MTD_funded_amount,
       sum(total_payment) as MTD_recevied_amount
from Bank_loan_data
where MONTH(issue_date) = 12
group by loan_status;
```

### Output

![Query 26 Output](query_outputs/26.png)

## 27. AVG amount different grade

```sql
SELECT grade,
     round(avg(loan_amount),4)*100 as avg_grade_funded_amount,
     round(avg(total_payment),4)*100 as avg_grade_recevied_amount
from Bank_loan_data
group by grade;
```

### Output

![Query 27 Output](query_outputs/27.png)

## 28. MONTH

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

### Output

![Query 28 Output](query_outputs/28.png)

## 29. STATE

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

### Output

![Query 29 Output](query_outputs/29.png)

> **Output note:** Original query uses the alias total_applications_by_state for both COUNT(id) and SUM(loan_amount); the image labels the second duplicate as total_applications_by_state_2 so both returned values remain visible.

## 30. Term

```sql
SELECT TERM,
       count(id) as total_applications,
       sum(loan_amount) as total_funded_dif_term,
       sum(total_payment) as total_received_dif_term
from Bank_loan_data
group by term;
```

### Output

![Query 30 Output](query_outputs/30.png)

## 31. EMPLOYEE_LENGTH

```sql
SELECT emp_length,
       count(id) as total_applications,
       sum(loan_amount) as total_funded_dif_emp_len,
       sum(total_payment) as total_received_dif_emp_Len
from Bank_loan_data
group by emp_length
order by emp_length desc;
```

### Output

![Query 31 Output](query_outputs/31.png)

## 32. PURPOSE

```sql
SELECT PURPOSE,
       count(id) as total_applications,
       sum(loan_amount) as total_funded_dif_emp_purpose,
       sum(total_payment) as total_received_dif_purpose
from Bank_loan_data
group by purpose
order by purpose desc;
```

### Output

![Query 32 Output](query_outputs/32.png)

## 33. HOME_OWNERSHIP

```sql
SELECT home_ownership,
       count(id) as total_applications,
       sum(loan_amount) as total_funded_dif_emp_home,
       sum(total_payment) as total_received_dif_home
from Bank_loan_data
group by home_ownership
order by  home_ownership;
```

### Output

![Query 33 Output](query_outputs/33.png)

## 34. See the results when we hit the Grade A in the filters for dashboards.

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

### Output

![Query 34 Output](query_outputs/34.png)

---

# 🛠️ Skills Used

**SQL | Data Analysis | KPI Analysis | Aggregation | CASE WHEN | GROUP BY | Date Functions | Business Analysis**

# 👨‍💻 Author

**Sai M**

Aspiring Data Analyst

**Skills:** SQL | Python | Excel | Power BI | PostgreSQL | Data Analytics

# 🔗 Connect With Me

**GitHub:** https://github.com/stej07033

**LinkedIn:** https://www.linkedin.com/posts/madanapalli-sai-19b835389

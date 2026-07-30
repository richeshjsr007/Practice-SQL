# Practice-SQL -- GROUP BY & HAVING
select * from tab
//
DESC EMPLOYEES;
DESC customers;
DESC products;
DESC loans;
DESC repayments;
DESC accounts;
DESC transactions;

-- 1.	Count total customers in each city.
SELECT city, COUNT (customer_id)
      FROM CUSTOMERS
      GROUP BY CITY;
      
-- 2.	Count customers by gender.
SELECT GENDER, COUNT(customer_id)
    FROM customers
    GROUP BY GENDER;
    
-- 3.	Find total number of loans issued by each branch.
SELECT b.branch_name, count(l.loan_id)
    FROM branches b
    INNER JOIN LOANS L ON B.BRANCH_ID = L.BRANCH_ID
    GROUP BY B.BRANCH_NAME;
    
-- 4.	Find total loan amount for each loan product.
select p.product_name, sum(l.loan_amount)
    FROM products p
    INNER JOIN LOANS L ON P.PRODUCT_ID = L.PRODUCT_ID
    GROUP BY p.product_name;
    
-- 5.	Calculate average customer income by city.
SELECT CITY, AVG(INCOME)
 FROM CUSTOMERS
 GROUP BY CITY;

-- 6.	Find maximum loan amount in each branch.
SELECT B.BRANCH_NAME, MAX(L.LOAN_AMOUNT)
FROM BRANCHES B
INNER JOIN LOANS L ON B.BRANCH_ID = L.BRANCH_ID
GROUP BY B.BRANCH_NAME;

-- 7.	Find minimum loan amount by loan product.
select p.product_name, MIN(l.loan_amount)
    FROM products p
    INNER JOIN LOANS L ON P.PRODUCT_ID = L.PRODUCT_ID
    GROUP BY p.product_name;
    
-- 8.	Count repayments by payment status.
SELECT PAYMENT_STATUS, COUNT(AMOUNT_PAID)
FROM REPAYMENTS
GROUP BY PAYMENT_STATUS;

-- 9.	Calculate total transaction amount by transaction type.
SELECT TRANSACTION_TYPE, SUM(AMOUNT)
FROM TRANSACTIONS
GROUP BY TRANSACTION_TYPE;

-- 10.Find number of employees in each branch.
SELECT  B.BRANCH_NAME, COUNT(E.EMPLOYEE_ID)
         FROM BRANCHES B
         LEFT JOIN EMPLOYEES E ON B.BRANCH_ID = E.BRANCH_ID
         GROUP BY B.BRANCH_NAME;
         
-- 11. Find branches where total loan amount exceeds ₹5 crore.
SELECT B.BRANCH_NAME, SUM(L.LOAN_AMOUNT) AS LOAN_AMOUNT
FROM BRANCHES B
INNER JOIN LOANS L ON B.BRANCH_ID = L.BRANCH_ID
GROUP BY B.BRANCH_NAME
HAVING SUM(L.LOAN_AMOUNT) > 50000000

-- 12.	Display cities having more than 100 customers.
SELECT city, COUNT(customer_id)
FROM customers
GROUP BY city
HAVING COUNT(customer_id) >100;

-- 13.	Find products with average loan amount greater than ₹5 lakh.
select p.product_name, AVG(l.loan_amount) AS Avg_loan
    FROM products p
    INNER JOIN LOANS L ON P.PRODUCT_ID = L.PRODUCT_ID
    GROUP BY p.product_name
    HAVING AVG(l.loan_amount)> 500000 ;
    
-- 14.	Find branches with more than 500 active loans.
SELECT B.BRANCH_NAME, COUNT(*)AS Active_loan
FROM BRANCHES B
INNER JOIN LOANS L ON B.BRANCH_ID = L.BRANCH_ID
WHERE L.LOAN_STATUS = 'Active'
GROUP BY B.BRANCH_NAME
HAVING COUNT(*)> 500
ORDER BY Active_loan DESC;

-- 15.	Calculate total repayment collected by branch.
SELECT b.branch_name, SUM(r.amount_paid) AS total_repayment_collected
FROM BRANCHES b 
Inner join loans l on b.branch_id = l.branch_id
INNER join repayments r on l.loan_id = r.loan_id 
GROUP BY b.branch_name ;

-- 16.	Find average DPD by branch.
SELECT b.branch_name, AVG(DPD) AS AVG_DPD
FROM BRANCHES b 
INNER join loans l on b.branch_id = l.branch_id
INNER join repayments r on l.loan_id = r.loan_id 
GROUP BY b.branch_name ;

-- 17.	Find total outstanding loan amount by city.
SELECT C.CITY, 
 SUM (L.LOAN_AMOUNT -(select coalesce(sum(AMOUNT_PAID),0)from repayments where loan_id = l.loan_id) ) AS total_outstanding
 FROM customers C
 INNER JOIN loans L ON C.CUSTOMER_ID = L.CUSTOMER_ID
 GROUP BY C.CITY
 
-- 18.	Show account type-wise average balance.
-- 19.	Find customer count by branch and gender.
-- 20.	Find branch-wise average customer income.


    
 

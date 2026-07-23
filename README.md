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

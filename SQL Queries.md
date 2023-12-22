### 1. Write a SQL query to find the second highest salary from the 'emp' table. (Columns: id, salary)
```
SELECT MAX(salary) AS second_highest_salary
FROM emp
WHERE salary < (SELECT MAX(salary) FROM emp);
```

### 2. Write a SQL query to find numbers that consecutively occur 3 times in the 'id' column of a table.
(Columns: id, numbers)
```
SELECT DISTINCT a.numbers
FROM table_name a, table_name b, table_name c
WHERE a.numbers = b.numbers AND b.numbers = c.numbers
AND a.id = b.id - 1 AND b.id = c.id - 1;
```

### 3. Write a SQL query to find the days when the temperature was higher than its previous dates. 
(Columns: Days, Temp)
```
SELECT Days, Temp
FROM table_name t1
WHERE Temp > (SELECT Temp FROM table_name t2 WHERE t2.Days = t1.Days - 1);
```

### 4. Write a SQL query to delete duplicate rows in a table.
```
DELETE FROM table_name
WHERE ROWID NOT IN (SELECT MIN(ROWID) FROM table_name GROUP BY column1, column2, ...);
```

### 5. Write a SQL query for the cumulative sum of salary for each employee from January to July.
(Columns: Emp_id, Month, Salary)
```
SELECT Emp_id, Month, SUM(Salary) OVER (PARTITION BY Emp_id ORDER BY Month) AS Cumulative_Salary
FROM salary_table
WHERE Month BETWEEN 'January' AND 'July';
```

### 6. Write a SQL query to display year-on-year growth for each product. 
(Columns: transaction_id, Product_id, transaction_date, spend, Output: year, product_id, yoy_growth)
```
SELECT EXTRACT(YEAR FROM transaction_date) AS year,
    Product_id,
    (spend - LAG(spend, 1, 0) OVER (PARTITION BY Product_id ORDER BY transaction_date)) / LAG(spend, 1, 0) OVER (PARTITION BY Product_id ORDER BY transaction_date) * 100 AS yoy_growth
FROM transactions;
```

### 7. Write a SQL query to find the rolling average of posts on a daily basis for each user_id. 
(Columns: user_id, date, post_count)
```
SELECT user_id,
    date,
    ROUND(AVG(post_count) OVER (PARTITION BY user_id ORDER BY date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW), 2) AS rolling_average
FROM posts_table;
```


### 8. Write a SQL query to get emp id and department for each department, 
considering employees who recently joined the organization and are currently working. 
(Columns: emp id, first name, last name, date of join, date of exit, department)
```
SELECT e.emp_id, e.first_name, e.last_name, e.date_of_join, e.date_of_exit, d.department
FROM employees e
JOIN departments d ON e.department_id = d.department_id
WHERE e.date_of_join > DATE_SUB(CURRENT_DATE, INTERVAL 1 YEAR)
AND e.date_of_exit IS NULL;
```


### 9. Write a query to get mean, median, and mode for earning? (Columns: Emp_id, salary)
```
SELECT 
 AVG(salary) AS mean_earning, 
 PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY salary) AS median_earning,
 MODE() WITHIN GROUP (ORDER BY salary) AS mode_earning
FROM earnings_table;
```

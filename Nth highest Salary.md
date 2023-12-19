
## find 3rd highest salary using RANK()
```
SELECT * FROM(
SELECT emp_name, salary, RANK() 
over(ORDER BY salary DESC) AS ranking FROM employee) AS k
WHERE ranking=3;
```

## Find 3rd highest salary using ROW_NUMBER()
```
SELECT * FROM(
SELECT emp_name, salary, ROW_NUMBER() 
over(ORDER BY salary DESC) AS ranking FROM employee) AS k
WHERE ranking=3;
```
## find 3rd highest salary using limit
```
SELECT emp_name AS Employee, salary AS Salary FROM employee ORDER BY salary DESC LIMIT 2,1;
```

## find 3rd highest salary using DENSE_RANK()
```
SELECT * FROM(
SELECT emp_name, salary, DENSE_RANK() 
over(ORDER BY salary DESC) AS ranking FROM employee) AS k
WHERE ranking=3;
```

# Using RANK()
https://www.shiksha.com/online-courses/articles/find-nth-highest-salary-in-sql/
```
SELECT emp_name, salary, RANK()
 OVER(ORDER BY salary DESC) AS Nth_highest_salary
  FROM employee;
```
# Using ROW_NUMBER()
```
SELECT emp_name, salary, ROW_NUMBER()
 OVER(ORDER BY salary DESC) AS Nth_highest_salary
  FROM employee;
```



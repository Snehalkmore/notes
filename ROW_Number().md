

## ROW_NUMBER window function (https://learnsql.com/blog/row-number-over-in-sql/)
used to get unique id for each row
```
SELECT
  country || '_' ||
  ROW_NUMBER() OVER (PARTITION BY country ORDER BY lastname ASC)
                                                            as room_label,
  firstname,
  lastname,
  country
FROM athletes;
```
![image](https://github.com/Snehalkmore/notes/assets/14993594/55ec7365-038a-499c-b1a2-8cea5c8e48cb)



## rank() window function
```
SELECT id,
  salesman_id,
  sales_item,
  sales_num,
  sales_price,
  rank() over (order by sales_num)
FROM sales
ORDER BY sales_num;
```
![image](https://github.com/Snehalkmore/notes/assets/14993594/b186a493-eaad-40e6-b78c-cf03dd8c9c1c)


## rank() partition over
```
SELECT id,
  salesman_id,
  sales_item,
  sales_num,
  sales_price,
  rank() over (order by sales_num desc)
FROM sales
ORDER BY sales_num;
```

![image](https://github.com/Snehalkmore/notes/assets/14993594/55070922-f725-41ee-94a3-dfbc9917e154)



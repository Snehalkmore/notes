

## ROW_NUMBER function in windows
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

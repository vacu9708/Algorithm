# (Self) cartesian product
FROM performs cartesian product.
~~~sql
from table1 A, table1 B
~~~

# Subquery
[example](https://github.com/vacu9708/Algorithm/blob/main/Algorithm%20traning/SQL%20training/medium/%ED%97%A4%EB%B9%84%20%EC%9C%A0%EC%A0%80%EA%B0%80%20%EC%86%8C%EC%9C%A0%ED%95%9C%20%EC%9E%A5%EC%86%8C.md)

# CASE, date comparison
[date format(MySQL official)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_date-format)
- [example](https://github.com/vacu9708/Algorithm/blob/main/Algorithm%20traning/SQL%20training/medium/%EC%A1%B0%EA%B1%B4%EB%B3%84%EB%A1%9C%20%EB%B6%84%EB%A5%98%ED%95%98%EC%97%AC%20%EC%A3%BC%EB%AC%B8%EC%83%81%ED%83%9C%20%EC%B6%9C%EB%A0%A5%ED%95%98%EA%B8%B0.md)
- [example(using LIKE)](https://github.com/vacu9708/Algorithm/tree/main/Algorithm%20traning/SQL%20training/medium)

# GROUP BY, HAVING
A GROUP BY reduces the number of rows returned by rolling them up.
- Executed after FROM WHERE
- **GROUP BY**: groups rows before SELECT.
- **HAVING**: filters grouped rows.
- [example(GROUP BY+HAVING)](https://github.com/vacu9708/Algorithm/blob/main/Algorithm%20traning/SQL%20training/medium/%EC%9E%AC%EA%B5%AC%EB%A7%A4%EA%B0%80%20%EC%9D%BC%EC%96%B4%EB%82%9C%20%EC%83%81%ED%92%88%EA%B3%BC%20%ED%9A%8C%EC%9B%90%20%EB%A6%AC%EC%8A%A4%ED%8A%B8%20%EA%B5%AC%ED%95%98%EA%B8%B0.md)
- [example(Subquery + GROUP BY)](https://github.com/vacu9708/Algorithm/blob/main/Algorithm%20traning/SQL%20training/medium/%EC%A6%90%EA%B2%A8%EC%B0%BE%EA%B8%B0%EA%B0%80%20%EA%B0%80%EC%9E%A5%20%EB%A7%8E%EC%9D%80%20%EC%8B%9D%EB%8B%B9%20%EC%A0%95%EB%B3%B4%20%EC%B6%9C%EB%A0%A5%ED%95%98%EA%B8%B0.md)

# PARTITION BY
Similar to GROUP BY but PARTITION BY does not affect the number of rows returned.

# string
## substring
substring(string, position, length)
- [example](https://github.com/vacu9708/Algorithm/blob/main/Algorithm%20traning/SQL%20training/medium/%EC%B9%B4%ED%85%8C%EA%B3%A0%EB%A6%AC%20%EB%B3%84%20%EC%83%81%ED%92%88%20%EA%B0%9C%EC%88%98%20%EA%B5%AC%ED%95%98%EA%B8%B0.md)
## pattern comparison (can be utilized for date comparison)
### Example
- WHERE name LIKE 'a%' : any name that starts with 'a'
- WHERE name LIKE '%a%' : any name that has 'a'
- WHERE name LIKE '%a' : any name that ends with 'a'
- WHERE name LIKE '\_\_a\_\_' : any name that has a at the fixed location
## How to exclude results that have the same information with a different order
Use an inequality sign
### Ex) GPA가 같은 학생들의 sID, sName, GPA 쌍(pair)을 열거
~~~sql
SELECT A.sID, A.sName, A.GPA, B.sID, B.sName, B.GPA
from Student as A, Student as B
where A.GPA=B.GPA and A.sName!=B.sName and A.sName<B.sName
~~~

# DELETE + JOIN
### Example
Delete all duplicate rows except one based on orderId" Is this correct and natural english
~~~
DELETE o1 FROM orders o1 JOIN (
SELECT MIN(id) as minId, orderId FROM orders GROUP BY orderId) o2 
ON o1.id != o2.minId and o1.orderId = o2.orderId
~~~

# CASE, date comparison
~~~sql
SELECT ORDER_ID, DATE_FORMAT(OUT_DATE, '%Y-%m-%d'),
    case
        when OUT_DATE is null then '출고미정'
        when out_date<='2022-05-01' then '출고완료'
        else '출고대기'
    end as 출고여부
from FOOD_ORDER
~~~
# date comparison using DATEDIFF()
~~~sql
when DATEDIFF(out_date,'2022-05-01')<=0 then '출고완료'
~~~

# GROUP BY, HAVING
- **GROUP BY**: Grouping rows before SELECT
- **HAVING**: Filtering grouped rows
- ### [example](https://github.com/vacu9708/Algorithm/blob/main/Algorithm%20traning/SQL%20training/medium/%EC%9E%AC%EA%B5%AC%EB%A7%A4%EA%B0%80%20%EC%9D%BC%EC%96%B4%EB%82%9C%20%EC%83%81%ED%92%88%EA%B3%BC%20%ED%9A%8C%EC%9B%90%20%EB%A6%AC%EC%8A%A4%ED%8A%B8%20%EA%B5%AC%ED%95%98%EA%B8%B0.md)

# SUBSTRING()
- ### [example](https://github.com/vacu9708/Algorithm/blob/main/Algorithm%20traning/SQL%20training/medium/%EC%B9%B4%ED%85%8C%EA%B3%A0%EB%A6%AC%20%EB%B3%84%20%EC%83%81%ED%92%88%20%EA%B0%9C%EC%88%98%20%EA%B5%AC%ED%95%98%EA%B8%B0.md)

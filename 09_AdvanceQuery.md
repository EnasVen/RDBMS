# 排序函數
排序常用以下3種:
1. ROW_NUMBER(): 回傳動態產生的排序編號。
2. RANK(): 同上，但相同值排名會相同，且其後排名跳過。(e.g. 1,2,2,4,5,6...)
3. DENSE_RANK(): 同上，但相同值排名相同，其後排名連續。(e.g. 1,2,2,3,4,5...)

(重要!)群組排序:  
```
-- 依據 customer_id 分組，並且將其底下staff_id的amount值做排序。 --
SELECT customer_id , staff_id , amount , row_number() over(partition by customer_id order by amount desc) FROM sakila.payment where amount >= 6;
```

# (MS SQL)暫存資料表
使用#代表local暫存；##代表global暫存。  
```
SELECT ename, title, salary
INTO #tbl
FROM    employee
WHERE   deptno = 100;
```
MySQL內沒有#功能，只能預先建立TABLE再INSERT INTO。  

# (MS SQL) PIVOT/UNPIVOT
提供長寬資料轉換，類似樞紐分析表，或R語言的gather、reshape。
```
-- PIVOT --
SELECT 運算後需要的欄位 FROM 來源資料表名稱
PIVOT (彙總函數) FOR pivot欄位 
IN (欄位列表) 別名
WHERE 條件式

-- UNPIVOT --
SELECT 運算後需要的欄位 FROM 來源資料表名稱
PIVOT (彙總函數) FOR unpivot欄位 
IN (欄位列表) 別名
WHERE 條件式
```

# CTE (Common Table Expression)
定義一個 table expression，給予一個暫時名字，讓使用者在查詢時可以多次使用，不用產生永久的View。  
```
WITH tbl_name AS (SELECT ...),
tbl_name AS (SELECT ...)
SELECT 欄位 FROM 某個tbl_name;

```

# EXISTS
子查詢回傳1個以上的record則為TRUE，透過EXISTS可替換IN的子查詢，並可搭配NOT關鍵字。  
```
SELECT * FROM WHERE EXISTS (SELECT ...);
```

# ROLLUP / CUBE / GROUPING
產生累計值的record，例如:計算小結。  
CUBE是GROUP BY語法的延伸，可以產生更多小計的交叉運算，比ROLLUP產生更細的小結。
GROUPING回傳0或1，小結record則回傳1，用於協助使用者了解每一筆小計是如何產生。  
```
SELECT [column] | group_function(column) , GROUPING(expr) ...
FROM tbl
[WHERE conditions]
[GROUP BY [ROLLUP|CUBE] group_by_expression]
[HAVING having_expression]
[ORDER BY column]
```












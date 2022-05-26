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

#














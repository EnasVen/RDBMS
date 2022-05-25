# 合併查詢
合併包含各類join，下圖看了應該是秒懂:  
![Image](https://github.com/EnasVen/RDBMS/blob/main/sql-join.png)

紀錄一些常用的join形式，以ON語法做欄位連接:  
1.  CROSS JOIN : 將兩張TABLE所有可能的排列組合列出來，也就是Cartesian Product。  
```
SELECT table_column1, table_column2
FROM table_name1
CROSS JOIN table_name2;
-- 等價寫法 -- 
SELECT table_column1, table_column2
FROM table_name1, table_name2;
-- 等價寫法 --
SELECT table_column1, table_column2...
FROM table_name1
JOIN table_name2;
```

2. INNER JOIN : 取交集
```
SELECT table_column1, table_column2...
FROM table_name1
INNER JOIN table_name2 
ON table_name1.column_name=table_name2.column_name;
-- 等價寫法 --
SELECT table_column1, table_column2...
FROM table_name1
INNER JOIN table_name2 
USING (column_name);
```
3. LEFT/RIGHT JOIN : 保留左/右方資料，串接和右/左方有交集的部分
```
SELECT table_column1, table_column2...
FROM table_name1
LEFT JOIN table_name2 
ON table_name1.column_name=table_name2.column_name;
```
4. FULL JOIN : 為LEFT+RIGHT JOIN，不符合串接匹配的資料會以NULL形式納入。  
```
SELECT table_column1, table_column2...
FROM table_name1
FULL JOIN table_name2 
ON table_name1.column_name=table_name2.column_name;
```

通常在join的使用上會將表格使用別名，須注意一旦使用別名，該TABLE在整個STATAMENT都必須使用別名!  

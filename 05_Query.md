# 基本查詢
```
SELECT {* | expr | col[別名] , ... | DISTINCT col} FROM table_name
[WHERE conditions]
[GROUP BY colnames | expr]
[HAVING group_conditions]
[ORDER BY col_name]
[LIMIT [offest.] row_count];
```

# 算術運算子
基礎四則運算與一般語言相同，須注意求商為div；求餘數為%。  
運算子可透過()來改變運算順序。  
數字欄位可使用四則運算；日期欄位只能使用加減法，需搭配INTERVAL關鍵字使用(SUB=減；ADD=加):  
```
SELECT DATE_SUB("2017-06-15", INTERVAL 10 DAY);
```
須注意運算式會以單一欄位輸出，且NULL運算均維持NULL:  
```
SELECT 17/5 , 50 DIV 9 , 41%8 , 11*NULL;
```

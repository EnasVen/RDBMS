# 子查詢
在主SELECT敘述中包含另一個子SELECT敘述，語法如下:  
```
SELECT col 
FROM tbl
WHERE expr operator ( SELECT col FROM tbl );
```

subquery需要加上小括號，屬於優先運算。  
如果subquery無回傳資料，則mainquery也會無資料。  

實務上常見的子查詢錯誤:  
```
SEELCT a,b 
FROM tbl
WHERE c = (SELECT MIN(d) FROM GROUP BY d)
```
saleary比對單一值，但是小括號回傳的是多列資料。  
須注意表格別名不可以使用字串符號!  

如果要使用多列回傳值的subquery，需要使用比對運篹子，例如:IN/ALL/ANY/SOME(可搭配NOT):  
```
-- < ANY 表示小於maximum ; > ANY 表示大於 minimum
SELECT a,b,c 
FROM tbl
WHERE c < ANY( select c from tbl WHERE condition);

-- < ALL 表示小於minimum ; > ALL 表示大於 maximum
SELECT a,b,c 
FROM tbl
WHERE c > ALL( select c from tbl WHERE condition);
```

# 不同位置的子查詢
```
-- 放在 SELECT 區(運算較多次)  --
SELECT col , ROUND(d*5 / (SELECT SUM(b) FROM tbl WHERE conditions))
FROM tbl
WHERE e = 100;;
```

-- 放在 FROM 區(運算1次)  --
SELECT col ,  ROUND(d*5/t.total)
FROM tbl , (SELECT SUM(b) 'total' FROM tbl WHERE conditions) t
WHERE e=100;;
```

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

# 別名
運算或選取的欄位名稱可透過AS關鍵字重新賦予新名稱:  
```
SELECT col AS abc , 50+5 AS 'result today' from table_name;
```
須注意別名如果有空白，要加上''作為字串使用!(中文建議也加上字串符號)  

# 字串處理
字串可以透過以下關鍵字處理:  
1. SUBSTRING({string | col},pos[,len]) : 擷取部分字串，如果pos值為正，則從左邊開始
```
SELECT SUBSTRING(text_col , 1 2) FROM table_name;
SELECT SUBSTRING('DAVID' , 1 2);
SELECT SUBSTRING('THIS IS ONE' , -5);

```
2. CONCAT(str1 , str2 [, ...]) : 串接字串
```
SELECT CONCAT(colA , '++' , colB) FROM employee;
```
3. LENGTH(str) : 字串長度佔多少個byte
```
SELECT LENGTH('蘋果好吃888') AS 'len';
```
上述例子會回傳15!(中文字=3byte)

4. CHAR_LENGTH(str) : 總共幾個字元(中英文都算一個字)
```
SELECT CHAR_LENGTH('蘋果好吃888') AS 'len';
```
上述例子會回傳7!(中英文都算1個字元)

5. (MSSQL) Literal Char String : 直接用加號組合字串
```
SELECT empno + '+++' + deptno FROM employee;
```

# 日期處理
SYSDATE()與NOW()可以回傳當前時間，但用途不同:  
SYSDATE()如果呼叫多次，每次都會取最新的時間；而NOW()只會存取第一次呼叫的時間!  
```
SELECT SYSDATE() , SLEEP(2) , SYSDATE();
SELECT NOW() , SLEEP(2) , NOW();
```

INTERVAL關鍵字可以將時間做平移，單位可以是YEAR/QUARTER/MONTH/DAY/HOUR/MINUTE/SECOND:  
```
SELECT SYSDATE() + interval 5 day;
SELECT SYSDATE() - interval 10 month;
```

CURDATE()與CURTIME()可以獲得現在的日期、時間。  
前面的DATE_SUB或DATE_ADD也可以使用下面的寫法來達成同樣目的(預設是day作單位，要使用其他單位則必須使用INTERVAL關鍵字):  
```
SELECT ADDDATE(CURDATE() , 5); -- 預設單位DAY --
SELECT SUBDATE(CURDATE() , INTERVAL 5 HOUR);
```

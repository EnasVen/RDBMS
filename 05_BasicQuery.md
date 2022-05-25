# 基本查詢
```
SELECT {* | expr | col[別名] , ... | DISTINCT col} FROM table_name
[WHERE conditions]
[GROUP BY colnames | expr]
[HAVING group_conditions]
[ORDER BY col_name]
[LIMIT [offest.] row_count];
```
須注意運算式expr後面一定要給alias!!  

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

6. UPPER() LOWER() : 大小寫轉換
```
SELECT UPPER(col_name) FROM tbl;
```
7. CHARINDEX() : 尋找特定字元出現的位置 (MS SQL)
```
SELECT CHARINDEX('a' , name) FROM tbl;
```
8. REPLACE() : 替代字串
```
SELECT replace(deptno , 1 , 9) FROM employee;
```
9. REVERSE() : 反轉字串
```
SELECT REVERSE(name) FROM employee;
```
10. RTRIM() : 去除字串空白
```
SELECT rtrim(salary) FROM employee;
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

YEAR()、MONTH()與DAY()可回傳年月日的INT數值:  
```
SELECT * , YEAR(date_col) AS yr FROM table_name;
```

計算時間差異可以使用DATEDIFF()來獲得(以天數為單位):  
```
SELECT DATEDIFF(date1 , date2) FROM table_name;
```

# 條件查詢
在SELECT語法中加入條件即為條件查詢:  
1. 消除重複: 
  - 注意若欄位內有null，則DISTINCT後會包含NULL!
  - 若DISTINCT後面有2個以上欄位，則查找相異組合
```
SELECT [ALL|DISTINCT] col_name FROM table_name;
```
2. CASE WHEN ELSE / IF:
  - 可完成多種條件判斷的語法
```
SELECT * , a*(IF b <80 , 9 , -9) 'c' FROM table_name;
```
```
SELECT * , 
CASE
  WHEN colA > 100 THEN 'A'
  WHEN colA BETWEEN 70 AND 99 THEN 'B'
  ELSE 'C'
 END 'casewhen_Col'
FROM table_name
```
3. WHERE:
  - 在SELECT後加入WHERE來做進階篩選。
```
SELECT *|[ALL|DISTINCT] col_name | expr , ... FROM table_name
[WHERE conditions]
```
WHERE內可使用以下特殊運算子:
> BETWEEN...AND : 指定欄位落在特定數值範圍內  
```
SELECT * FROM tbl WHERE col|expr BETWEEN v1 AND v2;
```
> IN(set) : 指定欄位需落在set內  
```
SELECT * FROM tbl WHERE col|expr IN (v1,v2,v3,...);
```
上述IN後面的set也可以放入select結果，稱為子查詢。  
> IS NULL / IS NOT NULL : 判斷是否為空  
```
SELECT * FROM tbl WHERE col IS NULL;
```
> LIKE : 包含某字串的pattern，以%辨識  
```
SELECT * FROM tbl WHERE col LIKE '%ABC%' [ESCAPE '/']; -- 指定跳脫字元 --
SELECT * FROM tbl WHERE col LIKE '%ABC_' -- 指定包含ABC字串， _代表其後仍有字元 --
SELECT * FROM tbl WHERE col LIKE '%ABC\_' -- 以跳脫字元處理_，讓這個底線成為判斷文字 --
SELECT * FROM tbl WHERE col REGEXP '^2.*0$'; -- 以正規表達處理 --
```
> AND / OR / NOT : 邏輯運算子，用法同Python
```
SELECT * FROM tbl WHERE colA IS NULL AND  colB <= 660;
SELECT * FROM tbl WHERE col IS NOT NULL;
SELECT * FROM tbl WHERE col NOT LIKE '%ABC%';
SELECT * FROM tbl WHERE col|expr NOT BETWEEN v1 AND v2;
SELECT * FROM employee where deptno IS NOT NULL AND NOT EXISTS (select * from department where salary > 70000);
```
4. ORDER BY ; 根據欄位做單一或多重排序，預設升冪排序ASC，降冪排序則需使用DESC關鍵字。
```
SELECT a,b,c FROM employee ORDER BY a,b DESC; -- 只會對b排序，a仍為預設ASC --
SELECT a,b,c FROM employee ORDER BY a DESC , b DESC; -- 兩者都為降冪排序 --
SELECT a,b,c FROM employee ORDER BY c*50 -- 使用運算式排序 --
SELECT a,b,c FROM employee ORDER BY 3 -- 使用第3個欄位來排序 --
```
須注意欄位別名在排序的時候不能加字串符號:
```
SELECT a,b,c as 'C' FROM employee ORDER BY 'C' -- 這樣寫是錯的! -- 
```

5. LIMIT : 為MySQL才有的排序功能，在MsSQL內則為TOP N [WITH EVEN] 
```
SELECT * FROM tbl LIMIT 3;
SELECT * FROM tbl LIMIT 5,3; -- 跳過前5筆資料後取3筆 --
```

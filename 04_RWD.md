# 新增資料
將record新增到表格內的語法如下:
```
INSERT INTO table_name[(col1 [, col2 , ...])] VALUES (v1 [, v2 , ...])
```
新增可以寫入完整欄位或是部分欄位。  
如果要使用DEFAULT值來新增:  
```
INSERT INTO table_name(col1 , col2) VALUES(DEFAULT , DEFAULT)
```

須注意若給了colname，則VALUE必須要有相應數量的值，否則最好不寫，直接給table name:
```
INSERT INTO tbl(a,b,c) VALUES (a1 , b1 , c1);
INSERT INTO tbl VALUES (a1,b1,NULL)
INSERT INTO tbl(a,b) VALUES (a1,b1)
```

同時新增多筆record: 
```
INSERT INTO tbl(a,b,c) VALUES (a1 , b1 , c1) , (a2 , b2 , c2);
```

# 修改資料
修改table內的資料，其語法如下:  
```
UPDATE table_name
SET col = v1 [, col2 = v2]
[WHERE 條件式];
```
注意UPDATE和ALTERE TABLE使用方式不同:  
UPDATE用於修改資料內容，不更動表格結構；ALTER TABLE用於修改表格的結構。  

# 刪除資料
刪除現有資料可用以下語法:  
```
DELETE [FROM] table_name
[WHERE 條件式];
```

刪除所有資料可使用truncate:  
```
TRUNCATE TABLE table_name;
```
相較於DELETE，TRUNCATE的優點為使用的交易紀錄空間較少。  
須注意當UPDATE或DELETE資料時，若主表/子表有參考/FOREIGN KEY時，會發生錯誤。  

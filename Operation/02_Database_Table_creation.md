# 資料庫建置
```
CREATE DATABASE db01;
CREATE DATABASE [IF NOT EXIST] db01;
```
上面兩列的指令差異在於直接創建DB的話，如果以存在同名DB會報錯；IF NOT EXIST 則不會。

# 資料庫檢視
```
SHOW DATABASES;
```
執行上述指令後會發現多出一些DB，像是:  
information_schema  
mysql  
performance_schema  
這些是MySQL的系統用DB，專門給DBA操控使用。  


# 切換到預設DB
```
USE db01;
```

# 資料表建置
```
CREATE TABLE table01 (
id INT PRIMARY KEY,
name CHAR(20) ,
bdate DATE , 
tel CHAR(20)
)

```
PK可以寫在欄位定義後面，也可獨立寫在最後一列。  
上面為創建資料表的範例，總體來說語法可歸納如下:  
```
CREATE TABLE table_ame(
col_name data_type [attributes] [constraints],
col_name data_type [attributes] [constraints],
...
col_name data_type [attributes] [constraints]
)
```
# 資料表檢視(狀態)
```
SHOW TABLES;
SHOW TABLE STATUS [FROM|IN db_name];
```

# 查看表格欄位設計
```
DESC table_name;
```

# (MSSQL) 查詢表格的所有欄位名稱/資料型態
```
EXEC  sp_columns  departments
```

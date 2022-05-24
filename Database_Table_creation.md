# 資料庫建置
```
CREATE DATABASE db01;
CREATE DATABASE IF NOT EXIST db01;
```
上面兩列的指令差異在於直接創建DB的話，如果以存在同名DB會報錯；IF NOT EXIST 則不會。

# 資料表建置
```
CREATE TABLE table01 (
id INT PRIMARY KEY,
name CHAR(20) ,
bdate DATE , 
tel CHAR(20)
)

```
上面為創建資料表的範例，總體來說語法可歸納如下:  
```
CREATE TABLE table_ame(
col_name data_type [attributes] [constraints],
col_name data_type [attributes] [constraints],
...
col_name data_type [attributes] [constraints]
)
```

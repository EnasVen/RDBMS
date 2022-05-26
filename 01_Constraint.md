# 限制條件
設定CONSTRAINT的原因在於維護資料完整性與一致性。  
設置可分為column type與table type。  
column type就是像手動建置table時，寫在col後面的字眼；而table type就是寫在column定義後面，以逗點連接，CONSTRAINT開頭:  
```
CREATE TABLE `emp1` (
  `empno` decimal(4,0) NOT NULL PRIMARY KEY,
  `ename` varchar(30) NOT NULL,
  `hiredate` date NOT NULL,
  `email` VARCHAR(30) UNIQUE,
  `salary` INT unsigned CHECK (salary>=24000),
  `deptno` decimal(3,0) NOT NULL,
  `title` varchar(20) NOT NULL default 'engineer',
-- table constraint --
CONSTRAINT emp1_deptno_fk FOREIGN KEY(deptno) references department(deptno)
);
```
詳細的語法如下:  
```
-- col type --
col_name data_type [CONSTRAINT constraint_name] constraint_type
-- table type --
column ... , 
[CONSTRAINT constraint_name] constraint_type (col_name1 , col_name2)
```


CONSTRAINT有以下關鍵字:  
1. DEFAULT
  - 新增資料時，如果該欄位沒有給值，會以DEFAULT值代入
  - DEFAULT value 只能是 literal value，不能是expr或者函數
  - 只能以column level新增
```
col datatype DEFAULT value
```
如果創建表格的時候沒有給DEFAULT value，則INSERT/UPDATE呼叫DEFAULT時會給NULL
```
INSERT INTO tbl VALUES (x,y,DEFAULT);
-- --
UPDATE tbl 
SET a = DEFAULT
WHERE c = c1;
```

2. CHECK
  - 用來檢查欄位是否在值域內
  - 欄位值可以是NULL
  - 如果要設定2個欄位以上，需要以table level設置
```
CREATE TABLE x (
col1 INT CHECK (col1 >= 55)
col2 INT 
)
```
3. UNIQUE
4. PRIMARY KEY
5. FOREIGN KEY
6. NOT NULL
7. AUTO_INCREMENT


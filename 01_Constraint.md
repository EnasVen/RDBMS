設定CONSTRAINT的用途在於維護資料完整性與一致性。  
設置可分為column type與table type。  
宣告時機為CREATE TABLE以及ALTER TABLE時!  
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
# DEFAULT
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

# CHECK
  - 用來檢查欄位是否在值域內
  - 可以是column level也可以是table level
  - 欄位值可以是NULL，但一旦給值就必須符合約束條件
  - 如果要設定2個欄位以上，需要以table level設置
```
CREATE TABLE x (
col1 INT CHECK (col1 >= 55)
col2 INT CONSTRAINT col2_positive CHECK (col2 > 0)
col3 INT CHECK (col3 < 99)
CHECK col1 <> col3
CHECK (c1*5 < 600)
CONSTRAINT col1_nonzero CHECK (col1 -90 > 3 )
)
```

# UNIQUE
  - 欄位值必須唯一
  - column level 或 table level都可以
  - 單一table內可以有多個UNIQUE約束條件
  - 欄位值可以為NULL
```
col_name datatype [CONSTRAINT constraint_name] UNIQUE
```

# PRIMARY KEY
  - 不可為NULL且不可重複
  - tabel level與column level都可以
  - 單一table內只能宣告一次主鍵
  - 單一table內不一定要設置主鍵
  - 若主鍵為一組欄位，則稱為複合主鍵(composite PK)，以table level設置
```
col_name datatype [CONSTRAINT cons_pk_name] PRIMARY KEY(col1 , col2)
```

# FOREIGN KEY
  - 只能以table level宣告
  - 可定義在單一欄位或一組欄位
  - 子表的FK欄位需對應到母表的PK或者UNIQUE欄位，且資料型態要"完全"相同(DECIMAL(4)的話，就不能對到DECIMAL(3))
  - 對應欄位名稱可以不用一樣
  - (規範1)子表新增或修改時，FK欄位值必須對應到母表對應欄位的一個已存在值，否則拒絕新增或修改
  - (規範2)母表刪除或修改時，若子表有其對應的資料，則無法刪除或修改!
  - 上面兩個規範稱為RESTRICT，後面可透過ON語法來設置DELETE與UPDATE功能(預設RESTRICT)
  - CASCADE關鍵字可以讓UPDATE/DELETE動作一次處理完畢(更新/移除母表資料時，同步更新/移除相關的子表資料)
 ```
 -- 設置 --
 CONSTRAINT emp1_deptno_fk FOREIGN KEY(deptno) references department(deptno)
 -- 變更FK遇到刪除新增修改時的動作 --
 ON DELETE {RESTRICT|CASCADE|SET NULL|NO ACTION}
 ON UPDATE {RESTRICT|CASCADE|SET NULL|NO ACTION}
 -- 變更FK條件 --
 ALTER TABLE `db01`.`emp1` 
DROP FOREIGN KEY `emp1_deptno_fk`;
ALTER TABLE `db01`.`emp1` 
ADD CONSTRAINT `emp1_deptno_fk`
  FOREIGN KEY (`deptno`)
  REFERENCES `db01`.`department` (`deptno`)
  ON DELETE CASCADE
  ON UPDATE CASCADE;
 ```
 
# NOT NULL
  - NOT NULL只能以column level撰寫，不能以table level建置
```
col_name datatype NOT NULL
```
# AUTO_INCREMENT
用於自動欄位編號


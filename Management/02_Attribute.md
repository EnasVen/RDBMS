# AUTO_INCREMENT
  - 設置欄位自動編號用(流水號)，必須是整數型態，通常使用UNSIGNED來加大值域
  - 必須設置在約束條件為PK或UNIQUE的欄位上
  - 預設初始值1，每一筆record加1
  - 若無設置初始值或給NULL，default為1
  - 使用select LAST_INSERT_ID()來取得最後的自動編號(但這個方法在一次新增多筆資料時只會抓到該批次的第1個record)
  - 刪除紀錄後，AUTO_INCREMENT欄位不會重新使用被刪除的流水號(從資料表就能看出有空缺)
  - 使用TRUNCATE TABLE後，可以reset流水號，讓編號從自訂預設值或1開始
 ```
 CREATE TABLE a (
 col_name datatype [PRIMARY KEY|UNIQUE]
 )
AUTO_INCREMENT [= 101]
 ```

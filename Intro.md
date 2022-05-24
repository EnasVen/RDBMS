# 資料庫概論
DBMS為DataBase Management Sysyem的縮寫，具備資料的建立、存取與控制功能。  
DBMS有以下5種，其中NoSQL與RDB為目前企業主流使用。  
1. Hierarchical 
2. Network
3. Relation
4. Objext-Oriented
5. NoSQL

1970年 Dr.Codd 提出RDB的最初理論，一個RDBMS需要具備以下結構:  
1. 結構元件 : 一組用以建立資料的結構型態
2. 處理元件 : 一組運算式用來操作資料結構
3. 完整性元件 : 確保資料正確與一致的法則

# Primary
每一筆紀錄會有一個唯一的辨識值(UID)，用來代表table的主鍵值(Primary Key)。  
PK必須唯一，不可重複。  
RDBMS並無規定每一張table都要有PK。  
設定PK可以讓查詢的速度變快。

# Foreign Key
child table透過FK來關連到parent table。  
FK會參考到另一張table的PK。  
child 的 FK欄位 = parent 的 PK欄位  

# 關聯表
關聯表(relation)可視為一個二維表格，用來儲存實體或關係資料的地方。  
關聯表由行(Column)列(Row)組成，在資料庫領域我們通常將col稱為關聯表的attribute(屬性)；而row稱為record(資料錄)。  
行列之間無順序性質

關聯表必須滿足三大完整性:  
1. 實體完整性(Entity Integrity) : 
  - 每一筆table中的資料都是唯一可辨識的(不重複)
  - 透過Primary Key設置完成
2.  參考完整性(Referential Integrity) :
  - 對於table中的欄位值必須關連到父表中的Primary Key值
  - 透過Foreign Key設置完成
3.  區域完整性(Domain Integrity) : 
  - 確保table中的欄位值在允許的範圍內
  - 透過DEFAULT , CHECK , NOT NULL等設定完成

# ER-Model
為一種描述資料庫結構的資料抽象化方式。  
其組成包括:  
1. 實體(Entity) : 資料庫中所存放的個體
2. 屬性(Attribute) : 描述個體性質
3. 關係(RelationShip) : 描述個體之間的相關性

資料庫的設計可透過ER Diagram的方式，以 實體-關係-實體 的圖來建立一對多的情境來完成建置。  

# 關聯式資料庫語言
SQL為Structured Query Language，即結構化查詢語言。  
透過SQL我們可以對資料庫進行查詢、新刪修的目的。  

SQL指令分為3類:  
1. DDL(Data Definition Language):資料定義語言
  - 用來建置資料庫的指令，例如: CREATE TABLE , DROP INDEX ... etc
2. DML(Data Manipulation Language):資料處理語言
  - 用來處理資料庫內容的指令，例如: INSERT , UPDATE , DELETE ...etc
3. DCL(Data Control Language):資料控制語言
  - 用來授予或回收權限的指令，例如: GRANT , REVOKE ... etc

微軟又將DML分成以下兩種:
1. TCL(Transaction Control Language):交易控制語言
  - 例如: COMMIT TRANSACTION
2. DML(Data Query Language):交易資料查詢語言
  - 例如: SELECT

# SQL 撰寫規則
1. 不區分大小寫
  - 關鍵字通常使用大寫
  - table name和attribute name通常為小寫
2. 可寫成一行或多行
  - 不必像Python一樣有固定的indentation
3. 以;作為敘述結束符號

# 命名規則
1. 必須以文字開頭
2. 字元長度最多為128
3. 只能包含(A-Z , a-z , 0~9 , _ , $)
4. 不可使用系統關鍵字
5. 不可與同一個schema所命名的其他物件同名
6. 同一張table下的attribute name不可重複



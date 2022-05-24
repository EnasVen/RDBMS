# 資料型態與值域
MySQL資料儲存型別分為以下幾種，其中length為總長度(default=10)；scale為小數位數(default=0):  
1. 整數型態
  - TINYINT[(length)]: 1byte，預設長度4，值域<img src="https://latex.codecogs.com/png.image?\dpi{110}-2^{7}\sim&space;2^7-1" />
  - SMALLINT[(length)]: 2byte，預設長度6，值域<img src="https://latex.codecogs.com/png.image?\dpi{110}-2^{15}\sim&space;2^{15}-1" />
  - MEDIUMINT[(length)]: 3byte，預設長度9，值域<img src="https://latex.codecogs.com/png.image?\dpi{110}-2^{23}\sim&space;2^{23}-1" />
  - INT[(length)]: 4byte，預設長度11，值域<img src="https://latex.codecogs.com/png.image?\dpi{110}-2^{31}\sim&space;2^{31}-1" />
  - BIGINT[(length)]: 8byte，預設長度20，值域<img src="https://latex.codecogs.com/png.image?\dpi{110}-2^{64}\sim&space;2^{64}-1" />
2. 浮點數型態
  - FLOAT[(length,scale)]: 4byte，總長度超過6位數時會以科學記號表示。，值域<img src="https://latex.codecogs.com/png.image?\dpi{110}-3.4E+38\sim&space;3.4E+38" />
  - DOUBLE[(length,scale)]: 8bytes，總長度超過15位數時會以科學記號表示，值域<img src="https://latex.codecogs.com/png.image?\dpi{110}-1.79E+308\sim&space;1.79E+308" />
  - DECIMAL[(length,scale)]/NUMERIC[(length,scale)]: 固定小數位數 
3. 字串型態
  - CHAR[(n)]: 固定長度字串，預設長度為1，n最大為255byte，未填滿自動補空白。
  - VARCHAR[(n)]: 變動長度字串，n最大為65535byte。儲存空間為字元數+1byte(n<256)或+2byte(n>=256)
  - TINYTEXT: 變動長度字串，n最大為255byte。儲存空間為字元數+1byte
  - TEXT: 變動長度字串，n最大為65535byte。儲存空間為字元數+2byte
  - MEDIUMTEXT: 變動長度字串，n最大為16772215byte。儲存空間為字元數+3byte
  - LONGTEXT: 變動長度字串，n最大為4294967295byte。儲存空間為字元數+4byte
4. 日期型態
  - DATETIME: 1000/1/1~9999/12/31，輸入格式為'YYYY-MM-DD hh:mm:ss'
  - TIMESTAMP: 1970/1/1~2037/12/31，輸入格式為'YYYY-MM-DD hh:mm:ss'
  - DATE: 1000/1/1~9999/12/31，輸入格式為'YYYY-MM-DD'
  - TIME: 輸入格式為'hh:mm:ss'

日期分隔符號可以用/也可以用-


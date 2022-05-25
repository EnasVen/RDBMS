# 彙總函數
透過以下不同函數可以做簡易的敘述性統計:  
1. AVG
2. SUM
3. COUNT
4. MAX/MIN
5. STDEV/VAR
以下僅以AVG和COUNT作範例:
```
SELECT COUNT(*) FROM tbl;
SELECT AVG(col) FROM tbl;
SELECT COUNT(DISTINCT col) FROM tbl;
```
須注意彙總函數除了COUNT(*)有包含NULL之外，其餘都是排除NULL後再計算!  
如果要把NULL當作0來計算，寫法如下:  
```
SELECT AVG(ISNULL(col,0)) FROM tbl;
```

須注意彙總時不可有個別欄位:  
```
SELECT col1 , AVG(col2) FROM tbl; -- 這個寫法是錯誤的 --
```
# 群組運算
使用GROUP BY可以對1個甚至多個欄位做運算，語法如下:  
```
SELECT [欄位] 彙總函數(欄位) [,...] FROM tbl
[WHERE 分組前篩選條件]
[GROUP BY 欄位]
[HAVING 分組後篩選條件]
[ORDER BY 欄位];
```
須注意ORDER BY要放在GROUP BY分群之後，且WHERE不可用於過濾分群資料!(除非使用子查詢或外部參考)  

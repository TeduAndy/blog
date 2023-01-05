---
title: MSSQL 通用語法
date: 2023-01-04 08:00:00
categories: SQL
---

<br>

### **Begin try catch 用法**

- **說明: SQL 遇到語法無法執行，出錯時執行另外的行動**
- **用法:**
```SQL
Begin try
	// 這邊執行要執行的語法
End try

Begin catch
	// 拋錯時需要執行的語法
End catch
```

<br>

### **Begin try catch 加入交易 Transaction**
- **說明: 在執行多筆更新或者創建多筆資料時，遇到其中一筆錯誤但是其他筆都有進去，此時應該全部返還回去，重新來過，確保資料的正確性**
- **用法:**
```SQL
Begin try
	Begin Transaction  // 開啟交易
	// 這邊執行要執行的語法
	Commit Transaction // 上面執行的語法如果能順利走到這裡則做確認交易
End try
Begin catch
	Rollback Transaction // 上面語法出現錯誤時會跳來這邊，直接做回復資料
End catch
```

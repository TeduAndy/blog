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


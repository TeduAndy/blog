---
title: SQL 函數使用方法
date: 2022-11-02 15:48:00
categories: SQL
---


### **1.Decode 函数**
#### **說明：**
```SQL
Decode(表達式, 條件1, 結果1, 條件2, 結果, 其他)
```
#### 實例：
表名: product
| ID     | item     | price    | 
| :----: | :----:   | :----:   | 
| A01    | 口香糖    | 10       |
| A01    | 茶葉蛋    | 8        |
| A02    | 香菸      | 80       |
| A02    | 報紙      | 10       |
```SQL
Select ID, item, Decode(price, '10', '十', '80', '八十', '其他') From product
```
#### 輸出：
| ID     | item     | price    | 
| :----: | :----:   | :----:   | 
| A01    | 口香糖    | 十       |
| A01    | 茶葉蛋    | 其他     |
| A02    | 香菸      | 八十     |
| A02    | 報紙      | 十       |

<br>

### **2.計算型函數**
+ **AVG (平均)**
+ **COUNT (計數)**
+ **MAX (最大值)**
+ **MIN (最小值)**
+ **SUM (總合)**
#### **說明：通常會搭配 Groub By 使用 **
```SQL
Select "函數名"("欄位名") From "表格名";
```
#### 實例：
表名: product
| ID     | item     | price    | 
| :----: | :----:   | :----:   | 
| A01    | 口香糖    | 10       |
| A01    | 茶葉蛋    | 8        |
| A02    | 香菸      | 80       |
| A02    | 報紙      | 10       |
```SQL
以 ID 作為分組
Select ID, Sum(price) From product Groub By ID
```
#### 輸出：
| ID     | price     |
| :----: | :----:   |
| A01    | 18    | 
| A02    | 90    |

<br>

### **3.Partition By的用法**


#### 一、rank()

**rank() over(partition by A order by B)是按照A进行分组，分组里面的数据按照B进行排序，over即在什么之上，rank()即跳跃排序(比如存在两个第一名，接下来就是第三名) 举例：**
```SQL
select 课程, 学生ID, 分数, rank() over (partition by 课程 order by 分数 desc) as 排名 from 成绩表
```

#### 二、row_number()

**row_number() over(partition by A order by B)row_number(): 如果有两个第一名时，只返回一个结果。 举例：**
```SQL
select 课程, 学生ID, 分数, row_number() over (partition by 课程 order by 分数 desc) as 排名 
from 成绩表
```

#### 三、dense_rank()

**dense_rank() over(partition by A order by B)dense_rank(): 连续排序(如果有两个第一名时，接下来仍然是第二名) 举例：**
```SQL
select 课程, 学生ID, 分数, rank() over (partition by 课程 order by 分数 desc) as 排名 
from 成绩表
```

<br>

### **4.Substr的字串擷取用法**

#### 說明：
- 用來擷取欄位的某一部分使用，每一個資料庫名稱不全相同。
- MySQL: SUBSTR( ), SUBSTRING( )
- Oracle: SUBSTR( )
- SQL Server: SUBSTRING( )

#### example：
```SQL
 Select SUBSTR(欄位名, 從第幾個開始) From table
```

<br>

#### 實例(table:pet)：
| Name   | favorite | 
| :----: | :----:   | 
| 張一   |   dog    |
| 王二   |   dog    | 
| 李三   |   cat    |
```sql
-- 正數開始
Select  SUBSTR(favorite, 2) As favorite From pet

-- 負數開始
Select SUBSTR(favorite, -2) As favorite From pet

-- 兩個 SQL 最後結果都是一樣
```
| favorite | 
| :----:   | 
|   og    |

<br>

### **5. TO_CHAR的轉成字串用法**

#### 說明：
- 將日期、數字其他型別轉換成字串格式

<br>

#### example：
```SQL
 Select TO_CHAR(欄位名) As 欄位名 From table
```
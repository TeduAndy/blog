---
title: SQL 常用語法
date: 2022-07-18 16:54:51
categories: SQL
---
<style>
	.center{
		mar
	}
</style>

## **讀取資料**
```SQL
SELECT *(或者字段名) FROM 表格 WHERE 條件 AND 條件
SELECT *(或者字段名) FROM 表格 WHERE 條件 OR 條件
```

<br>

## **插入資料(單一)**
```SQL
INSERT INTO 表名(字段名, 字段名 ) VALUES (插入的值, 插入的值)
```

<br>

## **插入資料(單一)**
```SQL
INSERT INTO 表名(字段名, 字段名 ) VALUES (插入的值, 插入的值)
```

<br>

## **插入多筆資料**
```SQL
INSERT INTO 新表名(字段名1, 字段名2, … ) SELECT 字段名1, 字段名2..  FROM 舊表明
```

<br>

## **更新語句**
```SQL
UPDATE 表名 SET 字段名="" WHERE 條件
```

<br>

## **刪除語句(表內的某一條)**
```SQL
DELETE FROM 表名 WHERE 條件
```

<br>

## **刪除 表**
```SQL
DROP table 表名
```

<br>

## **刪除 資料庫**
```SQL
DROP database 資料庫名
```

<br>

## **創建資料庫**
```SQL
CREATE DATABASE 資料庫名字 CHARACTER SET utf8
```

<br>

## **創建表**
```SQL
CREATE TABLE 表名 (欄位名字 欄位型態 not null, 欄位名字 欄位型態, PRIMARY KEY(欄位名字))
```

<br>

## **函數使用(運算類)**

+ **AVG (平均)**
+ **COUNT (計數)**
+ **MAX (最大值)**
+ **MIN (最小值)**
+ **SUM (總合)**
#### **example：**
```SQL
SELECT "函數名"("欄位名") FROM "表格名";
```

<br>

## **GROUP BY 使用**
```SQL
SELECT Store_Name, SUM(Sales)
FROM Store_Information
GROUP BY Store_Name;

說明: 針對店名 算出 sales 總和

輸出之後為這樣

Store_Name	   SUM(Sales)
Los Angeles	     1800
San Diego	     250
Boston	             700
```

<br>

## **HAVING 使用**
<br>
#### 說明：
	HAVING 子句通常是在一個 SQL 句子的最後。
	一個含有 HAVING 子句的 SQL 並不一定要包含 GROUP BY 子句。

#### example：
```SQL
SELECT Store_Name, SUM(Sales)
FROM Store_Information
GROUP BY Store_Name
HAVING SUM(Sales) > 1500;

說明: 找出 營業額總和 大於 1500 的店家
```

<br>

## **LEFT JOIN 使用**
```SQL
SELECT table_column1, table_column2...
FROM table_name1
LEFT JOIN table_name2
ON table_name1.column_name=table_name2.column_name;
```
**LEFT JOIN <font color='red'>可以用來建立左外部連接</font>，查詢的 SQL 敘述句 LEFT JOIN <font color='red'>左側資料表 (table_name1)的所有記錄都會加入到查詢結果中，即使右側資料表 (table_name2) 中的連接欄位沒有符合的值也一樣。</font>**

<br>

## **RIGHT JOIN 使用**
```SQL
SELECT table_column1, table_column2...
FROM table_name1
RIGHT JOIN table_name2
ON table_name1.column_name=table_name2.column_name;
```

<br>

## **INNER JOIN 使用**
```SQL
SELECT table_column1, table_column2...
FROM table_name1
INNER JOIN table_name2
ON table_name1.column_name=table_name2.column_name;
```
**LEFT JOIN <font color='red'>可以用來建立兩邊的交集</font>，查詢的 SQL 敘述句 INNER JOIN <font color='red'>左側跟右側資料表都有相同 (table_name1) 的記錄都會加入到查詢結果中，沒有符合的值就不會</font>。**

<br>

## **Partition By的用法**


### 一、rank()

**rank() over(partition by A order by B)是按照A进行分组，分组里面的数据按照B进行排序，over即在什么之上，rank()即跳跃排序(比如存在两个第一名，接下来就是第三名) 举例：**
```SQL
select 课程, 学生ID, 分数, rank() over (partition by 课程 order by 分数 desc) as 排名 from 成绩表
```

### 二、row_number()

**row_number() over(partition by A order by B)row_number(): 如果有两个第一名时，只返回一个结果。 举例：**
```SQL
select 课程, 学生ID, 分数, row_number() over (partition by 课程 order by 分数 desc) as 排名 
from 成绩表
```

### 三、dense_rank()

**dense_rank() over(partition by A order by B)dense_rank(): 连续排序(如果有两个第一名时，接下来仍然是第二名) 举例：**
```SQL
select 课程, 学生ID, 分数, rank() over (partition by 课程 order by 分数 desc) as 排名 
from 成绩表
```

<br>

## **CASE 關鍵字 (SQL CASE Keyword)**
<br>
#### 說明：
	CASE 類似於程式語言裡的 if/then/else 語句，用來作邏輯判斷。
#### example：
```SQL
CASE
WHEN condition THEN result
[WHEN···]
[ELSE result]
END;

或者

CASE expression
WHEN value THEN result
[WHEN···]
[ELSE result]
END;
```

#### 實例：
| Name   | Answer | 
| :----: | :----: | 
| 張一 |   1    |
| 王二 |   2    | 
| 李三 |   3    |
```SQL
select Name, case Answer
	when 1 then '喜歡'
	when 2 then '不喜歡'
	when 3 then '還OK'
END
FROM questionnaire;

select Name, case
	when Answer=1 then '喜歡'
	when Answer=2 then '不喜歡'
	when Answer=3 then '還OK'
END
AS Answer
FROM questionnaire;
```
#### 結果：
| Name   | Answer | 
| :----: | :----: | 
| 張一 |   喜歡    |
| 王二 |   不喜歡  | 
| 李三 |   還可以  |

<br>

## **ALTER TABLE**

**可用方法:**

- **加欄位**
- **刪欄位**
- **改變欄位名稱**
- **改變欄位的資料種類**

#### 1.加入欄位
```SQL
ALTER TABLE 表名 ADD 欄位名稱 資料類型(20);
```

#### 2.改欄位名稱
```SQL
ALTER TABLE 表名 CHANGE 欄位名稱 新名稱 資料型態();
```

#### 3.修改欄位資料型態
```SQL
ALTER TABLE 表名 MODIFY 欄位名稱 修改的資料型態();
```

#### 4.刪除欄位
```SQL
ALTER TABLE 表名 DROP 欄位名稱;
```

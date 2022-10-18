---
title: Oracle 常用進階語法
date: 2022-10-12 16:54:51
categories: SQL
---

## listagg 串聯多筆成一筆

#### 實例：
| ID     | item     | price    | 
| :----: | :----:   | :----:   | 
| A01    | 口香糖    | 10       |
| A01    | 茶葉蛋    | 8        |
| A02    | 香菸      | 80       |
| A02    | 報紙      | 10       |


```SQL
select ID, 
listagg(Item, ',') within group (order by price) as ItemList
from Order
group by OrderNo
```

#### 輸出：
| ID     | ItemList     | 
| :----: | :----:       | 
| A01    | 茶葉蛋,口香糖 | 
| A02    | 報紙, 香菸    |

#### 使用說明：
```SQL
select ID, 
listagg(相同ID但是欄位值不同且需要合併, 合併時使用的連接符) within group (order by 參照某個欄位讓合併的進行排序連接) as ItemList
from Order
group by ID
```



---
title: GIT 常用指令
date: 2022-07-19 09:03:25
categories: GIT
---

## 常用指令


### **1.建立新的本地端 Repository。**
```GIT
git init
```

<br>

### **2.複製遠端的 Repository 檔案到本地端。**
```GIT
git clone [Repository URL]
```

<br>

### **3.檢查本地端檔案異動狀態。**
```GIT
git status
```

<br>

### **4.將指定的檔案（或資料夾）加入版本控制。用 `git add .` 可加入全部。**
```GIT
git add [檔案或資料夾]
```

<br>

### **5.提交（commit）目前的異動。**
```GIT
git commit
```

<br>

### **6.提交（commit）目前的異動並透過 `-m` 參數設定摘要說明文字。**
```GIT
git commit -m "提交說明內容"
```

<br>

### **7.獲取目前工作目錄的 dirty state，並保存到一個未完成變更的 stack，以方便隨時回復至當初的 state。**
```GIT
git stash
```

<br>

### **8.查看先前的 commit 記錄。**
```GIT
git log
```

<br>

###  **9.將本地端 Repository 的 commit 發佈到遠端。**
```GIT
git push
```

<br>

### **10.發佈至遠端指定的分支（Branch）**
```GIT
git push origin [BRANCH_NAME]
```
<br>

### **11.添加遠端分支**
```Git
git remote add [name] [your https url]
            [遠端網址別名]   [github網址]
```

<br>

### **12.查看分支。**
```GIT
git branch
```

<br>

### **13.建立分支。**
```GIT
git branch [BRANCH_NAME]
```

<br>

### **14.取出指定的分支(切換分支)**
```GIT
git checkout [BRANCH_NAME]
```

<br>

### **15.建立並跳到該分支。**
```GIT
git checkout -b [BRANCH_NAME]
```

<br>

### **16.強制刪除指定分支（須先切換至其他分支再做刪除）。**
```GIT
git branch -D [BRANCH_NAME]
```

<br>

### **17.強制恢復到指定的 commit（透過 Hash 值）。**
```GIT
git reset --hard [HASH]
```

<br>

### **18.切換到指定的 commit（與 `git checkout [BRANCH_NAME]` 相同)。**
```GIT
git checkout [HASH]
```

<br>

### **19.修改分支名稱。**
```GIT
git branch -m <OLD_BRANCH_NAME> <NEW_BRANCH_NAME>
```

<br>

### **20.檢視歷史提交紀錄**
```Git
git log --oneline
```

<br>

+ **21.遠端資料最新版拉到本地（本地更新）**
```Git
git pull (全部)

git pull origin master
                [分支]
```

<br>

### **22.刪除本地分支**
```Git
git branch -d <branch>
                [分支]
```

<br>

### **23.刪除遠端分支**
```Git
git push origin :<branch>
                  [分支]
```

<br>


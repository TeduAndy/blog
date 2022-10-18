---
title: GIT 常用指令
date: 2022-07-19 09:03:25
categories: GIT
---

## 常用指令


+ **建立新的本地端 Repository。**
```GIT
git init
```

<br>

+ **複製遠端的 Repository 檔案到本地端。**
```GIT
git clone [Repository URL]
```

<br>

+  **檢查本地端檔案異動狀態。**
```GIT
git status
```

<br>

+ **將指定的檔案（或資料夾）加入版本控制。用 `git add .` 可加入全部。**
```GIT
git add [檔案或資料夾]
```

<br>

+ **提交（commit）目前的異動。**
```GIT
git commit
```

<br>

+ **提交（commit）目前的異動並透過 `-m` 參數設定摘要說明文字。**
```GIT
git commit -m "提交說明內容"
```

<br>

+ **獲取目前工作目錄的 dirty state，並保存到一個未完成變更的 stack，以方便隨時回復至當初的 state。**
```GIT
git stash
```

<br>

+ **查看先前的 commit 記錄。**
```GIT
git log
```

<br>

+  **將本地端 Repository 的 commit 發佈到遠端。**
```GIT
git push
```

<br>

+  **發佈至遠端指定的分支（Branch）**
```GIT
git push origin [BRANCH_NAME]
```

<br>

+  **查看分支。**
```GIT
git branch
```

<br>

+  **建立分支。**
```GIT
git branch [BRANCH_NAME]
```

<br>

+  **取出指定的分支。**
```GIT
git checkout [BRANCH_NAME]
```

<br>

+  **建立並跳到該分支。**
```GIT
git checkout -b [BRANCH_NAME]
```

<br>

+  **強制刪除指定分支（須先切換至其他分支再做刪除）。**
```GIT
git branch -D [BRANCH_NAME]
```

<br>

+  **強制恢復到指定的 commit（透過 Hash 值）。**
```GIT
git reset --hard [HASH]
```

<br>

+  **切換到指定的 commit（與 `git checkout [BRANCH_NAME]` 相同)。**
```GIT
git checkout [HASH]
```

<br>

+  **修改分支名稱。**
```GIT
git branch -m <OLD_BRANCH_NAME> <NEW_BRANCH_NAME>
```

+ **檢視歷史提交紀錄**
```Git
git log --oneline
```

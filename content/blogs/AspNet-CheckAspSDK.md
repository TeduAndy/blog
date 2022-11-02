---
title: ASP.NET 查看環境安裝版本
date: 2022-11-01 08:00:00
categories: Asp.net
---


### **打開 cmd**

#### **查看 Asp.Net Framework**
```cmd
reg query "HKLM\Software\Microsoft\NET Framework Setup\NDP" /s /v version | findstr /i version | sort /+26 /r
```

<br>


#### **查看 Asp.net Core 版本**

<br>

##### **指令一: Help** 
```
dotnet help
```

<br>

##### **指令二: 當前運行版本** 
```
dotnet --version
```

<br>

##### **指令三: 查看已安装所有SDK版本** 
```
dotnet --list-sdks
```

<br>

##### **指令三: 查看已安装所有版本，包括地址** 
```
dotnet --info
```



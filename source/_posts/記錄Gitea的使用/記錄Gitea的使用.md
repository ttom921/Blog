---
title: 記錄Gitea的使用
categories:
  - 記錄
tags:
  - git
date: 2018-05-24 16:04:31
---

因為在專案使用，使會有問是產生，要追踨問題，所以使用這套不用錢的來試一下
目前安裝在windows上，官方是說有跨平台
* 最簡單的方法
  [直接下載](https://dl.gitea.io/gitea/)只要一個指令就可以看到歡迎畫面了
  1. 將下載的執行檔修變檔名成gitea.exe
  2. 在d:下建立了gitea的資料夾,將執行檔移到目錄
  執行執行檔，設定為SQLite3
  儲存庫的位置 D:\gitea-repositories  
  取消OpenID
  可以從原來的專案匯入git
  

  
* 設定檔的說明
  在 custom/conf/app.ini  
```
 [repository]
 DEFAULT_PRIVATE = true
 [service]
 DISABLE_REGISTRATION 禁用註冊，啟用只能用管理員添加用戶  
```
只設定ROOT_URL = http://localhost:3000/ 修改成自已服務器的IP
* 可以附加檔案
在 custom/conf/app.ini
```
[attachment]
; Whether attachments are enabled. Defaults to `true`
ENABLED = true
; Path for attachments. Defaults to `data/attachments`
PATH = data/attachments
; One or more allowed types, e.g. image/jpeg|image/png
ALLOWED_TYPES = */*
; Max size of each file. Defaults to 4MB
MAX_SIZE = 4
; Max number of files per upload. Defaults to 5
MAX_FILES = 5
```

* 在專案有標籤
  **注意第一次一定要按下，標籤會產生一組預設的標籤，可以來分類**
* 組織的建立
  + 1 先建立組織
  + 2 再建立team
      可設定權限
  + 3 再將人員加入team
  
* 可以有備份功能
  執行就會有zip檔，它會備份設定檔和儲存庫，要覆原時直接解壓覆蓋原來的檔案位置和路徑
  
  ```
   gitea-1.4.1-windows-4.0-amd64.exe dump
  ```
* 備份的批次檔
```
Taskkill /IM gitea.exe /F
for /f "delims=" %%a in ('wmic OS Get localdatetime  ^| find "."') do set dt=%%a
set datestamp=%dt:~0,8%
set YYYY=%dt:~0,4%
mkdir  Z:\prjback\gitea\%YYYY%\%datestamp%
set giteaext="gitea.exe"
rem "執行程式的備份"

%giteaext% dump
copy *.zip Z:\prjback\gitea\%YYYY%\%datestamp%
del *.zip
gitea.exe

```
 
* 參考資料
  * [用Gitea架設自用的Git Server](http://jdev.tw/blog/5089/windows-git-server-gitea)
  * [開發者另類的自架 Git 服務選擇: Gitea](https://blog.wu-boy.com/2017/01/new-git-code-hosting-option-gitea/)
  * [建置自己的 Git 伺服器與網站](https://yami.io/gitea/)
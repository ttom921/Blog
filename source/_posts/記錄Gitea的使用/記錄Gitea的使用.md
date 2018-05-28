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
  在d:下建立了gitea的資料夾,將執行檔移到目錄
  執行執行檔，設定為SQLite3
  儲存庫的位置 D:\gitea-repositories  
  取消OpenID
  可以從原來的專案匯入git
* 可以有備份功能
  執行就會有zip檔，它會備份設定檔和儲存庫，要覆原時直接解壓覆蓋原來的檔案位置和路徑
  ```
  gitea-1.4.1-windows-4.0-amd64.exe dump
  ```
* 參考資料
  * [用Gitea架設自用的Git Server](http://jdev.tw/blog/5089/windows-git-server-gitea)
  * [開發者另類的自架 Git 服務選擇: Gitea](https://blog.wu-boy.com/2017/01/new-git-code-hosting-option-gitea/)
  * [建置自己的 Git 伺服器與網站](https://yami.io/gitea/)
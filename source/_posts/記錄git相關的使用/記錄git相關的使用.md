---
title: 記錄git相關的使用
categories: [記錄]
tags: [git]
date: 2018-03-08 10:08:33
---
### 在github出現安全的問題
如下的警告
"We found potential security vulnerabilities in your dependencies."
可到它的列表看那一個模組需要升級
例如
ssri 有問題它會要你升級到那一版
```
npm install ssri@5.2.2 --save
```
### 如何在tortoisegit合併branch
+ 1-1 首先，我們要先把儲存庫目前的版本HEAD切換回主要分支master上。這個動作叫做Checkout
+ 1-2 當你按右鍵的時候,然後選擇的是TortoiseGit中的「合併」功能
+ 1-3 請選擇你要拿來合併的分支，也就是你剛剛開發完新功能的分支

##### 參考
* [完成新功能開發：合併Branch](http://blog.pulipuli.info/2013/02/github-part3-git.html#postcatagithub-part3-git.html0_anchor12)


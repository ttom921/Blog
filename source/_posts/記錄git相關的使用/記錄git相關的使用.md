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
#### 列出git的版本圖
```
git log --all --decorate --oneline --graph
```
* [討論git版本圖](https://stackoverflow.com/questions/1057564/pretty-git-branch-graphs)
* [Git 版本控制 branch model 分支模組基本介紹](https://blog.wu-boy.com/2011/03/git-%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6-branch-model-%E5%88%86%E6%94%AF%E6%A8%A1%E7%B5%84%E5%9F%BA%E6%9C%AC%E4%BB%8B%E7%B4%B9/)
* [Git Branch 的操作與基本工作流程](https://blog.gogojimmy.net/2012/01/21/how-to-use-git-2-basic-usage-and-worflow/)

#### 列出所有的git的branch的指令
```
git branch -a # 列出所有 branch
```
#### 刪除git的branch的指俞
```
git branch -d new-branch
git push origin :cat
```
#### 列出所有git的tab
local端
```
git tag -l
```
Remote端
```
git ls-remote --tags origin
```
#### 刪除git的tag
local端
```
git tag -d 12345
```
Remote端
```
git push --delete origin tagName
```

### 如何在tortoisegit合併branch
+ 1-1 首先，我們要先把儲存庫目前的版本HEAD切換回主要分支master上。這個動作叫做Checkout
+ 1-2 當你按右鍵的時候,然後選擇的是TortoiseGit中的「合併」功能
+ 1-3 請選擇你要拿來合併的分支，也就是你剛剛開發完新功能的分支

##### 參考
* [完成新功能開發：合併Branch](http://blog.pulipuli.info/2013/02/github-part3-git.html#postcatagithub-part3-git.html0_anchor12)


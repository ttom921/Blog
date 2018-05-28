---
title: 記錄Hexo的升級
categories:
  -  記錄
tags:
  - Hexo
date: 2018-05-27 22:40:30
---
#### 記錄Hexo的升級
在Hexo的目錄下，看那些需要升級
下面的指令會顯示那些需要升級
```
npm outdated
```
顯示如下
```
Package      Current  Wanted  Latest  Location
hexo           3.5.0   3.7.1   3.7.1  hexo-site
hexo-server    0.2.2   0.2.2   0.3.2  hexo-site
```
修改一下package.json的文件，好了就npm更新一下
```
npm install --save
```


* 參考資料
  * [将 Hexo 升级到 v3.5.0](https://tommy.net.cn/2018/02/26/upgrade-hexo-to-v3-5-0/)
---
title: 記錄Hexo的使用
date: 2018-01-28 09:59:49
categories: [記錄]
tags: [hexo]
---
## 第一次從github上下載專案後，要先安裝hexo
``` bash
$npm install hexo -g
```
## 在local端測試，執行以下

``` bash
$hexo server
```
## 記錄完後要上傳和產生
``` bash
$hexo g
$hexo d
```
## Hexo 常用簡寫命令
``` bash
$hexo n #生成文章，或者source\_posts手動編輯
$hexo n #本地發佈預覽
$hexo g #生成public靜態文件
$hexo d #部署之前生成的文件
```
## Hexo 設定
我的設定是如下
```
permalink: :title/
new_post_name: :title\:title.md 
post_asset_folder = true
```
會產生一個和文章相同的資料夾，
下面會在有一樣的名稱的資料夾，post_asset_folder = true ，意思是產生文章的時候，順便產生與文章同名的資料夾。目的是為了管理資源，使同一篇文章的圖片或檔案，都收錄在同一資料夾中
## 產生新的文章
指令如下
```
hexo new post "記錄Hexo的使用"
```
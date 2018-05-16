---
title: 記錄Vim顏色的使用
categories:
  - 設定
tags:
  - CentOS
date: 2018-05-16 10:11:54
---
#### 這是記錄Vim的顏色的設定
原來的設定有在註解看不清楚，所以來設定一下
 * 下載molokai的配色
    先檢查vim安裝的目錄
	```
	whereis vim
	```
	在到vim的安裝目錄，會看到vim74或vim73,看你安裝的版本，我的是vim74，在vim74下有目錄是colors,將下載解壓的molokai.vim
	放在此，在參考資料下有gitthub,請自行下載，下載後放在colors的目錄下
 * 在使用者建立配色
   在~目錄建立文件
   ```
   vi .vimrc
   ```
   目前的內容如下
   ```
   set t_Co=256
   :set nu
   :colorscheme molokai
   hi Comment ctermfg=lightblue
   ```
   
* 參考資料
 * [molokai](http://worldend.logdown.com/posts/746211-adjust-the-color-of-comment-in-vim)
 * [調整 VIM 的註解顏色](https://vim.ink/vim-color-schemes.html)
 * [VIM学习笔记：设置VIM的配色方案](http://www.cnblogs.com/heiing/archive/2012/02/02/2335825.html)
 * [個人化自己的vim文字編輯器(.vimrc設定教學)](https://magiclen.org/vimrc/)
 
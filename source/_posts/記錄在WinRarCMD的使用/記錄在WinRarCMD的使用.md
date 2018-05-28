---
title: 記錄在WinRarCMD的使用
categories:
  - 記錄
tags:
  - CentOS
date: 2018-05-16 13:40:55
---
#### 記錄一下WinRar如何使用cmd
* 單一檔案壓縮
```
"C:\Program Files\WinRAR\WinRAR.exe"  a -afzip -ep1 111.zip 111.txt
```
* 包括資料夾
```
"C:\Program Files\WinRAR\WinRAR.exe"  a -afzip -ep1 222.zip "D:\tools\Putty\dirrar" -r
``` 
* 資料夾下的資料
```
"C:\Program Files\WinRAR\WinRAR.exe"  a -afzip -ep1 222.zip "D:\tools\Putty\dirrar\*.*" -r
``` 
* 參考資料
 * [Compressing files with WinRar command-line - files in use (https://stackoverflow.com/questions/17876046/compressing-files-with-winrar-command-line-files-in-use)
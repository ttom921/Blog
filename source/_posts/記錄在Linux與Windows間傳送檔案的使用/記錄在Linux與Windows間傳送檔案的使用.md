---
title: 記錄在Linux與Windows間傳送檔案的使用
categories:
  - 記錄
tags:
  - centos
date: 2018-05-16 12:03:13
---
#### 記錄將windwos的檔案傳送到linux
可以從PuTTY官方下載putty.exe以及pscp.exe。

* 將Windows中的檔案傳送至Linux中的某個資料夾下
要輸入密碼
```
pscp D:\tools\Putty\111.txt root@192.168.2.222:/home/ttom
```
不要輸入密碼
```
pscp -pw xxxxxxxx D:\tools\Putty\111.txt root@192.168.2.222:/home/ttom
```
* 參考資料
 * [PuTTY官方](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
 * [使用PSCP在Linux與Windows間傳送檔案](https://jeremysu0131.github.io/Tool-Putty-%E4%BD%BF%E7%94%A8PSCP%E5%9C%A8Linux%E8%88%87Windows%E9%96%93%E5%82%B3%E9%80%81%E6%AA%94%E6%A1%88/)
 * [在Linux與Windows間傳送檔案 – 步驟教學](https://loveamberbird.wordpress.com/2013/08/21/%E3%80%90%E7%AD%86%E8%A8%98%E3%80%91%E5%9C%A8linux%E8%88%87windows%E9%96%93%E5%82%B3%E9%80%81%E6%AA%94%E6%A1%88%E6%AD%A5%E9%A9%9F%E6%95%99%E5%AD%B8/)
---
title: 記錄LinuxShell的使用
categories:
  - 記錄
tags:
  - linux,bash
date: 2018-05-23 10:18:07
---
#### 記定vim的顏色
所以通常小弟僅修改在使用者家目錄下的 .vimrc 來針對每個使用者調整預設的顏色
```
shell# vim /home/eric/.vimrc
 
hi Comment ctermfg=cyan
```
#### 記錄bash的使用
  因為會用到linux的script所以在此記錄一下。
* 基本標頭寫法
```
 #!/bin/bash
 # Program:
 #       This program shows "Hello World!" in your screen.
 # History:
 # 2018-05-23	ttom	First release
 PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
 export PATH
 echo -e "Hello World! \a \n"
 exit 0
```
* 產生日期  
```
 diryear="`date +'%Y'`"
 dirmonth="`date +'%m'`" 
 slideshow="`date +'%Y-%m-%d'`"
 
```
* FTP的操作
```
 ftp_server='******' 
 ftp_username='******' 
 ftp_password='******'  
```
* mysql的備份
```
 db_user='root'
 db_pwd='11111111'
 db_backup='Gomo.Dev'
 filename="$db_backup-"`date +%Y-%m-%d-%H-%M-%S`
 mysqlfile_name="$filename.sql"
 #mysql的備份
 mysqldump -u $db_user -p$db_pwd -R --databases $db_backup > $mysqlfile_name

```
* 壓縮
```
  zipfile="$filename.zip"
  zip $zipfile $mysqlfile_name
  rm -rf $mysqlfile_name

```
* ftp上傳
```
 diryear="`date +'%Y'`"
 dirmonth="`date +'%m'`"
 ftp -n $ftp_server <<END_SCRIPT
 quote USER $ftp_username
 quote PASS $ftp_password
 binary
 cd gomo
 mkdir "$diryear"
 cd "$diryear"
 mkdir "$dirmonth"
 cd "$dirmonth"
 pwd
 put "$zipfile"
 quit
 END_SCRIPT
 rm -rf $zipfile
 echo "finish -> $zipfile"
```





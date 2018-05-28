---
title: 記錄Linux指令的使用
categories:
  - 記錄
tags:
  - Linux
date: 2018-05-28 09:32:40
---
#### 記錄Linux指令的使用
### pi的bash
```
#!/bin/bash
# Program:
#       User input a scale number to calculate pi number.
# History:
# 2015/07/16    VBird   First release
PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
export PATH
echo -e "This program will calculate pi value. \n"
echo -e "You should input a float number to calculate pi value.\n"
#read -p "The scale number (10~10000) ? " checking
num=7000           # 開始判斷有否有輸入數值
echo "num is $num"
echo -e "Starting calculate pi value.  Be patient."
time echo "scale=${num}; 4*a(1)" | bc -lq

```
### 指令crontab
啟動crontab
```
sudo service crond start
```
檢查是crontab的指令是否有執行
```
tail -f /var/log/cron
```
* 編輯crontab
crontab -e 進入編輯
```
crontab -e 
```
* 列出crontab
```
crontab -l
```
* 每一分鐘執行一次

以下是範列
```
*/1 * * * * ttom /home/ttom/cal_pi.sh
```
### 系統郵件
在linux裏會有出現
```
您有新郵件在 /var/spool/mail/ttom
```
可以使用mail的讀取
清空很簡單，只需要進入/var/spool/mail就好
```
echo ''>ttom
```
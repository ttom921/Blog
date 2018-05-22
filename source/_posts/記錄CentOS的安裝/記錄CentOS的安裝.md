---
title: 記錄CentOS的安裝
categories: [記錄]
tags: [CentOS,MariaDB,Nginx ]
date: 2018-03-01 10:28:43
---
  記錄CentOS的安裝,主機板有使用UEFI和沒有使用UEFI
## 有使用UEFI
  在設置biso的UEFI的設罝，將QuickBoot/FastBoot和Secure Boot已被禁用
## 在使用ISO燒錄的注意事項
  目前使用Rufus,選擇GPT
## 文字模式安裝
inst.text  
```
vmlinuz initrd=initrd.img linux dd quiet
vmlinuz initrd=initrd.img inst.stage2=hd:/dev/sdc4 quiet
```
   
## 防火牆設定
顯示目前的設定
```
 firewall-cmd --list-all
```
需要打開的防火牆
```
firewall-cmd --permanent --add-port=3306/tcp
firewall-cmd --permanent --add-port=8080/tcp
firewall-cmd --permanent --zone=public --add-port=22/tcp
firewall-cmd --reload
```
## 關閉 SELinux
開啟檔案 /etc/selinux/config:
 vi /etc/selinux/config
找到以下一行:
SELINUX=enforce
改成:
SELINUX=disabled

## 安裝MariaDB 
  透過 MariaDB 官方提供的 Repositories快速的在 Linux 上佈署 MariaDB 是蠻簡單的事情
像是 Ubuntn 或 Debian 也都只需要跟著步驟操作即可首先連結到 [Setting up MariaDB Repositories](https://downloads.mariadb.org/mariadb/repositories/#mirror=ossplanet) 頁面
選擇 系統、版本 和 MariaDB 版本，稍等一下就會顯示安裝步驟
以 CentOS 7 為例
先在 /etc/yum.repos.d/MariaDB.repo 檔案，內容如下
```
# MariaDB 10.2 CentOS repository list - created 2017-11-28 09:28 UTC
# http://downloads.mariadb.org/mariadb/repositories/
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.2/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
```
接著時間下 yum 指令來進行安裝
```
yum install MariaDB-server MariaDB-client
或
sudo MariaDB-server MariaDB-client
```
若詢問是否 Importing GPG key 就同意吧,等跑完就安裝起好了
啟動 並設定開啟 自動啟動
```
# 馬上啟動 MariaDB
systemctl start mariadb
# 設定開機自動啟動
systemctl enable mariadb
```
若是全新安裝，就是跟著做安全性的初始化
```
# 設定 root 的密碼
# 將 new-password 取代成要使用的新密碼
[root@git ~]# /usr/bin/mysqladmin -u root password 'new-password'
 
[root@git ~]# /usr/bin/mysql_secure_installation
 
# 輸入目前的 root 密碼，直接輸入剛剛設定的密碼
Enter current password for root (enter for none):
 
# 是否變更 root 密碼，因為是剛設定 應該不用變更了
Change the root password? [Y/n]
 
# 是否移除匿名帳號，按下 y 選擇移除
Remove anonymous users? [Y/n]
 
# 是否拒絕遠端使用 root 權限登入
# 依照個別需求，沒特別需要遠端管理就按 y 吧
Disallow root login remotely? [Y/n]
 
# 是否移除 test 這個測試資料庫，和相關權限
# 沒有需求就移除吧
Remove test database and access to it? [Y/n]
 
# 是否重新載入權限資料表，按 y
Reload privilege tables now? [Y/n]

```
### MariaDB設定utf8
在  /etc/my.cnf.d/server.cnf
```
[mysqld]
init-connect='SET NAMES utf8mb4'
collation_server=utf8mb4_unicode_ci
character_set_server=utf8mb4
``` 
在 /etc/my.cnf.d/mysql-clients.cnf
```
[mysql]
default-character-set=utf8mb4

```
## mysql命令
```
sudo systemctl restart mariadb
sudo systemctl status mariadb
```
若啟動失敗，可至 /var/log/mariadb/error.log 查看錯誤記錄
## 新增使用者帳號
在 host_db 主機登入資料庫
```
$ mysql -u root -p
```
新增一個可從 host_web 主機登入的使用者 username ，密碼為 password
```
CREATE USER 'username'@'host_web' IDENTIFIED BY 'password';
```
加上所有權限
```
grant all privileges on *.* to root@'%' identified by '12345678' with grant option;
FLUSH PRIVILEGES;
```
## Core安裝
Add the dotnet product feed
```
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[packages-microsoft-com-prod]\nname=packages-microsoft-com-prod \nbaseurl= https://packages.microsoft.com/yumrepos/microsoft-rhel7.3-prod\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/dotnetdev.repo'
```
1. Install the .NET SDK
```
sudo yum update
sudo yum install libunwind libicu
sudo yum install dotnet-sdk-2.1.4
```
2. 驗證.NET Core安裝
來到這裡你已經成功安裝.NET Core，建立一個專案測試一下 
```
#建立Console專案
 [root@localhost ~]# dotnet new console -o hwapp 
#移至目錄
 [root@localhost ~]# cd hwapp 
#restore dependencies，例如JSON.NET，EntityFramework，Bootstrap等Library
 [root@localhost ~]# dotnet restore 
#執行 
[root@localhost ~]# dotnet run 
#***Output***: #> Hello World! 

```
#### 安裝Nginx
在 RHEL, CentOS 或 Fedora 安裝 Nginx, 最簡單的方法是先加入 Nginx 的 CentOS 7 yum repository, 然後用 Yum 安裝
* 編寫最新的 Nginx 套件位置
```
#vim /etc/yum.repos.d/nginx.repo
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=0
enabled=1
```
* 更新一下所有套件庫的快取資料。
```
yum -y update
```
* 利用 yum 安裝
```
yum install nginx
```
* 啟動防火牆
```
firewall-cmd --permanent --zone=public --add-service=http
firewall-cmd --permanent --zone=public --add-service=https
firewall-cmd --reload
```
* 設定ngix
安裝好 Nginx 網頁伺服器後, 便可以用 systemctl 啟動/停止/重新啟動 Nginx, 現在啟動 Nginx 及設定開機自動啟動:
```
systemctl start nginx.service
systemctl enable nginx.service
```
#### 設定nginx
以下是default的設定範例 /etc/nginx/conf.d/default.conf

```
server {
    listen 80;
    location / {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection keep-alive;
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
		proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header REMOTE-HOST $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Cookie $http_cookie;
    }
}

```
建立好設定檔後透過以下命令重新啟動 nginx
```
systemctl restart nginx.service
sudo service nginx restart
sudo nginx -t 以驗證組態檔的語法

```

#### 建立服務檔
指令如下
```
vim /etc/systemd/system/gomoshop.service
```
內容如下
```
[Unit]
Description=GomoShop  running on Centos7

[Service]
WorkingDirectory=/home/wwwdata/wwwshop
ExecStart=/usr/bin/dotnet /home/wwwdata/wwwshop/Gomo.CC.UI.Portal.dll
Restart=always
RestartSec=10  # Restart service after 10 seconds if dotnet service crashes
SyslogIdentifier=dotnet-gomoshop
User=root
Environment=ASPNETCORE_ENVIRONMENT=Production

[Install]
WantedBy=multi-user.target
```
指令參考
```
systemctl enable gomoshop.service
systemctl status gomoshop.service
systemctl restart gomoshop.service
journalctl -fu gomoshop.service

```

## 參考  

1. [Rufus的官方網站](https://rufus.akeo.ie/?locale=zh_TW)
2. [Rufus製作Ubuntu 16.04 USB安裝隨身碟](http://blog.xuite.net/yh96301/blog/450717778-Rufus%E8%A3%BD%E4%BD%9CUbuntu+16.04+USB%E5%AE%89%E8%A3%9D%E9%9A%A8%E8%BA%AB%E7%A2%9F)
3. [Core安裝](https://www.microsoft.com/net/learn/get-started/linux/centos)
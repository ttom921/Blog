---
title: 記錄FtpServer的使用
categories:
  - 設定
tags:
  - FTP
date: 2018-04-11 13:57:01
---
### FileZilla Server的注意事項
使用「FileZilla Clinet」連線「FileZilla Server」時發生下面問題，「425 Can't Open Data Connection 無法取得目錄列表」
這時候大家一定會檢查「防火牆」，但已經設定「防火牆規則」開放「21 Port」輸入
當您使用「FileZilla Clinet」連線「FileZilla Server」時，預設使用「被動模式 Passive Mode」，
這時候我們需要設定「FileZilla Server - Passive Mode Settings」，
開啟「FileZilla Server」=>「Edit」=>「Settings」

1. 點選「Passive mode settings」
2. 輸入 Port 範圍「6000-6010」
PS. ( Port 的範圍不要跟您的設定互相衝突即可 )

接下設定「Windows 防火牆」

* [FileZilla Server 防火牆設定](http://my-fish-it.blogspot.tw/2011/07/ss-filezilla-server-ftp.html)
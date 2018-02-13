---
title: VS的IIS Express可以以IP來訪問
date: 2018-02-13 09:52:12
categories: [設定]
tags: [Web]
---
在使用VS執行web程式，只能以localhost:post來訪問，當以你電腦的ip或是127.0.0.1:post來訪問時，
在網頁上會出現"Bad Request - Invalid Hostname"處理的方法如下
1. 在專案的資料夾下有.vs\config\applicationhost.config，將此檔案打開找此"bindings",將要使用
的ip加入如下面的例子
```
<bindings>
    <binding protocol="http" bindingInformation="*:55018:localhost" />
	<binding protocol="http" bindingInformation="*:55018:192.168.2.144" />
</bindings>
```
2. 以管理員的身份來執行VS,接下來打開要執行專案,build和執行它,之後在右下角的tray icon,會有
IIS Express的圖示,就會看到，你剛才設定的ip,選擇它就可以了

3. 參考

3.1 [VS2015 使用IIS Express 支持非localhost访问](http://blog.csdn.net/small_tu/article/details/50961478)
3.2 [VS-Visual Studio-IIS Express 支持局域网访问](http://www.cnblogs.com/liluping860122/p/4685564.html)

---
title: 記錄測試時手機可以core
categories:
  - 設定
tags:
  - core
date: 2018-05-08 16:31:29
---
#### Core相關
   在自已測試時，有時會需要手機來測試一下自已的web網路有無問題
   所以需要來連結自已的server,設定上很簡單
* 在windows 
  先將自已的防火牆的port打開
* 設定 launchSettings.json
  在要執行的設定檔加入設定如下範例
 ```
 "Gomo.CC.UI.Portal(Dev)": {
      "commandName": "Project",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_URLS": "http://*:5000",// <--這是主要的
        "ASPNETCORE_ENVIRONMENT": "Development"
      },
      "applicationUrl": "http://localhost:5000/"
  }
 ``` 
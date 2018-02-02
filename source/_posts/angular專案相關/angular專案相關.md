---
title: angular專案相關
date: 2018-01-30 15:13:18
categories: [專案]
tags: [angular]
---
測試帳號
ttom@gomo2o.com 1234 admin
test@gomo2o.com 1234 General,ShopManager
shop@gomo2o.com 1234 ShopStaff
## 建立新的專案
```
ng new Gomo3Shop --routing --style scss
```
若不想要建立資料夾，可以加上 --flat 參數

## 安裝bootstrap3
```
npm install bootstrap@3
npm install font-awesome
npm install jquery
npm install -D @types/jquery
```
## 使用bootstrap3 
這是全域的使用在.angular-cli.json裏設定
```
"styles": [
  "styles.css",
  "../node_modules/bootstrap/dist/css/bootstrap.css",
  "../node_modules/font-awesome/css/font-awesome.css"
]
"scripts": [
  "../node_modules/jquery/dist/jquery.js",
  "../node_modules/bootstrap/dist/js/bootstrap.js"
],
```
## 加入toast
```
npm install ngx-toastr --save
npm install @angular/animations --save
//加入css
"styles": [
  "styles.scss",
  "../node_modules/ngx-toastr/toastr.css"
]
//加入 add ToastrModule to app NgModule
import { CommonModule } from '@angular/common';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { ToastrModule } from 'ngx-toastr';
import { FormsModule, ReactiveFormsModule } from '@angular/forms';
```
在App NgModul裏要加入
```
CommonModule,
BrowserAnimationsModule, // required animations module
ToastrModule.forRoot(), // ToastrModule added
```
## 加入 oidc-client
```
npm install  oidc-client --save
```
注意要複制到assets下的odic-client.min.js 是要複制node_modules\oidc-client\lib下的odic-client.min.js
在.angular-cli.json裏設定
```
"assets": [
        "assets",ng
        "favicon.ico",
        { "glob": "silent-renew.html", "input": "./", "output": "./" }
      ],
```	  
## Import jQuery in app.module.ts.	
```
import * as $ from 'jquery'; 
```
## 以下是建立專案元件
```
//登入畫面
ng g m repairLogin 
ng g c repairLogin\repairLogin --flat
//登入後首頁
ng g m repairSigned --routing
ng g c repairSigned\repairSigned --flat
ng g c repairSigned\repairHome
ng g c repairSigned\repairNavigate
ng g c repairSigned\repairAside
ng g c repairSigned\repairNavBottom
//報表相關
ng g m repairReport --routing
ng g c repairReport\repairReport --flat
ng g c repairReport\revenue
ng g c repairReport\inventory
ng g c repairReport\accountReceivable
ng g c repairReport\accountPayable
//公用
ng g c shared\components\pageNotFound
ng g c shared\components\loginCallback

ng g s shared\services\auth
```

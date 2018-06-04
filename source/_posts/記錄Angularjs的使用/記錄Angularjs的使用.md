---
title: 記錄Angularjs的使用
categories:
  - 前端
  - angularjs
tags:
  - 記錄
  - angularjs
date: 2018-06-01 11:46:33
---
### bundle的用法
在asp core裏可以將常用的js來壓成min來使用可以減少js檔的大小
例如
```
<bundle name="wwwroot/css/site.min.css" />
```
它會自動的在develop或是release裏自動的產生以下的碼
```
<environment names="Development">
    <link rel="stylesheet" href="~/css/site1.css" />
    <link rel="stylesheet" href="~/css/site2.css" />
    <link rel="stylesheet" href="~/css/site3.css" />
</environment>
<environment names="Staging,Production">
    <link rel="stylesheet" href="~/css/site.min.css" asp-append-version="true" />
</environment>
```
這樣在開發時可以使用原始碼來除錯，在正式時可以使用min檔來加快程式的運行
* 參考資料
 * [Meziantou.AspNetCore.BundleTagHelpers](https://github.com/meziantou/Meziantou.AspNetCore.BundleTagHelpers)

### 多國語系bind的用法
* 直接來翻譯
```
ng-bind="'CustomerProfileCustomerType' | translate"
```
* 使用變數
```
ng-bind="AsideWork"
```
### 多國語系placeholder的用法
* 直接來翻譯
```
placeholder="{{'RepairWorkPicPlsInpPlateNo' | translate}}"
```
### 記錄動態加入欄位
* [AngularJS | Adding Form Fields Dynamically](http://www.shanidkv.com/blog/angularjs-adding-form-fields-dynamically)

### 記錄drog&drop多圖片
* [Using Plupload To Upload Files In AngularJS](https://www.bennadel.com/blog/2652-using-plupload-to-upload-files-in-angularjs.htm)
* [A simple drag/drop upload directive for AngularJS](https://grobmeier.solutions/drag-drop-upload-angularjs-07092015.html)
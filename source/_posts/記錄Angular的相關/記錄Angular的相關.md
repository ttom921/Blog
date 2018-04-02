---
title: 記錄Angular的相關
categories:
  - 前端
tags:
  - angular
date: 2018-03-30 09:25:59
---
#### 在學習angular的英雄列表
在學習angular的官方教學遇到的問題和解決的方法
* 服務章節
  有 of 找不到,時要修改如下
  ```
  import { Observable } from 'rxjs/Observable';
  import { of } from 'rxjs/observable/of';
  ```
* Http章節
  有出現api/heroes的服務時,找不到是因為版本的問題，目前是angular5的版本，
而安裝會是最新的，所以安目前的版本
```
npm remove angular-in-memory-web-api@0.6.0
npm i --save angular-in-memory-web-api@0.5.0
```
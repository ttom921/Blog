---
title: Javescript相關
date: 2018-02-01 14:01:49
categories: [前端]
tags: [CSS]
---
  記錄有關一些javascript的用法
## 日期轉換的用法
將時間的字串，先取出來,再利用dataToYMD轉成相要的顯示字串
new Date().toISOString(); // e.g. "2016-11-21T08:00:00.000Z"
```
function GetCurDate()
{
    var strDate = $("#dummyDate").val().substring(0, 10);
    //console.log(strDate);
    var d = new Date(Date.parse(strDate));
    var szformatDate = dateToYMD(d);
    return szformatDate;
}
function dateToYMD(date) {
    var d = date.getDate();
    var m = date.getMonth() + 1;
    var y = date.getFullYear();
    return '' + y + '/' + (m <= 9 ? '0' + m : m) + '/' + (d <= 9 ? '0' + d : d);
}
```

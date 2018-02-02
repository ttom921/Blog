---
title: css和印表機
date: 2018-02-01 10:08:48
categories: [前端]
tags: [CSS]
---
記錄有關css和印表機相關的使用
## 有關css檔的設定
將原來的css檔在用 print的包起來
```
@media print {
	#tab {
        ....
    }
	 .col-1 {
        ....
    }
}
```
將要隱藏的元件加入要 id="hidden_div", 在加入以下的代碼
```
function printScreen(printlist) {
        // 注意要hide的元件,要加入id="hidden_div"
        // 將原來的css檔用@media print{} 包起來
        var value = document.getElementById(printlist).innerHTML;

        var printPage = window.open("", "列印", "");
        printPage.document.open();
        printPage.document.write('<html><head></head><body onload="window.print()">');
        printPage.document.write("<PRE>");
        printPage.document.write(value);
        printPage.document.getElementById('hidden_div').style.display = 'none'
        printPage.document.write("</PRE>");
        printPage.document.close("</BODY></HTML>");

    }
```
## IE相關問題
在ie11中如果在印表時發現，在td的標記中如果沒有將space移除,則會有佔位的情形
```
<td>
	<input type="text"/>
</td>
//改成
<td><input type="text"/></td>
```
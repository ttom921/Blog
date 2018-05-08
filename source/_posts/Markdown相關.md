---
title: Markdown相關
categories: [記錄]
tags: [Markdown]
date: 2018-01-29 22:21:53
---
#### 特列顯示
~~刪除線~~
```
~~刪除線~~
```
#### Markdown 產生程式碼區塊
在Markdown裡面產生程式碼區塊的方法很簡單，就是用三個\`\`\` 的符號
將程式碼的上下都用括起來

舉例：
 \`\`\`
程式碼放這邊
 \`\`\`

這樣會產生的畫面就是
```
程式碼放這邊
```
#### Markdown 連結設定 
![image](https://lh3.googleusercontent.com/ytDZt9pKlh84wDUYE04K49g-MGXYxfV1mET4-HpPtR9QpglNIT-v5Co_zzOC1FU0V0m2rnnhQ39afPeZlV47TOdZr4sLWAOAhzBEZ6AVJyyl8pM6OUNft2F5BxJuY2wtgCF1WAzcVd7WPIoT1FqgdDViYOKGYK9qn5nDdiRAc1bB3UIBPkBh_rDlbcrlROteZFRmegY81Gpx4uqR4cHYa0x9BVnA9M1vEYbxaH4IKvMAHdCQtKbls49RepPxbwqqXy4M_fOP6EMPCI-oX6A-fqXTE42auU5NyQheKKROPBZnbgcEm2Ffz-6-fxJiGzXm_DO9058v3cS9qAjzZmQCrCXDQKh3tWymRB9gHK4dgoruZJWws1Q6p9izxufh0SQ8KfL5TagK-xQK8s2ietie2kHwcWbwKOWpM4BQtNGqTMGbKT9nzVxkxk9kBiqEll7bcETz-O3zYeRMT6Adl6JDnfjshnIns6rj-dgwairU-ZYBHr7z7pdYL-rs92GrBtonZv1n1UUwKr1CG78Q3me-ZwBMXcJecTaeks0t2TL56BPYTh4SVphUZX_XGAApZp9DKdpeoN51tC8Sbh7yeGpSwWkl5rfbPBRH0lJntNs=w1032-h774-no)

```
[Google](http://www.google.com/)
![image](https://lh3.googleusercontent.com/ytDZt9pKlh84wDUYE04K49g-MGXYxfV1mET4-HpPtR9QpglNIT-v5Co_zzOC1FU0V0m2rnnhQ39afPeZlV47TOdZr4sLWAOAhzBEZ6AVJyyl8pM6OUNft2F5BxJuY2wtgCF1WAzcVd7WPIoT1FqgdDViYOKGYK9qn5nDdiRAc1bB3UIBPkBh_rDlbcrlROteZFRmegY81Gpx4uqR4cHYa0x9BVnA9M1vEYbxaH4IKvMAHdCQtKbls49RepPxbwqqXy4M_fOP6EMPCI-oX6A-fqXTE42auU5NyQheKKROPBZnbgcEm2Ffz-6-fxJiGzXm_DO9058v3cS9qAjzZmQCrCXDQKh3tWymRB9gHK4dgoruZJWws1Q6p9izxufh0SQ8KfL5TagK-xQK8s2ietie2kHwcWbwKOWpM4BQtNGqTMGbKT9nzVxkxk9kBiqEll7bcETz-O3zYeRMT6Adl6JDnfjshnIns6rj-dgwairU-ZYBHr7z7pdYL-rs92GrBtonZv1n1UUwKr1CG78Q3me-ZwBMXcJecTaeks0t2TL56BPYTh4SVphUZX_XGAApZp9DKdpeoN51tC8Sbh7yeGpSwWkl5rfbPBRH0lJntNs=w1032-h774-no) 
```
#### Markdow 表格的設定
如下的範例
```
-|默認左對齊|居中對齊|內容右對齊
:-:|-|:-:|-:
1|Left|Center|Right
2|Left|Center|Right
3|Left|Center|Right
```
-|默認左對齊|居中對齊|內容右對齊
:-:|-|:-:|-:
1|Left|Center|Right
2|Left|Center|Right
3|Left|Center|Right

#### 無序號
以`* 標題`來表示
如有有下一級`+ 1-1`來表示
```
* 註冊流程
* db備份
* 車主
   + 1-1 車主主畫面的圖要換
```
* 註冊流程
* db備份
* 車主
   + 1-1 車主主畫面的圖要換
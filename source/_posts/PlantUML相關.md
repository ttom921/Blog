---
title: PlantUML相關
categories:
  - UML
tags:
  - PlantUML
date: 2018-01-30 21:53:12
---

## PlantUML和Hexo整合
安装hexo-tag-plantuml
```bash
npm install hexo-tag-plantuml --save
```
## 語法
```
{% plantuml %}
start
:配置Java環境; 
:下載pantuml.jar;
:編寫描述文件; 
:執行; 
stop
{% endplantuml %}
```

{% plantuml %}
start
:配置Java環境; 
:配置Java環境.jar;
:編寫描述文件; 
:執行; 
stop
{% endplantuml %}
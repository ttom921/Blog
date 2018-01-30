---
title: PlantUML相關
date: 2018-01-30 21:53:12
categories: [UML]
tags: [PlantUML]
---
##PlantUML和Hexo整合
安装hexo-tag-plantuml
```bash
npm install hexo-tag-plantuml --save
```

{% plantuml %}
start
:配置Java环境; 
:下载pantuml.jar;
:编写描述文件; 
:执行; 
stop
{% endplantuml %}
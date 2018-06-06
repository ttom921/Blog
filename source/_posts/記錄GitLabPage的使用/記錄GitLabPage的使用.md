---
title: 記錄GitLabPage的使用
categories:
  - 記錄
  - GitLabPage
tags:
  - git
date: 2018-06-06 16:11:29
---
### 記錄如何來使用Gitlab的page
 1. 首先要在Gitlab上來註冊一個帳號
 2. 在上面創建一個username.gitlab.io的專案
     ** 注意 username 是你的帳號 **
 3. 使用git將目前的專案上傳到gitlab
 4. 在gitlab上使用網頁來加入下面的檔案 .gitlab-ci.yml
    ** 注意自已的node的版本 **
```
image: node:8.9.4
pages:
  cache:
    paths:
    - node_modules/

  script:
  - npm install hexo-cli -g
  - npm install hexo-generator-feed --save
  - npm install
  - hexo g
  artifacts:
    paths:
    - public
  only:
  - master
```
 

###### 參考資料
 * [利用gitlab pages和hexo搭建一个个人博客](https://blog.csdn.net/winter_evening/article/details/72353953)
 * [GitLab+Hexo小记](http://www.ombres.me/2017/12/14/gitlab-hexo/)
 * [使用 GitLab CI 实现 Hexo 持续部署](https://blog.nfz.moe/archives/hexo-auto-deploy-with-gitlab-ci.html)
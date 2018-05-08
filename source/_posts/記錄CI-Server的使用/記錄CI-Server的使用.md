---
title: 記錄CI Server的使用
categories:
  - 設定
tags:
  - Jenkins
date: 2018-04-26 15:23:51
---
#### CI server
CI Server是Continuout Integration Server (持續整合伺服器)的縮寫
* 安裝Jenkins http://localhost:8080/
  目前是以windows為主，目前版本為jenkins-2.107.2，會有密碼在安裝的目錄下有，
  接下會問要麼plugin,主要選擇git和msbuilder
  建立使用者可參考[在windows安裝jenkins和入門](https://dotblogs.com.tw/kinanson/2017/08/17/135639)
  建立專案可參考[如何使用 Jenkins 2 建置 .NET 專案](https://blog.yowko.com/2017/02/jenkins-2-build-dotnet-project.html)
  在vs2017的msbuil放在
  ```
  D:/Program Files (x86)/Microsoft Visual Studio/2017/Professional/MSBuild/15.0/Bin/amd64
  ```
  要下載nuget
  msbuild 的參數
  ```
  /p:Configuration=En-Release 
 /p:DeployOnBuild=true
 /p:PublishProfile="英文版.pubxml"
 /p:UserName=username
 /p:Password=userpassword
 /p:AllowUntrustedCertificate=True
 /p:EnableMSDeployAppOffline=true
  ```
* 刪除工作的資料
  有時會卡住，在windows下可以到服務的管理列表，找到Jenkins來重新起動。
  刪除此專案的資料，可以到安裝的目錄下的jobs的資料夾，找到專案的名稱，保留**config.xml**，剩下的可以刪除
* 設定有中文文字
    
##### 使用Pipleline
  **注意專案名稱不能使用中文，不然在console下不能執行,發行檔也不能使用中文** 
* 使用msbuild
    * 1.1 先從git將程式碼取下
    * 1.2 要nuget來restore
	```
	D:\tools\NuGet restore
	```
    * 1.3 以msbuild	
	```
	"D:/Program Files (x86)/Microsoft Visual Studio/2017/Professional/MSBuild/15.0/Bin/amd64/"msbuild /p:Configuration=Dev-Release
	```
	* 1.4 發佈
	```
	"D:/Program Files (x86)/Microsoft Visual Studio/2017/Professional/MSBuild/15.0/Bin/amd64/"msbuild /p:Configuration=Dev-Release /p:DeployOnBuild=true /p:PublishProfile=開發版.pubxml /p:UserName=xxxxx /p:Password=xxxx /p:AllowUntrustedCertificate=True /p:EnableMSDeployAppOffline=true 
	```
* 使用dotnet來處理
  * 1.1 先從git將程式碼取下
    可以使用它的語法產生器來生成git取得程式碼
  ```
  stage('取出專案'){
      checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '*/dev']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'XXXXXXX-XXX-XXX_XXXX', url: 'http://127.0.0.1:88/Bonobo.Git.Server/Gomo.CC_git.git']]]
  }
  ``` 
  * 1.2 建置專案
  ```
  stage('建置'){
        bat 'dotnet build --configuration Release'
    }
  ```
  * 1.3 發佈專案到IIS
    目前是使用webdeploy和IIS來發行網店
  ```
  stage('發佈'){
      bat 'dotnet publish --configuration Release /p:PublishProfile=develop.pubxml /p:UserName=username /p:Password=userpassword /p:AllowUntrustedCertificate=True'
    }
  ```
  

* 參考資料
 * [Jenkins官方](https://jenkins.io/)
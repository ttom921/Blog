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
* 可設定node
  目地是為了使用那一個服務器來幫忙建立專案，所以有命名，在設定node時要將名稱代入ex node('master')，才可執行該服務器
  
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
* 發佈到linux
  * 1.1 取出專案
```
 stage('linux-取出專案'){
        checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '*/dev']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'xxx-xxx_xxx_xx_xx_xx', url: 'http://10.0.0.10:88/Bonobo.Git.Server/Gomo.CC_git.git']]]
    }
```
 * 1.2 建置專案
 ```
  stage('linux-建置'){
         bat 'dotnet build -c Release /p:DeployOnBuild=true /p:PublishProfile=dev_linux.pubxml'
    }
 ```
 * 1.3  建立壓縮檔
 ```
     def buildNumber = env.BUILD_NUMBER
     def workspace = env.WORKSPACE
     def buildUrl = env.BUILD_URL
     def dirprjrelease= env.WORKSPACE+'/Gomo.CC.UI.Portal/bin/Release/PublishOutput'
     def dateFormat = new SimpleDateFormat("yyyyMMddHHmm")
     def date = new Date()
     def usedate=dateFormat.format(date)
     def zipfile=usedate +'.zip'
     def winrar = "\"C:/Program Files/WinRAR/WinRAR.exe\""
     def winparam = "a -afzip -ep1"
	 def pscp ="D:/tools/Putty/pscp.exe"
	stage('test'){
        bat "${winrar} ${winparam} ${zipfile} \"${dirprjrelease}/*.*\" -r "
    } 
 ```
 * 1.4  上傳壓縮檔
 ```
  stage('上傳檔案'){
       bat"echo y | \"${pscp}\" -pw 12345678 \"${workspace}/${zipfile}\" root@192.168.2.222:/home/ttom "
    }
 ```
* 1.5 停止服務
```
   stage('停止服務'){
        sh "cd ${zipdest}"
        sh "systemctl stop gomoshop.service"
    }
```
* 1.7 開始服務
```
    stage('開始服務'){
        sh "systemctl restart gomoshop.service"
    }
```	
* 1.6 解壓壓縮檔
```
 stage('unzip檔案'){
        sh "unzip -o ${zipdest}/${zipfile} -d ${zipdest}"
    }
``` 
* 1.7 刪除壓縮檔
```

```
  * 1.1 刪除壓縮檔
  * 1.2 建立壓縮檔 
  * 1.3 上傳壓縮檔
  * 1.4 停止服務
  * 1.5 解壓壓縮檔
  * 1.6 刪除壓縮檔
  * 1.7 開始服務
  
  
  
* 參考資料
 * [Jenkins官方](https://jenkins.io/)
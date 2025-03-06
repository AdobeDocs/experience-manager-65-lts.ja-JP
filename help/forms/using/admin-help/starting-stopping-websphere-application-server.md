---
title: WebSphere Application Server の起動と停止
description: 一部の手順では、AEM Forms 製品をデプロイする WebSphere のインスタンスを停止または起動する必要があります。このドキュメントでは、WebSphere Application Server の起動および停止方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 20cd6efb-edcf-4c87-b0f5-bdec5a0f6280
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 100%

---

# WebSphere Application Server の起動と停止 {#starting-and-stopping-websphere-application-server}

一部の手順では、AEM Forms 製品をデプロイする WebSphere のインスタンスを停止または起動する必要があります。アプリケーションサーバーが起動しているかどうかわからない場合は、まず WebSphere Application Server のステータスを表示します。

## WebSphere Application Server のステータスの表示 {#view-the-status-of-websphere-application-server}

1. コマンドプロンプトで、`[appserver root]/bin`ディレクトリに移動します。
1. 次のコマンドを入力します。*server_name* には、WebSphere Application Server の名前を指定します。

   * （Windows）`serverStatus.bat`*server_name*
   * （Linux、UNIX）/ `serverStatus.sh`*server_name*

## WebSphere Application Server の起動 {#start-websphere-application-server}

1. コマンドプロンプトで、`[appserver root]/bin`ディレクトリに移動します。
1. 次のコマンドを入力します。*server_name* には、WebSphere Application Server の名前を指定します。

   * （Windows）`startServer.bat`*server_name*
   * （Linux、UNIX）/ `startServer.sh`*server_name*

## WebSphere Application Server の停止 {#stop-websphere-application-server}

1. コマンドプロンプトで、`[appserver root]/bin`ディレクトリに移動します。
1. 次のコマンドを入力します。*server_name* には、WebSphere Application Server の名前を指定します。

   * （Windows）`stopServer.bat`*server_name*
   * （Linux、UNIX）/ `stopServer.sh`*server_name*

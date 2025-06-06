---
title: サービスの開始と停止
description: AEM Forms モジュール、アプリケーションサーバー、データベースに関連付けられたサービスを開始および停止する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: a4ff69d2-a429-49b9-ba48-9dd56ccdf23e
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 100%

---

# サービスの開始と停止 {#starting-and-stopping-services}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

AEM Forms に含まれるサービスには以下の 2 種類があります。

* AEM Forms アプリケーションサーバーおよびデータベースを制御するサービス
* AEM Forms モジュールを制御するサービス

## AEM Forms モジュール関連サービスの開始と停止 {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM Forms モジュール（例えば、Forms、Rights Management、Output）がサービスとして動作します。これらの AEM Forms モジュールのサービスは、場合によって起動または停止する必要があります。例えば、サービスの設定を変更した後には、AEM Forms サービスを停止してから再起動する必要があります。

>[!NOTE]
>
> 「Ctrl + C」コマンドを使用して SDK を再起動することをお勧めします。Java プロセスの停止など、別の方法を使用して AEM SDK を再起動すると、AEM 開発環境で不整合が生じる場合があります。

1. 管理コンソールで、**サービス**／**アプリケーションおよびサービス**／**サービスの管理**&#x200B;をクリックしてください。
1. サービスの管理ページで、停止または開始するサービスの隣のチェックボックスをオンにして、「停止」または「開始」をクリックします。

## アプリケーションサーバーおよびデータベースのサービスの開始と停止 {#start-or-stop-services-for-the-application-server-and-database}

AEM Forms の完全な実装には、以下のアプリケーションサーバーおよびデータベースのサービスが含まれています。

* AEM Forms 用の *`[application server]`*
* AEM Forms 用の *`[database]`*

Windows では、これらのサービスには、**管理ツール**／**サービスパネル**&#x200B;からアクセスできます。例えば、自動オプションを使用して JBoss に AEM Forms をインストールした場合、システムでは以下のサービスを使用できます。

* JBoss for Adobe Experience Manager フォーム
* MySQL for Adobe Experience Manager フォーム

これらのサービスを開始または停止するには、サービスパネルのリストからサービスを選択し、パネルの適切なアクションボタンをクリックします。

UNIX® または Linux では、コマンドラインから次のテキストを入力します。*`[service name]`* には、確認するサービスの名前を指定します。

```java
     ps -A | grep [service name]
```
